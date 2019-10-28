# 文件及文件目录操作 

microPython支持标准的Python的文件模块，可以使用open()这类原生函数

## 创建一个文件  

```python
"""
在当前路径下创建名为myFile的txt文件
w为只写模式，既若不存在该名称文件便创建，若存在则覆盖，想要不覆盖的只写，可选模式为a
模式不填的话默认为r，即只读
"""
f = open('myFile.txt', 'w')  
f.write('hello world!')
f.close()  # close()相当于关闭文件并保存文件,如果没有close(),写入的内容可能会存在缓冲区中,相当于你的操作就是失败的
```  

[想深入了解open()函数](https://www.runoob.com/python/file-methods.html) 

## 查看一个文件 

```python
f = open('myFile.txt')
f.read()
f.close()
```

## 文件夹操作

需要引入os模块 

```python
import os
os.getcwd() # 查看当前所在目录
os.listdir()  # 查看当前目录内的所有文件
os.mkdir('dir')  # dir为你想创建的目录名
os.chdir('dir')  # dir为当前目录的相对目录，必须要存在的。若os.chdir('..')则表示退回上级目录
os.remove('xx')  # xx为当前目录内存在的文件，需要带后缀格式如.txt
os.rmdir('dir')  # 可删除一个空目录，若非空则会抛出异常
```    

```python
# 删除非空文件夹  
import os

def delDir(name):
    os.chdir(name)
    for i in os.listdir():
        os.remove(i)
    os.chdir('..')
    os.rmdir(name)
    os.sync() 
```  

## 实操

1. 首先清空main.py   

![](https://s2.ax1x.com/2019/10/18/KeSWqK.png)   

2. 

