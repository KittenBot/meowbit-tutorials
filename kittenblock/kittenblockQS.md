# Kittenblock快速开始 

## 连接Meowbit 

将Meowbit通过USB与电脑连接后，Meowbit的屏幕应显示如下界面（我们就称之bootloader界面）  

![](https://s2.ax1x.com/2019/08/23/mDeQjs.jpg ':no-zoom')  

!>如果不是这个界面，则检查一下Meowbit头上的电源开关是否打开(置向左边),或者USB连接是否稳定。  
`请注意`屏幕中的版本号应为v2.7.5以上，若不是请点击跳转到更新bootloader [更新](more/upgrade) 

此时，我们可以看到电脑中出现一个新的盘符，这表示Meowbit已经成功和电脑连接了  

![](https://s2.ax1x.com/2019/08/23/mDe8H0.png ':no-zoom')    

## kittenblock中连接串口 

1. 打开Kittenblock软件(请确保软件为最新，若不是会有提示更新),选择Meowbit硬件  

![](https://s2.ax1x.com/2019/08/23/mDeYNT.png ':no-zoom')  

2. 选择好硬件后，确保硬件在bootloader界面，点击【恢复固件】后待进度条走完，不出意外Meowbit会黑屏(这是由于供执行的main.py内初始是没有代码的)  

![](https://s2.ax1x.com/2019/08/23/mDet4U.png ':no-zoom')   

随后可见电脑出现`PYBFLASH`字样的盘符,此时你已经成功进入micropython模式

![](https://s2.ax1x.com/2019/08/23/mDi2Of.png ':no-zoom')

!>如果它的名字是 *可移动磁盘*，则需要按1下右侧边上面第一颗按键（Reset键），返回到bootloader界面后，按住A键不放，同时再次按1下Reset键。此时可见盘符为PYBFLASH字样无误  

?>按住A键不放同时按下Reset键作用为清空Flash，让Meowbit回到初始状态，可用于一些出错卡住等情况。

3. 恢复固件后,Meowbit就进入到了Micropython模式，同时可以看到电脑正试图安装驱动，驱动安装成功后，在Kittenblock中就可查找到可连接的Meowbit了 

![](https://s2.ax1x.com/2019/08/23/mDea34.png ':no-zoom')  
![](https://s2.ax1x.com/2019/08/23/mDeUCF.png ':no-zoom')  

!>某些WIN7用户可能会出现驱动自动安装失败的问题，这类用户可以跳转到这里查看方法：[手动安装串口驱动](../micropython/micropython快速开始?id=安装串口驱动这一点win10或mac用户可以忽略)  

## 加载必要库到Meowbit  

Kittenblock串口成功连上后，我们需要加载必要的库到Meowbit中，否则Meowbit将无法成功调用某些方法.。  

1. 首先将Kittenblock切换成编程模式，打开插件安装目录  

![](https://s2.ax1x.com/2019/11/05/KzXJ1S.png ':no-zoom')  


2. 把这些库都发送到Meowbit的PYBFLASH盘符下  
 
![](https://s2.ax1x.com/2019/08/23/mDeDD1.png)   

## 模块简述 

`boot.py`是启动文件，一上电micropython会最优先执行这个文件，一般包括所有运行环境和库文件的初始化，它指定了当你开机后首先运行的是名字为main的.py程序 

`main.py`是用户的主程序，大家平时学习开发主要是编辑这个文件 

`buzz.py`这个是附加的蜂鸣器驱动库  

`mpu6050.py`这是六轴陀螺仪的驱动库，里面定义了可调用的一些函数 

`tft.py`这是彩屏显示的驱动库  

`turtle.py`这是海龟绘图的库  

## 开始编程前  

开始编程Meowbit，以下几个kittenblock的按钮功能需要明白：

- `恢复固件`是在线通信前提，使Meowbit处于工作模式   

- `Reset和Play`在线测试程序需先点击Reset再点击Play，但不需要每次Play都Reset，比如用了循环执行或main.py内有正在跑的程序，那就必须Reset  

- `上传`把程序下载到Meowbit，下载完程序后，可点击软件中的Reset或按两下Meowbit右侧的复位键复位程序才可运行   

- `Stop`终止当前运行的程序，效果和Reset差不多  

![](https://s2.ax1x.com/2019/11/05/KzXUmj.png)  

## 使用kittenblock编写你的第一个程序  

1. 如图搭建程序    

![](https://s2.ax1x.com/2019/11/05/KzXd7n.png ':no-zoom')  

!>图形化编程确保上图箭头处的勾勾是选上的，这样才可以将积木块实时转译成代码。如果你想直接写代码执行，可以将勾勾去掉 

2. 运行程序  

![](https://s2.ax1x.com/2019/11/05/KzXDhV.png ':no-zoom')  

电机play，当标志变为如下，则运行成功，若要停止或更换别的程序运行则需要再次点击这个按钮变为原本的play标志即可 

![](https://s2.ax1x.com/2019/11/05/KzXy1U.png ':no-zoom')  



!>点击`运行`是在线运行程序，相当于REPL的感觉，上面程序的现象是绿色LED灯循环亮灭。若需要脱机运行时，则点击旁边的`上传`。

## 注意事项  

- 在使用海龟绘图和彩屏显示等其他功能时，常常会涉及到屏幕像素xy坐标位置，屏幕像素体系如下图  
![](https://s2.ax1x.com/2019/08/23/mDeR8e.png ':no-zoom')  

- Meowbit要在kittenblock中编程必须是在micropython模式下，最好在间隔长时间不使用或者进入过Arcade编程模式，再次使用时请首先恢复固件  
