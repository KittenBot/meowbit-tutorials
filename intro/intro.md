# 喵比特简介 {docsify-ignore-all}

Meowbit(喵比特)是一款兼容Microbit金手指40PIN接口(既兼容市面上几乎所有的Microbit扩展板)的编程游戏机，用于学习makecode图形化编程与micropython编程。

## 硬件参数

- 主控板大小尺寸：52x76x12mm
- 主控芯片：STM32F401RET6,32位ARM Cortex M4内核
- USB充电电压：5V（电流1A或以上）
- 主控板最大输出电流：300MA
- 外部电池接口输入电压：3.7~4.2V

## 硬件资源

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


## 编程方式

`makecode图形化编程模式: Makecode平台`  
- 由微软推出的一款支持部分开源硬件的JS编程语言图形化编程平台(包括Microbit、Adafruit、Arcade等等)，而喵比特支持新推出的Arcade系列  

微软官方arcade编程平台：https://arcade.makecode.com    
喵家喵比特在线编程平台：http://meowbit.kittenbot.cn


`micropython编程模式: Mu editor/Kittenblock(基于Scratch3.0) `   

- MicroPython是Python3的精简实现，包括Python标准库的一小部分，并且经过优化，目的是可在硬件中高效运行。(同时python也是近年开始陆续在各地高考中开设考试科目的一门编程语言)  
  
micropython编程平台MU下载链接：http://cdn.kittenbot.cn/mu/Mu_1.0.1.exe


## 支持系统

Windows，macOS



