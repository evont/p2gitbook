刚体 \(Body\) 指的是具有质量、位置、速度以及一些用于碰撞的形状的物理对象；

## 构造器

---

一个 Object 对象，包含刚体的基本物理属性

构造器函数如下：

```js
constructor(options?: {
    force?: number[]; // x轴方向及y轴方向作用力
    position?: number[];
    velocity?: number[]; //x轴方向及y轴方向作用力
    allowSleep?: boolean; 
    collisionResponse? :boolean;
    angle = 0? :number;
    angularForce = 0? :number;
    angularVelocity = 0? :number;
    ccdIterations = 0? :number;
    ccdSpeedThreshold = -1? :number;
    fixedRotation = false? :boolean;
    gravityScale? :number;
    id? :number;
    mass = 0? :number;
    sleepSpeedLimit? :number;
    sleepTimeLimit? :number;
});
```

创建刚体的例子如下：

```js
// Create a typical dynamic body
   var body = new Body({
                  mass: 1,
                  position: [0, 0],
                  angle: 0,
                  velocity: [0, 0],
                  angularVelocity: 0
              });

// Add a circular shape to the body
   body.addShape(new Circle({ radius: 1 }));

// Add the body to the world
   world.addBody(body);
```

## 属性

---

* #### **aabb **:AABB

  刚体的包围盒
* #### **aabbNeedsUpdate **:Boolean

  标志包围盒是否需要更新，使用 [updateAABB\(\)](#updateaabb--void) 进行更新
* #### **allowSleep **:Boolean

  如果设置为真，刚体将会自动进入睡眠状态。需要注意的是，你需要在所有事件发生前在世界中启用睡眠。
  默认为true
* #### **angle **:Number

  角度
  这一属性没有限定在标准的0 - 2π 之间，可以设置为任意数字，如果你需要设置它为这一区间的数字，可以用下列函数进行换算；
  ```js
    function normalizeAngle(angle){
        angle = angle % (2*Math.PI);
        if(angle < 0){
            angle += (2*Math.PI);
        }
        return angle;
    }
  ```
* #### **angularDamping **:Number

  角度阻尼，0 - 1之间的数字，默认为0.1
* #### **angularForce **:Number

  作用于刚体的角力
* #### **angularVelocity **:Number

  角速度，每秒转动设定的弧度
* #### **boundingRadius **:Number

  边界圆半径
* #### **ccdIterations **:Number

  在连续碰撞检测时遍历碰撞所使用的迭代次数，次数越多将使得连续碰撞检测碰撞的误差变小，但次数越少将提高性能。
  默认为10；
* #### **ccdSpeedThreshold **:Number

  如果刚体的速度超过此阈值，连续碰撞检测将被启用。将该值设置为一个负数将完全禁用该刚体的连续碰撞检测；
  默认为-1；

* #### **collisionResponse **:Boolean

  当与其他刚体碰撞时是否产生碰撞作用力。需要注意的是，碰撞仍会产生，但会被禁用。即：该刚体会穿过其他刚体，但仍然会触发碰撞等事件。
  
* #### **damping **:Number

  在速度的方向上作用于刚体的线性阻尼，取值在0 - 1之间；
  默认为0.1
  
* #### **fixedRotation **:Boolean

  若为真，则将固定刚体的旋转
  
* #### **fixedX **:Boolean

  若为真，则将固定刚体在X轴上的移动，此时刚体依然可以在Y轴上移动。
 
* #### **fixedY **:Boolean

  若为真，则将固定刚体在Y轴上的移动，此时刚体依然可以在X轴上移动。
  
* #### **force **:Array
  
  作用于刚体的外力。
  
* #### **gravityScale **:Number

  重力比例因子，如果希望刚体忽略重力影响，将其设置为0即可，如果希望刚体反重力，将其设置为-1；
  默认为1；
  
* #### **id **:Number

  刚体的唯一标志
  
* #### **idleTime **:Number
  
  刚体持续睡眠的时间

* #### **inertia **:Number
  
  刚体围绕Z轴上的惯性

* #### ** interpolatedAngle **:Number
  
  刚体的插入角度，用于渲染

* #### ** interpolatedPosition **:Array

  刚体的插入位置，用于渲染

* #### ** invInertia **:Number

  反惯性
  
* #### ** invMass **:Number
  
  反重力

* #### ** mass **:Number
  
  质量
  
* #### ** position **:Array
  
  位置

* #### ** previousAngle **:Number
  
  刚体的前一角度

* #### ** previousPosition **:Array
  
  刚体的前一位置

* #### ** shapes **:Array
  
  刚体的形状，可以多个

* #### ** sleepSpeedLimit **:Number
  
  如果刚体当前的速度（数量速度speed， 非velocity矢量速度）小于这一数值，刚体将被视为需进入惺忪状态
  默认为0.2

* #### ** sleepState **:Number
  
  Body.AWAKE(唤醒模式), Body.SLEEPY(惺忪状态) 和 Body.SLEEPING(休眠模式) 之一。
  刚体初始的睡眠状态为Body.AWAKE(唤醒模式), 如果其当前速度低于 [sleepSpeedLimit](#sleepSpeedLimit), 刚体的睡眠状态将变为Body.SLEEPY(惺忪状态)， 如果刚体保持Body.SLEEPY(惺忪状态) [sleepTimeLimit](#sleepTimeLimit) 秒将进入Body.SLEEPING(休眠模式)
  默认为Body.AWAKE

* #### ** sleepTimeLimit **:Number
  
  如果刚体保持Body.SLEEPY(惺忪状态)超出这一限制时间将进入休眠。
  默认为1

* #### ** type **:Number
  
  Body.STATIC（静力学模型）, Body.DYNAMIC（动力学模型） 和 Body.KINEMATIC（运动学模型） 之一
  刚体的运动类型， STATIC 刚体不可移动，也不受作用力和碰撞影响， DYNAMIC 刚体将根据碰撞和作用力运动，KINEMATIC 刚体根据其velocity 属性移动，也不受作用力和碰撞影响。
  
 示例：
 ```js
 // 刚体默认为静力学模型，静力学模型刚体永远不移动
     var body = new Body();
     console.log(body.type == Body.STATIC); // true
 ```
  
 ```js
 // 将刚体的质量设置为非零数值时，它将变成能够运动及与其他刚体进行交互的动力学模型
   var dynamicBody = new Body({
                        mass : 1
                    });
   console.log(dynamicBody.type == Body.DYNAMIC); // true
 ```
 
 ```js
// 将刚体的质量设置为非零数值时，它将变成能够运动及与其他刚体进行交互的动力学模型
var dynamicBody = new Body({
mass : 1
});
console.log(dynamicBody.type == Body.DYNAMIC); // true
```
 
* #### ** mass **:Number
  
  质量

* #### ** mass **:Number
  
  质量

* #### ** mass **:Number
  
  质量

* #### ** mass **:Number
  
  质量


## 静态属性



## 方法

---

* #### **updateAABB\(\)  **:void

  更新刚体的包围盒，并设置aabbNeedsUpdate 为false

* **copy  **:void

  参数为一个AABB 类型对象

  将指定的AABB 对象复制到当前对象中

* **extend  **:void

  参数为一个AABB 类型对象

  继承指定的AABB 对象，使得当前对象覆盖对应的AABB 对象

* **overlaps  **:boolean

  参数为一个AABB 类型对象

  检测当前AABB 对象是否覆盖指定的AABB 对象

* **overlapsRay  **:number

  参数为一个Ray 对象

  检测当前AABB 对象是否被指定的Ray 对象击中，如果没有击中则返回 -1，如果击中则返回 0 - 1 之间的一个数；

* **setFromPoints**

  参数为四个：  
     要设置AABB 对象的新坐标点数组\(Points :Array\)  
     位移位置数组\(Position :Array\)  
     要旋转的角度\(Angle :Number\)  
     加给包围盒的边距\(skinSize: Number\)

  在指定位置创建AABB对象并进行位移及旋转，同时拓宽包围盒边距。  




### 事件

---

* **sleep **

* **sleepy **

* **wakeup **



