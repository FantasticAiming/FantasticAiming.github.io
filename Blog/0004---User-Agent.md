# User Agent

![User-Agent](https://raw.githubusercontent.com/FantasticAiming/FantasticAiming.github.io/main/Img/202306152235916.png)

在 `Window` 对象中有一个 `navigator` 属性。这个属性是一个很有用的对象，它包含了许多与浏览器信息相关的属性，其中的 `userAgent` 属性就可以返回当前浏览器的 `User Agent` 字符串。获取方法如下所示：

``` js
const uA = navigator.userAgent
```

`User Agent` 可简写为 `UA`，直译成中文是“用户代理”。它是客户端在向服务端发送请求时，向服务端提供的**客户端及其环境的信息**。当客户端指的是浏览器时，可以将 UA 称为**浏览器标识**。

UA 是由一串字符串构成，下面是一个示例：

``` shell
Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36
```

该 UA 字符串各部分的含义如下：

- `Mozilla/5.0`：表示当前浏览器所使用的用户代理标识符的版本号。它几乎是一个固定的写法。
- `(Windows NT 10.0; Win64; x64)`：表示当前浏览器所处操作系统的一些信息。该字段表示浏览器所在的操作系统是 `64` 位的 `Window 10.0` 操作系统，以及所使用的处理器的架构是 `64` 位的。
- `AppleWebKit/537.36`：表示当前浏览器所使用的渲染引擎。该字段表示浏览器使用的渲染引擎是 `537.36` 版本的 `Webkit` 引擎。
- `(KHTML, like Gecko)`：表示当前浏览器所支持的 Web 标准与技术。该字段表示浏览器具有类似于 `KHTML` 和 `Gecko` 引擎的渲染能力。这个字段主要是为了保证浏览器的兼容性。
- `Chrome/114.0.0.0`：表示当前浏览器的内核名称以及版本号。该字段表示浏览器所使用的内核是 `114.0.0.0` 版本的 `Chrome` 内核。
- `Safari/537.36`：表示浏览器所支持的一些特性和功能。该字段表示浏览器支持 `537.36` 版本的 `Safari` 浏览器。

`UA` 的组成是由浏览器厂商自己定义的，同一浏览器在不同环境或者不同版本下的 `UA` 基本都是不同，不同浏览器就更不用说了。

虽然在不同情况下，浏览器的 `UA` 字符串往往是不相同的，但是，`UA` 字符串的第一部分，基本都会是 `Mozilla/5.0`。这其实是一个历史遗留问题。在早期的网络时代，Netscape Navigator （网景浏览器）是最流行的浏览器，而其 `user-agent` 字符串是以 `Mozilla` 作为开头。当其他浏览器出现时，它们为了能够访问使用了网景浏览器专有代码的网站，便将自己的 `user-agent` 字符串中的第一部分也设置为了 `Mozilla` 这个字符串，这个传统流传至今。