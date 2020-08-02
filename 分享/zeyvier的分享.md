# zeyvier的第一次分享

[TOC]



## 前言

**本次分享内容本身需结合我前面写的项目流程来食用**

[项目流程传送门](https://share.mubu.com/doc/3ArvCKpTB-x)

## 关于项目实现的一些想法

1. ### UNITY中用到的C#内容：

   总体而言，在我们只是初步的入门开始制作一个游戏的时候，我们的C#只需要吃透面向对象的这一个理念便足以，我们能想象到的大多数IDEA例如碰撞的判定，人物的移动等，UNITY的前浪工程师们已经帮助我们实现好了，所以当下，我们C#在学习完面向对象的操作后就可以放下了，关于写脚本，当下最主要的是去查找UNITY的官方API及其使用教程（这点类似于MATLAB的api以及文档，前浪们也认真的去写过，但这些文档基本是英文（读的时候全当练四级（逃）））。

2. ### UNITY编程中不太一样的点：

   在大家都熟悉的C和C++中，我们每一段代码都是程序的一部分，在C中，我们面向过程，面向程序本身进行编程，在C++中，我们面向对象编程，而在UNITY开发中，我们使用的是组件编程，我们没一段程序所针对的都是具体的组件本身，C++的编程类似于给你几个零件，让你从头开始造出一辆车，而UNITY有点类似于在UNITY的界面中，让你造出车的样子，在通过面向组件，对这辆车的各部分增加功能，我们只需要对对应的组件进行功能的开发即可，这点是和C++不同的，C++是从框架到细节都需要自己去造，UNITY则是已经给了你一个框架，让你往这个框架里添加功能，举个例子

   下面是一个控制小车前进以及转弯的实例：

   这是一个典型的UNITY脚本文件，这个脚本可以比较简单的说明UNITY编程的一些特点

   1. 组件化：这段代码所实现的是如何让一个GameObject动起来，而我们所需要注意的是这只是一个组件，我们将该组件拖拽到相应的物品上面，这个物品就会按照脚本里所说的方式实现相应的功能，与此相似的，我们可以创造出许多类似的组件，例如加速器，按下shift加速，跳跃器，按下空格完成跳跃。
   2. 依赖于UNITY内置的函数：我们可以看到：在该代码中，我们实现功能所依靠的主要是UNITY内置的函数，如Input获取我们的输入信息，使用Vector3来决定物体移动时候的方向以及一次走多少，使用transform.Translate控制物体的移动,使用translate.Rotate控制物体的旋转，这些复杂的函数不需要我们来实现，我们所需要做的则是组织起来这些函数到组件里。

   ```c#
   using System.Collections;
   using System.Collections.Generic;
   using UnityEngine;
   
   public class PlayController : MonoBehaviour
   {
       //Variable
       public float speed = 6f;
       public float turnspeed = 25f;
       public float horizontalInput;
       public float forwardInput;
       // Start is called before the first frame update
       void Start()
       {
           
       }
   
       // Update is called once per frame
       void Update()
       {
           //输入
           horizontalInput = Input.GetAxis("Horizontal");
           forwardInput = Input.GetAxis("Vertical");
           //前进
           transform.Translate(Vector3.forward*Time.deltaTime*forwardInput*turnspeed);
           //转弯
           transform.Rotate(Vector3.up * Time.deltaTime * horizontalInput*turnspeed);
       }
   }
   ```

   例子2：

   该脚本是一个控制摄像机跟随物体的功能，如图UNITY的万物都可添加组件，包括你的摄像机，也可以使用组件来进行操作，例如如果把实例1中的组件添加到摄像机上，则可以使摄像机移动。

   ```C#
   using System.Collections;
   using System.Collections.Generic;
   using UnityEngine;
   
   public class FollowPlayer : MonoBehaviour
   {
       public GameObject player; //有reference 所以必须要public
       public Vector3 offset = new Vector3(0, 10, -100);
       // Start is called before the first frame update
       void Start()
       {
           
       }
   
       // Update is called once per frame
       void Update()
       {
           transform.position = player.transform.position + offset;
           //transform.rotation = player.transform.rotation;
       }
   }
   ```

   

3. ### 我们接下来应该怎么学：

   1. 弄清楚基础的UNITY编程中的函数，如start，update等，这些基础的函数我们一定要搞清楚
   2. 学会使用UNITY官方的组件如碰撞器，触发器，刚体
   3. 学会查找API，查找所要使用的API来实现功能（课是难以看完的，我们需要有一点搞到哪个功能，就在UNITY reference里查API的好习惯）
   4. 教程方面，我最近发现了个宝藏教程  [create with code](https://learn.unity.com/course/create-with-code?uv=2018.4)
   5. 抽时间学一下unity里的画布系统，很多游戏按钮都需要这个东西

4. ### 团队合作

   1. 每周组内抽点时间做一到两次分享还是蛮重要的，不然大家就把这茬给忘记了

   2. 可以多写自己的心得以及学习记录并上传，巩固知识，并且可以让大家从你的知识来进步

   3. 由于UNITY的组件开发，分工比较容易，例如我们要做一个会动的人：可以一个人做这个人的移动组件，一个人做这个人跳跃组件，一个人做这个人的碰撞检测函数，一个人做这个人的触发函数。

      *最后编辑于 2020/7/21 zeyvier*
