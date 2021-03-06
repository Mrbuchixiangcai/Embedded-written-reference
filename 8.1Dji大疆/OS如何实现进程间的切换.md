## OS 如何实现进程的切换

### 进程切换的三部分

​	![process_status.png](/OS/photo/process_status.png)

### OS如何实现进程间的切换

- a) 首先: OS 获取CPU的控制权
  - 协作方式: 当进程在进行系统调用是, 将CPU的控制权转交给OS
  - 非协作方式: 设置**定时器**中断，OS在控制中得到安全感
- b) 保存和恢复上下文切换
  - OS 为正在执行的进程**保存**一些寄存器的值;
  - 并为即将执行的进程**恢复**一些寄存器的值;
- c) 完成进程三部分内容的切换
  - 用户级上下文
    - 正文、数据、用户堆栈以及共享存储区；
  - 寄存器上下文
    - 通用寄存器、程序寄存器(IP)、处理器状态寄存器(EFLAGS)、栈指针(ESP)
  - 系统级上下文: 
    - 进程控制块task_struct、
    - 内存管理信息(mm_struct、vm_area_struct、pgd、pte)
    - 内核栈
