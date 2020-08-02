# zeyvier的第二次分享

---

### 前言：

​		这个礼拜我要裂开了嘤嘤嘤，学车+实验+复习+学UNITY，四倍的快乐。

### 关于大家都喜欢的UNITY

​		~~学不动力~~

上次分享了那个生成函数 

``` c#
Instantiate(gameObject,position,rotation) //也许拼的不对，不过VS自带有联想功能
```

这次来个：

1.更高级的移动方式

```c#
private Rigidbody playerRb;//刚体组件
void start(){
    playerRb = GetComponent<Rigidbody>();
}
void Update(){
        playerRb.AddForce(focalPoint.transform.forward * speed * forwardInput);
        //加力，这个东西就贼牛逼，贼顺滑
}
```

**2.如何进行脚本沟通**（重要）

```c#
//假设现在有一个类
public class playerController : MonoBehaviour
{
 	public bool gameover = true;
    void move(){
        transform.Translate(Vector.forward);
    }
    
}
//现在在另一个Script里面就可以
public class playerController : MonoBehaviour
{
 	public playerController gameObject;
    void start(){
        gameObject = GameObject.Find("player").GetComponent<playerController>(); 
    }
    void update(){
        if(gameObject.gameover){
            gameObject.move(); //这样的话，另一个对象就会移动
        }
    }
}
```

**3.画布系统**

这里不举例，就是说一波：使用这个系统，就能实现我们项目里面的各种按钮以及各种界面了，推荐一定要看一下。

[这个项目里面包含了我上面所说的画布系统](https://learn.unity.com/project/unit-5-user-interface?language=en&courseId=5cf96c41edbc2a2ca6e8810f)

4.碰撞器

就是两个东西如果碰到一块就发生点化学反应，e.g:

在这个里面，我们可以通过对比tag来判断碰撞的对象

```c#
private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Powerup"))//对比tag
        {
            hasPowerup = true;
            Destroy(other.gameObject);
            StartCoroutine(PowerupCountdownRoutine());
            powerupIndicator.gameObject.SetActive(true);
        }
    }
```

5.动画系统&特效系统&音乐系统

先放个教程https://learn.unity.com/project/unit-3-sound-and-effects?uv=2018.4&courseId=5cf96c41edbc2a2ca6e8810f

8.如何检测鼠标的神奇操作

基础 OnMouseDown

进阶 鼠标射线功能（我们主要用这个功能）（我现在还没完全搞懂）



