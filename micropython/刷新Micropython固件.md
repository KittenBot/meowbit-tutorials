
!>由于喵比特支持两种不同学习模式，分别是微软的Makecode平台和Micropython模式。因此在切换学习模式的时候需要重新刷入新的固件。

## 进入DFU模式

DFU在此可以理解为强制固件切换，要更换固件首先需要进到这个模式下。按住并保持喵比特侧方的DFU按键，紧接着插上usb数据线。

![](https://s2.ax1x.com/2019/01/26/knLsSI.jpg)

![](https://s2.ax1x.com/2019/01/26/knL0FH.gif ':no-zoom')

成功进入DFU模式后，在电脑设备管理器中会看到一个新的设备（这时候DFU按键就可以松开了），不同电脑显示名称有所区别，但是都会有STM32 xxxx的设备，比如：

![](https://s2.ax1x.com/2019/01/26/knLcOf.png ':no-zoom')  
  
## 刷新固件

!>如果你还不了解刷固件前的准备流程，建议先看  [刷入固件](parameter/01固件更新教程)  

如果你已经看过了上述教程，那么在DFU模式下可以直接点击micropython.bat进行刷新固件操作  
  
?>1.双击micropython.bat文件  

![](https://s2.ax1x.com/2019/01/29/kQPPc8.png)  

?>2.等待进度条过完提示可以继续以后既刷新成功  
  
![](https://s2.ax1x.com/2019/01/29/kQPu90.png)  
 
!>切忌在刷新未完成前中断或拔插USB，这会造成某些难以解决的错误  
  
?>3.刷新成功后请按喵bit顶部的复位按钮（或者拔掉喵bit的usb线并重新插上），如果一切正常大家可以看到电脑多了一个名为pybflash的u盘盘符,伺候便可以正常使用micropython模式编程了。

![](https://s2.ax1x.com/2019/01/29/kQYwxf.png)

