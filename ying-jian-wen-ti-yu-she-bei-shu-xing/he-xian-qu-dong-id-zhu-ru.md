# 核显驱动（id注入）

本篇不要求系统，理论上能够访问互联网和编辑文件即可。

## 两种方法

1. 直接用军刀注入
2. 手动写配置文件

显然，本文介绍第二种。

## 开始操作

### 确认你的显卡

首先搞清楚你的iGPU型号，比如我的就是`HD570`

### 解决AAPL,ig-platform-id explainer

在你的PciRoot(0x0)/Pci(0x2,0x0)的下方加入AAPL,ig-platform-id，类型是Data，然后爬去[这里](https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md)，找到你的显卡，找到帧缓冲器，会给你几个推荐选项，比如我是笔记本，那么我就选择`0x19160000`，然后拿出一张纸，先把`0x`去掉，变成`19160000`，再分割成`19 16 00 00`，再倒过来`00 00 16 19`，最后整合一下成为`00001619`，填充到那里即可：



| Key                 | Type | Value |
| ------------------- | ---- | ----- |
| AAPL,ig-platform-id | Data | #自己的值 |

### 解决device-id

加入device-id，类型依旧是Data，之后我们前去[这里](https://ark.intel.com/content/www/us/en/ark/products/77486/intel-core-i34150-processor-3m-cache-3-50-ghz.html)，搜索一下你的CPU，看看对应的显卡，最下面有一个设备id，拿出小本本，记好，我的是`0x191B`，你的位数可能跟我不一样，完全没关系，先去掉`0x`，又变成了`191B`，然后把他填充成八位数，缺几个加几个0，`0000191B`，再分割一下`00 00 19 1B`，最后换位置`1B190000`，扔进去，大功告成：



| Key       | Type | Value |
| --------- | ---- | ----- |
| device-id | Data | #自己的值 |

