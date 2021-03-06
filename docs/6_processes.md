## 1. 进程和程序

进程是一个执行中的程序的实例.一个程序可能被多个进程使用, 多个进程可以构成同一个程序. 一个进程是由内核定义的, 为了执行一个程序分配了系统资源的一个抽象实体.

从内核角度, 一个进程由用户内存空间构成, 这其中包含了程序代码和变量, 一系列关于进程状态的维护信息的内核数据结构. 内核数据结构记录的信息包含各种和进程有关的ID编号, 虚拟内存表, 打开的文件描述符表, 和信号发送和处理有关的信息, 进程资源使用和限制, 当前工作目录等信息.

## 2. 进程ID和父进程ID

## 3. 进程的内存布局

每一个进程的内存分配有很多部分组成, 通常成为段, 这些段包含以下几个方面:

- *text segment* 包含进程所运行程序的机器语言指令. 文本段是只读的所以进程不会被错误指针值偶然修改自身的指令. 可能有很多进程运行一个程序, 文本段是共享的, 因此一个程序代码的拷贝可以映射到所有进程的虚拟地址空间.
- *initialized data segment* 包含显示初始化的全局和静态变量, 这些变量的值在程序加载到内存中时从可执行文件读取.
- *uninitialized data segment* 包含未显示初始化的全局和静态变量. 程序开始前, 系统初始化这个段中所有内存为0. 由于历史原因, 通常叫做bss段, 从古老的汇编助记符"block started by symbol"继承来的一个名字. 将全局和静态变量从那些未初始化的段放到一个已初始化的单独的段的主要原因是, 当一个程序存储到磁盘上时, 不必分配空间到未初始化数据. 反之, 可执行程序紧急需要记录未初始化数据段所需的位置和大小, 该空间在运行时被程序分配.
- *stack* 栈是一个动态增长和收缩的包含栈帧的端. 一个栈帧分配一个函数. 一个栈帧存储函数的本地变量(自动变量), 参数和返回值.
- *heap* 堆是一个在运行时可以动态内存分配的区域. 堆顶叫做程序中断点.

## 4. 虚拟内存管理
