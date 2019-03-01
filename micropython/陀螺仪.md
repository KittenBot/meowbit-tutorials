# 陀螺仪  

喵bit上还板载了在创客项目中非常常见的6轴陀螺仪和加速度计mpu6050，理论上我们甚至可以diy一个平衡小车或无人机。

## 读取陀螺仪数据

回到mu的终端repl，我们首先要导入mpu6050的库。由于陀螺仪芯片是使用i2c接口和主芯片进行通信，我们还需导入i2c的对象。

```python
	import mpu6050
	from pyb import I2C, Pin
	
	i2c = I2C(1)
	acc = mpu6050.accel(i2c) #实例化accel类
	
	acc.get_values()	#调用方法，返回一次全部数值
```

大家可以在终端中多执行几次`acc.get_values()`这个命令。

---

?>方法 accel.get_ac_x() 

获取x轴的陀螺仪数值 

?>方法 accel.get_ac_y()  

获取y轴的陀螺仪数值 

?>方法 accel.get_ac_z()  

获取z轴的陀螺仪数值 

?>方法 accel.get_g_x()  

获取x轴的重力加速度

?>方法 accel.get_g_x()  

获取y轴的重力加速度

?> 方法 accel.get_g_x()  

获取z轴的重力加速度  

?>方法 accel.get_values()  

测试用