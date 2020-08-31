# 喵比特简介 {docsify-ignore-all}

- 喵比特是一款可图形化编程 适合STEAM教育的游戏掌机，游戏编程的自由度高，例如场景，角色形象以及剧情脚本均能够通过拖拽积木块和绘制的方式实现。
- 除开游戏编程的能力，喵比特自身是一块硬件主控板，能够像microbit那样实现硬件项目创作，由于自身带有彩屏，在创作的过程中可视程度更高。  


## 硬件参数

- 主控板大小尺寸：52x76x12mm
- 主控芯片：STM32F401RET6,32位ARM Cortex M4内核
- USB充电电压：5V（电流1A或以上）
- 主控板最大输出电流：300mA
- 外部电池接口输入电压：3.7~4.2V

## 入门须知 

`保护你的板子：`
- 接插USB的时候请尽量温柔一下，由于USB座子是通过焊接固定在板子上的，过于暴力或可导致板子下次使用无法被电脑识识别  
- 静电或短路极为可能损坏板子上的原件，所以建议日常使用均要确保硅胶保护套穿在它的身上  

`硬件资源：`  
![](https://s2.ax1x.com/2019/01/26/knIGbd.png)

![](https://s2.ax1x.com/2019/01/26/knId8f.png)

1. 充电/工作指示灯
2. 光敏传感器
3. 电源拨动开关
4. 可编程LED灯 x 2
5. 复位按键
6. DFU模式按键（用于刷固件切换编程模式、也用于makecode固件下调出菜单）
7. 160 x 128 tft彩屏
8. 温度传感器
9. 方向可编程按键 x 4
10. 可编程蜂鸣器
11. 可编程A、B按键
12. 兼容Microbit40PIN金手指接口
13. USB程序下载口
14. SD卡槽(存储程序、后续拓展蓝牙/wifi模块)
15. JacDac
16. 6轴陀螺仪和加速度计
17. 3.7V锂电池接口
18. 主控芯片
19. 默认烧录unicode字符表的2MByte的spi-flash
20. 签名栏


`供电方式：`
- 通过接插USB，USB的另一端可以是电脑或者充电宝，确保5V。
- 通过接插3.7V锂电包（PH2.0端子）。在该端口接插的电池电压必须不得超过4.2V或不低于3.0V  



## 引脚排布

![](https://s2.ax1x.com/2020/01/18/1Sbv9O.png)


## 编程方式

`形化游戏编程: Makecode Arcade`  

由微软推出的一款支持部分开源硬件的JS编程语言图形化编程平台(包括Microbit、Adafruit、Arcade等等)，而喵比特支持新推出的Arcade系列  

微软官方arcade编程平台：https://arcade.makecode.com    

`micropython代码编程: Mu editor`  

MicroPython是Python3的精简实现，包括Python标准库的一小部分，并且经过优化，目的是可在硬件中高效运行。(同时python也是近年开始陆续在各地高考中开设考试科目的一门编程语言)  
  
MU下载链接：http://cdn.kittenbot.cn/mu/Mu_1.0.1.exe  

`(基于Scratch3.0)图形化编程: Kittenblock` 

kittenblock是基于Scratch3.0的编程界面，对于有Scratch基础的人很亲切，本质上可以进行基于micropython的在线控制和离线程序上传  
  
Kittenblock下载链接：https://www.kittenbot.cn/kittenblock 

!> 对于想编游戏的小伙伴请选择Arcade


## 支持系统

Windows，macOS



