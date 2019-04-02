# Mac下的 tree 命令 输出目录树层结构

 - mac 下使用 brew包管理工具安装 tree

```bash
brew install tree
```
 - 查看信息

```bash
tree --help
```
 - 指定遍历层级

```bash
tree -L 2
```

 - 导出到文件 Readme.md

把一个目录的结构树

```bash
tree -L 2 >README.md //然后我们看下当前目录下的 README.md 文件
```

 - 显示项目的层级

```bash
tree -L 3
```

[参考资料][1]

[1]: https://www.jianshu.com/p/9411d60950bf