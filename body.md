刚体 \(Body\) 指的是具有质量、位置、速度以及一些用于碰撞的形状的物理对象；

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

  ```
    包围盒的上边界坐标数组，包含x,y 值
  ```

* **lowerBound**

  ```
    包围盒的下边界坐标数组，包含x,y 值
  ```

### 方法

---

* **containsPoint  **:boolean

  ```
  参数为包含指定的坐标点的数组 [ x, y ]；

  检测指定的点是否在包围盒中；
  ```

* **copy  **:void

  ```
  参数为一个AABB 类型对象

  将指定的AABB 对象复制到当前对象中
  ```

* **extend  **:void

  ```
  参数为一个AABB 类型对象

  继承指定的AABB 对象，使得当前对象覆盖对应的AABB 对象
  ```

* **overlaps  **:boolean

  ```
  参数为一个AABB 类型对象

  检测当前AABB 对象是否覆盖指定的AABB 对象
  ```

* **overlapsRay  **:number

  ```
  参数为一个Ray 对象

  检测当前AABB 对象是否被指定的Ray 对象击中，如果没有击中则返回 -1，如果击中则返回 0 - 1 之间的一个数；
  ```

* **setFromPoints**

  ```
  参数为四个：
     要设置AABB 对象的新坐标点数组(Points :Array)
     位移位置数组(Position :Array)
     要旋转的角度(Angle :Number)
     加给包围盒的边距(skinSize: Number)

  在指定位置创建AABB对象并进行位移及旋转，同时拓宽包围盒边距。
  ```






