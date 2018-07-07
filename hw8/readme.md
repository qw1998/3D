- 血条制作
  - IMGUI设计
    直接利用代码生成即可。
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class IMGUI : MonoBehaviour
{
    private Rect blood;//血条
    private float value;//代表当前血量
    void Start()
    {
        value = 100f;
        blood = new Rect(250, 100, 150, 20);
    }

    // Update is called once per frame
    void OnGUI()
    {
        if (GUI.Button(new Rect(20, 20, 80, 40), "down"))
        {
            if (value >= 10)
            {
                value -= 10;
            }
            else
            {
                value = 0;

            }
        }
        if (GUI.Button(new Rect(20, 130, 80, 40), "up"))
        {
            value += 10;
        }
        GUI.HorizontalScrollbar(blood, 0.0f, value, 0.0f, 100f);
    }
}
```
结果如下：

  - UGUI设计
   新建对象canvas，书写代码将摄像机与之相绑定。将Silder中的Silder部分如下设置，
   然后在Fill Area中设置血条颜色，最后设置两个按钮的颜色，大小等等如下图。
   最后结果如下：
   
   
