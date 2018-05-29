####作业：简单粒子制作
- 按参考资源要求，制作一个粒子系统，参考资源

  如同参考设置生成3个粒子系统，一个为光源，一个为光晕，一个为星光。
  光源不能动，speed设置为0，光晕也不能动，只是动态生成与消失，而星光可以动。
  光源作为光晕和星光的载体。设置其余变量即可。
  
  - 基本属性
    粒子系统组件，设置粒子的大小，速度，消失时间等等。
    shape决定粒子发散的形状。
    renderer决定轨迹的图像等其他属性。
  
  设置图如下：

- 使用 3.3 节介绍，用代码控制使之在不同场景下效果不一样

  代码如下：
  ```
  using System.Collections;
  using System.Collections.Generic;
  using UnityEngine;

  public class NewBehaviourScript : MonoBehaviour
  {

    public ParticleSystem temp;
    public int i = 0;

    void Update()
    {
        if (i % 4 == 0) {
            temp.startColor = Color.red;
        }
        else if (i % 4 == 1) {
            temp.startColor = Color.yellow;
        }
        else if (i % 4 == 2) {
            temp.startColor = Color.green;
        }
        else if (i % 4 == 3) {
            temp.startColor = Color.blue;
        }
        i++;
    }
}
  ```
