# Makefile

## Example

```makefile
PYTHON=python3.9
PACKAGES=pymongo

all: layer-pymongo.zip

clean:
    - rm -rf resources
    - rm -rf .aws-sam/*
    - rm layer-pymongo.zip

layer-pymongo.zip:
    mkdir -p resources/python
    PYTHONUSERBASE=resources/python $(PYTHON) -m pip install --user $(PACKAGES)
    wget -O resources/python/rds-combined-ca-bundle.pem https://s3.amazonaws.com/rds-downloads/rds-combined-ca-bundle.pem
    cd resources && zip -r ../layer-pymongo.zip python && cd ..
    rm -rf resources

build: resources/layer-pymongo.zip template.yaml
    sam build

sam: build
    sam deploy --capabilities CAPABILITY_NAMED_IAM --guided
```

## 介绍

`Makefile`包含5个东西：

* 显式规则: 定义如何生成一个或多个目标文件
* 隐式规则: 利用make的自动推导功能来自动生成目标文件
* 变量定义: 类似C语言里面的宏定义
* 文件指示: 引用别的`Makefile`; 指定有效部分; 定义多行命令
* 注释: 只有行注释, 使用`#`

!!!warning

    命令必须要以TAB键开头, 并且必须要有一个空格分隔符

## 规则

### 规则的语法

```makefile
targets: prerequisites
    command
    ...

# 或者
targets: prerequisites; command
    command
    ...
```

* `targets`: 可以是目标文件, 执行文件, 标签
* `prerequisites`: 生成target所依赖的文件或者target
* `command`: 命令行, 如果不与`target: prerequisites`在同一行, 则必须要以TAB键开头

!!!info

    一般来说,`make`会以标准Shell(/bin/sh)来执行命令, 但是也可以使用其他的Shell

### 变量

* 定义变量：`<变量名>=<值>`
* 使用变量：`$(变量名)`

### 通配符

* `*`: 匹配任意字符
* `~`: 当前用户的`HOME`目录
* `?`

### 命令书写

* 显示命令: 命令前加`@`
* 命令执行: 为了让上一条命令的结果应用与下一条命令, 需要使用分号分隔命令
* 命令出错: 命令前加`-`, 表示不管命令出不出错都认为是成功的

## 执行

!!!example

    `make`或者`make <label>`

## 参考链接

* [Makefile教程-CSDN](https://blog.csdn.net/weixin_38391755/article/details/80380786)
* [跟我一起写Makefile](https://seisman.github.io/how-to-write-makefile/introduction.html)
