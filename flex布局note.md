# flex 布局
#### 为什么要使用flex布局？
~~针对传统布局方案的痛点，flex布局肯定有存在的优势和价值~~~~首先了解传统布局的形式，相对比flex布局又是什么形式。

####  传统布局与flex布局区别

传统布局，基于盒子模型，依赖display，position，float等。

如垂直居中可能用到position+transform。

使用flex设置垂直居中只需要设置align-items: center;

#### align-items和justify-content的区别

采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。

**`justify-content`**是[flex](https://so.csdn.net/so/search?q=flex&spm=1001.2101.3001.7020)布局中的一个属性，用来调整container中的items布局。**`justify-content`** 属性定义了浏览器之间，如何分配顺着弹性容器主轴(或者网格行轴) 的元素之间及其周围的空间。

**`align-items`**属性将所有直接子节点上的**`align-self`**值设置为一个组。**`align-self`**属性设置项目在其包含块中在交叉轴方向上的对齐方式。
