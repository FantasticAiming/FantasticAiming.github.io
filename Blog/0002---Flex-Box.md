# 弹性布局 —— Flex Box

![FlexBox2](https://raw.githubusercontent.com/FantasticAiming/FantasticAiming.github.io/main/Img/202306142229007.png)

## 前言

文章的开头，推荐一个练习弹性布局的闯关形式的小游戏，[FLEXBOX FROGGY](https://flexboxfroggy.com/)，蛮有趣的。虽然游戏难度不大，但可以当作验证自己对 Flex Box 的掌握度。

介绍弹性布局的文章其实已经有很多了，本文并没有什么出彩的地方，更没有什么高级用法，旨在分享我个人对于弹性布局各种属性的理解，如果能帮助到其他人那就再好不过了。

在正式介绍之前，我想说明一个点，那就是在使用 Flex 盒子的属性进行各种布局时，对于文字来说，在不修改 `direction` 属性时，只会影响文字的位置，不会影响文字的顺序。例如 `Hello` 无论如何也不会变成 `olleH`。

## Flex Box 概况

Flex 容器示意图：

![img](https://raw.githubusercontent.com/FantasticAiming/ITBlog/main/Img/202306130910807.png)

main axis：主轴。

- main start：主轴的起点。
- main end：主轴的终点。
- main size：Flex 容器中单个项目（元素）所占据的主轴的大小（长度）。

cross axis：侧轴，也叫交叉轴（也有翻译为横轴的，但是我认为这样容易误解为是主轴，因为主轴默认情况就如上图所示，是一个横着的状态。我个人比较习惯称之为侧轴）。

- cross start：侧轴的起点。
- cross end：侧轴的终点。
- cross size：Flex 容器中单个项目（元素）所占据的侧轴的大小（长度）。

flex item：Flex 项目，即 Flex 容器中的项目。也可以叫作 Flex 元素或 Flex 容器中的元素或元素等，看个人喜好。

CSS 提供了以下属性来对 Flex Box 进行布局：

|      属性       |                             说明                             |
| :-------------: | :----------------------------------------------------------: |
|     display     |                  指定 HTML 元素的布局方式。                  |
| flex-direction  |                 指定 Flex 容器中主轴的方向。                 |
|    flex-wrap    |                指定 Flex 容器中元素的换行规则                |
|    flex-flow    |     flex-direction 和 flex-wrap 两个属性的合并（简写）。     |
| justify-content | 指定 Flex 容器中的元素在主轴方向上的对齐方式或空间分配方式。 |
|  align-content  | 指定 Flex 容器中的元素在侧轴方向上的对齐方式或空间分配方式。 |
|   align-items   |   指定 Flex 容器中主轴方向上的元素在侧轴方向上的对齐方式。   |
|      order      |              设置 Flex 容器中的元素的排列顺序。              |
|   align-self    | 设置元素在侧轴上的对齐方式，优先级高于 Flex 容器的 align-items 属性。 |
|      flex       |             设置 Flex 容器中的元素如何分配空间。             |
|    flex-grow    | 设置当 Flex 容器中的元素在主轴的方向超出容器时所要缩放的程度。 |
|   flex-shrink   | 设置当 Flex 容器中的元素在主轴的方向超出容器时所要缩放的程度。 |
|   flex-basis    |               设置元素在主轴方向上的默认大小。               |

这些属性大致可以分为两类：

- 弹性盒子容器本身的属性：`flex-direction`，`flex-wrap`，`flex-flow`，`justify-content`，`align-items`，`align-content`。
- 弹性盒子中项目（元素）的属性：`order`，`align-self`，`flex-grow`，`flex-shrink`，`flex-basis`。
- 这些属性可以有多种分类方式，不过分类方式并不重要，了解并掌握属性的使用才重要。

以上属性不全都是 Flex 布局专用的。Grid 布局也会用到以上的一些属性。如 Grid 容器中的内联轴（inline axis）的一些设置等。



## display

通过将元素的 `display` 属性设置为 `flex` 或者 `inline-flex` 可以将盒子设置为弹性盒子（或叫做 Flex 盒子，Flex 容器）。

- `display: flex`：这种方式生成的是块级的 Flex 容器。
- `display: inline-flex`：这种方式生成的是行内块级的 Flex 容器。

当一个元素设置为了 Flex 布局以后，其子元素的 `float`，`clear` 和 `vertical-align` 等属性将失效。



## flex-direction

`flex-direction` 属性用于指定 Flex 容器中主轴的方向，该方向同时也是元素排列的方向。

|     属性值     |                   说明                   |
| :------------: | :--------------------------------------: |
|      row       | **默认值**。将主轴的方向设置为从左到右。 |
|  row-reverse   |       将主轴的方向设置为从右到左。       |
|     column     |        将主轴的方向设置为从上到下        |
| column-reverse |        将主轴的方向设置为从上到下        |

注意，`row` 和 `row-reverse` 值是会受到容器方向性影响的：

- 当容器的 `direction` 属性值是 `ltr`（默认值）时，`row` 表示从左到右，`row-reverse` 表示从右到左。
- 当容器的 `direction` 属性值是 `rtl` 时，`row` 表示从右到左，`row-reverse` 表示从左到右。

当 `flex-direction` 的值为 `row` 或者 `row-reverse` 时，侧轴的方向为从上到下。而当它的值为 `column` 或 `column-reverse` 时，侧轴的方向为从左到右。

另外，当修改 Flex 容器的主轴方向（`flex-direction`）之后，主轴上元素的默认对齐方向（`justify-content`）也会改变。

- `row`：`justify-content` 的默认值为 `start`（左对齐）。
- `row-reverse`：`justify-content` 的默认值为 `end`（右对齐）。
- `column`：`justify-content` 的默认值为 `start`（上对齐）。
- `column-reverse`：`justify-content` 的默认值为 `end`（下对齐）。

事实上，当将 `flex-direction` 设置为 `column` 时，`justify-content` 就相当于默认情况（即：`flex-direction: row;`）下 `align-content` 的作用，同理，`align-content` 就相当于默认情况下 `justify-content` 的作用。



## flex-wrap

`flex-wrap` 属性用于指定 Flex 容器中元素的换行规则。

注意，该属性控制的只是容器中的元素，不包括容器中的文字。

|    属性值    |                             说明                             |
| :----------: | :----------------------------------------------------------: |
|    nowrap    | **默认值**。让 Flex 容器中的元素单行排列。当元素总宽度大于容器的宽度时，那么所有的元素都会被等比例缩小。 |
|     wrap     |            当 Flex 容器中的元素超出容器时会换行。            |
| wrap-reverse | 当 Flex 容器中的元素超出容器时会换行，但是 cross-start 和 cross-end 置换位置。 |

注意，如果将 `flex-wrap` 的值设置为 `nowrap`，那么 Flex 容器中的元素依然是有可能会超出容器的。包括但不限于以下几种情况：

- 给元素指定了 `min-width` 属性。
- 将所有元素的 `flex-shrink` 设置为 `0`。
- 注意，以上的所举例子不是一定会导致元素溢出容器的，得看具体的情况。



## flex-flow

`flex-flow` 属性是 `flex-direction` 和 `flex-wrap` 的合并。

``` css
div {
    ...
    flex-flow: row-reverse wrap;
}
```

书写顺序无要求，并且可以只指定 `flex-direction` 或 `flex-wrap`（即只设定一个值）。



## justify-content

`justify-content` 属性用于指定 Flex 容器中的元素在主轴方向上的对齐方式或空间分配方式。

注意，`justyf-content` 的默认值是会受到  `flex-direction` 影响的，以下表格的默认值指的是当 `flex-direction` 的值为 `row` 时。具体可查看上面关于 `flex-direction` 的介绍。

|    属性值     |                             说明                             |
| :-----------: | :----------------------------------------------------------: |
|     start     | 让 Flex 容器中的元素排列在主轴的起点端（可以理解为左对齐）。 |
|      end      | 让 Flex 容器中的元素排列在主轴的终点端（可以理解为右对齐）。 |
|  flex-start   | **默认值**。效果与 start 相同。该值只适用于 Flex 布局，对于非 Flex 布局，使用该值将会被自动替换为 start。 |
|   flex-end    | 效果与 end 相同。该值只适用于 Flex 布局，对于非 Flex 布局，使用该值将会被自动替换为 end。 |
|    center     | 让 Flex 容器中的元素排列在主轴的中间，即每行的第一个元素到主轴起点的距离与每行最后一个元素到主轴终点的距离相等（可以理解为居中对齐）。 |
| space-between | 让 Flex 容器中的元素均匀的分布主轴上，主轴上每个元素的间距是相等的。每行第一个元素在主轴的起点，最后一个元素在主轴的终点。 |
| space-around  | 效果与 space-between 基本一致。不同的是，每行第一个元素不是在主轴的起点，它离主轴起点的距离是每个元素间距的一半；同样，每行最后一个元素离主轴终点的距离也是每个元素间距的一半。 |
| space-evenly  | 与 space-between 基本一致。不同的是，主轴上每个元素的间距，每行第一个元素与主轴起点的距离，每行最后一个元素与主轴终点的距离，全都相等。 |

`space-between`，`space-around`，`space-evenly` 三者的异同：

- 同：元素之间的距离都相等。
- 异：
  - `space-between` 首尾元素分别与主轴起止点距离为 0。
  - `space-space-around` 首尾元素分别与主轴起止点距离为每个元素之间距离的一半。
  - `space-evenly` 首尾元素分别于主轴起止点距离与每个元素之间的距离相等。



## align-content

`align-content` 属性用于指定 Flex 容器中的元素在侧轴方向上的对齐方式或空间分配方式。

|    属性值     |                             说明                             |
| :-----------: | :----------------------------------------------------------: |
|     start     |            让 Flex 容器中的元素沿着侧轴起点排列。            |
|      end      |            让 Flex 容器中的元素沿着侧轴终点排列。            |
|  flex-start   | 让 Flex 容器中的元素沿着侧轴起点排列。该值只适用于 Flex 布局，对于非 Flex 布局，使用该值将会被自动替换为 start。 |
|   flex-end    | 让 Flex 容器中的元素沿着侧轴终点排列。该值只适用于 Flex 布局，对于非 Flex 布局，使用该值将会被自动替换为 end。 |
|    center     |            让 Flex 容器中的元素排列在侧轴的中间。            |
| space-between | 让 Flex 容器中的元素均匀的分布在侧轴上，侧轴上每个元素的间距是相等的。每列第一个元素在侧轴的起点，最后一个元素在侧轴的终点。 |
| space-around  | 与 space-between 基本一致。不同的是，每列第一个元素不是在主轴的起点，它离侧轴起点的距离是每个元素间距的一半；同样，每列最后一个元素离侧轴终点的距离也是每个元素间距的一半。 |
| space-evenly  | 与 space-between 基本一致。不同的是，侧轴上每个元素的间距，每列第一个元素与侧轴起点的距离，每列最后一个元素与侧轴终点的距离，全都相等。 |
|    stretch    | 让 Flex 容器中的元素在侧轴的方向上被拉伸到跟 Flex 容器一样的高度。 |
|    normal     | **默认值**。按默认位置填充，就像没有 align-content 属性一样  |

当 Flex 容器为单行模式时，`align-content` 属性是不会生效的。

- 注意，此处所说的单行模式，是指将 `flex-wrap` 设置为 `nowrap` 的情况。如果容器 `flex-wrap` 的值为 `wrap`，但是由于元素较少而只显示一行，那么这种情况下 `align-content` 是可以生效的。 

`space-between`，`space-around`，`space-evenly` 三者的异同。

- 同：元素之间的距离都相等。
- 异：
  - `space-between` 首尾元素分别与侧轴起止点距离为0。
  - `space-space-around` 首尾元素分别与侧轴起止点距离为每个元素之间距离的一半。
  - `space-evenly` 首尾元素分别于侧轴起止点距离与每个元素之间的距离相等。



## align-items

`CSS align-items` 属性用于指定 Flex 容器中主轴方向上的元素在侧轴方向上的对齐方式。

|   属性值   |                             说明                             |
| :--------: | :----------------------------------------------------------: |
| flex-start | 让 Flex 容器中主轴上的元素沿着侧轴起点开始排列（可以理解为居上对齐）。 |
|  flex-end  | 让 Flex 容器中主轴上的元素沿着侧轴终点开始排列（可以理解为居下对齐）。 |
|   center   | 让 Flex 容器中主轴上的元素排列在侧轴的中间（可以理解为侧轴上的居中对齐）。 |
|  stretch   | **默认值**。让 Flex 容器中主轴上的元素在侧轴的方向上被拉伸到跟 Flex 容器一样的高度。 |

`stretch` 这一个属性值的效果不是“一定”的，它的实际效果与 Flex 容器中元素宽高的设定有关。以下所提到的“完全拉伸”指的是“元素在侧轴的方向上被拉伸到跟 Flex 容器一样的高度”，“不完全拉伸”则是“元素在侧轴方向上会被拉伸，但没有拉伸到跟 Flex 容器一样的高度”，而“不会被拉伸”则是字面意思。

- 当元素同时设置了宽高，那么元素将不会被拉伸。
- 当元素只设置了高：那么元素将不会被拉伸。
- 当元素只设置了宽：那么元素会被拉伸，但不一定是**完全**拉伸。

  - 如果盒子中每一行的元素数量一致时，就会被完全拉伸。
  - 当盒子中每一行的元素不一致时，如最后一行只有 1 个元素，而其他行有 3 个元素。那么第二，三列的元素不会被完全拉伸。

以下代码用于演示“元素只设置了宽，且盒子中每一行的元素数量一致时”这种情况，可以自行调整代码进行其他情况的演示。如想要测试“只设置了宽，但是每一行的元素不一致时”这种情况，可以把内容为 `10` 的 `div` 的注释取消掉。

``` html
<!-- 元素只设置了宽，且盒子中每一行的元素数量一致时 -->
<!DOCTYPE html>
<html lang="zh-CN">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Flex Test</title>

  <style>
      * {
          margin: 0;
          padding: 0;
          box-sizing: border-box;
      }

      body { background-color: #122033; }

      .my-flex-box {
          display: flex;
          width: 500px;
          height: 500px;
          margin: 100px auto;
          flex-direction: row;
          flex-wrap: wrap;
          justify-content: space-between;
          align-items: stretch;
          background-color: skyblue;
      }

      .my-flex-item {
          width: 150px;
          /* height: 50px; */
          background-color: pink;
          text-align: center;
      }
  </style>
</head>

<body>
  <div class="my-flex-box">
      <div class="my-flex-item">1</div>
      <div class="my-flex-item">2</div>
      <div class="my-flex-item">3</div>
      <div class="my-flex-item">4</div>
      <div class="my-flex-item">5</div>
      <div class="my-flex-item">6</div>
      <div class="my-flex-item">7</div>
      <div class="my-flex-item">8</div>
      <div class="my-flex-item">9</div>
      <!-- <div class="my-flex-item">10</div> -->
  </div>
</body>

</html>
```

代码运行效果如下图所示：

![pic1](https://raw.githubusercontent.com/FantasticAiming/ITBlog/main/Img/202306131224123.png)

注意，不要把 `align-content` 与 `align-items` 这两个属性混淆，它们看似很像，然而作用是不一样的。可以将 Flex 容器看成一个大盒子，里面的每一行是小盒子。前者主要是用于控制大盒子，而后主要用于控制小盒子。

- 假如现在有两行或多行元素：
  - `align-items: center;`：表示的是将每一行内的元素在侧轴上进行居中对齐，即让小盒子里的元素在侧轴上居中对齐。
  -  `align-content: center`：表示的是将这两行元素排列在侧轴的中间位置，即让小盒子排列在侧轴中间。如果小盒子的大小都相同，那么 `align-content: center;` 会让所有盒子都紧紧贴在一起。
  - 实际上，不管高度如何，当值为 `start`，`end`，`flex-start`，`flex-end` 时，它都会让每一行紧紧贴在一起。
- 假如只有一行元素，那么 `align-items: center;` 和 `align-content: center;` 都能实现让该行元素排列在侧轴中间，但是，前者还能实现行内（小盒子内）的元素在侧轴方向上居中对齐。
  - 注意，这里说的是一行元素，而不是说 Flex 容器为单行模式（`flex-wrap: nowrap;`）。Flex 容器默认情况下就是单行模式，所以如果要测试，请把 `flex-wrap` 的值设置为 `wrap` 或 `wrap-reverse`。
- 虽然 `align-items: center;` 是用于让小盒子内的元素居中的，但是它其实也会改变小盒子在大盒子中的位置的，参照参照上面“一行元素”的特点。而如果有多行元素，它虽不会让小盒子完全在中间，但也会大致分布在中间

以下代码用于演示“两行或多行元素”的情况，可以自行调整代码进行其他情况的演示。

``` html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background-color: cornflowerblue;
        }

        .flex-demo {
            display: flex;     
            width: 600px;
            height: 600px;
            margin: 30px auto;
            flex-wrap: wrap;
            align-items: center;
            align-content: center;     
            background-color:greenyellow;
        }

        .flex-demo div {
            flex-basis: 25%;
        }

        .item-demo1 {
            height: 60px;
            background-color: orange;
        }

        .item-demo2 {
            height: 80px;
            background-color: aqua;
        }
        
        .item-demo3 {
            height: 45px;
            background-color: yellow;
        }

        .item-demo4 {
            height: 100px;
            background-color: red;
        }
    </style>
</head>

<body>
    <div class="flex-demo">
        <div class="item-demo1"></div>
        <div class="item-demo2"></div>
        <div class="item-demo3"></div>
        <div class="item-demo4"></div>

        <div class="item-demo1"></div>
        <div class="item-demo2"></div>
        <div class="item-demo3"></div>
        <div class="item-demo4"></div>

        <div class="item-demo1"></div>
        <div class="item-demo2"></div>
        <div class="item-demo3"></div>
        <div class="item-demo4"></div>
    </div>
</body>

</html>
```

代码运行效果如下图所示：

![pic2](https://raw.githubusercontent.com/FantasticAiming/ITBlog/main/Img/202306131225445.png)



## order

> 该属性是在 Flex 容器中的元素上设置的，不是在 Flex 容器中设置的。

`order` 属性用于设置 Flex 容器中的元素的排列顺序。容器中的元素会先按照 `order` 的值升序排列（即 `order` 越小越靠前），再按照 HTML 代码中元素的书写顺序排列。

该属性的值**默认为 0**，可以设为任意整数，包括负数。如果设置为小数将没有效果，相当于默认值 0。

``` html
<style>
    ...
    .li-2 {
        ...
        order: 1;
    }
    
    .li-4 {
        ...
        order: -2;
    }
</style>
...
<ul>
    <li class="li-1"></li> <!-- order: 0 -->
    <li class="li-2"></li> <!-- order: 1 -->
    <li class="li-3"></li> <!-- order: 0 -->
    <li class="li-4"></li> <!-- order: -2 -->
</ul>
```

以上代码最终的显示顺序是：`li-4`，`li-1`，`li-3`，`li-2`。



## align-self

> 该属性是在 Flex 容器中的元素上设置的，不是在 Flex 容器中设置的。

`align-self` 属性用于设置元素在侧轴上的对齐方式，它会覆盖 Flex 容器中的 `align-items` 属性值。

该属性其实跟 `align-items` 的效果一样，不过，这个属性是在元素中书写的，即应用于指定的元素，而不是整个盒子中的元素，且它会覆盖 `align-items` 的设置，或者说，`align-self` 的优先级更高。

|   属性值   |                             说明                             |
| :--------: | :----------------------------------------------------------: |
|    auto    | 默认值。继承父容器 align-items 的属性值，如果没有父容器，则为 stretch。 |
| flex-start |                    让元素排列在侧轴起点。                    |
|  flex-end  |                    让元素排列在侧轴终点。                    |
|   center   |                   让元素排列在侧轴的中间。                   |
|  stretch   |           让元素在侧轴方向拉伸到与容器一样的高度。           |



## flex-grow

> 该属性是在 Flex 容器中的元素上设置的，不是在 Flex 容器中设置的。

`flex-grow` 属性用于设置将 Flex 容器中主轴方向上剩余空间分配给元素的比例，属性值越高那么元素所分配的空间所占的比例就越高，属性值可以是小数但不能是负数，如果写负数那将会自动变为**默认值 0**。

当该属性的值大于 0 时，那么它将会影响相应元素在主轴方向上最终的长度值。

- 在 MDN 的描述中，说的不是主轴，而是主尺寸（main size），而这个所谓的主尺寸是由 `flex-direction` 决定的，而 `flex-direction` 又是用于设置主轴的方向，因此此处直接说主轴并没有问题。
- 剩余空间指的是 Flex 容器在主轴方向的大小减去所有项在主轴方向的大小之和所得的结果。

如果每个项都将 `flex-grow` 的值都设置为相同的值，那么剩余空间将会平均分配给每个项。



## flex-shrink

> 该属性是在 Flex 容器中的元素上设置的，不是在 Flex 容器中设置的。

`flex-shrink` 属性用于设置当 Flex 容器中的元素在主轴的方向超出容器时所要缩放的程度。属性值越高，那么缩放的程度越大（即变得越小）。属性值可以是小数但不能是负数，如果写负数将会自动变为**默认值 1**。

当该属性的值大于 0 时，那么它将会影响相应元素在主轴方向上最终的长度值。

注意，由于该属性值默认值为 1，所以默认情况下即使元素的宽度超出容器的宽度，那么通常也是会在容器内的。如果把该属性值设置为 0，那么当元素超出容器时就会真正的溢出。

- 这里说宽度是因为一般情况下，主轴的方向就是宽的方向。
- 另外，即使将该属性值设置为非 0 的值，当元素中的内容超出容器宽度时，项依然还是有可能会超出容器的，也就是说，非 0 值不能保证一定将元素束缚于容器之中。解决方案看具体需求，如可以通过 `overflow: hidden` 将溢出部分隐藏起来。

另外，`flex-grow` 和 `flex-shrink` 两者其实是一对的，前者用于控制“当 Flex 容器中有剩余空间时”元素在主轴方向上的“增长指数”，而后者用于控制“当 Flex 容器中没有剩余空间时”元素在主轴方向上的“收缩指数”。



## flex-basis

`flex-basis` 用于设置元素在主轴方向上的默认大小。由于主轴的方向通常就是宽的方向，因此也可以说是设置元素默认的宽度值。当然，如果主轴的方向为 `column` 或者 `column-reverse` 那么设置的就是高度。

`flex-basis` 属性的优先级高于 `width` 和 `height`。

|            属性值             |                             说明                             |
| :---------------------------: | :----------------------------------------------------------: |
| 具体的带单位的数值，如：300px |                将元素默认的宽度设置为 300px。                |
|            百分比             |      将元素默认的宽度设置为 Flex 容器宽度对应的百分比。      |
|             auto              | **默认值**。将 `width` 属性值设置为元素默认的宽度。一个有趣的解释为 "请参照我的 width"。 |
|            content            |            根据元素的内容自动调整元素默认的宽度。            |

“flex-basis 的优先级是高于 `width` 和 `height`的”这句话其实不完全准确。事实上，Flex 盒子中的元素的 `width` 是没有任何效果的，而通过修改 `width` 的值之所以可以改变元素的大小，是因为 `flex-basis` 默认的值为 `auto`，而这个值又表示使用 `width` 的值作为元素的宽度，所以，修改 `width` 才能够修改元素的大小。因此，严格意义上讲，这两者是不具备优先级关系的，因为 `width` 根本是不起作用的。分析到此不难看出，当 `flex-basis` 的值不为 `auto` 时，那么 `width` 将完全失效。

> 以上结论的依据出自 W3C：This component sets the `flex-basis` longhand, which specifies the flex basis: the initial main size of the flex item, before free space is distributed according to the flex factors.
>
> [W3C 链接直达](https://www.w3.org/TR/css-flexbox-1/#:~:text=This%20component%20sets%20the%20flex-basis%20longhand%2C%20which%20specifies%20the%20flex%20basis%3A%20the%20initial%20main%20size%20of%20the%20flex%20item%2C%20before%20free%20space%20is%20distributed%20according%20to%20the%20flex%20factors)

另外，元素的最终大小不只是与 `flex-basis` 有关，还与`flex-grow`，`flex-shrink`，`min-width`，`max-width` 有关。注意，`min-width` 和 `max-width` 的优先级是高于其他属性的。另外，`box-sizing` 也是会影响元素的最终大小的。



## flex

`flex` 属性是 `flex-grow`，`flex-shrink`，`flex-basis` 的简写。值得一提的是，这三个属性都会影响到元素最终的宽度值或高度值（假设主轴方向是 `row` 或者 `row-reverse`）。

该属性的可以设置一个值，两个值，或三个值。

- 一个值：值必须为以下情况之一：
  - 纯数字（无单位的数字）：如 `1`，那么表示的是 `flex-grow` 的值。
  - 带单位的值：如 `300px`，那么表示将 `flex-basis` 设置为 `300px`。
  - 关键字：
    - `initial`：
      - **默认值**。相当于 `flex: 0 1 auto`，即三个属性都为默认值。
      - 元素会根据自身宽高属性来设置尺寸。
      - 会缩短自身以适应 `flex` 容器。
      - 不会伸长并吸收（填充）`flex` 容器中的剩余空间以适应 `flex` 容器。
    - `auto`：
      - 相当于 `flex: 1 1 auto`。
      - 元素会根据自身宽高属性来设置尺寸。
      - 会缩短自身以适应 `flex` 容器。
      - 会伸长并吸收 `flex` 容器中的剩余空间以适应 `flex` 容器。
    - `none`：
      - 相当于 `flex: 0 0 auto`。
      - 元素会根据自身宽高属性来设置尺寸。
      - 元素是完全非弹性的，既不会缩短，也不会伸长以适应 `flex` 容器。
- 两个值：第一个值必须为无单位的数字，表示 `flex-grow` 属性的值；第二个值必须为以下情况之一：
  - 纯数字：表示的是 `flex-shrink` 的值。
  - 带单位的值：表示的是 `flex-basis` 的值。
- 三个值：
  - 第一个值必须为纯数字，表示的是 `flex-grow` 的值。
  - 第二个值必须为纯数字，表示的是 `flex-shrink` 的值。
  - 第三个值必须为带单位的是值，表示的是 `flex-basis` 的值。

- 注意，当该属性只有一个值或两个值时，对于没有设置到值的属性都会保持默认值，除非使用具体了属性并将该属性写在 `flex` 属性的后面（CSS 的层叠性。当然也可以利用优先级的方式，这里不作过多说明）。