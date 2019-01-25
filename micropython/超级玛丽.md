# 编一段音乐

有了[蜂鸣器](micropython/蜂鸣器编程.md)的知识我们知道如何播放一个音符，那么要播一首曲子呢？首先我们要建立一个音符和频率对应的表格，在喵bit根目录下建立note.py文件，再将下面的内容复制进去：
```python
	# define frequency for each tone
	B0  = 31
	C1  = 33
	CS1 = 35
	D1  = 37
	DS1 = 39
	E1  = 41
	F1  = 44
	FS1 = 46
	G1  = 49
	GS1 = 52
	A1  = 55
	AS1 = 58
	B1  = 62
	C2  = 65
	CS2 = 69
	D2  = 73
	DS2 = 78
	E2  = 82
	F2  = 87
	FS2 = 93
	G2  = 98
	GS2 = 104
	A2  = 110
	AS2 = 117
	B2  = 123
	C3  = 131
	CS3 = 139
	D3  = 147
	DS3 = 156
	E3  = 165
	F3  = 175
	FS3 = 185
	G3  = 196
	GS3 = 208
	A3  = 220
	AS3 = 233
	B3  = 247
	C4  = 262
	CS4 = 277
	D4  = 294
	DS4 = 311
	E4  = 330
	F4  = 349
	FS4 = 370
	G4  = 392
	GS4 = 415
	A4  = 440
	AS4 = 466
	B4  = 494
	C5  = 523
	CS5 = 554
	D5  = 587
	DS5 = 622
	E5  = 659
	F5  = 698
	FS5 = 740
	G5  = 784
	GS5 = 831
	A5  = 880
	AS5 = 932
	B5  = 988
	C6  = 1047
	CS6 = 1109
	D6  = 1175
	DS6 = 1245
	E6  = 1319
	F6  = 1397
	FS6 = 1480
	G6  = 1568
	GS6 = 1661
	A6  = 1760
	AS6 = 1865
	B6  = 1976
	C7  = 2093
	CS7 = 2217
	D7  = 2349
	DS7 = 2489
	E7  = 2637
	F7  = 2794
	FS7 = 2960
	G7  = 3136
	GS7 = 3322
	A7  = 3520
	AS7 = 3729
	B7  = 3951
	C8  = 4186
	CS8 = 4435
	D8  = 4699
	DS8 = 4978
```  

这个音符表记录了所有的音符对应的频率。之后回到我们的main.py文件
  
```python
	from note import *
	from pyb import Pin, Timer

	buzz = Pin("BUZZ")
	tim = Timer(4, freq=3000)
	ch = tim.channel(3, Timer.PWM, pin=buzz)
	
	mario = [E7, E7, 0, E7, 0, C7, E7, 0, G7, 0, 0, 0, G6, 0, 0, 0, C7, 0, 0, G6, 0, 0, E6, 0, 0, A6, 0, B6, 0, AS6, A6, 0, G6, E7, 0, G7, A7, 0, F7, G7, 0, E7, 0,C7, D7, B6, 0, 0, C7, 0, 0, G6, 0, 0, E6, 0, 0, A6, 0, B6, 0, AS6, A6, 0, G6, E7, 0, G7, A7, 0, F7, G7, 0, E7, 0,C7, D7, B6, 0, 0]
	
	for i in mario:
	    if i == 0:
	        ch.pulse_width_percent(0)
	    else:
	        tim.freq(i) # change frequency for change tone
	        ch.pulse_width_percent(30)
	
	    pyb.delay(150)
```

前面第一部分是我们的蜂鸣器初始化代码，之后我们定义和播放马里奥的启动音乐~

将main.py保存，按下复位按钮，看看是不是喵bit现在还有欢迎音效了呢？

