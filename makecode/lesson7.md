# 第七节：精灵行走效果 {docsify-ignore-all}

前面章节学到的控制精灵移动的时候，精灵的图案一直都是静态不变的，这样缺少了动感，所以本节课我们来讲讲如何让精灵动态移动。为此我们有两种方法可供选择

?>本节课目标是使用现有的图像素材做一个能让精灵动态行走的程序  

为了完成目标我们由简入深来说这两种方式： 

1. 使用图像翻转(使用`水平翻转`图像积木块来做最粗糙的动态效果)
2. 使用`动画`插件来做更高级的动态效果

## 要点1：使用图像的'水平翻转'功能
  
`水平翻转`积木块在Advanced选项下的`图像`分栏里  
![](https://s2.ax1x.com/2019/02/18/k6Lrad.png)

举个简单的例子了解一下它的实际用处    
  
![](https://s2.ax1x.com/2019/02/18/k6LsIA.png)  
 
![](https://s2.ax1x.com/2019/02/18/k6LdKO.gif)  

## 要点2：动画插件
  
动画我们众所周知就是由帧组成的多张图片，在这些帧之间添加短而适当的延时，看起来就像真的动起来一样。并且帧数越多动作看起来越流畅  
  
首先我们添加动画这个插件，在扩展中叫做animation，添加后可以看到左侧分栏出现了一个`动画`  
   
![](https://s2.ax1x.com/2019/02/18/k6LUxK.gif)   

接着我们使用现成的图像来作为帧组成一个简单的向下行走的动画作为示范解读一下动画插件里积木块的用法。 

可以看出我们使用到的积木块只有上面4个，而且几乎是按顺序来用  
①. 首先是动画的创建，我们给动画去个名字，按照动画的方式比如向下走我们用down  
②. 有了容器，我们便可以往里面放东西了，这个东西就是你的动画所需要的图片帧，之前提到的动画由多个图片帧按照一定的延时间隔来实现的，而这个延时间隔就是①中积木块的最后一个参数。    
③. 好了，东西放完了，我们该觉得让哪个角色来使用这个动画，因为游戏中不同的精灵十分多，我们需要把动画指定给特定的精灵  
④. 有了动画，我们便可以选择是否使用，以及在什么情况下用。比如这里，我们选择的是当方向下按键被按下的时候就让这个动画使能(执行动画)  
 
![](https://s2.ax1x.com/2019/02/18/k6L6PI.png)  

![](https://s2.ax1x.com/2019/02/18/k6LDVH.gif)   

那么有同学可能好奇了，上面那个程序中最后一行，为什么需要呢，明明也没有进行4步的前3步呀

![](https://s2.ax1x.com/2019/02/18/k6L5ZQ.png)  
  
如果你将它去掉你可以发现，当你按下方向键下松开后，屏幕里的精灵还在不断重复动画效果。有时候我们希望做到的效果是我不按它不动我按了它才动。由于一个精灵对象只能被使能一种动画，而且动画一旦使能目前还不能自动关闭，所以需要给他一个空动画，这样便能够使其保持在松开按键那一刻的那个动画帧，但这么做任存在缺点，多往下走几次试试看能不能发现。  
  
## 完美主义的运动程序

新建一个项目，将下面程序代码复制到你的项目下试试看4个方向行走  

```javascript
enum SpriteKind {
    Player,
    Projectile,
    Food,
    Enemy
}
enum ActionKind {
    Walking,
    Idle,
    Jumping,
    down,
    up,
    stay,
    stay_up,
    stay_down,
    stay_left,
    stay_right,
    lefat,
    left,
    rigjt,
    right
}
let anim8: animation.Animation = null
let anim7: animation.Animation = null
let anim6: animation.Animation = null
let anim5: animation.Animation = null
let anim4: animation.Animation = null
let anim3: animation.Animation = null
let anim2: animation.Animation = null
let anim: animation.Animation = null
let direction = 0
let mySprite: Sprite = null
mySprite = sprites.create(img`
    . . . . . f f 4 4 f f . . . . .
    . . . . f 5 4 5 5 4 5 f . . . .
    . . . f e 4 5 5 5 5 4 e f . . .
    . . f b 3 e 4 4 4 4 e 3 b f . .
    . . f 3 3 3 3 3 3 3 3 3 3 f . .
    . f 3 3 e b 3 e e 3 b e 3 3 f .
    . f 3 3 f f e e e e f f 3 3 f .
    . f b b f b f e e f b f b b f .
    . f b b e 1 f 4 4 f 1 e b b f .
    f f b b f 4 4 4 4 4 4 f b b f f
    f b b f f f e e e e f f f b b f
    . f e e f b d d d d b f e e f .
    . . e 4 c d d d d d d c 4 e . .
    . . e f b d b d b d b b f e . .
    . . . f f 1 d 1 d 1 d f f . . .
    . . . . . f f b b f f . . . . .
`, SpriteKind.Player)
mySprite.setFlag(SpriteFlag.StayInScreen, true)
controller.moveSprite(mySprite)
direction = 0
anim = animation.createAnimation(ActionKind.down, 80)
anim2 = animation.createAnimation(ActionKind.up, 80)
anim3 = animation.createAnimation(ActionKind.left, 80)
anim4 = animation.createAnimation(ActionKind.right, 80)
anim5 = animation.createAnimation(ActionKind.stay_up, 80)
anim6 = animation.createAnimation(ActionKind.stay_down, 80)
anim7 = animation.createAnimation(ActionKind.stay_left, 80)
anim8 = animation.createAnimation(ActionKind.stay_right, 80)
anim.addAnimationFrame(img`
    . . . . . f f 4 4 f f . . . . .
    . . . . f 5 4 5 5 4 5 f . . . .
    . . . f e 4 5 5 5 5 4 e f . . .
    . . f b 3 e 4 4 4 4 e 3 b f . .
    . . f 3 3 3 3 3 3 3 3 3 3 f . .
    . f 3 3 e b 3 e e 3 b e 3 3 f .
    . f 3 3 f f e e e e f f 3 3 f .
    . f b b f b f e e f b f b b f .
    . f b b e 1 f 4 4 f 1 e b b f .
    f f b b f 4 4 4 4 4 4 f b b f f
    f b b f f f e e e e f f f b b f
    . f e e f b d d d d b f e e f .
    . . e 4 c d d d d d d c 4 e . .
    . . e f b d b d b d b b f e . .
    . . . f f 1 d 1 d 1 d f f . . .
    . . . . . f f b b f f . . . . .
`)
anim.addAnimationFrame(img`
    . . . . . . . f f . . . . . . .
    . . . . . f f 4 4 f f . . . . .
    . . . . f 5 4 5 5 4 5 f . . . .
    . . . f e 4 5 5 5 5 4 e f . . .
    . . f b 3 e 4 4 4 4 e 3 b f . .
    . f e 3 3 3 3 3 3 3 3 3 3 e f .
    . f 3 3 e b 3 e e 3 b e 3 3 f .
    . f b 3 f f e e e e f f 3 b f .
    f f b b f b f e e f b f b b f f
    f b b b e 1 f 4 4 f 1 e b b b f
    . f b b e e 4 4 4 4 4 f b b f .
    . . f 4 4 4 e d d d b f e f . .
    . . f e 4 4 e d d d d c 4 e . .
    . . . f e e d d b d b b f e . .
    . . . f f 1 d 1 d 1 1 f f . . .
    . . . . . f f f b b f . . . . .
`)
anim.addAnimationFrame(img`
    . . . . . f f 4 4 f f . . . . .
    . . . . f 5 4 5 5 4 5 f . . . .
    . . . f e 4 5 5 5 5 4 e f . . .
    . . f b 3 e 4 4 4 4 e 3 b f . .
    . . f 3 3 3 3 3 3 3 3 3 3 f . .
    . f 3 3 e b 3 e e 3 b e 3 3 f .
    . f 3 3 f f e e e e f f 3 3 f .
    . f b b f b f e e f b f b b f .
    . f b b e 1 f 4 4 f 1 e b b f .
    f f b b f 4 4 4 4 4 4 f b b f f
    f b b f f f e e e e f f f b b f
    . f e e f b d d d d b f e e f .
    . . e 4 c d d d d d d c 4 e . .
    . . e f b d b d b d b b f e . .
    . . . f f 1 d 1 d 1 d f f . . .
    . . . . . f f b b f f . . . . .
`)
anim.addAnimationFrame(img`
    . . . . . . . f f . . . . . . .
    . . . . . f f 4 4 f f . . . . .
    . . . . f 5 4 5 5 4 5 f . . . .
    . . . f e 4 5 5 5 5 4 e f . . .
    . . f b 3 e 4 4 4 4 e 3 b f . .
    . f e 3 3 3 3 3 3 3 3 3 3 e f .
    . f 3 3 e b 3 e e 3 b e 3 3 f .
    . f b 3 f f e e e e f f 3 b f .
    f f b b f b f e e f b f b b f f
    f b b b e 1 f 4 4 f 1 e b b b f
    . f b b f 4 4 4 4 4 e e b b f .
    . . f e f b d d d e 4 4 4 f . .
    . . e 4 c d d d d e 4 4 e f . .
    . . e f b b d b d d e e f . . .
    . . . f f 1 1 d 1 d 1 f f . . .
    . . . . . f b b f f f . . . . .
`)
anim2.addAnimationFrame(img`
    . . . . . f f 4 4 f f . . . . .
    . . . . f 5 4 5 5 4 5 f . . . .
    . . . f e 3 3 3 3 3 3 e f . . .
    . . f b 3 3 3 3 3 3 3 3 b f . .
    . . f 3 3 3 3 3 3 3 3 3 3 f . .
    . f 3 3 3 3 3 3 3 3 3 3 3 3 f .
    . f b 3 3 3 3 3 3 3 3 3 3 b f .
    . f b b 3 3 3 3 3 3 3 3 b b f .
    . f b b b b b b b b b b b b f .
    f c b b b b b b b b b b b b c f
    f b b b b b b b b b b b b b b f
    . f c c b b b b b b b b c c f .
    . . e 4 c f f f f f f c 4 e . .
    . . e f b d b d b d b b f e . .
    . . . f f 1 d 1 d 1 d f f . . .
    . . . . . f f b b f f . . . . .
`)
anim2.addAnimationFrame(img`
    . . . . . . . . . . . . . . . .
    . . . . . f f 4 4 f f . . . . .
    . . . . f 5 4 5 5 4 5 f . . . .
    . . . f e 3 3 3 3 3 3 e f . . .
    . . f b 3 3 3 3 3 3 3 3 b f . .
    . . f 3 3 3 3 3 3 3 3 3 3 f . .
    . f b 3 3 3 3 3 3 3 3 3 3 b f .
    . f b b 3 3 3 3 3 3 3 3 b b f .
    . f b b b b b b b b b b b b f .
    f c b b b b b b b b b b b b f .
    f b b b b b b b b b b b b c f .
    f f b b b b b b b b b b c f . .
    . f c c c f f f f f f f e c . .
    . . . f b b d b d d e 4 4 e . .
    . . . f f 1 1 d 1 d e e f . . .
    . . . . . f b b f f f . . . . .
`)
anim2.addAnimationFrame(img`
    . . . . . f f 4 4 f f . . . . .
    . . . . f 5 4 5 5 4 5 f . . . .
    . . . f e 3 3 3 3 3 3 e f . . .
    . . f b 3 3 3 3 3 3 3 3 b f . .
    . . f 3 3 3 3 3 3 3 3 3 3 f . .
    . f 3 3 3 3 3 3 3 3 3 3 3 3 f .
    . f b 3 3 3 3 3 3 3 3 3 3 b f .
    . f b b 3 3 3 3 3 3 3 3 b b f .
    . f b b b b b b b b b b b b f .
    f c b b b b b b b b b b b b c f
    f b b b b b b b b b b b b b b f
    . f c c b b b b b b b b c c f .
    . . e 4 c f f f f f f c 4 e . .
    . . e f b d b d b d b b f e . .
    . . . f f 1 d 1 d 1 d f f . . .
    . . . . . f f b b f f . . . . .
`)
anim2.addAnimationFrame(img`
    . . . . . . . . . . . . . . . .
    . . . . . f f 4 4 f f . . . . .
    . . . . f 5 4 5 5 4 5 f . . . .
    . . . f e 3 3 3 3 3 3 e f . . .
    . . f b 3 3 3 3 3 3 3 3 b f . .
    . . f 3 3 3 3 3 3 3 3 3 3 f . .
    . f b 3 3 3 3 3 3 3 3 3 3 b f .
    . f b b 3 3 3 3 3 3 3 3 b b f .
    . f b b b b b b b b b b b b f .
    . f b b b b b b b b b b b b c f
    . f c b b b b b b b b b b b b f
    . . f c b b b b b b b b b b f f
    . . c e f f f f f f f c c c f .
    . . e 4 4 e d d b d b b f . . .
    . . . f e e d 1 d 1 1 f f . . .
    . . . . . f f f b b f . . . . .
`)
anim3.addAnimationFrame(img`
    . . . f 4 4 f f f f . . . . . .
    . . f 4 5 5 4 5 f b f f . . . .
    . . f 5 5 5 5 4 e 3 3 b f . . .
    . . f e 4 4 4 e 3 3 3 3 b f . .
    . . f 3 3 3 3 3 3 3 3 3 3 f . .
    . f 3 3 e e 3 b e 3 3 3 3 f . .
    . f 3 3 e e e f f 3 3 3 3 f . .
    . f 3 e e e f b f b b b b f . .
    . . f e 4 4 f 1 e b b b b f . .
    . . . f 4 4 4 4 f b b b b f f .
    . . . f e e e f f f b b b b f .
    . . . f d d d e 4 4 f b b f . .
    . . . f d d d e 4 4 e f f . . .
    . . f b d b d b e e b f . . . .
    . . f f 1 d 1 d 1 d f f . . . .
    . . . . f f b b f f . . . . . .
`)
anim3.addAnimationFrame(img`
    . . . . . . . . . . . . . . . .
    . . . f 4 4 f f f f . . . . . .
    . . f 4 5 5 4 5 f b f f . . . .
    . . f 5 5 5 5 4 e 3 3 b f . . .
    . . f e 4 4 4 e 3 3 3 3 b f . .
    . f 3 3 3 3 3 3 3 3 3 3 3 f . .
    . f 3 3 e e 3 b e 3 3 3 3 f . .
    . f 3 3 e e e f f 3 3 3 3 f . .
    . . f e e e f b f b b b b f f .
    . . . e 4 4 f 1 e b b b b b f .
    . . . f 4 4 4 4 f b b b b b f .
    . . . f d d d e 4 4 b b b f . .
    . . . f d d d e 4 4 f f f . . .
    . . f d d d b b e e b b f . . .
    . . f b d 1 d 1 d d b f . . . .
    . . . f f f b b f f f . . . . .
`)
anim4.addAnimationFrame(img`
    . . . . . . f f f f 4 4 f . . .
    . . . . f f b f 5 4 5 5 4 f . .
    . . . f b 3 3 e 4 5 5 5 5 f . .
    . . f b 3 3 3 3 e 4 4 4 e f . .
    . . f 3 3 3 3 3 3 3 3 3 3 f . .
    . . f 3 3 3 3 e b 3 e e 3 3 f .
    . . f 3 3 3 3 f f e e e 3 3 f .
    . . f b b b b f b f e e e 3 f .
    . . f b b b b e 1 f 4 4 e f . .
    . f f b b b b f 4 4 4 4 f . . .
    . f b b b b f f f e e e f . . .
    . . f b b f 4 4 e d d d f . . .
    . . . f f e 4 4 e d d d f . . .
    . . . . f b e e b d b d b f . .
    . . . . f f d 1 d 1 d 1 f f . .
    . . . . . . f f b b f f . . . .
`)
anim4.addAnimationFrame(img`
    . . . . . . . . . . . . . . . .
    . . . . . . f f f f 4 4 f . . .
    . . . . f f b f 5 4 5 5 4 f . .
    . . . f b 3 3 e 4 5 5 5 5 f . .
    . . f b 3 3 3 3 e 4 4 4 e f . .
    . . f 3 3 3 3 3 3 3 3 3 3 3 f .
    . . f 3 3 3 3 e b 3 e e 3 3 f .
    . . f 3 3 3 3 f f e e e 3 3 f .
    . f f b b b b f b f e e e f . .
    . f b b b b b e 1 f 4 4 e . . .
    . f b b b b b f 4 4 4 4 f . . .
    . . f b b b 4 4 e d d d f . . .
    . . . f f f 4 4 e d d d f . . .
    . . . f b b e e b b d d d f . .
    . . . . f b d d 1 d 1 d b f . .
    . . . . . f f f b b f f f . . .
`)
anim5.addAnimationFrame(img`
    . . . . . f f 4 4 f f . . . . .
    . . . . f 5 4 5 5 4 5 f . . . .
    . . . f e 3 3 3 3 3 3 e f . . .
    . . f b 3 3 3 3 3 3 3 3 b f . .
    . . f 3 3 3 3 3 3 3 3 3 3 f . .
    . f 3 3 3 3 3 3 3 3 3 3 3 3 f .
    . f b 3 3 3 3 3 3 3 3 3 3 b f .
    . f b b 3 3 3 3 3 3 3 3 b b f .
    . f b b b b b b b b b b b b f .
    f c b b b b b b b b b b b b c f
    f b b b b b b b b b b b b b b f
    . f c c b b b b b b b b c c f .
    . . e 4 c f f f f f f c 4 e . .
    . . e f b d b d b d b b f e . .
    . . . f f 1 d 1 d 1 d f f . . .
    . . . . . f f b b f f . . . . .
`)
anim6.addAnimationFrame(img`
    . . . . . f f 4 4 f f . . . . .
    . . . . f 5 4 5 5 4 5 f . . . .
    . . . f e 4 5 5 5 5 4 e f . . .
    . . f b 3 e 4 4 4 4 e 3 b f . .
    . . f 3 3 3 3 3 3 3 3 3 3 f . .
    . f 3 3 e b 3 e e 3 b e 3 3 f .
    . f 3 3 f f e e e e f f 3 3 f .
    . f b b f b f e e f b f b b f .
    . f b b e 1 f 4 4 f 1 e b b f .
    f f b b f 4 4 4 4 4 4 f b b f f
    f b b f f f e e e e f f f b b f
    . f e e f b d d d d b f e e f .
    . . e 4 c d d d d d d c 4 e . .
    . . e f b d b d b d b b f e . .
    . . . f f 1 d 1 d 1 d f f . . .
    . . . . . f f b b f f . . . . .
`)
anim7.addAnimationFrame(img`
    . . . f 4 4 f f f f . . . . . .
    . . f 4 5 5 4 5 f b f f . . . .
    . . f 5 5 5 5 4 e 3 3 b f . . .
    . . f e 4 4 4 e 3 3 3 3 b f . .
    . . f 3 3 3 3 3 3 3 3 3 3 f . .
    . f 3 3 e e 3 b e 3 3 3 3 f . .
    . f 3 3 e e e f f 3 3 3 3 f . .
    . f 3 e e e f b f b b b b f . .
    . . f e 4 4 f 1 e b b b b f . .
    . . . f 4 4 4 4 f b b b b f f .
    . . . f e e e f f f b b b b f .
    . . . f d d d e 4 4 f b b f . .
    . . . f d d d e 4 4 e f f . . .
    . . f b d b d b e e b f . . . .
    . . f f 1 d 1 d 1 d f f . . . .
    . . . . f f b b f f . . . . . .
`)
anim8.addAnimationFrame(img`
    . . . . . . . . . . . . . . . .
    . . . . . . f f f f 4 4 f . . .
    . . . . f f b f 5 4 5 5 4 f . .
    . . . f b 3 3 e 4 5 5 5 5 f . .
    . . f b 3 3 3 3 e 4 4 4 e f . .
    . . f 3 3 3 3 3 3 3 3 3 3 3 f .
    . . f 3 3 3 3 e b 3 e e 3 3 f .
    . . f 3 3 3 3 f f e e e 3 3 f .
    . f f b b b b f b f e e e f . .
    . f b b b b b e 1 f 4 4 e . . .
    . f b b b b b f 4 4 4 4 f . . .
    . . f b b b 4 4 e d d d f . . .
    . . . f f f 4 4 e d d d f . . .
    . . . f b b e e b b d d d f . .
    . . . . f b d d 1 d 1 d b f . .
    . . . . . f f f b b f f f . . .
`)
animation.attachAnimation(mySprite, anim)
animation.attachAnimation(mySprite, anim2)
animation.attachAnimation(mySprite, anim3)
animation.attachAnimation(mySprite, anim4)
animation.attachAnimation(mySprite, anim5)
animation.attachAnimation(mySprite, anim6)
animation.attachAnimation(mySprite, anim7)
animation.attachAnimation(mySprite, anim8)
game.onUpdate(function () {
    if (controller.up.isPressed()) {
        animation.setAction(mySprite, ActionKind.up)
        direction = 1
    } else if (controller.down.isPressed()) {
        animation.setAction(mySprite, ActionKind.down)
        direction = 2
    } else if (controller.left.isPressed()) {
        animation.setAction(mySprite, ActionKind.left)
        direction = 3
    } else if (controller.right.isPressed()) {
        animation.setAction(mySprite, ActionKind.right)
        direction = 4
    } else {
        if (direction == 1) {
            animation.setAction(mySprite, ActionKind.stay_up)
        } else if (direction == 2) {
            animation.setAction(mySprite, ActionKind.stay_down)
        } else if (direction == 3) {
            animation.setAction(mySprite, ActionKind.stay_left)
        } else if (direction == 4) {
            animation.setAction(mySprite, ActionKind.stay_right)
        }
    }
})

```  

---  

**这节课我们学到了什么？**  
- 动画的概念和如何使用动画  
- 逻辑的概念，通过妥当使用变量来记录按键，并通过判断值来执行对应的操作  
  