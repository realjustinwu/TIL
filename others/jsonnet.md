# Jsonnet

Jsonnet 是模版语言，是 Json 的简单拓展。[例子](https://github.com/google/jsonnet/tree/master/examples)  
主要用来为大型复杂的服务，跟编程一样，管理所有的配置。

- [Jsonnet 语言](#jsonnet-语言)
  - [值](#值)
  - [可见性](#可见性)
  - [字段继承](#字段继承)
- [标准库](#标准库)

## Jsonnet 语言

Jsonnet 是一种完整的纯函数式编程语言。（跟命令式语言的最大区别是，定义东西是什么，而不是能做什么）。

### 值

Jsonnet 有7种类型的值。

- null – 全局唯一的值（空）
- boolean – true 或者 false.
- string – Unicode strings
- number – IEEE754 64-bit 浮点数
- function - 纯函数，有输入参数和返回值
- array - 数组
- object - JSON 对象

<details><summary>function 例子</summary>
{% highlight jsonnet %}
local func = function(x) x * 2;
local func(x) = x * 2; # 同上
func(21)
local foo(x, y=1) = x + y; # 带默认参数
[
  foo(1),
  foo(1, 1),
  foo(x=1, y=1),
  foo(y=1, x=1),
  foo(x=1),
]
{% endhighlight %}
</details>

<details><summary>Array 例子</summary>
{% highlight jsonnet %}
local arr = [error "a", 2+2, error "b"];
arr[1];
# output: 4, 没有使用不会报错，函数式语言是懒加载的
[x * x for x in std.range(1, 3)];
# output: [1, 4, 9]
[x for x in std.range(1, 10) if x % 3 == 0]; 
# output: [3, 6, 9]
[
  [x, y]
  for x in std.range(1, 2)
  for y in std.range(x, 2)
]
# output: [[1,1], [1,2], [2,2]]
[
  x
  for y in std.range(1, 2)
  for x in std.range(1, 2)
]
# output: [1, 2, 1, 2]
[
  x
  for y in std.range(1, 2)
  for x in std.range(1, 2)
]
# output: [1, 1, 2, 2]
[
    [x, y]
    for x in std.range(1, 10)
    if x % 3 == 0
    for y in std.range(1, 10),
    if y % 2 == 0
]
{% endhighlight %}
</details>

<details><summary>Object 例子</summary>
{% highlight jsonnet %}
local obj = {
  "foo": 1,
  "bar": {
    "arr": [1, 2, 3],
    "number": 10 + 7,
  }
};
[
  obj.foo,
  obj["foo"],
  obj["f" + "oo"]
]
# output: [1, 1, 1]
local obj = {
  name: "Alice",
  greeting: "Hello, " + self.name,
};
[
  obj,
  obj + { name: "Bob" },
  obj + { greeting: super.greeting + "!"},
  obj + { name: "Bob", greeting: super.greeting + "!"},
]
# output:
# [
#  {"greeting": "Hello, Alice", "name": "Alice"},
#  {"greeting": "Hello, Bob", "name": "Bob"},
#  {"greeting": "Hello, Alice!","name": "Alice"},
#  {"greeting": "Hello, Bob!","name": "Bob"}
# ]
{% endhighlight %}
</details>

<details><summary>继承的例子</summary>
{% highlight jsonnet %}
local add = {
  params: {
    a: error "please provide argument a",
    b: error "please provide argument b",
  },
  result: self.params.a + self.params.b
};
(add + { params: { a: 1, b: 2} }).result
# output: 3
{% endhighlight %}
</details>

<details><summary>引用自身</summary>
{% highlight jsonnet %}
local obj = {
  name: "Alice",
  greeting: "Hello, " + obj.name,
}; obj
# output: {"greeting": "Hello, Alice","name": "Alice"}
{% endhighlight %}
</details>

### 可见性

- `:` – 默认可见，除非父节点字段是隐藏的
- `::` – 隐藏
- `:::` – 强制可见

<details><summary>Show</summary>
{% highlight jsonnet %}
{
  default: "foo",
  default_then_hidden: "foo",
  hidden:: "foo",
  hidden_then_default:: "foo",
  hidden_then_visible:: "foo",
  visible::: "foo",
  visible_then_hidden::: "foo",
}
+
{
  default_then_hidden:: "foo",
  hidden_then_default: "foo",
  hidden_then_visible::: "foo",
  visible_then_hidden:: "foo",
}
Output:
{
  "default": "foo",
  "hidden_then_visible": "foo",
  "visible": "foo"
}
{% endhighlight %}
</details>

### 字段继承

- `:`: 直接使用后一个 obj 的字段完全代替上一个 obj 的字段
- `+:`: 把后一个 obj 的字段，merge 到上一个 obj。如果是 array 就拼接到尾部
- `+::`: 同上，并隐藏字段
- `+:::`: 同上，并强制显示

## 标准库

