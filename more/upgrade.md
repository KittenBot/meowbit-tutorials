# 喵比特版本迭代

## bootloader迭代记录

下载地址：https://cdn.kittenbot.cn/meowbit/meowbit-flasher.uf2

2019.8.1 : v2.7.5<sup style="color:red" class="animated infinite flash">NEW</sup>   
* 版本特性：v2.7.5支持了Meowbit在kittenblock中的图形化编程，重写了底层库，使用学习起来更为方便了。  

对于还不了解kittenblock的小伙伴来说，简单介绍一下：
Kittenblock是喵家的自主基于Scratch3.0二次开发并创新的图形化编程软件，其中不但包含了对microbit，Arduino等开源硬件及自家的普片支持，独特的人工智能，由简单的语音识别朗读，翻译，到视屏侦测，视觉识别，天气预报，至轻量级机器学习，最后进阶到难度较高的TensorFlow足以让你由浅入深体验人工智能的魅力。而此时，kittenblock将正式支持Meowbit，让你手里的Meowbit结合其他硬件和酷炫的物联网和AI功能一并玩出新花样吧~  
`Kittenblock的下载地址为：` https://www.kittenbot.cn/kittenblock

!> 请注意，kittenblock中使用meowbit务必需要v2.7.5以上固件版本。固件版本号查看方式在篇尾。

----- 
 
2019.5.7 : v2.7.0  

2019.3.20 ：v2.3.6



## 喵比特的bootloader升级

每次增加新的功能，让喵比特支持更多东西以后，就需要对引导程序做一个升级新，而喵家程序猿已经将这个升级变得非常简单，没有多余的操作，你只需要在主界面下，将最新的bootloader.uf文件拖入MEOWBIT盘符下即可完成升级,未来每次更新我们都会通过迭代记录的方式告诉大家。

下面我们来详细介绍一下这简单的流程:

1. 下载新的bootloader.uf2(地址在上面，每次更新都使用同一个地址，请注意迭代记录)
 
2. 将bootloader.uf2拖入MEOWBIT盘符(有可能你的盘符不是meowbit，但请确保meowbit显示是主界面)

![](image/blup01.png)  

会出现如下界面，我们一定要选择最后一个Update并且按下按键A

![](image/blup02.png)  

之后会出现这个界面，提示需要按下reset按键，按下右侧上面的reset即可

![](image/blup04.png)   

成功后，就可以看到界面中间的版本号已经更新成最新的了。目前是v2.7.5哦

![](https://s2.ax1x.com/2019/05/07/EsiIPK.png)  

