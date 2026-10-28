# Valkey 配方（提取中）

```toml
format = "recipkg/1"

[package]
name = "valkey"
version = "0.1.3"
kind = "software"
description = "Valkey 数据结构服务器的重建配方；当前仍在提取。"
entry = "BUILD_PROMPT.md"

[dependencies.quality]
git = "https://github.com/recipkg/recipkg.git"
rev = "41e5b55c6612a9a5a10e499b5ace6a1a3fed0f2b"
subdir = "recipes/software-quality"
```

上游 [valkey-io/valkey 9.1.2](https://github.com/valkey-io/valkey/tree/7f1dffedff6de73058b2c2a389422b6ecd56c8fb)，固定提交 `7f1dffedff6de73058b2c2a389422b6ecd56c8fb`；上游 [COPYING](https://github.com/valkey-io/valkey/blob/7f1dffedff6de73058b2c2a389422b6ecd56c8fb/COPYING) 包含 Valkey 贡献者和 Redis Ltd. 的 BSD-3-Clause 声明，其他依赖的许可须另核对。现阶段只观察少量行为，尚不能用于重建兼容服务或处理真实数据；见 `COVERAGE.md`。
