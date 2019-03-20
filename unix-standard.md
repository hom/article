## `C`语言标准

### `ANSI C`
**American National Standards Institute (ANSI)**

### `ISO C`
**International Organization for Standardization (ISO)**
 
### `POSIX C`可移植操作系统接口
**Portable Operating System Interface(POSIX)**
> 正式称呼为`IEEE Std 1003`

### `IEEE`电气电子工程师学会
**Institute of Electrical and Electronics Engineers(IEEE)**

## `C`标准函数库
### 头文件
- `ANSI C`共包括15个头文件
- 1995年`NA1`批准3个头文件：`iso646.h` `wchar.h` `wctype.h`
- `C99`增加6个头文件：`complex.h` `fenv.h` `inttypes.h` `stdbool.h` `stdint.h` `tgmath.h`
- `C11`增加5个头文件：`stdalign.h` `stdatomic.h` `stdnoreturn.h` `threads.h` `uchar.h`

### 按照标准定义的各个头文件将`ISO C`库分为29个区

头文件|说明|添加
-----|----|---
`<assert.h>`|验证程序断言
`<complex.h>`|复数算术运算支持|`C99`
`<ctype.h>`|自负分类和映射支持
`<errno.h>`|出错码
`<fenv.h>`|浮点环境|`C99`
`<float.h>`|浮点常量及特性
`<inttypes.h>`|整形格式转换|`C99`
`<iso646.h>`|赋值、关系及一元操作符宏|`NA1`
`<limits.h>`|实现常量
`<locale.h>`|本地化类别及定义
`<math.h>`|数学函数、类型声明及常量
`<setjmp.h>`|非局部`goto`
`<signal.h>`|信号
`<stdalign.h>`|用于查询和指定对象的数据结构对齐方式|`C11`
`<stdarg.h>`|可变长度参数表
`<stdatomic.h>`|对于线程之间共享数据的原子操作|`C11`
`<stdbool.h>`|布尔类型和值|`C99`
`<stddef.h>`|标准定义
`<stdint.h>`|整型|`C99`
`<stdio.h>`|标准`I/O`库
`<stdlib.h>`|实用函数
`<stdnoreturn.h>`|用于指定非返回函数。|`C11`
`<string.h>`|字符串操作
`<tgmath.h>`|通用类型数学宏
`<threads.h>`|定义用于管理多个线程以及互斥锁和条件变量的函数|`C11`
`<time.h>`|时间和日期
`<uchar.h>`|用于操作Unicode字符的类型和函数。|`C11`
`<wchar.h>`|扩充的多字节和宽字符支持|`NA1`
`<wctype.h>`|宽字符分类和映射支持|`NA1`

## `IEEE POSIX`标准库

### `POSIX`标准定义的必须的头文件

头文件|说明
-----|---
`<aio.h>`|异步`I/O`
`<cpio.h>`|`cpio`归档值
`<dirent.h>`|目录项
`<dlfcn.h>`|动态链接
`<fcntl.h>`|文件控制
`<fnmatch.h>`|文件名匹配类型
`<glob.h>`|路径名模式匹配与生成
`<grp.h>`|组文件
`<iconv.h>`|代码集变换实用程序
`<langinfo.h>`|语言类型与函数
`<monetary.h>`|货币类型与函数
`<netdb.h>`|网络数据库实例
`<nl_types.h>`|消息类
`<poll.h>`|投票函数
`<pthread.h>`|线程
`<pwd.h>`|口令文件
`<regex.h>`|正则表达式
`<sched.h>`|执行调度
`<semaphore.h>`|信号量
`<strings.h>`|字符串操作
`<tar.h>`|归档值
`<termios.h>`|终端`I/O`
`<unistd.h>`|符号常量
`<wordexp.h>`|字扩充类型
    |
`<arpa/inet.h>`|因特网定义
`<net/if.h>`|套接字本地接口
`<netinet/in.h>`|因特网地址族
`<netint/tcp.h>`|传输控制协议定义
    |
`<sys/mman.h>`|存储管理声明
`<sys/select.h>`|`select`函数
`<sys/socket.h>`|套接字接口
`<sys/stat.h>`|文件状态
`<sys/statvfs.h>`|文件系统信息
`<sys/times.h>`|进程时间
`<sys/types.h>`|基本系统数据类型
`<sys/un.h>`|`UNIX`域套接字声明
`<sys/utsname.h>`|系统名
`<sys/wait.h>`|进程控制

### 可选部分分为40个功能分区

#### `POSIX`定义的可选头文件

头文件|说明
-----|---
`<fmtmsg.h>`|消息显示结构
`<ftw.h>`|文件树漫游
`<libgen.h>`|路径名管理函数
`<ndbm.h>`|数据库操作
`<search.h>`|搜索表
`<syslog.h>`|系统出错日志记录
`<utmpx.h>`|用户账户数据库
    |
`<sys/ipc.h>`|`IPC`
`<sys/msg.h>`|`XSI`消息队列
`<sys/resource.h>`|资源操作
`<sys/sem.h>`|`XSI`信号量
`<sys/shm.h>`|`XSI`共享存储
`<sys/time.h>`|时间类型
`<sys/uio.h>`|矢量`I/O`操作

头文件|说明
-----|---
`<mqueue.h>`|消息队列
`<spawn.h>`|实时`spawn`接口

#### `POSIX`定义的可选接口组合选项码
选项码|符号常量|说明|`SUS`强制
-----|-------|---|-------
`ADV`|`_POSIX_ADVISORY_INFO`|建议性信息（实时）
`CPT`|`_POSIX_CPUTIME`|进程`CPU`时间时钟（实时）
`FSC`|`_POSIX_FSYNC`|文件同步|`*`
`IP6`|`_POSIX_IPV6`|`IPv6`接口
`ML`|`_POSIX_MEMLOCK`|进程存储区加锁（实时）
`MLR`|`_POSIX_MEMLOCK_RANG`|存储区域加锁（实时）
`MON`|`_POSIX_MONOTONIC_CLOCK`|单调时钟（实时）
`MSG`|`_POSIX_MESSAGE_PASSING`|消息传送（实时）
`MX`|`__STDC_IEC_559__`|`iec60559`浮点选项
`PIO`|`_POSIX_PRIORITIZED_IO`|优先输入和输出
`PS`|`_POSIX_PRIORITIZED_SCHEDULING`|进程调度（实时）
`RPI`|`_POSIX_THREAD_PRIO_INHERIT`|健壮的互斥量优先权继承（实时）
`RPP`|`_POSIX_THREAD_PRIO_PROTECT`|健壮的互斥量优先权保护（实时）
`SHM`|`_POSIX_SHARED_MEMORY_OBJECTS`|共享存储对象（实时）
`RS`|`_POSIX_RAW_SOCKETS`|原始套接字
`SIO`|`_POSIX_SYNCHRONIZED_IO`|同步输入和输出（实时）
`SPN`|`_POSIX_SPAWN`|产生（实时）
`SS`|`_POSIX_SPORADIC_SERVER`|进程阵发性服务器（实时）
    | 
`TCT`|`_POSIX_THREAD_CPUTIME`|线程`CPU`时间时钟（实时）
`TPI`|`_POSIX_THREAD_PRIO_INNERIT`|非健壮的互斥量优先权继承（实时）
`TPP`|`_POSIX_THREAD_PRIO_PROTECT`|非健壮的互斥量优先权保护（实时）
`TPS`|`_POSIX_THREAD_PRIORITY_SCHEDULING`|线程执行调度（实时）
`TSA`|`_POSIX_THREAD_ATTR_STACKADDR`|线程栈地址属性|`*`
`TSH`|`_POSIX_THREAD_PROCESS_SHARED`|线程进程共享同步|`*`
`TSP`|`_POSIX_THREAD_SPORADIC_SERVER`|线程阵发性服务器（实时）
`TSS`|`_POSIX_THREAD_ATTR_STACKSIZE`|线程栈长度属性|`*`
`TYM`|`_POSIX_TYPED_MEMORY_OBJECTS`|类型存储对象（实时）
`XSI`|`_XOPEN_UNIX`|`X/OPEN`扩充接口|`*`

## `SUS`
**单一`UNIX`规范(`Single UNIX Specification`)**是`POSIX.1`标准的一个超集。

