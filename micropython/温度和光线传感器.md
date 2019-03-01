# 光线/温度传感器   

喵bit上还有一颗光线传感器和温度传感器，可以用于检测环境光强和温度。这两个传感器都基于读取外部模拟值电平实现。

## 读取光线和温度传感器ADC值

我们首先先初始化ADC对象，之后调用read函数返回电压值。注意喵bit的adc是12位的，也就是adc原始值范围是0~4095。

```python
from pyb import ADC, Pin

adc = ADC(Pin('LIGHT'))
adc.read()
```

同样道理将LIGHT换成TEMP引脚，大家可以将下面代码敲到repl中，看看温度传感器的原始值

```python
from pyb import ADC, Pin

adc = ADC(Pin('TEMP'))
adc.read()
```

返回值如下：

	>>> adc.read()
	2199

但是怎么和温度关联起来呢？


**温度传感器**

喵bit上面的温度传感器实际上是一颗热敏电阻，它随着温度变化会改变自身的电阻值大小，进而分的电压也不同。具体还需要涉及选型和温度曲线的标定等等知识，这里就不再详述了，代码里面都有。大家直接在根目录下创建一个thm.py文件，将项目的驱动代码复制到里面就行了：

```python
import math

def adc2temp(adcValue, res=10000, beta=3300, norm=25.0, normread=10000, zero=273.5):
	sensor = 4096.0*res/adcValue - res
	value = (1.0 / ((math.log(sensor / normread) / beta) + (1.0 / (norm + zero)))) - zero
	return value
```

记得重启喵bit，之后重新打开终端：

我们使用刚刚的adc2temp函数对adc原始值做映射：

	>>> import thm
	>>> thm.adc2temp(adc.read())
	29.83557

!>注意：我们读的实际上板子上的温度，由于板子有各种原件和液晶屏的背光在发热，实际上比环境温度要高几度。
