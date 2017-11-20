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
// 运动学模型刚体仅在改变其矢量速度时发生移动
 var kinematicBody = new Body({
                    type: Body.KINEMATIC
                    });
```
 
* #### ** velocity **:Array
  
  当前速度

* #### ** vlambda **:Array
  
  在世界最后一次步进(step)中添加到刚体的约束速度。

* #### ** wlambda **:Array
  
  在世界最后一次步进(step)中添加到刚体的角约束速度。

* #### ** world **:World
  
  刚体进入的物理世界，当设置为Null 时，意味着刚体未进入如何物理世界


## 方法

---

* #### **addShape(shape :Shape, [offset :Array], [angle :Number])  **:void

  参数为一个必需参数和两个可选参数：
    1. Shape 将依附到刚体上的形状，必需
    2. offset 形状的局部偏移，可选
    3. angle 形状的局部角度，可选
      
  将一个形状依附到这个刚体上，可以在添加形状时传入一个局部变换值，使得形状拥有相对刚体重心的位置和角度。这将自动更新刚体的属性和包围半径
  
  示例：
  ```js
  var body = new Body(),
      shape = new Circle({ radius: 1 });

  // 将形状置于刚体中间
  body.addShape(shape);

  // 添加另一个形状, 将其放置于距离刚体重心X轴方向1单位的位置
  body.addShape(shape,[1,0]);

  // 添加另一个形状, 将其放置于距离刚体重心Y轴方向1单位的位置，同时将其旋转90度(逆时针方向)
  body.addShape(shape,[0,1],Math.PI/2);
  ```
  
* #### **adjustCenterOfMass\(\)  **:void

  调整形状的偏移量，使得其中心变成刚体的重心。

* #### **applyDamping\(dt :Number\)  **:void
  
  参数为当前时间戳
  施加阻尼

* #### **applyForce\(force :Array,[relativePoint :Array]\)  **:void
   
  参数为一个必需参数和一个可选参数：
    1. force 施加在刚体上的力，必需
    2. relativePoint 相对重心的施力点，可选
    
  在相对刚体重心的一个点施加作用力， 这个点可以是刚体表面上的任意一点， 这种情况下施加作用力将影响刚体的force 作用力和angularForce 角速度，如果这一点为0， 这一作用力将直接施加在刚体重心，产生的扭矩将为0

* #### **applyForceLocal\(localForce :Array,[localPoint :Array]\)  **:void
  
  参数为一个必需参数和一个可选参数：
    1. localForce 施加在刚体所在物理空间的向量力，必需
    2. localPoint 刚体所在的物理世界中的一个关联点，如果不给出，它将被设置为零，所有的冲量将施加到刚体重心，可选
    
  对物体所在位置施加一个作用力

* #### **applyImpulse\(impulse :Array, [relativePoint :Array]\)  **:void
  
  参数为一个必需参数和一个可选参数：
    1. impulse 施加在刚体所在物理空间的冲量，必需
    2. relativePoint 刚体所在的物理世界中的一个关联点，如果不给出，它将被设置为零，所有的冲量将施加到刚体重心，可选
    
  在相对刚体的某一点上施加一个冲量(冲量是一个短时间内加到刚体上的力，冲量= 力 * 时间)，这个点可以是刚体表面上的任意一点。冲量将影响刚体的velocity 速度和angularVelocity 角速度

* #### **applyImpulseLocal\(\)  **:void

  参数为一个必需参数和一个可选参数：
    1. impulse 施加在刚体所在物理空间的冲量，必需
    2. relativePoint 刚体所在的物理世界中的一个关联点，如果不给出，它将被设置为零，所有的冲量将施加到刚体重心，可选
    
  在相对刚体的某一点上施加一个冲量(冲量是一个短时间内加到刚体上的力，冲量= 力 * 时间)，这个点可以是刚体表面上的任意一点。冲量将影响刚体的velocity 速度和angularVelocity 角速度

* #### **emit\(event\)  **:EventEmitter

  参数为需要触发的事件

  触发一个事件，并返回自身，用于链式调用

* #### **fromPolygon\(path :Array, [Options :Object]\)  **:Boolean

  参数为一个装满类似[0,0],[0,1]的位置点的数组，必需；
  第二个是一个可选的配置项，里面包括：
    1. optimalDecomp 是否开启最优分解，当顶点大于10个时性能将下降默认为false，可选
    2. skipSimpleCheck 如果你已经知道路径不会相交，将其设置为true，跳过检查
    3. removeCollinearPoints 设置为一个数字（角度阈值）去除共线点，或false保持所有点。
    
  读取一个多边形路路径，转化为凸型并将其放置在适当的偏移点上。
  
  如果成功则返回true，否则为false

* #### **getAABB\(\)  **:AABB

  返回从刚体中的AABB实例，如果必要这个AABB 将会被更新；

* #### **getArea\(\)  **:Number 

  返回刚体所包含的形状总面积

* #### **getVelocityAtPoint\(result :Array, relativePoint :Array\)  **:Array

  参数为一个放置结果的向量数组，一个面向世界的向量，需要得到速度信息的点的位置。
  
  返回刚体上一个点的速度

* #### **has\(\)  **:void

  更新刚体的包围盒，并设置aabbNeedsUpdate 为false

* #### **updateAABB\(\)  **:void

  更新刚体的包围盒，并设置aabbNeedsUpdate 为false

* #### **updateAABB\(\)  **:void

  更新刚体的包围盒，并设置aabbNeedsUpdate 为false

* #### **updateAABB\(\)  **:void

  更新刚体的包围盒，并设置aabbNeedsUpdate 为false

* #### **updateAABB\(\)  **:void

  更新刚体的包围盒，并设置aabbNeedsUpdate 为false

* #### **updateAABB\(\)  **:void

  更新刚体的包围盒，并设置aabbNeedsUpdate 为false

* #### **updateAABB\(\)  **:void

  更新刚体的包围盒，并设置aabbNeedsUpdate 为false

* #### **updateAABB\(\)  **:void

  更新刚体的包围盒，并设置aabbNeedsUpdate 为false

* #### **updateAABB\(\)  **:void

  更新刚体的包围盒，并设置aabbNeedsUpdate 为false

* #### **updateAABB\(\)  **:void

  更新刚体的包围盒，并设置aabbNeedsUpdate 为false

* #### **updateAABB\(\)  **:void

  更新刚体的包围盒，并设置aabbNeedsUpdate 为false

* #### **updateAABB\(\)  **:void

  更新刚体的包围盒，并设置aabbNeedsUpdate 为false

* #### **updateAABB\(\)  **:void

  更新刚体的包围盒，并设置aabbNeedsUpdate 为false






### 事件

---

* **sleep **

* **sleepy **

* **wakeup **



