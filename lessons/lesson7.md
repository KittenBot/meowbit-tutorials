# 第七节：精灵行走效果

前面章节学到的控制精灵移动的时候，精灵的图案一直都是静态不变的，这样缺少了动感，所以本节课我们来讲讲如何让精灵动态移动。为此我们有两种方法可供选择

?>本节课目标是使用现有的图像素材做一个能让精灵动态行走的程序  

为了完成目标我们由简入深来说有两种方式：
1. 使用图像翻转(使用`水平翻转`图像来做最粗糙的动态效果)
2. 使用`动画`插件来做更高级的动态效果

## 要点1：使用图像的'水平翻转'功能  
  
`水平翻转`积木块在Advanced选项下的`图像`分栏里  
![](image/l7_p1.png)

举个简单的例子了解一下它的实际用处  
  


![](image/l7_1.gif)

简单来说我们可以通过这些事件来改变精灵的位置，但绝不仅仅如此，亦可以通过事件来给精灵一定的运动速度(这个速度也就是平常所说的位置的改变率，通常单位是km/h或m/h)。

当给的速度不是0，那么精灵便可以运动。



本节课我们将介绍

1. `控制器`事件
2. 递增x和y坐标  
3. 设置速度vx和vy
4. 结合`控制器`事件实现简单的运动功能
5. 结合`Images`分栏下的图像翻转实现行走动作

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