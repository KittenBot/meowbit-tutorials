```python
from pyb import SPI

spi = SPI(1)  #创建一个SPI对象，如果没有没有附加参数，则SP1对象创建但未初始化

SPI.init(SPI.MASTER, baudrate = 600000, polarity = 1, crc = 0x7) #(mode, baudrate=328125, *, prescaler, polarity=1, phase=0, bits=8, firstbit=SPI.MSB, ti=False, crc=None)

data = spi.send_recv(b'1234') #发送4个字节和接收4个字节
buf = bytearray(4)
spi.send_recv(b'1234', buf)   #发送4个字节和接收4个字节存储到buf
```