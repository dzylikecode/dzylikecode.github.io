# basic tutorial

## config

属性 type 可以是 Phaser.CANVAS，或者 Phaser.WEBGL，或者 Phaser.AUTO。这是你要给你的游戏使用的渲染环境（context）。推荐值是 Phaser.AUTO，它将自动尝试使用 WebGL，如果浏览器或设备不支持，它将回退为 Canvas。Phaser 生成的画布元素（canvas element）将径直添加到文档中调用脚本的那个节点上，不过也可以在游戏配置中指定一个父容器，如果你需要的话。

## image position

所有游戏对象的定位都默认基于它们的中心点

你可以用 setOrigin（设置原点）来改变这种情况。比如代码 this.add.image(0, 0, 'sky').setOrigin(0, 0)，将把图像的绘制定位点重置为左上角。通过属性 originX 和 originY

## image load to screen

代码 this.add.image 生成一个新的 Image（图形）类游戏对象，并把它添加到当前场景的显示列表（display list）中。你的所有游戏对象都活在这个列表中。你可以把图像放置在任何位置，Phaser 不会介意。当然，如果图像位于 0x0 到 800x600 这个区域之外，那么你视觉上看不到它，因为它已“脱离画面”，但它仍旧在场景中存在

场景（Scene）自身没有确定的尺寸，在所有方向上都是无限延展的。镜头（Camera）系统控制着你观看场景的视野，你可以随意移动、推拉已激活的镜头。你还可以另外生成一些镜头，用于别的观看场景的视野。

## physics system

Phaser 支持多种物理系统，每一种都以插件形式运作，任何 Phaser 场景都能使用它们。在本文写作时，已经装有 Arcade, Impact, Matter.js 三种物理系统。针对本教程，我们将给我们的游戏使用 Arcade 物理系统，它简单，轻量，完美地支持移动浏览器。

### 静态

在 Arcade 物理系统中，有动态的和静态的两类物体（body）。动态物体可以通过外力比如速度（velocity）、加速度（acceleration），得以四处移动。它可以跟其他对象发生反弹（bounce）、碰撞（collide），此类碰撞受物体质量和其他因素影响。

与此明显不同的是，静态物体只有位置和尺寸。重力对它没有影响，你不能给它设置速度，有东西跟它碰撞时，它一点都不动。名副其实，完全是静态的。所以用作地面和平台很完美，我们打算让玩家在上面来回跑动。

要调用 refreshBody()，这是因为我们缩放的是一个 静态 物体，所以必须把所作变动告诉物理世界（physic

### 动态

sprite 默认拥有一个动态物体

- player.setBounce(0.2);

  被赋予 0.2 的一点点反弹（bounce）值。这意味着，它跳起后着地时始终会弹起那么一点点。

## animation

- preload

  ```javascript
  this.load.spritesheet("dude", "assets/dude.png", {
    frameWidth: 32,
    frameHeight: 48,
  });
  ```

- create

  ```javascript
  this.anims.create({
    key: "left",
    frames: this.anims.generateFrameNumbers("dude", { start: 0, end: 3 }),
    frameRate: 10,
    repeat: -1,
  });
  ```

'left'动画使用 0, 1, 2, 3 帧，跑动时每秒 10 帧。'repeat -1'告诉动画要循环播放

其中, 'left' 是纹理的键值

- 补充信息

  在 Phaser 3 中，动画管理器（Animation Manager）是全局系统。其中生成的动画是全局变量，所有游戏对象都能用到它们。它们分享基础的动画数据，同时管理自己的时间轴（timeline）。这就使我们能够在某时定义一个动画，却可以应用到任意多的游戏对象上

## 碰撞

比如，在一个精灵上模仿重力效果，可以这么简单写：

player.body.setGravityY(300)

碰撞器（Collider）是施魔法的地方。它接收两个对象，检测二者之间的碰撞，并使二者分开。

## 键盘控制移动

玩家精灵只有键被按下时才移动，抬起时立即停止。Phaser 也允许你用动量（momentum）和加速度（acceleration）生成

- 下降

  ```javascript
  if (cursors.up.isDown && player.body.touching.down) {
    player.setVelocityY(-330);
  }
  ```

  设置初始速度为 -330, 此时玩家未被接触

  重力作用下，玩家会下降, 在接触到地面时, 又可以设置了

## 重复生成动态

因为它自动生成一个子项，重复 11 次就意味着我们总共将得到 12 颗

给它们的 bounce.y 赋予 0.4 到 0.8 之间的随机值，反弹范围在 0（不反弹）到 1 之间（完全反弹）。因为星星都是在 y 等于 0 的位置产出的，重力将把它们往下拉，直到与平台或地面碰撞为止。反弹值意味着它们将随机地反弹上来，直到最终恢复安定为止。

- this.physics.add.collider(stars, platforms);

  避免掉落出地面

- this.physics.add.overlap(player, stars, collectStar, null, this);

  检测玩家是否接触到星星, 如果是, 就调用 collectStar() 函数

## 计分

16 x 16 是显示文本的坐标位置。'score: 0'是要显示的默认字符串，接下来的对象包含字号、填充色。因为没有指定字体，实际上将用 Phaser 默认的，即 Courier。

## 完整代码

```javascript
var config = {
  type: Phaser.AUTO,
  width: 800,
  height: 600,
  physics: {
    default: "arcade", // arcade, matter, impact 三个物理引擎
    arcade: {
      gravity: { y: 300 },
      debug: false,
    },
  },
  scene: {
    preload: preload,
    create: create,
    update: update,
  },
};

var player;
var stars;
var bombs;
var platforms;
var cursors;
var score = 0;
var gameOver = false;
var scoreText;

var game = new Phaser.Game(config);

function preload() {
  this.load.image("sky", "assets/sky.png");
  this.load.image("ground", "assets/platform.png");
  this.load.image("star", "assets/star.png");
  this.load.image("bomb", "assets/bomb.png");
  this.load.spritesheet("dude", "assets/dude.png", {
    frameWidth: 32,
    frameHeight: 48,
  });
}

function create() {
  //  A simple background for our game
  this.add.image(400, 300, "sky");

  //  The platforms group contains the ground and the 2 ledges we can jump on
  platforms = this.physics.add.staticGroup();

  //  Here we create the ground.
  //  Scale it to fit the width of the game (the original sprite is 400x32 in size)
  platforms.create(400, 568, "ground").setScale(2).refreshBody();

  //  Now let's create some ledges
  platforms.create(600, 400, "ground");
  platforms.create(50, 250, "ground");
  platforms.create(750, 220, "ground");

  // The player and its settings
  player = this.physics.add.sprite(100, 450, "dude");

  //  Player physics properties. Give the little guy a slight bounce.
  player.setBounce(0.2);
  player.setCollideWorldBounds(true);

  //  Our player animations, turning, walking left and walking right.
  this.anims.create({
    key: "left",
    frames: this.anims.generateFrameNumbers("dude", { start: 0, end: 3 }),
    frameRate: 10,
    repeat: -1,
  });

  this.anims.create({
    key: "turn",
    frames: [{ key: "dude", frame: 4 }],
    frameRate: 20,
  });

  this.anims.create({
    key: "right",
    frames: this.anims.generateFrameNumbers("dude", { start: 5, end: 8 }),
    frameRate: 10,
    repeat: -1,
  });

  //  Input Events
  cursors = this.input.keyboard.createCursorKeys();

  //  Some stars to collect, 12 in total, evenly spaced 70 pixels apart along the x axis
  stars = this.physics.add.group({
    key: "star",
    repeat: 11,
    setXY: { x: 12, y: 0, stepX: 70 },
  });

  stars.children.iterate(function (child) {
    //  Give each star a slightly different bounce
    child.setBounceY(Phaser.Math.FloatBetween(0.4, 0.8));
  });

  bombs = this.physics.add.group();

  //  The score
  scoreText = this.add.text(16, 16, "score: 0", {
    fontSize: "32px",
    fill: "#000",
  });

  //  Collide the player and the stars with the platforms
  this.physics.add.collider(player, platforms);
  this.physics.add.collider(stars, platforms);
  this.physics.add.collider(bombs, platforms);

  //  Checks to see if the player overlaps with any of the stars, if he does call the collectStar function
  this.physics.add.overlap(player, stars, collectStar, null, this);

  this.physics.add.collider(player, bombs, hitBomb, null, this);
}

function update() {
  if (gameOver) {
    return;
  }

  if (cursors.left.isDown) {
    player.setVelocityX(-160);

    player.anims.play("left", true);
  } else if (cursors.right.isDown) {
    player.setVelocityX(160);

    player.anims.play("right", true);
  } else {
    player.setVelocityX(0);

    player.anims.play("turn");
  }

  if (cursors.up.isDown && player.body.touching.down) {
    player.setVelocityY(-330);
  }
}

function collectStar(player, star) {
  star.disableBody(true, true);

  //  Add and update the score
  score += 10;
  scoreText.setText("Score: " + score);

  if (stars.countActive(true) === 0) {
    //  A new batch of stars to collect
    stars.children.iterate(function (child) {
      child.enableBody(true, child.x, 0, true, true);
    });

    var x =
      player.x < 400
        ? Phaser.Math.Between(400, 800)
        : Phaser.Math.Between(0, 400);

    var bomb = bombs.create(x, 16, "bomb");
    bomb.setBounce(1);
    bomb.setCollideWorldBounds(true);
    bomb.setVelocity(Phaser.Math.Between(-200, 200), 20);
    bomb.allowGravity = false;
  }
}

function hitBomb(player, bomb) {
  this.physics.pause();

  player.setTint(0xff0000);

  player.anims.play("turn"); // turn red

  gameOver = true;
}
```
