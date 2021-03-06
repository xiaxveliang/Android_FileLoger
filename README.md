# Android 日志工具

最近项目开发中，遇到一个痛点：
项目模块较多，不同日志混合在一起；出现线上问题时，所有日志信息混合在一起，定位困难。
为解决这个问题，有了这个工具。这个工具有以下作用：

+ 开发模式
debug 为 true 时，打印在控制台，同时打印到文件；
+ 发版模式
debug 为 fase 时，只打印到文件；
+ 方便日志上传
支持日志压缩上传
+ 缓存文件 区分模块
支持不同功能模块，日志打印到不同文件中；

## 一、使用举例

+ 日志输出到控制台

![日志输出到控制台](https://raw.githubusercontent.com/xiaxveliang/StoryImage/master/小书匠/QQ20191205-154846.png)

+ 不同模块日志 分别打印到对应文件

![不同模块日志分别输出到对应文件](https://raw.githubusercontent.com/xiaxveliang/StoryImage/master/小书匠/QQ20191205-155239.png)

+ 对应文件中的日志

![对应文件中的日志](https://raw.githubusercontent.com/xiaxveliang/StoryImage/master/小书匠/QQ20191205-155253.png)

+ 压缩后的日志文件路径

![Screenshot_20191205_154950_com.huawei.hidisk](https://raw.githubusercontent.com/xiaxveliang/StoryImage/master/小书匠/Screenshot_20191205_154950_com.huawei.hidisk.jpg)


## 二、使用方式


+ 初始化
+ 打日志
+ 文件压缩上传


### 2.1、初始化

初始化建议放到Application中

``` java
    /**
     * 初始化日志
     */
    private void initLog() {
		// 这里网络模块、UI模块的Debug模式为true
        PalUiLog.init(MainApplication.this, true);
        PalNetLog.init(MainApplication.this, true);
    }
```

### 2.2、打日志


``` java
// UI模块日志：打印到控制台；同时打印到文件；
PalUiLog.d(TAG, "---onCreate---");
// 网络模块日志：打印到控制台；同时打印到文件；
PalNetLog.d(TAG, "---onCreate---");
```

### 2.3、文件压缩上传


``` java
	// 耗时操作，建议异步任务调用该方法
    private void zipLogFiles() {
		// 压缩App内部存储目录下的日志文件
        File file = ZipLogFile.zipLogFiles(MainActivity.this);
		// 若压缩成功，返回对应的文件
        if (file != null) {
            Toast.makeText(MainActivity.this, "日志文件生成成功：" + file.getAbsolutePath(),
                    Toast.LENGTH_LONG).show();
        }
    }
```

## 三、源码地址

[https://github.com/xiaxveliang/Android_FileLoger](https://github.com/xiaxveliang/Android_FileLoger)




