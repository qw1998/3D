效果GIF：
![image](https://github.com/qw1998/3D/blob/master/hw6/PNG/20180707_174149.gif)

- 游戏设计要求：
  - 创建一个地图和若干巡逻兵(使用动画)；
  - 每个巡逻兵走一个3~5个边的凸多边型，位置数据是相对地址。即每次确定下一个目标位置，用自己当前位置为原点计算；
  - 巡逻兵碰撞到障碍物，则会自动选下一个点为目标；
  - 巡逻兵在设定范围内感知到玩家，会自动追击玩家；
  - 失去玩家目标后，继续巡逻；
  - 计分：玩家每次甩掉一个巡逻兵计一分，与巡逻兵碰撞游戏结束；

- 场景的搭建，设计plane,cube,通过material的颜色装饰，拼接地图，地图如下：
![](https://github.com/qw1998/3D/blob/master/hw6/PNG/1.png)

- 状态机配置，人物状态均为下载内容，在asserts中下载即用，如图：
![](https://github.com/qw1998/3D/blob/master/hw6/PNG/2.png)
![](https://github.com/qw1998/3D/blob/master/hw6/PNG/3.png)

- 分别编写如下代码
  - Action
  - ActorController
  - Director
  - PActionManager （控制巡逻兵，挂载在每个巡逻兵上）
  - Factory （巡逻兵工厂，本次游戏只产生一次巡逻兵）
  - Recorder （记录分数）
  - Singleton （单例）
  - SceneController
  - UserGUI
