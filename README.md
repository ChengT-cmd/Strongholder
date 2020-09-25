
# Strongholder  
只用≤两个末影之眼找到我的世界要塞！不是作弊、命令！  
Find minecraft Stronghold  with only(or over) two ender-eye!NOT CHEATE!  
  
  ~~qwq Markdown有bug请忽略 懒得改了~~  
** 1.坐标 **

在数字上反映了玩家在主世界中的位置。坐标基于一个由三条交于一点（即原点）的坐标轴而形成的网格。玩家会出生在距离原点数百方块的位置上。x轴反映了玩家距离原点在东（+）西（-）方向上的距离；z轴反映了玩家距离原点在南（+）北（-）方向上的距离。（粘贴自wiki）。

** 2.调试屏幕 **

F3键呼出，显示区块缓存、内存使用、各种参数、玩家的当前坐标和当前游戏帧率图表（粘贴自wiki）。在“两点”法寻找要塞的过程中，我们需要关注调试屏幕中的三个数据：**X坐标①Z****坐标②**与**当前朝向****（****Facing****）**中的一个参数**③**。如下图所示：

![](https://attachment.mcbbs.net/forum/201806/16/105422b57pf5fzmzm249a0.png)

** 3.平面上两条非平行线交于一点 **

这是一个很直观的结论，事实上这是平行线定义的逆否命题。

在Minecraft中，_x_轴的正方向为正东方向，z轴的正方向为正南方向，而第二版块中**③**所表示的值（-180.0~180.0）表示一个角度，其以z轴正方向为始边，顺时针方向为正方向。基于以上原理，两次末影之眼确定要塞的原理大致如下图所示：

![](https://attachment.mcbbs.net/forum/201806/16/110507phyfslt477co7wta.png)

其中，**_A_点**与**_B_点**为末影之眼的抛出点，它们共同指向要塞**_S_点**。我们不难发现，如果这**两条直线不平行**，那么我们可以确定要塞的准确位置。下面，我们将来推导这一个要塞的坐标公式：（由于涉及到公式编辑，下只能用图片的形式展示）

![](https://attachment.mcbbs.net/forum/201806/16/113011f5d7ndw0mxwxjodi.jpg)

于是，_S_点的坐标得以导出，第二版块中的①，②，③分别对应式中的x，z，θ。

# 双击Stronghold.exe打开程序，为一个空白界面，接下来需要您输入数据。  
  
### __输入格式：__  
第一行为一个整数$n$，表示你要输入$n$个末影之眼的数据，请务必确保$n$不小于$2$且不大于$100$。  
接下来n行每行包括$3$个浮点数（小数），依次表示抛出点的$x$坐标，$z$坐标，以及朝向角度。  
  
输入完成后，程序会进行计算并输出，  
### __输出内容含义如下：__  
首先有至多$n*(n+1)/2$行，每行表示其中某两个末影之眼所解出的要塞坐标数据  
接下来有一个The final result is: 其后的$x$= ,$z$= 表示上述点的最小覆盖圆圆心，最后一行$r$=表示最小覆盖圆半径。  
同时在同目录自动保存一个名为“outputfile”的文本文档，输出时间以及控制台输出内容  
  
## __务必注意__  
1. $n$的取值一定是不小于$2$且不大于$100$的整数，否则将极易出现程序崩溃（程序中未在此处设置保护）。  
2. 请尽量确保输入数据中不要存在两个末影之眼数据的角度值相同（即平行），尽管程序已经写了保护代码。  
3. 本程序仍处于测试阶段，如您发现任何BUG请速与作者联系。  
  
### __JE样例输入：__  
```php  
4
-99.442 1028.999 118.2
-132.154 1112.965 129.0
-101.789 964.026 110.4
-165.525 874.021 99.3
```  
  
### __JE样例输出：__  
```php  
x=-503.171,z=812.522
x=-489.586,z=819.806
x=-498.074,z=816.649
x=-486.503,z=821.459
x=-493.562,z=820.303
x=-484.069,z=821.857

The final result is:
x=-493.620,z=817.189
r=10.631 
```  
  
### __BE样例输入：__  
```php
3
213.143 186.249 249.371 230.546
160.671 320.414 203.410 361.804
197.878 491.893 244.787 529.617
```  
  
### __BE样例输出：__  
```php
x=940.578,z=1075.704
x=972.749,z=1115.041
x=1022.559,z=1155.098

The final result is:
x=981.568,z=1115.401
r=57.062
```
  
### 以下操作可能导致**严重的误差**，请**务必**避免：  
1. 抛出的末影之眼中可能存在两个或更多指向不同要塞。这在程序中的表现为最小覆盖圆的半径可能很大，保证不同末影之眼的抛出点相距不太远即可；  
2. 抛出的末影之眼中可能存在两个或更多指向角度相同或极其接近。解决方法见下文的第一点。  
  
### 以下操作有助于**减小误差**：  
由于角度数据中，调试屏幕只保留了一位小数，而最大的误差往往来自于角度之差，因此要使角度之差尽量的大。  
1. 抛出一个末影之眼后，与其方向呈接近90度的一个锐角前进，在前进相同距离的情况下大体上可保证角度最大；  
2. 前进的距离可大致控制在80~180格，太小可能使角度差值不大，太大可能导致末影之眼指向不同的要塞；  
3. 多抛几个末影之眼，建议抛（不同位置）3~4个，由此定位的误差相对较小。  
  
到达理论点后：  
因为这只是一个大致位置，要塞可能在该点附近而不在该点上。因此可以向下挖后再向旁边挖挖。如果你愿意，也可以使用透视观察(服务器不要开挂awa~(2b2t当我没说))。

## 有关程序的重做    
源代码改于：[此处](https://www.mcbbs.net/forum.php?mod=viewthread&tid=799313)  
源程序作者：[此处](https://space.bilibili.com/166572139)
- [x]  $Π$精确到小数点后$50$位以上  
- [x] 优化旧算法、代码格式  
- [x] 优化程序格式   
- [x] 新增自动保存\[仅限Windows系统(包括JE和BE),未来将开发其他系统的版本\]  
- [x] 其他操作系统的版本（一代码多系统，但是失去所有颜色）
