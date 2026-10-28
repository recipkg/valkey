# 上游样本观察

2026-10-29 在 Linux x86_64_v3、CachyOS `valkey 9.1.2-1.1` 上运行 `/usr/bin/redis-server`；`--version` 报 `Valkey server v=9.1.2 sha=7f1dffed:1`，与固定提交短前缀相符，但发行版补丁、构建标志和完整源码一致性未核验。以下结论属于该二进制，不能当作固定源码构建或其他发行版的实测。

测试仅启动新进程：`--port 0` 禁止 TCP，Unix socket 和 `--dir` 均位于临时目录，自动快照和 AOF 禁用，使用私有测试数据；测试结束关闭进程并删除临时目录。客户端通过 RESP2 发送字节；具体可复现断言见 [verification/test_valkey.py](https://github.com/recipkg/standard-library-verification/blob/main/tests/test_valkey.py)。

- `SET` / `GET` 保持键 `6b00ff`、值 `76000d0aff` 字节；对该字符串键执行 `HGET` 得到 `WRONGTYPE`。`PEXPIRE` 为 0 返回整数 1，随后 `GET` 为空 bulk、`PTTL` 为 -2。`HSET` 两个新字段返回 2，`HGET` 正确取回一个字段。
- 客户端 A `WATCH counter` 后客户端 B 改写该键；A 进入 `MULTI` 并排队 `INCR`，`EXEC` 返回 RESP2 null array，数据保持 B 的值。正常事务排队 `INCR` 和 `GET` 后 `EXEC` 返回 `[5, "5"]`。
- 测试管理员创建 `reader`，启用并授权所有键、`GET` 与 `PING`；该用户凭测试密码认证后能 `GET`，执行 `SET` 得到 `NOPERM`，管理员读到的值未变化。
- `SET` 二进制字符串和 `HSET` 字段后执行同步 `SAVE`，正常停止并重启同配置、同数据目录，两个值被恢复。

未测权限的其他组合、非正常退出、持续写入期间备份、时钟跳变、复制及集群。内存、吞吐和延迟没有基准。
