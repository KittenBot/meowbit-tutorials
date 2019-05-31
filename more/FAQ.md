# FAQ-常见问题与解答

`喵比特跟Micorbit有什么区别？`

喵比特是小喵科技推出的一款围绕编程游戏的主控板，它目前已经成为微软MakeCode Aracde平台的官方支持硬件。Arcade平台是目前少有的能使用图形化编程游戏的平台，在这个平台上我们可以体验自由度超高的游戏编程，并且在硬件上延续了microbit的程序烧录方式，使得新手也可以最快的速度上手并全新投入在游戏创作上。

`用常规的makecode可以控制喵bit么？`  

不可以，喵bit有特定版本的makecode，叫做makecode Arcade

`Micorbit的程序可以直接烧录到喵bit中么？`

不可以，虽然都是makecode编程，但是编程积木块都是稍有差别，不能做成通用的

`仿真模拟器区真的可以仿真吗？ `

是的，仿真模拟器区所见即所得

`什么时候出离线版本？`

可能要到6、7月份的样子，由微软官方制作离线版

`喵比特可以插到Robotbit或者IObit上使用吗？`

支持，插件地址
robotbit： https://github.com/KittenBot/meow-robotbit  
iobit： https://github.com/KittenBot/meow-iobit

`喵比特可以和能量魔块套件一起使用么？`  

支持，插件地址 https://github.com/KittenBot/meow-powerbrick

`在micropython模式下发现本该有的盘符莫名消失了，喵比特显得不太正常？`   

文件系统的进入方法:  

![](https://s2.ax1x.com/2019/05/30/VKr2lR.gif)



有一下几种情况请逐一排查：
- 当进入micropython模式时发现右上角红绿灯双闪一阵子，表明你的程序中存在错误，通过进入文件系统将mian.py文件删除，之后通过复位按键切换再回到micropython模式就能看到蓝色背景的hello micropython初始程序了  
- 当micropython程序显示正常或者并没有双闪，但却看不到盘符
    - 可能是USB线连接不良，试着换下口或线
    - 可能是内部的文件损坏了，需要进入文件系统,之后看到如下盘符并格式化盘符,操作如下： ![](https://s2.ax1x.com/2019/05/30/VKrR61.png ':no-zoom')![](https://s2.ax1x.com/2019/05/30/VKsVBV.png)  
    ![](https://s2.ax1x.com/2019/05/30/VKsBjI.png)   

    之后重新将进入micropython的.uf2文件保存进喵比特即可。   
