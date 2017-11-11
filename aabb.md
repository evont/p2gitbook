AABB \( Axis aligned bounding box \)，中文意思为轴对称包围盒；

在游戏中，为了简化物体之间的碰撞检测运算，通常会对物体创建一个规则的几何外形将其包围。

由于轴对称包围盒，顾名思义，与坐标轴对称，所以给定一个最大的坐标点和一个最小的坐标点，就可以确定一个形状。

### 构造器 

---

一个 Object 对象，包含了 upperBound 上边界坐标及 lowerBound 下边界坐标

构造器函数如下：

```js
constructor(options?: {
    upperBound?: number[];
    lowerBound?: number[];
});
```

### 属性

---

* **upperBound**

        包围盒的上边界坐标数组，包含x,y 值

* **lowerBound**

        包围盒的下边界坐标数组，包含x,y 值

### 方法

---

* **containsPoint  **:boolean

        参数为包含**指定的坐标点**的数组 \[ x, y \]；

        检测指定的点是否在包围盒中；

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

        参数为四个，第一个是要设置AABB 对象的新坐标点数组\(Points :Array\)， 第二个是位移位置数组\(Position :Array\)，第三个是要旋转的角度\(Angle :Number\)，第四个是要加给包围盒的边距\(skinSize: Number\)

        在指定位置创建AABB对象并进行位移及旋转，同时拓宽包围盒边距。

