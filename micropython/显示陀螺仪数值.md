# 液晶屏实时显示陀螺仪数值  

显示陀螺仪的六轴加速度值只需要使用简单的英文字符、数字和标点符号，所以我们可以使用fb.text这个函数显示字符串


我们已经在[液晶屏显示与编程](micropython/液晶屏显示与编程)一节中对framebuf这个库的使用有所了解，我们可以使用`fb.text`这个函数显示字符串(显示的只有ascII字符:亦就是一般的英文字母和数字以及常见的标点符号)
## 编写程序

在main.py文件中编写，首先导入所需要的显示模块framebuf，和陀螺仪mpu6050库。由于陀螺仪芯片是使用i2c接口和主芯片进行通信，我们还需导入pyb模块中的i2c的对象
 
```python
import mpu6050
import framebuf
from pyb import I2C
import pyb
import time

fbuf = bytearray(160*128*2)
fb = framebuf.FrameBuffer(fbuf, 160, 128, framebuf.RGB565) 
tft = pyb.SCREEN()

time.sleep(1)

i2c = I2C(1)
acc = mpu6050.accel(i2c)

while True: 
    # 每次循环刷新显示前都清空上一次的显示数据    
    fb.fill(0)
    # 分别获取3轴的加速度值  
    ac_x = str(acc.get_ac_x())
    ac_y = str(acc.get_ac_y())
    ac_z = str(acc.get_ac_z())
    # 将加速度值和需要用到的轴标记存入数组用于遍历
    ac_value = [ac_x, ac_y, ac_z]
    ac_ori = ['x:', 'y:', 'z:']
    
    for index in range(len(ac_value)):
        fb.text(ac_value[index], 65, 25*(index+1), 0x00ff00)
        fb.text(ac_ori[index], 40, 25*(index+1), 0x00ff00)
    # 最后刷新显示上面的预设
    tft.show(fb)
    time.sleep(0.1)
```