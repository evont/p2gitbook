Angle Lock Equation（角锁方程）用于锁定两个刚体之间的相对角度，这一约束试图将两个向量之间的点积保持为0（[dot product](https://en.wikipedia.org/wiki/Dot_product)）。

## 构造器

---

接受两个必需参数和一个可选参数，前两个参数为需要限制相对角度的两个Body 对象，函数中为bodyA 和bodyB， 第三个参数是一个对象，包含了angle 和ratio，angle为赋予bodyA 的角度，第二个是变速比。

构造器函数如下：

```js
function AngleLockEquation(bodyA, bodyB, options){
    options = options || {};
    Equation.call(this,bodyA,bodyB,-Number.MAX_VALUE,Number.MAX_VALUE);
    this.angle = options.angle || 0;

    /**
     * The gear ratio.
     * @property {Number} ratio
     * @private
     * @see setRatio
     */
    this.ratio = typeof(options.ratio)==="number" ? options.ratio : 1;

    this.setRatio(this.ratio);
}
```

## 属性

---

* #### **bodyA**

  将要加入约束的第一个刚体，body 类型

* #### **bodyB**

  将要加入约束的第二个刚体，body 类型

* #### **enabled**

  设置或获取当前方程式的可用状态，如果为true， 它将被添加到求解中，Boolean 类型

* #### **G**

  两个连接对象的[雅克布矩阵](http://mathworld.wolfram.com/Jacobian.html) ，Array 类型，包含了6个数字，分别是两个对象的x, y 和 angle

* #### **maxForce**

  求解时施加的最大作用力，Number 类型

* #### **minForce**

  求解时施加的最小作用力，Number 类型

* #### **multiplier**

  由上一次求解得到的约束乘数，大致相当于约束所产生的作用力。Number 类型

* #### **needsUpdate**

  标志刚度或弛豫是否改变，Boolean 类型

* #### **relativeVelocity**

  相对速度，Boolean 类型

* #### **relaxation**

  稳定约束方程所需的步进， 通常为3到5个步进。Number 类型

* #### **stiffness**

  约束方程的刚度，通常使用一个较大的数字（〜1e7），但也可以自由设置一个数字以获得比较稳定的模拟。Number 类型

## 方法

---

* #### **addToWlambda\(deltalambda :Number\)  **:void

  参数为△λ\(delta lambda\)  
  添加约束速度到刚体中

* #### **computeB\(\) **:Number

  计算SPOOK 方程的RHS 值（Computes the RHS of the SPOOK equation）

* #### **computeGiMf\(\) **:Number

  $$G * inv(M) * f$$  
  计算G值乘以 [inv\(M\)](https://cn.mathworks.com/help/matlab/ref/inv.html?requestedDomain=www.mathworks.com) \(M 为每个物体对角线块的质量矩阵\) 乘以f \(刚体的作用力\)

* #### **computeGiMGt\(\)  **:Number

  $$G*inv(M)*G'$$  
  计算G值乘以[inv\(M\)](https://cn.mathworks.com/help/matlab/ref/inv.html?requestedDomain=www.mathworks.com) \(M 为每个物体对角线块的质量矩阵\) 乘以G的导数

* #### **computeGq\(\)  **:Number

  $$G*q$$  
   计算G值乘以q\(q 为广义刚体坐标\)

* #### **computeGW\(\)  **:Number

  $$ G*W$$  
  计算G值乘以W\(W 为刚体的速度\)

* #### **computeGWlambda  **:Number

  $$ G*Wlambda$$  
  计算G值乘以Wlambda \(W 为刚体的速度\)

* #### **computeInvC\(eps\) **:Number

  参数为eps，一个极小的正数，用于控制迭代精度；

  $$ C = G * inv（M）* G'+ eps$$  
  计算SPOOK等式的分母部分：C = G _ inv（M）_ G'+ eps

* #### **gmult  **:Number

  将雅克比接口乘以相应的位置或速度

* #### **setMaxTorque\(torque :Number\)  **:void

  参数为torque扭矩，Number 类型  
  设置方程的最大作用力

* #### **setRatio **:void

  设置方程的变速比

* #### **update **:void

  根据当前参数计算SPOOK参数.a，.b和.epsilon。 参见[SPOOK笔记](http://www8.cs.umu.se/kurser/5DV058/VT09/lectures/spooknotes.pdf)中的等式9,10和11。



