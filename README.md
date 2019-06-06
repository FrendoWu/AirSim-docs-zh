# AirSim中文文档翻译计划
<<<<<<< HEAD
=======
本项目是针对微软开源项目：[AirSim](https://github.com/microsoft/airsim/)的[文档](https://microsoft.github.io/AirSim/)进行的翻译计划。
>>>>>>> 8589e7f18b5fb43c7f4c37bcd505fe7ee4867934

本项目是针对微软开源项目：[AirSim](https://github.com/microsoft/airsim/)的[英文文档](https://microsoft.github.io/AirSim/)进行的翻译计划。

项目网址：[AirSim中文文档](https://frendowu.github.io/AirSim-docs-zh/)

翻译进度：■■■■■□□□□□□□□□□□□□□□□□□□□（约20%）

## 参与贡献

您需要：

- 安装支持Markdown格式的软体如[Typora](https://typora.io)
- 了解[Markdown基本用法](https://www.runoob.com/markdown/md-tutorial.html)
- 下载该项目的[归档安装包](https://github.com/FrendoWu/AirSim-docs-zh/archive/master.zip)，解压后找到/documents目录中您感兴趣的.md，用Typora等打开，进行翻译。（也可以在线查看[/documents](https://github.com/FrendoWu/AirSim-docs-zh/tree/master/documents)）



提交贡献方案有两个：

1. 将翻译好的Markdown文件打包发送至邮箱：`fre[.防爬虫]ndo.wu@gmail.com`，请删除`[.防爬虫]`字符。
2. 提交Pull request，[参考教程](https://gist.github.com/zxhfighter/62847a087a2a8031fbdf)



## 项目配置（供其他项目参考）

1. 安装 [mkdocs](https://www.mkdocs.org) 
2. 配置mkdocs.yml，其中docs_dir为md的位置，site_dir为生产的静态html位置，theme采用readthedocs主题。

```xml
site_name: AirSim中文文档
repo_url: https://github.com/FrendoWu/AirSim-docs-zh
docs_dir: documents
site_dir: docs
theme: readthedocs
extra:
  version: 1.2.1
nav:
    - "主页": 'README.md'
    - "搭建AirSim":
		...
```

3. 直接翻译docs_dir中的文件并保存，运行命令`mkdocs build`即可。