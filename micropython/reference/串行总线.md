```python
from pyb import UART 

uart = UART(6, 9600)   #使用USART6

uart.write('hello')
uart.read(5)  #最多读取5个字节
```