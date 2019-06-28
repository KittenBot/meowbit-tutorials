# 实战游戏1 - Jumping Mateo
<div style="width:100%"><p style="color:rgba(158, 161, 202, 0.88);text-align:right;">by Adri314 in makecode forum</p></div> 

## 流程梳理  

![](./newimage/game_1.png)  

首先我并不打算让大家先体验，为的是能够从半知半解中逐渐掌握并加以思考才更符合实战学习。  

## 实操步骤    
**准备工作**  

本次实战中的积木块可以根据颜色在对应颜色的分栏中找到，唯一需要额外添加的是【动画】这个插件，在扩展中可以找到  
![](./newimage/game_0.png) 
![](./newimage/game_6.png) 

1. **绘制精灵形象**   

![](./newimage/game_2.png) 

2. **创建精灵物理属性 - 移动**   
【当游戏更新】积木块是常用积木块，它的功能就等同于一般的无限循环，于是此处我们的意图就是让以50px/s的速度只允许x轴移动精灵  
![](./newimage/game_3.png)  

3. **创建精灵物理属性 - 重力加速度**   
重力加速度作用在y轴用ay表示，设定数值为300(300px/s<sup>2</sup>)  
此时可以看到模拟器的小人一开始就‘嗖’一下掉下去了    
![](./newimage/game_4.png)  

4. **创建精灵物理属性 - 跳跃**  
在明白跳跃的原理前我们必须知道2个物理公式： 

<p style= text-align:center;>v<sup>2</sup> - v<sub>0</sub><sup>2</sup> = 2ax </p>  
<p style= text-align:center;>v = v<sub>0</sub> + at </p> 

他们分别属于知道3个条件中的2个求得剩下的一个。之前我们已经设定了重力加速度为300  

!> 屏幕左上角为坐标(0,0) 

于是我们一直了a = 300，


