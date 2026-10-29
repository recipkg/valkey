# Valkey · Recipkg

**数据与存储：从开源键值数据结构服务器提取重建配方。**

[标准库](https://github.com/recipkg/standard-library) · [配方清单](RECIPE.md) · [构建要求](BUILD_PROMPT.md) · [验收条件](ACCEPTANCE.md) · [观察记录](OBSERVED.md) · [来源](SOURCES.md) · [来源与覆盖](COVERAGE.md)

![从软件与依赖整理配方，再交给 Agent 重建](https://raw.githubusercontent.com/recipkg/recipkg/main/assets/recipkg-cover.png)

本仓库是配方，不是上游源码或官方发行版。内容仍在提取：有限样本覆盖二进制数据、事务、ACL 与正常重启；完整协议、故障恢复、安全及独立重建尚未验收。

## 使用

```sh
recipe_dir="$(mktemp -d)"
recipkg pack . -o "$recipe_dir/valkey.recipe.tar.gz"
recipkg check "$recipe_dir/valkey.recipe.tar.gz"
recipkg build "$recipe_dir/valkey.recipe.tar.gz" --lang zh-CN --output "$recipe_dir/build.md"
printf '提示词：%s\n' "$recipe_dir/build.md"
```

打包包含固定的递归依赖；`build` 只输出提示词。归档检查和少量样本不证明完整重建或数据安全。
