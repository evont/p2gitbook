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
* **bodyB**
* **enabled**
* **G**
* **maxForce**
* **minForce**
* **multiplier**
* **needsUpdate**
* **relativeVelocity**
* **relaxation**
* **stiffness**

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



