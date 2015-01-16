

# 本机测试环境安装

若在本机运行测试，需要安装NodeJS 和 Karma。具体操作如下：

---

### 安装NodeJS

Karma基于nodeJS，所以访问 [NodeJS官网](http://www.nodejs.org) 下载安装即可。


### 安装Karma

karma 封装成npm包，所以都可以通过npm（Node Package Manager）命令安装。

windows 安装步骤可参考访问：http://karma-runner.github.io/0.12/intro/installation.html

如果是linux *or* Mac，直接命令如下：

```sh
$ sudo npm install -g karma-cli
$ npm install karma
$ npm install karma-jasmine karma-chrome-launcher
```


