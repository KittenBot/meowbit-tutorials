# LED的使用

![](https://s2.ax1x.com/2019/01/29/kQgdW8.png  ':no-zoom')

喵bit的右上角有两颗可编程的led，从左数分别绿灯LED(1),和红灯LED（2）。控制LED虽说作为硬件入门是最基本的一个项目，但其在任何一个大型项目的实际交互过程中的地位都是及其重要的（想想，LED不同颜色，不同的闪烁频率所代表的含义已经深入日常生活呢）

## 控制LED的方法
    
    on()      # 点亮
    off()     # 熄灭 
    toggle()  # 切换

除了on()和off()能够分别控制LED亮灭外，LED对象还提供了一个toggle()方法  
用处是在现有的状态上取反。也就是说若目前LED(1)状态为on()，则执行toggle()后，LED(1)显示为off()状态


## 例1：DISCO效果

使用toggle()方法来控制板载的两颗LED灯实现一个炫酷的disco效果

    from pyb import LED 
    import time

    leds = [LED(i) for i in range(1, 3)]   
    # for i in range(1,3)意指i=1，i=2。如此leds = [LED(1),LED(2)]
    
    # 由于toggle()需要知道现在的状态从而切换，所以在程序开始时需要将全部LED状态先置为off()
    for l in leds: 
        l.off()
        
    n = 0
    while True:
        n = (n + 1) % 3   # 让n在0,1,2中切换
        if n == 3:        # 由于LED只有1,2两颗，所以为了方便理解，我们排除3(不排除其实也没有问题)
            n == 1   
        leds[n].toggle()    
        time.sleep(0.05)  # 延时0.05s
        n += n 

!>想知道自己写的程序是否有错误，推荐使用Mu提供检查功能

![](./image/led_02.png)  
  


