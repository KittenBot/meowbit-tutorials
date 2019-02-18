# 第八节：精灵的重叠事件 {docsify-ignore-all}

精灵的重叠，顾名思义就是两个精灵相碰，重叠事件积木块的作用就是允许相碰后进入并执行一些动作。  

粗略来说，前些章节我们只对精灵有了初步了解，从这节开始我们将会频繁使用`类型`这个概念，细心的同学应该发现了，在创建精灵积木块尾部有一个默认的player类型，点开下拉框可以看到如:食物、敌人等等类型，这个类型其实并不是固定的，它只是方便我们区分不同的精灵并且对其同一类精灵能有一个统一的管理，类型的名字完全可以自由创建。 

我们本节课就以制作一个`解救公主`的小游戏来掌握这些概念  

为了使游戏丰富起来，我们需要用到之前学过的知识，比如倒计时和生命值。

游戏的大致流程如下
- 设置10s倒计时
- 地图内的怪物有规律移动
- 躲避这些怪物解救地图右下角的公主
- 失败的条件：
    - 生命值扣光
    - 时间结束还未救到公主
 
为了完成这个游戏我们需要如下几个知识点  

1. 精灵的`类型`和精灵的`运动`
2. 精灵与场景`砖块的触碰`事件
3. 精灵`重叠`事件


## 要点1：类型和运动

我们需要明确几种类型 
- player(玩家的控制单位)
- Enemy(敌人)
- princess(解救对象)
  
开局我们首先需要配置好地图场景砖块，各个精灵的图像，类型，和位置等属性  

![](https://s2.ax1x.com/2019/02/18/k6LbR0.png)

根据每个敌人需要移动的方向分别给敌人初始速度，为了使后续速度变化可控，我们使用speed这个变量来存储速度值。  

![](https://s2.ax1x.com/2019/02/18/k6LqzV.png)  
  
![](https://s2.ax1x.com/2019/02/18/k6L7in.gif)  
  
## 要点2：砖块的触碰事件

这一部分我们做`敌人`精灵运动时碰到墙该做的反应：往相反方向再次运动，不断重复。
  
根据如下程序，我们并不对某一个精灵进行碰撞检测，而是对`敌人`这个类型进行检测，当类型为`敌人`的精灵碰到墙后，我们就对这个碰到墙的精灵进行反应动作，所以此时我们需要将碰撞积木的第一个参数sprite作为对象变量。

![](https://s2.ax1x.com/2019/02/18/k6LOMT.png)  
  
![](https://s2.ax1x.com/2019/02/18/k6LHGq.gif)  

## 要点3：重叠事件
  
`重叠`事件在精灵分栏下  
  
![](https://s2.ax1x.com/2019/02/18/k6LXsU.png)  
  
首先需要明确的两点  
1. 当player碰到敌人，生命值-1，并且回到原位，只有3条命  
2. 当player碰到princess，游戏结束，成功  
  
**1. on start下加入`设置生命值为3`的积木块。制作player和enemy的重叠事件。**  

![](https://s2.ax1x.com/2019/02/18/k6LjLF.png)

**2. 制作碰到princess的事件**  
  
![](https://s2.ax1x.com/2019/02/18/k6LxZ4.png)
  
## 完成
  
```javascript
enum SpriteKind {
    Player,
    Projectile,
    Food,
    Enemy,
    princess
}
let princess: Sprite = null
let enemy3: Sprite = null
let enemy2: Sprite = null
let enemy1: Sprite = null
let player: Sprite = null
let speed = 0
let otherSprite: Sprite = null
let sprite: Sprite = null
scene.onHitTile(SpriteKind.Enemy, 2, function (sprite) {
    speed = -1 * speed
    if (sprite.vx != 0) {
        sprite.setVelocity(speed, 0)
    } else if (sprite.vy != 0) {
        sprite.setVelocity(0, speed * 1.5)
    }
})
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {
    sprite.setPosition(36, 103)
    info.changeLifeBy(-1)
})
sprites.onOverlap(SpriteKind.Player, SpriteKind.princess, function (sprite, otherSprite) {
    game.setDialogFont(FontType.font12)
    game.showLongText("谢谢你！！我的王子", DialogLayout.Bottom)
    pause(500)
    game.over(true)
})
scene.setTileMap(img`
    2 2 2 2 2 2 2 2 2 .
    2 . . . . . . . 2 .
    2 . . . . . . . 2 .
    2 . . . 2 . . . 2 2
    2 . . . 2 2 . . 2 2
    2 . . . 2 2 . . . 2
    . . . . 2 2 . . 2 2
    . . . . 2 2 2 . . .
`)
scene.setTile(2, img`
    . . . . . . . . . b b b b . . .
    . . . . . . b b b d d d d b . .
    . . . . . . b d d d d d d b . .
    . . . . b b d d d d d b b d . .
    . . . . b d d d d d d b b d b .
    . . . . c d d d d d b b d b c .
    . . . b c c b b b b d d b c c .
    . . b b c c c b d d b c c c c .
    . b b d d d b b b b b b c c c c
    . c d d d d d d b d b c c c b c
    . c b d d d b b d b c c c b b c
    c b c c c c b d d b b b b b c c
    c c b b b d d b c c b b b b c c
    c c c c c c c c c b b b b c c .
    . c c c c b b b b b b b c c . .
    . . . . c c c c c c c c . . . .
`, true)
player = sprites.create(img`
    . . . . . . f f f f . . . . . .
    . . . . f f f 2 2 f f f . . . .
    . . . f f f 2 2 2 2 f f f . . .
    . . f f f e e e e e e f f f . .
    . . f f e 2 2 2 2 2 2 e e f . .
    . . f e 2 f f f f f f 2 e f . .
    . . f f f f e e e e f f f f . .
    . f f e f b f 4 4 f b f e f f .
    . f e e 4 1 f d d f 1 4 e e f .
    . . f e e d d d d d d e e f . .
    . . . f e e 4 4 4 4 e e f . . .
    . . e 4 f 2 2 2 2 2 2 f 4 e . .
    . . 4 d f 2 2 2 2 2 2 f d 4 . .
    . . 4 4 f 4 4 5 5 4 4 f 4 4 . .
    . . . . . f f f f f f . . . . .
    . . . . . f f . . f f . . . . .
`, SpriteKind.Player)
enemy1 = sprites.create(img`
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . f f f f . . . . . . . . . .
    . . . . . . . . f f 1 1 1 1 f f . . . . . . . .
    . . . . . . . f b 1 1 1 1 1 1 b f . . . . . . .
    . . . . . . . f 1 1 1 1 1 1 1 1 f . . . . . . .
    . . . . . . f d 1 1 1 1 1 1 1 1 d f . . . . . .
    . . . . . . f d 1 1 1 1 1 1 1 1 d f . . . . . .
    . . . . . . f d d d 1 1 1 1 d d d f . . . . . .
    . . . . . . f b d b f d d f b d b f . . . . . .
    . . . . . . f c d c f 1 1 f c d c f . . . . . .
    . . . . . . . f b 1 1 1 1 1 1 b f . . . . . . .
    . . . . . . f f f c d b 1 b d f f f f . . . . .
    . . . . f c 1 1 1 c b f b f c 1 1 1 c f . . . .
    . . . . f 1 b 1 b 1 f f f f 1 b 1 b 1 f . . . .
    . . . . f b f b f f f f f f b f b f b f . . . .
    . . . . . . . . . f f f f f f . . . . . . . . .
    . . . . . . . . . . . f f f . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
`, SpriteKind.Enemy)
enemy2 = sprites.create(img`
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . f f f f . . . . . . . . . .
    . . . . . . . . f f 1 1 1 1 f f . . . . . . . .
    . . . . . . . f b 1 1 1 1 1 1 b f . . . . . . .
    . . . . . . . f 1 1 1 1 1 1 1 1 f . . . . . . .
    . . . . . . f d 1 1 1 1 1 1 1 1 d f . . . . . .
    . . . . . . f d 1 1 1 1 1 1 1 1 d f . . . . . .
    . . . . . . f d d d 1 1 1 1 d d d f . . . . . .
    . . . . . . f b d b f d d f b d b f . . . . . .
    . . . . . . f c d c f 1 1 f c d c f . . . . . .
    . . . . . . . f b 1 1 1 1 1 1 b f . . . . . . .
    . . . . . . f f f c d b 1 b d f f f f . . . . .
    . . . . f c 1 1 1 c b f b f c 1 1 1 c f . . . .
    . . . . f 1 b 1 b 1 f f f f 1 b 1 b 1 f . . . .
    . . . . f b f b f f f f f f b f b f b f . . . .
    . . . . . . . . . f f f f f f . . . . . . . . .
    . . . . . . . . . . . f f f . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
`, SpriteKind.Enemy)
enemy3 = sprites.create(img`
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . f f f f . . . . . . . . . .
    . . . . . . . . f f 1 1 1 1 f f . . . . . . . .
    . . . . . . . f b 1 1 1 1 1 1 b f . . . . . . .
    . . . . . . . f 1 1 1 1 1 1 1 1 f . . . . . . .
    . . . . . . f d 1 1 1 1 1 1 1 1 d f . . . . . .
    . . . . . . f d 1 1 1 1 1 1 1 1 d f . . . . . .
    . . . . . . f d d d 1 1 1 1 d d d f . . . . . .
    . . . . . . f b d b f d d f b d b f . . . . . .
    . . . . . . f c d c f 1 1 f c d c f . . . . . .
    . . . . . . . f b 1 1 1 1 1 1 b f . . . . . . .
    . . . . . . f f f c d b 1 b d f f f f . . . . .
    . . . . f c 1 1 1 c b f b f c 1 1 1 c f . . . .
    . . . . f 1 b 1 b 1 f f f f 1 b 1 b 1 f . . . .
    . . . . f b f b f f f f f f b f b f b f . . . .
    . . . . . . . . . f f f f f f . . . . . . . . .
    . . . . . . . . . . . f f f . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
    . . . . . . . . . . . . . . . . . . . . . . . .
`, SpriteKind.Enemy)
princess = sprites.create(img`
    . . . . . . 5 . 5 . . . . . . .
    . . . . . f 5 5 5 f f . . . . .
    . . . . f 1 5 2 5 1 6 f . . . .
    . . . f 1 6 6 6 6 6 1 6 f . . .
    . . . f 6 6 f f f f 6 1 f . . .
    . . . f 6 f f d d f f 6 f . . .
    . . f 6 f d f d d f d f 6 f . .
    . . f 6 f d 3 d d 3 d f 6 f . .
    . . f 6 6 f d d d d f 6 6 f . .
    . f 6 6 f 3 f f f f 3 f 6 6 f .
    . . f f d 3 5 3 3 5 3 d f f . .
    . . f d d f 3 5 5 3 f d d f . .
    . . . f f 3 3 3 3 3 3 f f . . .
    . . . f 3 3 5 3 3 5 3 3 f . . .
    . . . f f f f f f f f f f . . .
    . . . . . f f . . f f . . . . .
`, SpriteKind.princess)
player.setPosition(36, 103)
enemy1.setPosition(47, 72)
enemy2.setPosition(104, 32)
enemy3.setPosition(120, 88)
princess.setPosition(152, 120)
controller.moveSprite(player)
speed = 50
enemy1.setVelocity(speed, 0)
enemy2.setVelocity(0, speed * 1.5)
enemy3.setVelocity(speed, 0)
info.setLife(3)

```

---

**这节课我们学到了什么?**
- 不同类型的重叠事件，重叠事件出发后，其中的sprite参数如何使用

