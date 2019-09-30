



---



layout: post
title:  linux中dup/dup2详解
date:   2019/9/30
categories: linux

tags: linux
---

* content
{:toc}
- ![](D:\linuxStudy\笔记\file.png)

![](D:\linuxStudy\笔记\file-1.png)

上面两张图就是介绍一下：

每个进程有一个进程表项，每个文件描述符就是当成文件指针啦，对应有个文件表项，说简单点，就是每个文件指针指向一个文件，这里就不多说了，详细了解：<https://blog.csdn.net/lk07828/article/details/52813372>

下面开始进入主题了

## dup

```
#include <unistd.h>
int dup(int oldfd);

返回值：
当复制成功是，返回最小的尚未被使用过的文件描述符，若有错误则返回-1
```

- 其实我理解的dup就是复制oldfd这个描述符，而这个返回的新的描述符和oldfd指向同一个文件表项，然后他们就可以一起共享这个表啦，就这么简单，下面我画了张图，看图简单点

  ![](D:\linuxStudy\笔记\dup.png)



## dup2

```
#include <unistd.h>
int dup2(int oldfd, int newfd);

返回值： 
若dup2调用成功则返回新的文件描述符，出错则返回-1. 
```

dup2与dup区别是dup2可以用参数newfd指定新文件描述符的数值。若参数newfd已经被程序使用，则系统就会将newfd所指的文件关闭，若newfd等于oldfd，则返回newfd,而不关闭newfd所指的文件。 这是复制的，简化了一点，哈哈





