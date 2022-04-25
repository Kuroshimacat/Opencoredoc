---
description: 请在必须时进行操作
---

# 解决KASLR slide值和内存白名单

如果你遇到了内存上的问题，比如：

```
Error allocating 0x1197b pages at 0x0000000017a80000 alloc type 2
Couldn't allocate runtime area
```

或者其他的问题，那么首先启用`DevirtualiseMmio`，也可以看看这里来检查其他的[选项](https://dortania.github.io/OpenCore-Install-Guide/extras/kaslr-fix.html#and-who-is-this-info-for)，如果你懂英语的话。

随后你如果还是遇到了问题，那么我们要开始尝试silde值了。

## KASLR silde

首先打开你的Opencore编辑器，Tools加入OpenShell，重启后打开，输入`memmap`。你会看到一大堆输出，我们只需要Available后的Start内的内容，整理好，找到最大的值，随后打开十六位计算器，用Start值比200000，忽略小数，再+1，最后转换十六进制为十进制，但如果大于256，那么就尝试较小的一个值，直到得到一个合理的值，加入到`boot-args`，类似于：`silde=121`

## 内存白名单
