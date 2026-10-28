# 验收与限制

样本测试不连接现有服务，也不使用真实数据。指定候选服务端，运行：

```sh
RECIPKG_TEST_VALKEY_SERVER=/absolute/path/to/valkey-server python3 -m unittest discover -s tests -p test_valkey.py -v
```

在 [standard-library-verification](https://github.com/recipkg/standard-library-verification) 仓库执行。显式指定的路径不存在或启动失败应报错；未指定目标会跳过，跳过不是通过。测试检查二进制键和值、过期和 SET 条件，区分 null bulk 和 null array 的 WATCH 冲突、排队错误与执行错误，用户命令和键模式权限，RDB 与 AOF 正常重启、AOF 已确认写入后的进程终止恢复，以及本机单主单从初始同步与后续传播。程序仅控制自己创建的服务、临时目录和本机监听；平台必须支持 Unix socket。启动后需等可服务请求；测试不把 `LOADING` 当作已经完成恢复。

完整验收还需补充协议、数据结构和命令、ACL 与 TLS、并发、插件、复制、故障、崩溃恢复、持久化损坏、网络、目标平台和实测性能等合同。先补全未观察行为和可复现验证，再在独立实现上执行；不允许把有限样本或 `recipkg check` 当作完整兼容、安全或数据持久性保证。
