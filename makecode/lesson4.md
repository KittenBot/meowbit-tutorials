# 第四节：跟踪游戏进度信息 {docsify-ignore-all}

`游戏信息`分栏中包含一些变量(数据属性)，允许我们进行修改。这些属性与得分、生命值和时间有关，更直观简洁地丰富我们的游戏体验，跟踪游戏进度等等。我们将快速了解如何在编程中将他们用起来增加游戏逻辑乐趣  

本节课我们对于游戏信息展开学习并完成如下目标

1. 了解`得分`和`生命值` 
2. 使用`倒计时`功能 
3. 完成一个按键小游戏    

## 要点1：有关游戏信息的积木块 

跟踪游戏信息的几个要素可能包括计时，生命值以及得分，这几点保证了游戏的竞技性和进阶性

我们首先来试试得分和生命值这两个功能的使用体现在游戏里的样子  

首先设置一个初始分数为0、生命值为2，观察一下模拟器的显示,生命值是以爱心的图案显示在左上角，而得分则是以数字形式显示在右上角
 
![](https://s2.ax1x.com/2019/02/18/k6qkfx.png)

## 要点2：关于倒计时
  
倒计时这个功能我们依然是先看看他在游戏屏幕上的体现，如图在原程序上加入按下按键A开始倒计时的功能，当我们按下模拟器的按键A，可以看到倒计时的数字显示在屏幕中上方并从设定值10开始减少  
  
![](https://s2.ax1x.com/2019/02/18/k6qV1K.png)
  
## 要点3：完成一个小游戏

?>这个小游戏的目的是挑战你的手速，我们设定一个10秒倒计时，在这10s内我们按下按键B的次数不能低于60次。
按下按键A开始游戏倒计时，此时我们快速点击按键B看到右上角的分数一直在加，当这个分数在倒计时结束时还未达到60则判断为lose并弹出提示框随之生命值扣1  
  
这个小游戏需要的额外知识有：
- `显现`
- `逻辑`
  
![](https://s2.ax1x.com/2019/02/18/k6qZ6O.png)  

```javascript
info.onCountdownEnd(function () {
    if (info.score() > 60) {
        info.changeLifeBy(1)
        game.splash("winner")
    } else {
        info.changeLifeBy(-1)
        game.splash("loser")
    }
    info.setScore(0)
    info.stopCountdown()
})
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    info.startCountdown(10)
})
controller.B.onEvent(ControllerButtonEvent.Pressed, function () {
    info.changeScoreBy(1)
})
info.setScore(0)
info.setLife(2)
```  

---

**这节课我们学到了什么？**
- 说一说如果只使用`得分`积木块而不使用变量来跟踪游戏中的状态所潜在的一个问题