# 游戏 

## 游戏内容  

假设你使用过microbit，那么你肯定明白【无限循环】是一个最基本的循环体函数，有了它你可以不断执行你想要的程序，或者在程序中不断地检测环境变量。而以下这两个积木块的功能则与【无限循环】十分相似，在Arcade的游戏编程中，我们将使用这两个积木块来代替【无限循环】使用。这两个积木块的区别是前者几乎是无时无刻在执行(更新频率由游戏引擎决定)，而后者则相当于定时器，每隔一定时间就执行一次。

![](https://s2.ax1x.com/2019/05/30/VMFhKU.png ':no-zoom')  

```javascript  
//a：需要运行的代码，period:希望间隔运行代码的时间(毫秒)
function onUpdate(a: () => void): void; 
function onUpdateInterval(period: number, a: () => void): void;

//当游戏更新这个积木块内部不断循环的内容为 
while (!gameOver) {
    checkInputs()
    gameUpdate()
    showGameUpdates()
}
```

`例子：` 

![](https://s2.ax1x.com/2019/05/30/VMkOFs.png ':no-zoom')  

---  
游戏结束积木块，它的作用是用于结束整个游戏循环,通过后面的加号，可以扩展可选参数(获胜、失败)

![](https://s2.ax1x.com/2019/05/30/VMASyT.png ':no-zoom')  

```javascript  
//win：可选true或false用于显示到屏幕上玩家获胜与否，effect?:游戏结束时在背景显示内置特效
function over(win: boolean = false, effect?: effects.BackgroundEffect);
```  

`例子：`  

![](https://s2.ax1x.com/2019/05/30/VMA8fI.png ':no-zoom')  
  
---      
得到一个自从游戏程序开始运行的时间(单位是ms)

![](https://s2.ax1x.com/2019/05/30/VMABkj.png ':no-zoom')  

```javascript
//number:记录从游戏开始以来的毫秒数  
function runtime(): number; 
```    

重置游戏，恢复如初，从on start内容开始再执行
  
![](https://s2.ax1x.com/2019/05/30/VMADts.png ':no-zoom')  

```javascript  
function reset();
```  

`例子：`    

自喵比特上电开始，不断在屏幕上显示累加时间(单位ms)，当按下按键A，时间又从0开始，这意味着硬件已经重置  
![](https://s2.ax1x.com/2019/05/30/VMExqU.png) 

---  

## 提示(询问)  

用于在屏幕中间显示标题和副标题

![](https://s2.ax1x.com/2019/05/30/VMVVsK.png ':no-zoom')   

```javascript  
//subtitle显示在title下一行，且只能显示小于8px，故无法显示中文
function splash(title: string, subtitle?: string);
```  

!>在未来的正式版中能够使用这个积木块显示多国语言，但技术难度较大目前还处于测试阶段

`例子：`  

显现积木块本身拥有2个参数，参数1是大标题，参数2默认是隐藏的，可通过加号调出。同样是字符串形式。按照例子通过字符串组合将数字变为字符串可以显示变量。  

![](https://s2.ax1x.com/2019/05/30/VMVhWR.png ':no-zoom')   

---  

该积木块返回一个逻辑值(Boolean)，与逻辑判断积木块结合使用，当触发积木块后，玩家按A返回true，按B则为false。

![](https://s2.ax1x.com/2019/05/30/VMZiTg.png ':no-zoom')  
  
```javascript  
function ask(title: string, subtitle?: string): boolean;  //如同显现积木块那样可以描述两行
// 返回一个boolean

```  
<!-- > [!NOTE|style:flat] -->
!>只能显示基本的ASCII码（英文，数字，简单符号）

`例子：` 

该例子所实现的效果是，当按下按键A，出现询问语句，如果此时按下按键A，则会出现循环4次的动态切换比卡丘图案。 

![](https://s2.ax1x.com/2019/05/30/VM8QYV.png)  

分享链接： https://makecode.com/_FpV3orcJu9fc

`理解上述例子需要明白如下几个知识点：`  

!>  1. 通过下面的项目分享链接理解该积木块  
https://makecode.com/_Edr1imiKrb9y    
![](https://s2.ax1x.com/2019/05/30/VMJC28.png)  
2.要将图案添加进数组，我们在数组分栏下直接拖拽出来包含着数字或字符串的数组是无法添加的，由于图案的数据类型既不是数字也非字符串，而数组的所有元素的类型必须是相同的。所以我们需要先通过剑符号 - 来删掉所有元素，再通过 + 来增加你需要添加元素等同数量的空位
![](https://s2.ax1x.com/2019/05/30/VMYTXD.png) 
3.数组的长度：如果你的数组内含有1个元素那么数组长度积木块则返回1，以此类推  
4.数组的索引从0开始，这是为了配合机器语言。如果你有3个元素，那么他们分别用list[0],list[1],list[2]  

---  
  
当运行到【提问】积木块，会进入可输入字符的界面，当你输入字符并选择了界面中的OK，会跳出该积木块，并且该积木块会返回你所输入的字符串。

![](https://s2.ax1x.com/2019/05/30/VMUN0e.png ':no-zoom')  

```javascript   
function askForString(message: string, answerLength = 12);  
//message:提问的问题(字符串)， answerLength：可让玩家输入的字符个数(默认不选为12)
//返回值为玩家输入的字符串
```


!>只能显示基本的ASCII码（英文，数字，简单符号）  


`例子：100内随机加法题`  

这个例子实现的过程细节为：当你输入了问题的答案后，提问积木块相当于就返回了你所输入的答案值，之后将这个答案值与准确答案对比，若相等则鼓励并得分+1，否则结束答题并看到得分

![](https://s2.ax1x.com/2019/05/30/VMwyX6.png)   

分享链接：https://makecode.com/_Ma5dF9Lkp7vf

---  

## 对话框  

对话框积木块，就是GBA游戏中最常见对话功能。而Arcade则允许你不单单能够制作这样一个对话框，而且能够自定义样式。  

![](https://s2.ax1x.com/2019/05/30/VMDqHK.png ':no-zoom')   

```javascript
//str:你设计好的对话内容，layout：有left、right、top、bottom、center、full screen六种位置选择。  
function showLongText(str: string, layout: DialogLayout);  
```  


可以通过这个例子分享链接来体验一下: https://makecode.com/_iD8686DYhK3r

