Angle Lock Equation（角锁方程）用于锁定两个刚体之间的相对角度，这一约束试图将两个向量之间的点积保持为0（[dot product](https://en.wikipedia.org/wiki/Dot_product)）。

### 构造器

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

### 属性

---

* **bodyA**

        将要加入约束的第一个刚体，body 类型

* **bodyB**

        将要加入约束的第二个刚体，body 类型

* **enabled**

        设置或获取当前方程式的可用状态，如果为true， 它将被添加到求解中，Boolean 类型

* **G**

        两个连接对象的[雅克布矩阵](http://mathworld.wolfram.com/Jacobian.html) ，Array 类型，包含了6个数字，分别是两个对象的x, y 和 angle

* **maxForce**

       求解时施加的最大作用力，Number 类型

* **minForce**

       求解时施加的最小作用力，Number 类型

* **multiplier**

        由上一次求解得到的约束乘数，大致相当于约束所产生的作用力。Number 类型

* **needsUpdate**

        标志刚度或弛豫是否改变，Boolean 类型

* **relativeVelocity**

        相对速度，Boolean 类型

* **relaxation**

        稳定约束方程所需的步进， 通常为3到5个步进。Number 类型

* **stiffness**

       约束方程的刚度，通常使用一个较大的数字（〜1e7），但也可以自由设置一个数字以获得比较稳定的模拟。Number 类型

### 方法

---

* **addToWlambda**

        

* **computeB**
* **computeGiMf**
* **computeGiMGt**
* **computeGq**
* **computeGW**
* **computeGWlambda**
* **computeInvC**
* **gmult**
* **setMaxTorque**
* **setRatio**
* **update**



