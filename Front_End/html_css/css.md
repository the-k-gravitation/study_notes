## CSS 特性

### 继承性

`子级` 默认继承 `父级` 的 `文字控制属性`

### 层叠性

- 相同属性会覆盖： 后面的 CSS 属性覆盖前面的 CSS 属性
- 不同的属性会叠加： 不同的 CSS 属性都生效

### 优先级

优先级，也叫`权重`。当一个标签使用了多种选择器时， 基于不同类的选择器的 匹配规则。

规则： `通配符选择器 < 标签选择器 < 类选择器 < id 选择器 < 行内样式 < !important` 。 （选中标签的范围越大，优先级越低）

如果是复合选择器，则需要权重叠加计算。

`(行内样式, id选择器个数, 类选择器个数， 标签选择器个数)`

规则：

- 从左向右 依次比较个数，同一级个数多的优先级高， 如果个数相同，则向后比较
- !important 权重最高
- 继承权重最低

## 选择器

### 后代选择器

```css
div p {
  /* 会选择div下面所有的p，不管p嵌套有多深  */
}
```

### 子代选择器

```css
div > p {
  /* 中会选择div的直接子元素中的p，不会进行嵌套选择*/
}
```

### 交集选择器

```css
div.demo {
  /* 选择 div 标签中有 demo 类名的 div */
}
```

### 伪类选择器

伪类表示元素 `状态`，选中元素的某个状态设置样式。

`超链接` 一共有 4 个状态： `:link`、 `:visited`、 `:hover`、 `:active` , 对其设置时，需要按 `LVHA` 的顺序书写。

### 结构伪类选择器

作用： 根据元素的结构关系查找元素。

- :first-child()
- :last-child()
- :nth-child(N)

| 功能                  | 公式       |
| --------------------- | ---------- |
| 偶数                  | 2n         |
| 奇数                  | 2n+1; 2n-1 |
| 找到 5 的倍数的标签   | 5n         |
| 找到第个以后的标签    | n+5        |
| 找到第 5 个以前的标签 | -n+5       |

### 伪元素选择器

作用：创建虚拟元素（伪元素），用来摆放装饰性的内容。

- ::before 给所在元素里面 `最前面` 添加一个伪元素
- ::after 给所在元素里面 `最后面` 添加一个伪元素

注意：

1. 必须设置`content`属性
2. 伪元素默认是`行内`显示模式
3. 权重和标签选择器相同

## 显示模式

通过 `display` 属性来进行设置

### block 块级元素

1. 独占一行
2. 宽度默认为父级的 100%
3. 添加宽高属性会`生效`

### inline 行内元素

1. 一行可以显示多个
2. 设置`宽高`属性`不生效`
3. 宽高尺寸由内容撑开

### inline-block 行内块元素

1. 一行可以显示多个
2. 设置`宽高`属性`生效`
3. 宽高尺寸也可以由内容撑开

```css
img {
  width: 80px;
  height: 80px;
}
<!-- <img src='info.jpg'> -->
```

## 盒子模型

1. 组成部分：

   - content 内容
   - padding 内边距
   - border 边框线
   - margin 外边距

2. 盒子尺寸：

   默认情况下： `盒子尺寸 = 内容尺寸 + border尺寸 + 内边距尺寸`，盒子会变大，如果设置了 border 和 padding 的话。

   通过设置 `box-sizing: border-box;` 来开启内减模式，此时如果设置了 border 和 padding，盒子的总体大小会不变，border 和 padding 的尺寸也会成为盒子 width 和 height 中的一部分，实际的内容尺寸会变小。

   在使用 `margin: 0 auto;` 来进行`版心居中`设置时，盒子要有`宽度`设置，如果没有宽度设置，将不生效。

3. 元素溢出：

   通过 `overflow` 属性来控制溢出元素的内容显示方式。
   属性值： `hidden`, `scroll`, `auto`。

4. margin 在`垂直`方向上的合并现象:

   `垂直`方向上的兄弟元素， 其上下 margin 会合并，并取两个 margin 值中的较大值。

5. margin 塌陷问题：

   父子级的标签，在`子元素`上添加 `上外边距` 会产生塌陷现象，即导致父级一起向下移动。

   解决方法：

   - 取消子级 `margin`, 父级设置 `padding`。
   - 父级设置 `overflow: hidden;`
   - 父级设置 `border-top`。

6. 行内元素 - 内外边距问题

   给行内元素添加 `margin` 或者 `padding` 时，其在垂直方向不起作用。
   解决方法： 给行内元素 同时添加 `line-height` 属性。

   ```css
   span {
     margin: 10px;
     padding: 20px;

     <!-- 行高可以改变垂直位置 -->
     line-height: 100px;
   }
   ```

7. border-radius 圆角

   给盒子设置圆角

8. box-shadow 阴影

   作用： 给元素设置 阴影 效果
   属性值： `x轴偏移量 Y轴偏移量 模糊半径 扩散半径 颜色 内外阴影`

   - x 轴偏移量 Y 轴偏移量 必须提供
   - 默认是外阴影，如需内阴影，则提供 inset

   ```css
   div {
     box-shadow: 2px 5px 10px 2px rgba(0, 0, 0, 0.5);
     <!-- 内阴影 -->
     box-shadow: 2px 5px 10px 2px rgba(0, 0, 0, 0.5) inset;
   }
   ```

9. `vertical-align` 垂直对齐方式

    行内块和行内垂直方向对方方式。 对于行内元素和行内块元素，默认的对齐方式是基线对齐(baseline)，因为浏览器把 行内元素 和 行内块元素 当作文字来处理。

    属性值：
      - baseline: 基线对齐（默认）
      - top: 顶部对齐
      - middle: 居中对齐
      - bottom: 底部对齐

    ```html
    <div>
      <img src='./abc.jpg' alt=''>
      <a>垂直对齐方式</a>
    </div>
    ```

    ```css
    <!-- 给谁的高度高就添加在谁身上 -->
    img {
      vertical-align: middle;
    }
   ```

## 布局

### float 浮动

对元素设置 float 之后，其会脱离“标准流”的控制。

#### 清除浮动的方法

- 额外标签法

  在父元素内容的最后添加一个块级元素，并设置 `clear:both;`

- 单伪元素法

  ```css
  .clearfix::after {
    content: '';
    display: block;
    clear: both;
  }
  ```

- 双伪元素法(推荐)

  ```css
  <!-- .clearfix::before用来解决外边距塌陷问题 -- > .clearfix::before,
  .clearfix::after,
  .clearfix::before {
    content: '';
    display: table;
  }

  .clearfix::after {
    clear: both;
  }
  ```

- overflow

  父元素添加 `overflow: hidden;`

### flex

| 属性            | 说明                     |
| --------------- | ------------------------ |
| display: flex   | 创建 flex 容器           |
| justify-content | 主轴对齐方式             |
| align-items     | 侧轴对方方式             |
| align-self      | 某个弹性盒子侧轴对齐方式 |
| flex-direction  | 个性主轴方向             |
| flex            | 弹性伸缩比               |
| flex-wrap       | 弹性盒子换行             |
| align-content   | 行对齐方式               |

- `justify-content` 主轴对齐方式
  `align-content` 行对齐方式 （对单行弹性盒子不生效，要设置 flex-wrap）

  属性值：

  1. `flex-start`: 默认值，弹性盒子从起点开始依次排列
  2. `flex-end`: 弹性盒子从终点开始依次排列
  3. `center`: 弹性盒子沿 `主轴居中` 排列
  4. `space-between`: 弹性盒子沿主轴均匀排列， 空白间距均分在弹性盒子`之间`
  5. `space-around`: 弹性盒子沿主轴均匀排列， 空白间距均分在弹性盒子`两侧`
  6. `space-evenly`: 弹性盒子沿主轴均匀排列， 弹性盒子与容器之间间距相等

- `align-items` 侧轴对齐方式
  `align-self` 单独控制某个弹性盒子的侧轴对齐方式（设置在弹性盒子上）

  属性值：

  1. `stretch`: 弹性盒子沿着侧轴线被拉伸至铺满容器（当弹性盒子没有设置侧轴方向尺寸时，默认会拉伸）
  2. `center`: 弹性盒子沿侧轴居中排列
  3. `flex-start`: 弹性盒子从起点开始依次排列
  4. `flex-end`: 弹性盒子从终点开始依次排列

- `flex-direction` 主轴方向

  属性值：

  1. `row`: 水平方向，从左向右（默认）
  2. `column`: 垂直方向，从上向下
  3. `row-reverse`: 水平方向，从右向左
  4. `column-reverse`: 垂直方向，从下向上

- `flex` 设置弹性盒子的伸缩比

- `flex-wrap` 弹性盒子换行

  属性值：

  1. `wrap`: 换行
  2. `nowrap`: 不换行

### grid

## 定位

### relative 相对定位

特点：

1. 改变位置的参照物是 元素自己原来的位置
2. 元素不会脱离 标准流，原来的位置还是被其占据，虽然位置可能已经发生变化。
3. 标签显示模式不变。

一般不单独使用它，因为它位置改变了，但原来的位置还是被其占据。

```css
div {
  position: relative;
  top: 100px;
  left: 100px;
}
```

### absolute 绝对定位

使用场景： 子级绝对定位， 父级相对定位 （`子绝父相`） ,即子级的定位，相对于父级来进行定位

特点：

1. 元素脱离 标准流，不会占据其原来的位置。
2. 参照物：先找最近的已经定位的祖先元素，如果没找到有祖先元素进行了定位的，会以浏览器的可视区来进行定位。
3. 显示模式会发生改变。 元素的宽高属性会生效（绝对定位之后，元素具备了行内块级显示模式的特点）

### fixed 固定定位

特点：

1. 元素脱离 标准流，不会占据其原来的位置。
2. 参照物： 浏览器窗口。
3. 显示模式会发生改变。 如果设置了元素的宽高属性会生效（绝对定位之后，元素具备了行内块级显示模式的特点）

| 定位模式 | 属性值   | 是否脱标 | 显示模式             | 参照物                                  |
| -------- | -------- | -------- | -------------------- | --------------------------------------- |
| 相对定位 | relative | 否       | 保持标签原有显示模式 | 自己原来位置                            |
| 绝对定位 | absolute | 是       | 行内块特点           | 1. 已定位的父级元素， 2. 浏览器的可视区 |
| 固定定位 | fixed    | 是       | 行内块特点           | 浏览器窗口                              |

### z-index 堆叠层级

作用： 设置定位元素的层次顺序，改变定位元素的显示顺序。

### 定位居中

```css
div {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
```

## 字体修饰属性

- font-size 字体大小

  必须得有单位，否则属性不生效。

- font-weight 字体粗细
- font-style 字体倾斜

  - normal
  - italic

- line-height 行高

  - 数值 + 单位
  - 数值 --- 表示当前标签的`font-size`值的倍数

- font-family 字体族
- font 字体复合属性

  `font: font-style font-weight font-size/line-height font-family;`

  `字号` 和 `字体值` 必须书写，否则 font 属性不生效。

- text-indent 文本首行缩进

  - 数字 + 单位
  - 数字 + em （常用方式）

    ```css
    <!-- 表示首行缩进两个字 -->
    text-indent: 2em;
    ```

- text-align 内容对齐

  对齐的不是标签，而是标签中的内容。本质是控制内容的对齐方式，属性要设置给内容的`父级`。

- text-decoration 修饰线

  - none 无
  - underline 下划线
  - line-through 删除线
  - overline 上划线

- color 文本颜色

## 背景属性

- background-color 背景色
- background-image 背景图
- background-repeat 背景图平铺方式

  - no-repeat 不平铺
  - repeat 平铺（默认效果）
  - repeat-x 水平方向平铺
  - repeat-y 垂直方向平铺

- background-position 背景图位置

  属性值： `水平方向位置  垂直方向位置`

  - 关键字： `left`、`right`、`center`、`top`、`bottom`。 `只写一个关键字，另一个方向默认为居中`。

    ```css
    div {
      background-position: left bottom;
      <!-- background-position: center center; -->

      <!-- 只提供垂直方向的位置 ，水平默认为居中 -->
      background-position: bottom;

      <!-- 取值顺序可以颠倒 -->
      background-position: top right;
    }
    ```

  - 坐标（数字+单位，正负都可以）。`数字只写一个值表示水平方向， 垂直方向为居中`。

- background-size 背景图缩放

  - 关键字

    1. `cover`: 等比例缩放背景图片，`以使图片完全覆盖背景区`，可能背景图片部分会看不见的情况
    2. `contain`: 等比例缩放背景图片，`以使图片完全装入背景区`，可能出现背景区部分空白的情况，即当图片的宽或高与盒子重合时，就会停止缩放。

  - 百分比
    根据盒子尺寸计算图片大小

    ```css
    div {
      <!-- 100%： 图片的宽度跟盒子宽度一样，图片的高度按图片比例等比缩放 -->
      background-size: 100%;
    }
    ```

  - 数字+单位

- background-attachment 背景图固定
  属性值: `fixed`， 让背景图不会随着元素的内容滚动。

- background 背景复合属性
  不区分顺序

## CSS 精灵

css精灵，也叫 `CSS Sprites`, 是一种网页图片应用处理方式，把网页中一些背景图片整合到一张图片文件中，再通过 `background-position` 精确的定位出背景图片的位置。

实现步骤：

  1. 创建一个盒子元素，盒子尺寸与要显示的小图尺寸 相同。
  2. 设置盒子背景图为精灵图。
  3. 找到小图的`左上角`在精灵图中的位置坐标。
  4. 给盒子设置 `background-position` 属性，值为上步找到的位置的`负数`。

  ```css
  div { 
    width: 110px;
    height: 116px;
    background-image: url(./images/abcd.jpg);
    background-position: -98px -135px;
    <!-- 或者写在一起 -->
    background: url(./images/abcd.jpg) -98px -135px;
  }
  ```

## 动画

### transition 过渡效果

作用： 可以为一个元素在不同状态之间切换的时候添加过渡效果

属性值：`transition: transition-property transition-duration transition-timing-function transition-delay`
常用前两个： `过渡的属性 花费时间(s)`

### 改变转换原点

默认情况下，转换原点是 `盒子中心点`。

属性： `transform-origin: 水平原点位置 垂直原点位置` 。
取值：

- 方位名词（right, left, top, bottom, center）
- 像素单位数值
- 百分比

### transform 平面转换（2D转换）

作用： 为元素添加动态效果，一般与过渡配合使用。

#### 平移 translate

属性： `transform: translate(x, y);`

取值：

- 像素单位数值
- 百分比（参照盒子自身尺寸计算结果）
- 正负均可
- 单独设置X或Y轴移动，可以使用：translateX() 或者 translateY()。

```css
/* 只写一个值，表示沿着X轴移动 */
transform: translate(100px);
transform: translate(0, -100px);

transform: translate(50%, 150%);
```

#### 旋转 rotate

属性： `transform: rotate(旋转角度);`

注意：

- 角度单位是 `deg`
- 取值正负均可
- 正：顺时，负：逆时

#### scale 缩放

属性： `transform: scale(缩放倍数)；`， `transform: scale(x轴缩放倍数, y轴缩放倍数);`

#### skew 倾斜

属性： `transform: skew(角度度数deg);`

#### 多重转换

注意：

1. 旋转会改变坐标轴向
2. 多重转换时，以排在第一种转换形态的坐标轴为准
3. 要实现多重转换，必须得使用 transform 来进行组合。

```css
.box:hover img {

  /* 下面两个会得到完全不同的转换效果 */

  /* 此时，会以translate的坐标轴为准，即水平移动的同时还进行了旋转 */
  transform:translate(600px) rotate(360deg);

  /* 此时，会以rotate的坐标轴为准， 即旋转的同时还进行水平移动 */
  transform:rotate(360deg) translate(600px) ;
}
```

## 渐变

### 线性渐变

属性：

```css
background-image: linear-gradient(
  渐变方向,
  颜色1 终点位置,
  颜色2 终点位置,
  ...
);
```

取值：

- 渐变方向(可选)：
  1. to 方位名词
  2. 角度度数
- 终点位置(可选)：
  百分比

### 径向渐变

## SEO

### SEO 三大标签

- `title`: 网页标题标签
- `description`: 网页描述
- `keywords`: 网页关键词

## 开发技巧

### 网站的 Logo 制作

网站如果有 Logo 时，可以用 `h1>a` 的方式来处理，这样可以 SEO：

```html
<div class="logo">
  <h1><a href="#">网站的名称</a></h1>
</div>
```

```css
.logo a {
  display: block;
  width: 195px;
  height: 41px;
  background-image: url(../images/logo.png);
  <!-- 通过设置font-size：0来让 “网站名称”不显示出来，但能让搜索服务进行抓取 -->
  font-size: 0;
}
```

### input 设置flex:1 不生效的解决方法

因为对于 `input` 标签，浏览器会默认生效标签的默认宽度，所以在对其设置了`flex:1`时会出现没有作用的情况。
可以通过先设置 `width: 0;` 再设置 `flex:1` 来解决这个问题。

```css
input {
  width: 0;
  flex: 1;
}
```
