# makecode分栏积木块介绍  

## 音乐  

### 声音  

?>控制内置音乐的播放及停止

![](image/block_1_1.png ':no-zoom')  

!>默认音量128（0~255）  
![](image/block_1_0.png ':no-zoom') 

### 音律  

**音律通过音调和节拍组成**

?>音调  

![](image/block_1_2.png ':no-zoom')    

---
?>节拍   

BPM是Beat Per Minute的简称，中文名为拍子数，释义为每分钟节拍数的单位  

![](image/block_1_3.png ':no-zoom')   

---
?>例子

按下B键播放一段惊心动魄的急促音效

![](image/block_1_4.png ':no-zoom')   


## 控制器  

?>一个积木块实现将精灵的移动联系到键盘的方向键。

![](image/block_2_0.png ':no-zoom') 

```javascript
function moveSprite(sprite: Sprite, vx: number = 100, vy: number = 100);//方法
controller.moveSprite(mySprite)

```

---
?>用于检测按键按下的两种方式  

![](image/block_2_1.png ':no-zoom') 

```javascript
Controller.A.onEvent(ControllerButtonEvent.Pressed, function(){}) //当按键A按下的事件
Controller.A.isPressed(); //检测按键A是否按下(返回:boolean)
```  
---  
?>用于单独控制
![](image/block_2_2.png ':no-zoom')   

```javascript  

```


