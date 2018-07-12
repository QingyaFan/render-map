# GDAL

## 编码问题

## 二、安装

## 2.1 Mac上安装gdal最新版本

借助brew和osgeo，安装是从源码编译，可能要等一炷香的时间。

```lang=shell
brew tap osgeo/osgeo4mac
#brew search gdal (if you want to see the various available versions)
brew install gdal2 --with-postgresql --with-libkml
```

然而安装完成后，还需要安装命令行提示，执行相关环境变量的设置，才能正常的启动gdal命令，否则会找不到依赖。

## OGR2OGR

## 指定ogr读取文件采用的编码，不让其自动判断

shapefile有一个open option：ENCODING=encoding_name，在ogr2ogr命令行中使用`-oo ENCODING=encoding_name`指定；或者设置全局属性：SHAPE_ENCODING,ogr2ogr中使用`--config SHAPE_ENCODING=encoding_name`指定。

## 安装Mapserver后报错

安装MapServer后执行 `ogr2ogr --version`，报错：

```lang=txt
dyld: Library not loaded: /usr/local/opt/json-c/lib/libjson-c.2.dylib
  Referenced from: /usr/local/opt/gdal2/bin/ogr2ogr
  Reason: image not found
[1]    872 abort      ogr2ogr version
```

说明`json-c`版本不对，我们切换`json-c`的版本即可解决这个问题。

`brew switch json-c 0.12`，如果本机没有安装0.12这个版本，那么输出会提示你都安装了哪些版本，安装提示选择一个版本（为了兼容性，可以选择最低的），问题即可解决。

```lang=txt
Cleaning /usr/local/Cellar/json-c/0.12
Cleaning /usr/local/Cellar/json-c/0.12.1
Cleaning /usr/local/Cellar/json-c/0.13.1
5 links created for /usr/local/Cellar/json-c/0.12
```