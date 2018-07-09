GIF：
![](https://github.com/qw1998/3D/blob/master/hw9/pic/20180709_084412.gif)
视频地址：https://v.youku.com/v_show/id_XMzcxMjUwODM0OA==.html?spm=a2hzp.8244740.0.0

P&D 过河游戏智能帮助实现，程序具体要求：
- 实现状态图的自动生成，如图
参考师兄博客的状态图
![](https://github.com/qw1998/3D/blob/master/hw9/pic/1.png)
- 讲解图数据在程序中的表示方法
在GUI，新增一个NEXT按钮，以实现智能。为了让上下船的动画能执行完整再继续下一步。NextStatus为枚举类型，上船ON，船移动MOVE，和下船OFF；
```
void OnGUI()
{
    canCount++;
    if (status == 2)
    {
        // ...
    }
    else if (status == 1)
    {
        // ...
    }
    else
    {
        if (GUI.Button(new Rect(Screen.width / 3 - 200, Screen.height / 2, 100, 50), "Next", buttonStyle))
        {
            action.setMovingObj(null);
            if (next == NextStatus.ON)
            {
                if (canCount < 60.0f)
                {
                    return;
                }
                canCount = 0;
                action.nextOnBoat();
                next = NextStatus.MOVE;
            }
            else if (next == NextStatus.MOVE)
            {
                if (canCount < 75.0f)
                {
                    return;
                }
                canCount = 0;
                action.moveBoat();
                next = NextStatus.OFF;
            }
            else if (next == NextStatus.OFF)
            {
                if (canCount < 90.0f)
                {
                    return;
                }
                canCount = 0;
                action.nextOffBoat();
                next = NextStatus.ON;
            }
        }
    }
}
```
实现上船的函数，设置一个Boattatus枚举变量，有P, D, PP, DD, PD，决定了船上的角色，从而对应图中的状态分布。
```
public BoatStatus getNextBS()
    {
        BoatStatus status = new BoatStatus();
        int p = right_coast.getCount(true);
        int d = right_coast.getCount(false);
        if (boat.isRight())
        {
            p += boat.getCount(true);
            d += boat.getCount(false);
        }
        bool isRight = boat.isRight();

        // the right path
        if (p == 3 && d == 3 && isRight)
        {
            status = BoatStatus.PD;
        }
        else if (p == 2 && d == 2 && !isRight)
        {
            status = BoatStatus.P;
        }
        else if (p == 3 && d == 2 && isRight)
        {
            status = BoatStatus.DD;
        }
        else if (p == 3 && d == 0 && !isRight)
        {
            status = BoatStatus.D;
        }
        else if (p == 3 && d == 1 && isRight)
        {
            status = BoatStatus.PP;
        }
        else if (p == 1 && d == 1 && !isRight)
        {
            status = BoatStatus.PD;
        }
        else if (p == 2 && d == 2 && isRight)
        {
            status = BoatStatus.PP;
        }
        else if (p == 0 && d == 2 && !isRight)
        {
            status = BoatStatus.D;
        }
        else if (p == 0 && d == 3 && isRight)
        {
            status = BoatStatus.DD;
        }
        else if (p == 0 && d == 1 && !isRight)
        {
            status = BoatStatus.D;
        }
        else if (p == 0 && d == 2 && isRight)
        {
            status = BoatStatus.DD;
        }
        // the other status
        else if (p == 3 && d == 2 && !isRight)
        {
            status = BoatStatus.D;
        }
        else if (p == 3 && d == 1 && !isRight)
        {
            status = BoatStatus.DD;
        }

        return status;
    }
```
详细代码在code中
