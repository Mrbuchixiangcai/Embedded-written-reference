## Linux字符驱动和块驱动模型

### 字符驱动和块驱动的区别

| 区别     | 字符驱动               | 块驱动                             |
| -------- | ---------------------- | ---------------------------------- |
| 硬件     | 鼠标、键盘、摄像头     | u盘，SD卡，磁盘                    |
| 数据提供 | 提供字符流数据         | 数据块(512byte)                    |
| 数据访问 | 顺序                   | 支持偏移访问过lessk                |
| 寻址方式 | 字符寻址               | 不支持字符寻址                     |
| 结构体   | cdev, file_opeartions  | gendisk, block_device_operation    |
| 函数     | open,close,read和write | 无读写的操作函数                   |
|          |                        | bio, request, request_queue 结构体 |

+ 符设备和块设备的区别：仅仅在于内核内部管理数据的方式，也就是内核及驱动程序之间的软件接口，而这些不同对用户来讲是透明的。
+ 在内核中，和字符驱动程序相比，块驱动程序具有完全不同的接口。

### 字符设备驱动程序框架

1. 字符设备的注册
   + init函数注册设备，建立设备节点
   + 通过module_init宏来保证加载模块时会调用init函数。
2. 字符设备操作
   + 调用file_operation结构体的open、read、write函数
3. 总线模型和字符模型区别
   + probe函数跟init函数的区别
     + 使用平台总线模型时，才使用probe函数
   + 平台总线设备驱动模时
     + init函数只是向总线设备列表中添加了设备，
     + 当检测到相同名字的驱动程序，probe函数就会接着init函数的工作完成设备注册

### 块设备驱动系统架构：

![mtd_struct.png](https://github.com/quronghui/Embedded-written-reference/blob/master/OS/photo/mtd_struct.png)

