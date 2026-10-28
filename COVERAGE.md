# 来源、覆盖与缺口

- [Valkey 9.1.2 源码](https://github.com/valkey-io/valkey/tree/7f1dffedff6de73058b2c2a389422b6ecd56c8fb)，提交 `7f1dffedff6de73058b2c2a389422b6ecd56c8fb`；阅读固定版本 README、COPYING 和 SET、EXPIRE、MULTI、SAVE 命令元数据。源码声明的两份 BSD-3-Clause 版权见 COPYING；依赖另核对。
- 隔离运行发行版 `valkey 9.1.2-1.1`，对四项有限样本通过真实 RESP2 Unix socket 验证；发行版报告短提交号但完整构建来源未证实，详见 `OBSERVED.md`。
- `quality` 是固定版本的质量合同；没有找到需要强加的现成数据存储、协议或安全配方。Lua/模块等可选组件、客户端与其他依赖尚未完整分析。
- 尚未实现或验收独立重建；服务器完整协议、命令、配置、认证、持久化、崩溃恢复、复制、集群、平台和性能均未完成。不能用此草案处理真实数据或宣称完整兼容。
