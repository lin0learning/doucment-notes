## CSS3

#### 1. transform-origin

transform-origin：变形的原点（即坐标系 0， 0点）

- 一个值：设置 x轴 的原点，y轴默认50%
- 两个值：设置 x轴 和 y轴 的原点
- 三个值：设置 x轴、y轴 和 z轴的原点
- 必须是<length>，<percentage>，或者left，center，right，top，bottom关键字中的一个；

```css
transform-origin: top left;
```



#### 2. 3D动画 - transform

- 平移：translate3d(tx, ty, tz)
  - translateX(tx)、translateY(ty)、translateZ(tz)
- 缩放：scale3d(sx, sy, sz)
  - scaleX(sx)、scaleY(sy)、scaleZ( sz)
- 旋转：rotate3d(x, y, z, a)
  - rorateX(x)、rorateY(y)、rorateZ(z)
- 简写：rotate3d(x, y, z, deg)

注意：3D形变函数会创建一个**合成层**来启用**GPU硬件加速**。



#### 3. 3D透视 - perspective

- 值必须是 none length中的一个
- 透视的两种使用方式：
  1. 在父元素上定义CSS透视属性
  2. 如果它是子元素或单元素子元素，可以使用函数 `perspective()`



#### 4. 3D缩放 - scale

```css
transform: scaleX(2) scaleY(2);
/* 简写 */
transform: scale3d(2,2,1);   /* 区别: 此方法会创建一个合成层，开启GPU硬件加速，做到性能优化 */
```



#### 5. 3D空间 - transform - style

该CSS属性用于设置元素的<font color="red">子元素是定位在3D空间中</font>还是<font color="red">展在元素的2D平面</font>中。

**值类型：**

- flat：元素的子元素位于元素本身的平面内；
- preserve-3d：元素的子元素应位于<font color="red">3D</font>空间中。



制作动画采用定位，使其脱离标准流，不会产生回流或重绘的问题，节省了浏览器渲染性能（性能优化）。



#### 6. 3D背面可见性 - backface-visibility

- 该CSS属性指定某个元素当背面朝向观察者时是否可见。