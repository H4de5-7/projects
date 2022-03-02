# JAVA实现的飞机大战小游戏-Asteroids game

Asteroids game

up: speed up

down: slow down

left: turn left

right: turn right

shift: flash

## 背景

这是大二上学期面向对象编程课（java）的大作业。当时是六个人一组（但是因为自己对这个课设挺感兴趣的，就自己一个人陆陆续续地写了快两周写完了），老师要求实现一个飞机大战的游戏，与https://freeasteroids.org/ 类似，就是传统的飞机射击陨石的游戏。

## 要求

初始会有一定数量的陨石，飞机靠射击陨石获得分数，一定时间内会出现UFO。飞机、陨石、UFO、子弹在屏幕边界处不会消失，而是出现在屏幕的另一边。按ESC会出现菜单。

#### 陨石

1、陨石要有大、中、小三种。大陨石被击毁后会生成中陨石，中陨石被击毁后会生成小陨石。

2、陨石随机方向、速度运动。

3、将当前的陨石都击毁后会进入下一关。

#### 飞机

1、飞机有三条命，被击毁后会重生，有一段时间的无敌状态。

2、按shift可以闪现到安全位置。

3、可以左转（左箭头）、右转（右箭头）、加速（上箭头）、减速（下箭头）、射击（空格）。

</br>
#### UFO

1、一段时间随机出现。

2、以随机方向、速度运动

3、会向四面八方发射子弹。

<br />
## 代码逻辑

由于老师上课讲图形界面实现的时候用的是swing和awt（有点学院派了），我也就顺着用了。

主体代码分为窗口、画布、飞机、陨石、UFO、子弹、碎片七部分：

#### 窗口

Window类为运行的main类，里面定义了窗口的大小等参数，添加了画布，并且让画布运行。

#### 画布

Picture实现了画布的功能，将每个对象画出来，并且通过刷新画布来实现各个对象的动作（如飞机的飞行等）。当时接触数据结构的时间比较短，用的是数组来实现多个对象的储存以及删除等操作。。。现在来看肯定是链表更适合。包括把闪现的操作写在画布上而不是飞机的类中现在看来也是挺离谱的。可吐槽的点太多了。。

画布中的action函数通过定时刷新画布来实现飞机飞行等动作。

#### 飞机

Me类实现了飞机的各种参数以及加速、减速、左转、右转、射击、重置等功能。

MeListener类实现了对键鼠的监听。

在监测到玩家按下开始键之后会执行画布的一系列初始化操作（这里的逻辑也有点奇怪，把画布的初始化操作写在了监听器里面，应该写在窗口里面的）。

hit函数用来判断飞机是否被击毁。

当时老师要求只能用线条来画出飞机，但其实用图片的话有给好的函数进行旋转等操作（还更丝滑）。结果后来发现好像大家都用的图片来表示飞机。。用线条画飞机的话更麻烦，旋转等操作需要考虑围绕中心重新定位的问题，当时和学长讨论了两三个小时才确定旋转的函数怎么写（数学没整明白）。

#### 陨石

asteroids类实现了小陨石的各种操作，asteroidsl实现了中陨石的操作，asteroidsm实现了大陨石的操作。

#### UFO

与飞机、陨石的实现类似。

#### 子弹

需要考虑子弹的类型、子弹的重置等操作。

#### 碎片

碎片是飞机、陨石、UFO被击毁之后产生的，一段时间便会消失。

# 总结

一些代码的逻辑很不成熟，看个乐呵就行，但是这是我自己完成的第一个项目，挺有纪念意义的。

如果对飞机操作久的话飞机会闪烁（不知道为什么），可以用shift闪现重置飞机（因为是重新new了个飞机）。

对象都是用线条画出来的，不是很好看，下面是游戏界面：

![游戏界面](https://img-blog.csdnimg.cn/0e0a29ad4431484e99513e1b3124bc18.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBASDRkZTU=,size_20,color_FFFFFF,t_70,g_se,x_16)

需要把名为background1.jpg的背景图放在代码目录下（需要做背景图的扩展），下面是我用的背景图。

![扩展后的背景图](https://img-blog.csdnimg.cn/6f69200a275849999ac0ef507b8ae5af.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBASDRkZTU=,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)
