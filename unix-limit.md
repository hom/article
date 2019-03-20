## `UNIX`系统的实现需要定义一些限制

- 编译时限制(头文件)
- 与文件或目录无关的运行时限制(`sysconf` 函数)  
- 与文件或目录有关的运行时限制(`pathconf`、`fpathconf` 函数)

## `ISO C`限制

> `ISO C`定义的编译时限制都在头文件`<limits.h>`中

名称|说明|可接受的最小值|典型值|二进制
---|----|------------|-----|-----
`CHAR_BIT`|`char` 的位数|8|8|`2^8`
`CHAR_MAX`|`char` 的最大值|127|127|`2^7-1`
`CHAR_MIN`|`char` 的最小值|-128|-128|`-2^7`
`SCHAR_MAX`|`signed char` 的最大值|127|127|`2^7-1`
`SCHAR_MIN`|`signed char` 的最小值|-127|-128|`-2^7`
`UCHAR_MAX`|`unsigned char` 的最大值|255|255|`2^8-1`
||||
`INT_MAX`|`int` 的最大值|32,767|2,147,483,647|`2^31-1`
`INT_MIN`|`int` 的最小值|-32,767|-2,147,483,648|`-2^31`
`UINT_MAX`|`unsigned int` 的最大值|65,535|4,294,967,295|`2^32-1`
||||
`SHRT_MAX`|`short short` 的最大值|32,767|32,767|`2^15-1`
`SHRT_MIN`|`short short` 的最小值|-32767|-32768|`-2^15`
`USHRT_MAX`|`unsigned short` 的最大值|65535|65535|`2^16-1`
||||
`LONG_MAX`|`long` 的最大值|2,147,483,647|2,147,483,647|`2^31-1`
`LONG_MIN`|`long` 的最小值|-2,147,483,647|2,147,483,648|`-2^31`
`ULONG_MAX`|`unsigned long` 的最大值|4,294,967,295|4,294,967,295|`2^32-1`
||||
`LLONG_MAX`|`long long` 的最大值|9,223,372,036,854,775,807|9,223,372,036,854,775,807|`2^63-1`
`LLONG_MIN`|`long long` 的最小值|-9,223,372,036,854,775,807|9,223,372,036,854,775,808|`-2^63`
`ULLONG_MAX`|`unsigned long long` 的最大值|18,446,744,073,709,551,615|18,446,744,073,709,551,615|`2^64-1`
||||
`MB_LEN_MAX`|在一个多字节字符常量中的最大字节数|1|6|

### 不同平台中的`ISO`限制
> 该限制位于`<stdio.h>`中

限制|说明|FreeBSD|Linux|MacOS|Solaris|POSIX.1名称|POSIX.1中大小
----|---|------|------|-----|-------|----------|--------------
`FOPEN_MAX`|可同时打开的标准`I/O`流个数||16|||`_POSIX_STREAM_MAX`|8
`TMP_MAX`|`tmpnam` 函数产生的唯一文件名的最大个数||238,328
`FILENAME_MAX`|避免使用该常量||4096|||`_POSIX_NAME_MAX` `_POSIX_FILE_MAX`|`14`, `256`

## `POSIX`限制

### `POSIX.1`中与接口有关的限制分为7类
1. 数值限制：`LONG_BIT` `SSIZE_MAX` `WORD_BIT`
2. 最小值:下表中25个常量
3. 最大值：`_POSIX_CLOCKRES_MIN`
4. 运行时可以增加的值：`CHARCLASS_NAME_MAX` `COLL_WEIGHTS_MAX` `LINE_MAX` `NGROUPS_MAX` `RE_DUP_MAX`
5. 运行时不变值：下表中17个常量
6. 其他不变值：`NL_ARGMAX` `ML_MSGMAX` `NL_SETMAX` `NL_TEXTMAX`
7. 路径名可变值：`FILESIZEBITS` `LINK_MAX` `MAX_CANON` `MAX_INPUT` `NAME_MAX` `PATH_MAX` `PIPE_BUF` `SYMLINK_MAX`

### `<limits.h>`中`POSIX.1`的不变最小值

名称|说明：最小可接受值|值
---|---------------|---
`_POSIX_ARG_MAX`|exec函数的参数长度|4096
`_POSIX_CHILD_MAX`|每个实际用户ID的子进程数|25
`_POSIX_DELAYTIMER_MAX`|定时器最大超限运行次数|32
`_POSIX_HOST_NAME_MAX`|gethostname函数返回的主机名长度|255
`_POSIX_LINK_MAX`|至一个文件的链接数|8
`_POSIX_LOGIN_NAME_MAX`|登录名的长度|9
`_POSIX_MAX_CANON`|终端规范输入队列的字节数|255
`_POSIX_MAX_INPUT`|终端输入队列的可用空间|255
`_POSIX_NAME_MAX`|文件名中的字节数，包括null字节|14
`_POSIX_NGROUPS_MAX`|每个进程同时添加的组ID数|8
`_POSIX_OPEN_MAX`|每个进程的打开文件数|20
`_POSIX_PATH_MAX`|路径名中的字节数，包括null字节|256
`_POSIX_PIPE_BUF`|能原子的写到一个管道中的字节数|512
`_POSIX_RE_DUP_MAX`|基本正则表达式重复发生次数|255
`_POSIX_RTSIG_MAX`|为应用预留的实时信号编号个数|8
`_POSIX_SEM_NSEMS_MAX`|一个进程可以同时使用的信号量个数|256
`_POSIX_SEM_VALUE_MAX`|信号量可持有的值|32,767
`_POSIX_SIGQUEUE_MAX`|一个劲乘客发送和挂起的排队信号的个数|32
`_POSIX_SSIZE_MAX`|ssize_t对象的值|32,767
`_POSIX_STREAM_MAX`|一个进程能同时打开的标准I/O流数|8
`_POSIX_SYMLINK_MAX`|符号链接中的字节数|255
`_POSIX_SYMLOOP_MAX`|在解析路径名时可遍历的符号链接数|8
`_POSIX_TIMER_MAX`|每个进程的定时器数|32
`_POSIX_TTY_NAME_MAX`|终端设备名长度包括null字节|9
`_POSIX_TZNAME_MAX`|时区名字长度|
