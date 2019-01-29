## 进入dfu模式

!>喵比特出厂默认就是makecode固件，如果你只需要在makecode模式下使用可以暂时跳过并查阅下一章节 [Makecode模式须知](makecode/02喵bit版Makecode简介)  

如果你已经切换过micropython固件需要重新切回makecode，则跟随如下流程操作。  
  
DFU在此可以理解为强制固件切换，要更换固件首先需要进到这个模式下。按住并保持喵比特侧方的DFU按键，紧接着插上usb数据线。

![](https://s2.ax1x.com/2019/01/26/knLsSI.jpg)

![](https://s2.ax1x.com/2019/01/26/knL0FH.gif ':no-zoom')

成功进入DFU模式后，在电脑设备管理器中会看到一个新的设备（这时候DFU按键就可以松开了），不同电脑显示名称有所区别，但是都会有STM32 xxxx的设备，比如：

![](https://s2.ax1x.com/2019/01/26/knLcOf.png ':no-zoom')

## 刷新固件  
 
!>如果你还不了解刷固件前的准备流程，建议先看  [刷入固件](parameter/01固件更新教程)  
  
?>1.点击对应的makecode.bat刷入makecode模式的固件等待进图条过完即可  
  
![](https://s2.ax1x.com/2019/01/28/kK5bjO.png)  
  
?>2.之后按下喵bit侧边的复位按键  

![](https://s2.ax1x.com/2019/01/28/kKIAbQ.png ':no-zoom')

?>3.之后喵比特屏幕进入到如下界面，且电脑将会识别成U盘情况  

![](https://s2.ax1x.com/2019/01/28/kKI1rF.png ':no-zoom')  

![](https://s2.ax1x.com/2019/01/26/knOEAe.png ':no-zoom')  
  
!>通过复位按键来切换程序下载界面和程序执行界面，可以多按几次加深印象

