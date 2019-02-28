```python
from pyb import Pin, ADC

adc = ADC(Pin('A0'))    #A0具有ADC功能 (ADC1_IN0)
adc.read()              #读取值，0~4095
```