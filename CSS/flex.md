# Flex 布局

<style>
.box {
    display: flex;
}
.box-item {
    width: 200px;
    height: 200px;
    line-height: 200px;
    vertical-align: middle;
    margin: 5px;
    background-color: #ffd200;
    font-size: 100px;
    color: white;
    text-align: center;
}
.box-item-sm {
    width: 50px;
    height: 50px;
    line-height: 50px;
    vertical-align: middle;
    margin: 5px;
    background-color: #ffd200;
    font-size: 25px;
    color: white;
    text-align: center;
}
.box-item-auto {
    width: auto;
    height: auto;
    line-height: 50px;
    vertical-align: middle;
    margin: 5px;
    background-color: #ffd200;
    font-size: 25px;
    color: white;
    text-align: center;
}

</style>

Flex 是2009年提出的新的布局方案，用来代替原来的盒状模型。

- [容器属性](#容器属性)
  - [flex-direction: 主轴方向](#flex-direction-主轴方向)
  - [flex-wrap: 是否换行](#flex-wrap-是否换行)
  - [flex-flow: direction+wrap](#flex-flow-directionwrap)
  - [justify-content: 主轴上的对齐方式](#justify-content-主轴上的对齐方式)
  - [align-items: 交叉轴上的对齐方式](#align-items-交叉轴上的对齐方式)
  - [align-content: 多根轴线的对齐方式](#align-content-多根轴线的对齐方式)
- [项目的属性](#项目的属性)
  - [order: \<integer>: 项目的排列顺序](#order-integer-项目的排列顺序)
  - [flex-grow: \<number>: 定义项目的放大比例](#flex-grow-number-定义项目的放大比例)
  - [flex-shrink: \<number>: 定义了项目的缩小比例](#flex-shrink-number-定义了项目的缩小比例)
  - [flex-basis: \<length> or auto 在分配多余空间之前，项目占据的主轴空间](#flex-basis-length-or-auto-在分配多余空间之前项目占据的主轴空间)
  - [flex: flex-grow + flex-shrink + flex-basis](#flex-flex-grow--flex-shrink--flex-basis)
  - [align-self: item 的对齐方式](#align-self-item-的对齐方式)

## 容器属性

### flex-direction: 主轴方向

决定主轴的方向（即项目的排列方向）

![](./flex-container.png)

<style>
.box-row {
    flex-direction: row;
}
.box-rowr {
    flex-direction: row-reverse;
}
.box-column {
    flex-direction: column;
}
.box-columnr {
    flex-direction: column-reverse;
}
</style>

1. `flex-direction: row` （默认值）：主轴为水平方向，起点在左端。
    <details><summary>Show</summary>
    <div class="box box-row">
        <div class="box-item-sm">1</div>
        <div class="box-item-sm">2</div>
        <div class="box-item-sm">3</div>
    </div>
    </details>

2. `flex-direction: row-reverse` 主轴为水平方向，起点在右端。
    <details><summary>Show</summary>
    <div class="box box-rowr">
        <div class="box-item-sm">1</div>
        <div class="box-item-sm">2</div>
        <div class="box-item-sm">3</div>
    </div>
    </details>

3. `flex-direction: column` 主轴为垂直方向，起点在上沿。
    <details><summary>Show</summary>
    <div class="box box-column">
        <div class="box-item-sm">1</div>
        <div class="box-item-sm">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item-sm">4</div>
    </div>
    </details>

4. `flex-direction: column-reverse` 主轴为垂直方向，起点在下沿。
    <details><summary>Show</summary>
    <div class="box box-columnr">
        <div class="box-item-sm">1</div>
        <div class="box-item-sm">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item-sm">4</div>
    </div>
    </details>

### flex-wrap: 是否换行

默认情况下，项目都排在一条线，flex-wrap 可以设置拍不下之后换行

<style>
.box-wrap {
    flex-wrap: wrap;
}
.box-nowrap {
    flex-wrap: nowrap;
}
.box-wrapr {
    flex-wrap: wrap-reverse;
}
</style>

1. `flex-wrap: nowrap` （默认）：不换行
    <details><summary>Show</summary>
    <div class="box box-row box-nowrap">
        <div class="box-item">1</div>
        <div class="box-item">2</div>
        <div class="box-item">3</div>
        <div class="box-item">4</div>
        <div class="box-item">5</div>
        <div class="box-item">6</div>
    </div>
    </details>

1. `flex-wrap: wrap` 换行，第一行在上方。
    <details><summary>Show</summary>
    <div class="box box-row box-wrap">
        <div class="box-item">1</div>
        <div class="box-item">2</div>
        <div class="box-item">3</div>
        <div class="box-item">4</div>
        <div class="box-item">5</div>
        <div class="box-item">6</div>
    </div>
    </details>
3. `flex-wrap: wrap-reverse`  换行，第一行在下方。
    <details><summary>Show</summary>
    <div class="box box-row box-wrapr">
        <div class="box-item">1</div>
        <div class="box-item">2</div>
        <div class="box-item">3</div>
        <div class="box-item">4</div>
        <div class="box-item">5</div>
    </div>
    </details>

### flex-flow: direction+wrap

flex-flow 属性是 flex-direction 属性和 flex-wrap 属性的简写形式，默认值为 row nowrap。

<style>
.box-row-wrap {
    flex-flow: row wrap;
}
.box-row-nowrap {
    flex-flow: row nowrap;
}
</style>

1. `flex-flow: row wrap` 水平，换行
    <details><summary>Show</summary>
    <div class="box box-row-wrap">
        <div class="box-item">1</div>
        <div class="box-item">2</div>
        <div class="box-item">3</div>
        <div class="box-item">4</div>
        <div class="box-item">5</div>
    </div>
    </details>

2. `flex-flow: row nowrap` 水平，不换行
    <details><summary>Show</summary>
    <div class="box box-row-nowrap">
        <div class="box-item">1</div>
        <div class="box-item">2</div>
        <div class="box-item">3</div>
        <div class="box-item">4</div>
        <div class="box-item">5</div>
    </div>
    </details>

### justify-content: 主轴上的对齐方式

justify-content 属性定义了项目在主轴上的对齐方式。

<style>
.box-j-start {
    justify-content: flex-start;
}
.box-j-end {
    justify-content: flex-end;
}
.box-j-center {
    justify-content: center;
}
.box-j-between {
    justify-content: space-between ;
}
.box-j-around {
    justify-content: space-around;
}
</style>

1. `justify-content: flex-start` 左对齐
    <details><summary>Show</summary>
    <div class="box box-j-start">
        <div class="box-item-sm">1</div>
        <div class="box-item-sm">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item-sm">4</div>
        <div class="box-item-sm">5</div>
    </div>
    </details>

2. `justify-content: flex-end` 右对齐
    <details><summary>Show</summary>
    <div class="box box-j-end">
        <div class="box-item-sm">1</div>
        <div class="box-item-sm">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item-sm">4</div>
        <div class="box-item-sm">5</div>
    </div>
    </details>

3. `justify-content: center` 居中
    <details><summary>Show</summary>
    <div class="box box-j-center">
        <div class="box-item-sm">1</div>
        <div class="box-item-sm">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item-sm">4</div>
        <div class="box-item-sm">5</div>
    </div>
    </details>

4. `justify-content: space-between` 两端对齐
    <details><summary>Show</summary>
    <div class="box box-j-between">
        <div class="box-item-sm">1</div>
        <div class="box-item-sm">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item-sm">4</div>
        <div class="box-item-sm">5</div>
    </div>
    </details>

5. `justify-content: space-around` 左对齐
    <details><summary>Show</summary>
    <div class="box box-j-around">
        <div class="box-item-sm">1</div>
        <div class="box-item-sm">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item-sm">4</div>
        <div class="box-item-sm">5</div>
    </div>
    </details>

### align-items: 交叉轴上的对齐方式

align-items 属性定义项目在交叉轴上如何对齐。

<style>
.box-align-item-start {
  align-items: flex-start;
}
.box-align-item-end {
  align-items: flex-end;
}
.box-align-item-center {
  align-items: center;
}
.box-align-item-baseline {
  align-items: baseline;
}
.box-align-item-stretch {
  align-items: stretch;
}
</style>

1. `align-items: flex-start` 交叉轴的起点对齐
    <details><summary>Show</summary>
    <div class="box box-align-item-start">
        <div class="box-item-sm">1</div>
        <div class="box-item">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item">4</div>
        <div class="box-item-sm">5</div>
    </div>
    </details>

2. `align-items: flex-end` 交叉轴的终点对齐
    <details><summary>Show</summary>
    <div class="box box-align-item-end">
        <div class="box-item-sm">1</div>
        <div class="box-item">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item">4</div>
        <div class="box-item-sm">5</div>
    </div>
    </details>

3. `align-items: center` 交叉轴的中点对齐
    <details><summary>Show</summary>
    <div class="box box-align-item-center">
        <div class="box-item-sm">1</div>
        <div class="box-item">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item">4</div>
        <div class="box-item-sm">5</div>
    </div>
    </details>

4. `align-items: baseline` 项目的第一行文字的基线对齐
    <details><summary>Show</summary>
    <div class="box box-align-item-baseline">
        <div class="box-item-sm">1</div>
        <div class="box-item">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item">4</div>
        <div class="box-item-sm">5</div>
    </div>
    </details>

5. `align-items: stretch` 如果项目未设置高度或设为auto，将占满整个容器的高度
    <details><summary>Show</summary>
    <div class="box box-align-item-stretch">
        <div class="box-item-sm">1</div>
        <div class="box-item">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item">4</div>
        <div class="box-item-auto">5</div>
    </div>
    </details>
    
### align-content: 多根轴线的对齐方式

align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。


<style>
.box-align-content-container{
    flex-flow: row wrap;
    height: 300px;
    background: lightgrey;
}
.box-align-content-start {
  align-content: flex-start;
}
.box-align-content-end {
  align-content: flex-end;
}
.box-align-content-center {
  align-content: center;
}
.box-align-content-between {
  align-content: space-between;
}
.box-align-content-around {
  align-content: space-around;
}
.box-align-content-stretch {
  align-content: stretch;
}
</style>

1. `align-content: flex-start` 与交叉轴的起点对齐
    <details><summary>Show</summary>
    <div class="box box-align-content-container box-align-content-start">
        <div class="box-item-sm">1</div>
        <div class="box-item-sm">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item-sm">4</div>
        <div class="box-item-sm">5</div>
        <div class="box-item-sm">6</div>
        <div class="box-item-sm">7</div>
        <div class="box-item-sm">8</div>
        <div class="box-item-auto">auto</div>
    </div>
    </details>

2. `align-content: flex-end` 与交叉轴的终点对齐
    <details><summary>Show</summary>
    <div class="box box-align-content-container box-align-content-end">
        <div class="box-item-sm">1</div>
        <div class="box-item-sm">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item-sm">4</div>
        <div class="box-item-sm">5</div>
        <div class="box-item-sm">6</div>
        <div class="box-item-sm">7</div>
        <div class="box-item-sm">8</div>
        <div class="box-item-auto">auto</div>
    </div>
    </details>

3. `align-content: center` 与交叉轴的中点对齐
    <details><summary>Show</summary>
    <div class="box box-align-content-container box-align-content-center">
        <div class="box-item-sm">1</div>
        <div class="box-item-sm">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item-sm">4</div>
        <div class="box-item-sm">5</div>
        <div class="box-item-sm">6</div>
        <div class="box-item-sm">7</div>
        <div class="box-item-sm">8</div>
        <div class="box-item-auto">auto</div>
    </div>
    </details>

4. `align-content: space-between` 与交叉轴两端对齐，轴线之间的间隔平均分布
    <details><summary>Show</summary>
    <div class="box box-align-content-container box-align-content-between">
        <div class="box-item-sm">1</div>
        <div class="box-item-sm">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item-sm">4</div>
        <div class="box-item-sm">5</div>
        <div class="box-item-sm">6</div>
        <div class="box-item-sm">7</div>
        <div class="box-item-sm">8</div>
        <div class="box-item-auto">auto</div>
    </div>
    </details>

5. `align-content: space-around` 每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
    <details><summary>Show</summary>
    <div class="box box-align-content-container box-align-content-around">
        <div class="box-item-sm">1</div>
        <div class="box-item-sm">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item-sm">4</div>
        <div class="box-item-sm">5</div>
        <div class="box-item-sm">6</div>
        <div class="box-item-sm">7</div>
        <div class="box-item-sm">8</div>
        <div class="box-item-auto">auto</div>
    </div>
    </details>

6. `align-content: stretch` 轴线占满整个交叉轴。
    <details><summary>Show</summary>
    <div class="box box-align-content-container box-align-content-stretch">
        <div class="box-item-sm">1</div>
        <div class="box-item-sm">2</div>
        <div class="box-item-sm">3</div>
        <div class="box-item-sm">4</div>
        <div class="box-item-sm">5</div>
        <div class="box-item-sm">6</div>
        <div class="box-item-sm">7</div>
        <div class="box-item-sm">8</div>
        <div class="box-item-auto">auto</div>
    </div>
    </details>

## 项目的属性

### order: \<integer>: 项目的排列顺序

<style>
.item_order__1 {
    order: -1;
}
.item_order_0 {
    order: 0;
}
.item_order_1 {
    order: 1;
}
.item_order_9 {
    order: 9;
}
.item_order_100 {
    order: 100;
}
</style>

<details><summary>Show</summary>
    <div class="box box-row">
        <div class="box-item-sm item_order_100">100</div>
        <div class="box-item-sm item_order__1">-1</div>
        <div class="box-item-sm item_order_9">9</div>
        <div class="box-item-sm item_order_0">0</div>
        <div class="box-item-sm item_order_1">1</div>
    </div>
</details>

### flex-grow: \<number>: 定义项目的放大比例

默认为 0，即如果存在剩余空间，也不放大。

<style>
.item_grow_0 {
    flex-grow: 0;
}
.item_grow_1 {
    flex-grow: 1;
}
.item_grow_2 {
    flex-grow: 2;
}
</style>

<details><summary>Show</summary>
    <div class="box box-row">
        <div class="box-item-sm item_grow_0">0</div>
        <div class="box-item-sm item_grow_0">0</div>
        <div class="box-item-sm item_grow_0">0</div>
    </div>
        <div class="box box-row">
        <div class="box-item-sm item_grow_1">1</div>
        <div class="box-item-sm item_grow_1">1</div>
        <div class="box-item-sm item_grow_1">1</div>
    </div>
        <div class="box box-row">
        <div class="box-item-sm item_grow_0">0</div>
        <div class="box-item-sm item_grow_1">1</div>
        <div class="box-item-sm item_grow_2">2</div>
    </div>
</details>


### flex-shrink: \<number>: 定义了项目的缩小比例

默认为1，即如果空间不足，该项目将缩小。

<style>
.item_shrink_0 {
    flex-shrink: 0;
}
.item_grow_1 {
    flex-shrink: 1;
}
</style>

<details><summary>Show</summary>
    <div class="box box-row">
        <div class="box-item item_shrink_0">0</div>
        <div class="box-item item_shrink_0">0</div>
        <div class="box-item item_shrink_0">0</div>
    </div>
    <div class="box box-row">
        <div class="box-item item_shrink_1">1</div>
        <div class="box-item item_shrink_1">1</div>
        <div class="box-item item_shrink_1">1</div>
    </div>
    <div class="box box-row">
        <div class="box-item item_shrink_0">0</div>
        <div class="box-item item_shrink_1">1</div>
        <div class="box-item item_shrink_1">1</div>
    </div>
</details>

### flex-basis: \<length> or auto 在分配多余空间之前，项目占据的主轴空间

浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。

<style>
.item_basis_auto {
    flex-basis: auto;
    font-size: 20px;
}
.item_basis_100 {
    flex-basis: 100px;
    font-size: 20px;
}
</style>

<details><summary>Show</summary>
    <div class="box box-row">
        <div class="box-item item_basis_auto">auto</div>
        <div class="box-item item_basis_100">100</div>
    </div>
    <div class="box box-row">
        <div class="box-item item_basis_100">100</div>
        <div class="box-item item_basis_auto">auto</div>
    </div>
</details>

### flex: flex-grow + flex-shrink + flex-basis

默认值为 0 1 auto。后两个属性可选。
两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。

<style>
.item_flex_auto {
    flex: auto;
}
.item_flex_none {
    flex: none;
}
</style>

1. flex: auto
    <details><summary>Show</summary>
    <div class="box box-row">
        <div class="box-item item_flex_auto">auto</div>
        <div class="box-item item_flex_auto">auto</div>
    </div>
    <div class="box box-row">
        <div class="box-item-sm item_flex_auto">auto</div>
        <div class="box-item-sm item_flex_auto">auto</div>
    </div>
    </details>

2. flex: none
    <details><summary>Show</summary>
    <div class="box box-row">
        <div class="box-item item_flex_none">non</div>
        <div class="box-item item_flex_none">non</div>
    </div>
    <div class="box box-row">
        <div class="box-item-sm item_flex_none">non</div>
        <div class="box-item-sm item_flex_none">non</div>
    </div>
    </details>

### align-self: item 的对齐方式

允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。

<style>
.item_align_self {
    align-self: flex-end
}
</style>

<details><summary>Show</summary>
    <div class="box box-align-item-start">
        <div class="box-item-sm">1</div>
        <div class="box-item">2</div>
        <div class="box-item-sm item_align_self">3</div>
        <div class="box-item">4</div>
        <div class="box-item-sm">5</div>
    </div>
</details>
