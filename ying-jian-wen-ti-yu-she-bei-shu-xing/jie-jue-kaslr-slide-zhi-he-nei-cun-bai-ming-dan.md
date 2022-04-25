---
description: 请在必须时进行操作
---

# 解决KASLR slide值和内存白名单

如果你遇到了内存上的问题，比如：



```
Error allocating 0x1197b pages at 0x0000000017a80000 alloc type 2
Couldn't allocate runtime area
```

或者其他的问题，那么首先启用`DevirtualiseMmio`，也可以看看这里来检查其他的[选项](https://dortania.github.io/OpenCore-Install-Guide/extras/kaslr-fix.html#and-who-is-this-info-for)，
