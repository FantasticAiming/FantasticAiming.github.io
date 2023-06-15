# isNaN() 和 Number.isNaN()

![nan](https://raw.githubusercontent.com/FantasticAiming/FantasticAiming.github.io/main/Img/202306142235216.png)

## NaN 与 Number.NaN

在了解 `isNaN()` 和 `Number.isNaN()` 这两个方法之前，先来了解一下 `NaN` 和 `Number.NaN`。

在 JavaScript 中，存在一个有趣的全局变量 —— `NaN`。关于该变量，重点需要明确知道以下三点：

1. 该变量的数据类型是 `Number` 类型的。
2. 该变量用于表示（represent）一个无法表达（cannot be represented）的值。
   - “无法表达的值”可能稍微有点难懂，可以看几个例子。比如：`'hello' * 3`，`undefined / undefined`，`Infinity / Infinity`，`Infinity - Infinity`，`Infinity * 0`，`0 / 0`，`Math.sqrt(-1)`。所谓的“无法表达的值”通常就是一些不合理的运算。
     - 虽然 `0 / 0` 的结果为 `NaN`，但是，如果是 `2 / 0` 或者任意一个正数除以 0，那么结果会是 `Infinity` 无穷大，如果是负数，则是 `-Infinity` 无穷小。这三种情况算是比较特殊的，特别是后面两种情况。因为在数学中，0 是不允许作为除数的，然而，在计算机中，往往是可以的，而且计算结果会是无穷大或者是无穷小（不同的编程语言可能会有差异，但是在 JavaScript 中的结果就是如此）。
   - 在这里要强调一下，`NaN` 只是用于“表示”上面这类值，不是说 `NaN` 会“等于”这类值。这就好比我们在日常生活中，常常用“XXX”表示某一个人的人名，比如“张三”，“李四”，然而，“XXX”本身并不等于“张三”或“李四”。
3. `NaN` 不等于任何值，包括它自己。

`NaN` 这个变量名本身是“Not a Number”（不是数字）这一串英文的缩写。然而，这串英文很有可能会误导人，或者说，会给人一种很矛盾的感觉（你一边告诉我这玩意是数字类型，一边又告诉我这玩意不是一个数字，你可真逗！）。所以我个人建议无视“Not a Number”这一个解释。

至于 `Number.NaN`，它与 `NaN` 的含义是完全一样的，但是要注意它们是不相等的。原因已经说过了， `NaN` 不等于任何值，包括它自己。

关于 `NaN` 的认识到这里就差不多了，接下来就来了解一下 `isNaN()` 和 `Number.isNaN()` 这两个方法吧。



## isNaN() 与 Number.isNaN()

前面提到过，`NaN` 不等于任何值，也就是说，它不管与谁通过 `==` 或是 `===` 进行比较，结果永远都是 `false`。所以，我们在判断一个值或者一个表达式是否可用 `NaN` 来表示时，是不会使用 `==` 或 `===` 这种方式的，而是会使用 `isNaN()` 或是 `Number.isNaN()` 方法。

- `isNaN(value)`：该方法会先将参数 `value` 使用 `Number()` 方法强制转化为一个 `Number` 类型的数据（但不会修改原数据），然后判断转换后的结果是否为 `NaN` ，如果是，就返回 `true`，否则将返回 `false`。所以，对于该方法的描述，也可以说是“判断一个值在使用 `Number()` 方法强制转换后的结果是否为 `NaN`”。
  - `Number()` 能够将部分字符串（如 `'12345'` 这种全为数字的字符串），布尔值以及 `null` 强制转为 `Number` 类型的数据，而其他类型的数据（比如 `Undefined`，`Object` ，含有非数字的字符串）的转化结果会是 `NaN`。`'0001234'` 这种字符串也是可以转为数字的，转化的结果是 `1234`。
- `Number.isNaN(value)`：该方法用于判断参数 `value` 是否为 `NaN`，它不会像 `isNaN()` 一样对参数进行强制转换。

注意，虽然 `NaN` 与 `Number.NaN` 是相同的，但是 `isNaN()` 和 `Number.isNaN()` 是不同的。



## 学习成果验收

如果对以上的知识充分理解了，那么对于以下代码的执行结果应该不会有任何疑虑。

无输出结果版代码：

``` js
console.log(isNaN(NaN))
console.log(isNaN(Number.NaN))
console.log(isNaN('abc'))
console.log(isNaN('123'))
console.log(isNaN('[][]')
console.log(isNaN('{}{}'))
console.log(isNaN('+-'))
console.log(isNaN(undefined))
console.log(isNaN(null))
console.log(isNaN(true))
console.log(isNaN(false))
console.log(isNaN(123))
console.log(isNaN('js' + 3))
console.log(isNaN(undefined / 0))
console.log(isNaN(Infinity + undefined))
console.log(isNaN(0 / 0))
console.log(isNaN(9 / 0))


console.log(Number.isNaN(NaN))
console.log(Number.isNaN(Number.NaN))
console.log(Number.isNaN('abc'))
console.log(Number.isNaN('123'))
console.log(Number.isNaN('[][]'))
console.log(Number.isNaN('{}{}'))
console.log(Number.isNaN('+-'))
console.log(Number.isNaN(undefined))
console.log(Number.isNaN(null))
console.log(Number.isNaN(true))
console.log(Number.isNaN(false))
console.log(Number.isNaN(123))
console.log(Number.isNaN('js' + 3))
console.log(Number.isNaN(undefined / 0))
console.log(Number.isNaN(Infinity + undefined))
console.log(Number.isNaN(0 / 0))
console.log(Number.isNaN(9 / 0))


console.log(NaN == NaN)
console.log(Number.NaN == Number.NaN)
console.log(NaN == Number.NaN)
console.log(NaN === NaN)
console.log(Number.NaN === Number.NaN)
console.log(NaN === Number.NaN)


console.log(typeof NaN)
console.log(typeof Number.NaN)
```

含输出结果版代码：

``` js
console.log(isNaN(NaN)) // true
console.log(isNaN(Number.NaN)) // true
console.log(isNaN('abc')) // true
console.log(isNaN('123')) // false
console.log(isNaN('[][]')) // true
console.log(isNaN('{}{}')) // true
console.log(isNaN('+-')) // true
console.log(isNaN(undefined)) // true
console.log(isNaN(null)) // false
console.log(isNaN(true)) // false
console.log(isNaN(false)) // false
console.log(isNaN(123)) // false
console.log(isNaN('js' + 3)) // true
console.log(isNaN(undefined / 0)) // true
console.log(isNaN(Infinity + undefined)) // true
console.log(isNaN(0 / 0)) // true
console.log(isNaN(9 / 0)) // false


console.log(Number.isNaN(NaN)) // true
console.log(Number.isNaN(Number.NaN)) // true
console.log(Number.isNaN('abc')) // false
console.log(Number.isNaN('123')) // false
console.log(Number.isNaN('[][]')) // false
console.log(Number.isNaN('{}{}')) // false
console.log(Number.isNaN('+-')) // false
console.log(Number.isNaN(undefined)) // false
console.log(Number.isNaN(null)) // false
console.log(Number.isNaN(true)) // false
console.log(Number.isNaN(false)) // false
console.log(Number.isNaN(123)) // false
console.log(Number.isNaN('js' + 3)) // false
console.log(Number.isNaN(undefined / 0)) // true
console.log(Number.isNaN(Infinity + undefined)) // true
console.log(Number.isNaN(0 / 0)) // true
console.log(Number.isNaN(9 / 0)) // false


console.log(NaN == NaN) // false
console.log(Number.NaN == Number.NaN) // false
console.log(NaN == Number.NaN) // false
console.log(NaN === NaN) // false
console.log(Number.NaN === Number.NaN) // false
console.log(NaN === Number.NaN) // false


console.log(typeof NaN) // number
console.log(typeof Number.NaN) // number
```

