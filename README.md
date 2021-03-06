# PCB

## 一、PCB软件操作——Altium Designer

### 1、创建工程文件

#### ①创建原理图/PCB

文件&rarr;新建&rarr;原理图/PCB

#### ②创建原理图库/PCB元件库

文件&rarr;新建&rarr;库&rarr;原理图库/PCB元件库

#### ③总结：

一个完整的工程包括原理图+PCB+原理图库+PCB元件库，其中原理图库和PCB库可以不断积累，反复使用。

![工程文件](C:\Users\admin\Desktop\PCB作业\1.png)

### 2、原理图库的创建

①打开原理图库（.SchLib），修改初始元器件COMPONENT_1的名字为所制作元器件名字。

②通过绘制矩形、放置走线等绘制元器件。

![2](C:\Users\admin\Desktop\PCB作业\2.png)

### 3、PCB封装库的创建

①绘制封装图：根据相应元器件的数据手册，根据手册中的Pakage outline进行绘制封装图。

![3](C:\Users\admin\Desktop\PCB作业\3.png)

![4](C:\Users\admin\Desktop\PCB作业\4.png)

②添加封装：将画好的封装图导入到原理图库中对应的元器件。若多个元器件的封装图一样，可以根据Tools&rarr;Footprint Manager进行整体添加。

### 4、导入PCB

Design&rarr;Update PCB Document，检查错误，对显示出错误的元器件进行检查并修改，点击Execute Changes导入PCB。

**AD原理图导入到PCB文件中出现的常见错误：**

1、出现 unknow pin 报错
报错可能出现的问题：
1）没有封装
2）封装引脚的网络号缺失
3）管脚号不匹配（如：三极管PCB管脚定义的pin叫做A、B、C，而在原理图中定义的pin叫做1、2、3，这样会出现错误）
2、出现 footprint not found
问题：
1）原理图中的器件没有添加PCB的模型，故需要重新添加
**【”AD原理图导入到PCB文件中出现的常见错误“部分，来自原文链接：https://blog.csdn.net/lj1986817902/article/details/104730848】**

### 5、元件布局及布线

#### ①PCB布局——模块化布局

##### 1）确定PCB尺寸

需要对所选用的组件及各种插座的规格、尺寸、面积了解；对各部件的位置合理考虑，主要考虑电磁场兼容性、抗干扰角度，以及走线短、交叉少，电源、地的路径和去耦等方面。

**板框切割**：利用走线画出合适尺寸的板框后，Design&rarr;Board Shape&rarr;Define from selected objects。

##### **2）特殊部件布局**

尽可能缩短高频元器件之间的连线，减小它们之间的电磁干扰；元器件或导线之间有较高的电位差，应加大它们之间的距离，避免放电引起短路；超过15g的元器件应该用支架加以固定；<u>晶振尽量靠近IC，且布线要较粗，晶振外壳接地，每个IC的电源引脚旁要加旁路电容和滤波电容</u>。

##### 3）全部元器件布局——模块化布局

互相相关的器件放置的尽可能靠近，在抗噪声方面能够起到很好的效果。如时钟发生器、晶振和CPU的时钟输入端易产生噪音，可以放置的靠近一些；缩短高频元器件之间的连线；易受干扰的元器件不能互相离得太近，输入和输出器件尽量远离；易产生噪声的器件、小电流电路、大电流电路等应尽量远离逻辑电路。

以每个功能电路的核心组件为中心，围绕其进行布局。PCB上的元器件的放置顺序可以分为以下几步：

**第一步**——放置与结构有紧密配合的固定位置的元器件，如电源插座、指示灯、开关等，防止后用LOCK锁定，可以防止被误移动。

**第二步**——放置线路上的特殊组件和大的元器件。

**第三步**——同类型的元器件尽可能按照相同的的方向排列，便于贴装、焊接等，在PCB上组件均匀排放。

**第四步**——剩余组件的排列要充分考虑电磁干扰问题，各部件之间的引线要尽量短。

**TIPs：**

**交互式布局**：Tools&rarr;Cross select mode（PCB和原理图都要进行此操作，这样在原理图和PCB上才能进行交互操作）。

**软件内分屏**：Split Vertical。

#### ②PCB走线

1）输入/输出端用的导线尽量避免相邻平行；两相邻层的布线相互垂直；或在布线之间插一根零伏线。

2）PCB导线的最小宽度主要由导线和绝缘基板间的黏附强度和流过的电流决定；导线的最小间距由最坏情况下的 线间绝缘电阻和击穿电压决定。

3）PCB上的线宽不要突变，导线不突然拐角。

4)印刷电路中不允许有交叉电路，对于可能交叉的线条，可以用“钻”和“绕”解决。

5）阻抗高的布线尽量短，阻抗低的布线可以稍微长一些。

6）走线的走向呈线性，防止相互干扰。

**自动布线**：Route&rarr;Auto route&rarr;All

### 6、PCB表面敷铜（top和bottom层）

**敷铜的意义：**

**①**对于电源平面和地平面上的大面积敷铜，是为了降低电源平面和地平面的阻抗，加大走过的电流，减少损耗。

**②**对于高频高速信号走线进行敷铜，能够减少高速信号之间的串扰，起到了屏蔽的作用。例如晶振为高频发射源，因此在晶振附近进行敷铜就是这个道理。

**【”敷铜的意义“部分，来自原文链接：https://blog.csdn.net/weixin_40877615/article/details/93533043】**

**覆铜**：Place&rarr;多边形覆铜

## 二、实例（视频讲解）

原理图：

![5](C:\Users\admin\Desktop\PCB作业\5.png)

PCB图：

![6](C:\Users\admin\Desktop\PCB作业\6.png)

视频百度网盘链接：https://pan.baidu.com/s/1qb6KqdKL4dz_NTBk4dENBA         提取码：74b5 
