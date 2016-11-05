# Android  ABI和CPU的问题

1. 很多设备都支持多余一种的ABI。
2. 当一个应用安装在设备上，只有该设备支持的CPU架构对应的.so文件会被安装。

ABI目录（横向）和cpu（纵向） | armeabi | armeabi-v7a | arm64-v8a | mips | mips64 | x86 | x86_64 
--------- | ----------- | -------- | -------- | -------- | -------- | -------- | --------
ARMv5 | 支持 |  |
ARMv7 | 支持 | 支持 |
ARMv7 | 支持 | 支持 | 支持
MIPPS |  |  |  | 支持 |
MIPPS64 |  |  |  | 支持 | 支持 |
x86 | 支持 | 支持 |  |  |  | 支持 |
x86_64 | 支持 |  |  |  |  | 支持 | 支持 |
* <font color=red>注意：上表格中的空白部分，是我不知道它是否支持，极有可能是不支持</font>

* x86设备上，选择ABI的优先级:
	1. libs/x86目录中如果存在.so文件的话，会被安装
	2. 如果不存在，则会选择armeabi-v7a中的.so文件
	3. 如果也不存在，则选择armeabi目录中的.so文件
	4. x86设备能够很好的运行ARM类型函数库，但并不保证100%不发生crash，特别是对旧设备，因为是运行在x86设备上模拟arm的虚拟层上。


## 工具
1. 查看项目中ABI文件的架构类型，腾讯bugly，符号表工具，下载地址：http://bugly.qq.com/whitebook
2. Native Libs Monitor这个应用可以帮助我们理解手机上安装的APK用到了哪些.so文件，以及.so文件来源于哪些函数库或者框架。、


##疑难杂症
一、如果你的项目中，有其他优先级更高的ABI目录，但是你把ABI文件放到了优先级低的目录，则你的ABI文件无法被加载
二、如果你的项目中，ABI文件放在了，项目中优先级最高的ABI目录中（这个ABI目录是手机所支持的在项目中优先级最高的，但不一定是手机所支持的优先级最高的），则这个ABI文件，可以被加载，加载为ABI目录的所表示的架构类型。

例子：
我的手机cpu架构是ARMv7，项目中使用两个第三方SDK：企业A和企业B
企业A：ABI文件是armeabi-v7a，放进armeabi-v7a目录中。  企业B：ABI文件是armeabi-v5te，放进armeabi目录中。

解决办法：
1、使用同一优先级的ABI文件，ABI文件放入优先级相同的ABI目录
企业A：ABI文件是armeabi-v5te，放进armeabi目录中。  企业B：ABI文件是armeabi-v5te，放进armeabi目录中。  或  企业A：ABI文件是armeabi-v7a，放进armeabi-v7a目录中。  企业B：ABI文件是armeabi-v7a，放进armeabi-v7a目录中。
2、使用不同优先级的ABI文件，ABI文件放入优先级相同的ABI目录。一般情况不建议这么做。
企业A：ABI文件是armeabi-v7a，但是放进armeabi目录中。  企业B：ABI文件是armeabi-v5te，放进armeabi目录中。  或  企业A：ABI文件是armeabi-v7a，放进armeabi-v7a目录中。  企业B：ABI文件是armeabi-v5te，但是放进armeabi-v7a目录中。




