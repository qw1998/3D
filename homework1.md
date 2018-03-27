- 

> **游戏对象（GameObejct）是直接出现在游戏的场景中的组件，例如cube,UI,3d,2d都可以成为游戏对象，且显现在GameObject中，游戏对象可以有各种关系，比如子对象，基对象等。**
> 
> **资源（Asset）理论上是指所有unity可以利用的资源，包括游戏对象（GameObject），代码文件，文字，音频，各种可以在游戏中出现的内容都是资源。**
> 
> **游戏对象属于资源的一种，也可以说是资源组成的一部分，游戏对象是实体资源，是组件游戏框架的部件，而资源则不局限于此.**


- 
> **游戏对象目录存放场景的各种部件，部件之中有其子对象，游戏控制器也是游戏对象之一。**
> **资源目录具有各种资源的目录，例如：Scripts存放脚本代码，Prefabs存放预制，Textures/Icons图标，等等。**

- 代码及结果
```
// C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class NewBehaviourScript : MonoBehaviour
{
    void Awake()
    {
        Debug.Log("i'm Awaking");    
    }
    void Start()
    {
        Debug.Log("i'm Starting");
    }
    void Update()
    {
        Debug.Log("i'm Updating");
    }
    void FixedUpdate()
    {
        Debug.Log("i'm FixedUpdating");
    }
    void LateUpdate()
    {
        Debug.Log("i'm LateUpdating");
    }
    void OnGUI()
    {
        Debug.Log("i'm OnGUIing");
    }
    void OnDisable()
    {
        Debug.Log("i'm OnDisabling");
    }
    void OnEnable()
    {
        Debug.Log("i'm OnEnabling");
    }
}
```
![这里写图片描述](http://img.blog.csdn.net/20180327130223570?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXcxOTk4/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
大致为

**awake->onenable->start->fixedupdate->onGUI->update->lateupdate->ondisable**


- - GameObject unity视图中所有实例的基本类
  - Transform 一个对象的位置，角度和大小
  - Component 与游戏对象绑定的所有事物 
 - table对象的第一个选择框是activeSelf 属性，第二个文本框是对象名称，第三个选择框为static属性。第二行有Tag属性和Layer属性，第三行是prefabs(预设)属性。
 ![这里写图片描述](http://img.blog.csdn.net/20180327132153307?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXcxOTk4/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


- **static function Find (name : string) : GameObject**
 ```
 bool flag = GameObject.Find("table");
 if (flag) Debug.Log("find the table");
 else Debug.Log("not found");
 ```
 ![这里写图片描述](http://img.blog.csdn.net/20180327144806074?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXcxOTk4/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

  - public static GameObject CreatePrimitive(PrimitiveTypetype)

  - foreach (Transform child in transform) {
    Debug.Log(child.gameObject.name); }

  - foreach (Transform child in transform) { Destroy(child.gameObject); }

- - 预设相当于一个模板，可以生产相同属性的对象。
  - 预设和克隆都能产生出和原对象相同的对象。但对象克隆是复制原对象，复制后即与原对象无关，因此改变原对象不会对克隆出的对象产生影响。
  - 是一种树结构，它允许使用者递归地处理对象间的关系。

- 井字棋代码
```using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class NewBehaviourScript : MonoBehaviour
{
    private int[,] chess = new int[3, 3];
    private bool turn = true;
    private int count = 0;
    void Start()
    {
        reset();    
    }
    void OnGUI()
    {
        if (GUI.Button(new Rect(200, 50, 100, 30), "Reset")) reset();
        int result = check();
        if (result == 1) GUI.Label(new Rect(200, 25, 100, 100), "O win");
        else if (result == 2) GUI.Label(new Rect(200, 25, 100, 100), "X win");
        else if (result == 3) GUI.Label(new Rect(200, 10, 100, 100), "Draw, please reset");
        for (int i = 0; i < 3; ++i)
        {
            for (int j = 0; j < 3; ++j)
            {
                if (GUI.Button(new Rect(i * 50, j * 50, 50, 50),""))
                {
                    if (result == 4 && turn == true && chess[i, j] == 0)
                    {
                        chess[i, j] = 1;
                        count++;
                    }
                    else if (result == 4 && turn == false && chess[i ,j] == 0)
                    {
                        chess[i, j] = 2;
                        count++;
                    }
                    turn = !turn;
                }
                if (chess[i, j] == 1) GUI.Button(new Rect(i * 50, j * 50, 50, 50), "O");
                if (chess[i, j] == 2) GUI.Button(new Rect(i * 50, j * 50, 50, 50), "X");
            }
        }    
    }
    void reset()
    {
        turn = true;
        count = 0;
        for (int i = 0; i < 3; ++i)
        {
            for (int j = 0; j < 3; ++j)
            {
                chess[i,j] = 0;
            }
        }
    }
    int check()
    {
        for (int i = 0; i < 3; ++i)
        {
            // 纵向检查
            if (chess[0,i] != 0 && chess[0,i] == chess[1,i] && chess[1,i] == chess[2,i])
            {
                if (chess[0, i] == 1) return 1;
                else if (chess[0, i] == 2) return 2;
            }
            // 横向检查
            if (chess[i,0] != 0 && chess[i,0] == chess[i,1] && chess[i,1] == chess[i,2])
            {
                if (chess[i, 0] == 1) return 1;
                else if (chess[i, 0] == 2) return 2;
            }
        }
        // 斜向检查
        if (chess[1,1] != 0 && chess[0,0] == chess[1,1] && chess[1,1] == chess[2,2])
        {
            if (chess[1, 1] == 1) return 1;
            else if (chess[1, 1] == 2) return 2;
        }
        if (chess[1,1] != 0 && chess[0,2] == chess[1,1] && chess[1,1] == chess[2,0])
        {
            if (chess[1, 1] == 1) return 1;
            else if (chess[1,1] == 2) return 2;
        }
        // 平局
        if (count == 9) { return 3; }
        // 棋局未完
        return 4;
    }

}

```
