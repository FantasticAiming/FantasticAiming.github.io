# div 嵌套后 padding-right “失效”的问题

首先要说明一点，标题中之所以给失效加上了双引号，是因为 `padding-right` 并不是真正的失效，而是没有达到我想要的效果。

最近发现了一个问题，当 `div` 嵌套之后，如果内层的 `div` 内容过长，那么外部 `div` 的 `padding-right` 将可能会失效。

以下是示例代码：

``` css
.info-card {
    width: 400px;
    height: 400px;
    margin: 20px auto;
    padding: 10px;
    background-color: orange;
    overflow-x: auto;
}

.info-item {
    margin-bottom: 10px;
    background-color: yellow;
    white-space: nowrap;
    font-size: 18px;
    font-weight: 600;
}
```

``` html
<div class="info-card">
    <div class="info-item">
        <span class="info-name">aaaa:&nbsp;</span>
        <span class="info-value">AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA</span>
    </div>
    <div class="info-item">
        <span class="info-name">aaaa:&nbsp;</span>
        <span class="info-value">AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA</span>
    </div>
    <div class="info-item">
        <span class="info-name">aaaa:&nbsp;</span>
        <span class="info-value">AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA</span>
    </div>
</div>
```

代码的运行效果如下图所示：

![p1](https://raw.githubusercontent.com/FantasticAiming/ITBlog/main/img/202306122120591.png)

![p2](https://raw.githubusercontent.com/FantasticAiming/ITBlog/main/img/202306122120672.png)

而我理想中的效果是下图这样的：

![p3](https://raw.githubusercontent.com/FantasticAiming/ITBlog/main/img/202306122120602.png)

![p4](https://raw.githubusercontent.com/FantasticAiming/ITBlog/main/img/202306122120094.png)

之所出现这个问题，是因为黄色的盒子通过 `white-space: nowrap;` 强制盒子的内容（两个 `span`）以一行显示，并且这里没有对超出自身宽度的内容进行处理（如以滚动条形式或是使用省略号）。然而，我又确确实实想让黄色的内容完整在一行内显示，该怎么办呢？

老实说，我没有任何头绪。不过，虽然我不打算对 `span` 进行处理，可是，我至少应该让黄色的盒子能够完整地包裹住两个 `span` 吧。于是乎，我就把问题的焦点转移到“如何让黄色盒子的宽度能够自适应自身内容”，先把这一个问题解决掉了再说。

最开始，我是使用 `width: calc(100% - 20px)` 来实现的，即让黄色盒子的宽度等于橙色盒子的宽度减去橙色盒子的左右内边距。然而没有效果，因为橙色盒子在拥有了滚动条之后，本身的宽度其实是没有发生改变的。

然后，我又想着，给黄色的盒子加上 `overflow-x: auto;`。不过，这个方法我没有尝试就放弃了，因为这样做的话，虽然橙色盒子的 `padding-right` 能够生效，然而整体效果却不是我上面展示那样。这种方式，会让滚动条存在于黄色盒子，而不是橙色的盒子。

最后，我想到了一个东西 —— `fit-content`。通过将黄色盒子的宽度指定为这个值，就可以让它根据内容调整自己的宽度。

黄色盒子改进后的 CSS 代码如下：

``` css
.info-item {
    width: fit-content;
    margin-bottom: 10px;
    background-color: yellow;
    white-space: nowrap;
    font-size: 18px;
    font-weight: 600;
}
```

有趣的一幕来了，通过对黄色盒子进行改进后，橙色盒子的 `padding-right` 竟然生效了。就这样，问题莫名奇妙地解决了。

再次强调一点，在这一整个过程中，橙色盒子的 `padding-right` 其实并没有真正失效，只是没有达到我想要的效果。因为，通过 F12 检查元素可以发现 `padding-right` 一直是存在的。

另外，如果使用的是 QQ 浏览器，并且开启了 QQ 浏览器的“使用隐藏式的滚动条”，那么此篇文章的解决方案是没有效果的。
