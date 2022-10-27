[TOC]

#### 01- 继承和级联

CSS中的优先级分为两大类，继承和级联，其中<u>继承的CSS优先级一定位于最底层</u>。

例1：

```css
.text { color: orange;}
div [class] { color: red;}
div::first-line { color: blue;} /* 蓝色*/
div { color: green !important;}
```

```html
<div class="text">文字</div>
```

对比的不是选择器的优先级（权重），而是继承与否。color属性是一个可继承属性，::first-line设置的样式优先级大于任意的继承样式。DOM层级越深的元素所继承的CSS优先级越高。

```html
<!DOCTYPE html>
<html>
<body>
    <p>文字颜色</p>
</body>
</html>
```

```css
:root {
    color: red;
}
body {
    color: green;
}
```



#### 02- 关于级联

CSS中一层一层的优先级规则可以看成是级联。

日常开发代码 > @layer开发代码 > 插件注入代码 > 浏览器内置代码

#### 03- @layer 规则

将希望低优先级的CSS代码放在@layer规则中，不用担心选择器优先级过高的问题

例：

```css
@layer {
    .container .some-button { height: 30px;}
    :any-link { color: blue;}
    :any-link:hover { color: darkblue;}
}

/* 优先级大于@layer，无需在意选择器权重 */
.some-button { height: 40px;}
a { color: deepskyblue;}
a:hover { color: skyblue;}
```



#### 04- 了解 !important

任何CSS声明在后面设置了 !important之后，其级联层级就会跃升。

1. 层级跃阶
   级联层级提升；
2. 逆向跃阶
   原本级联水平高的CSS声明应用了!important后，其优先级反而变低；而原本级联水平低的CSS声明应用了!important后，CSS计算的优先级变高。

#### 05- 每一级中的优先级

1. 内联

   ```css
   <p style="color:aliceblue">颜色</p>
   ```

2. ID选择器

   ```css
   #some-id { color: aqua;}
   ```

3. 类、伪类、属性选择器

   ```css
   .some-id,
   [some-attr],
   :first-child { color: beige}
   ```

4. 标签选择器

   ```css
   some-tag { color: cadeblue;}
   ```

5. 通配符选择器、功能伪类

   ```css
   *, :not(), :is(), :where(any-selector) {
       color: darkcyan
   }
   ```

以上CSS选择器，权重从上往下排序