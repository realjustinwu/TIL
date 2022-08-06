# Jsonnet 入门

- [Jsonnet 句法](#jsonnet-句法)
  - [句法](#句法)
  - [变量](#变量)
  - [引用](#引用)
  - [运算](#运算)
  - [函数](#函数)
  - [条件语句](#条件语句)
  - [数组](#数组)
- [Jsonnet 常用命令](#jsonnet-常用命令)

## Jsonnet 句法

### 句法

1. 字段如果没有空格，可以不需要引号
2. array/object 尾部用 `,`
3. 字符串使用 `"` 或者 `'`
4. `|||` 定义多行的文本
5. Verbatim strings @'foo' and @"foo" are for single lines.

### 变量

1. 使用 local 定义变量
2. 在 json 内部定义变量，使用 `,` 后缀
3. 在 json 外部定义变量，使用 `;` 后缀

<details><summary>例子</summary>
{% highlight jsonnet %}
local house_rum = 'Banks Rum';
{
  local name = 'Justin',
  msg: 'hello ' + name,
}
# output: 
{
  "msg": "hello Justin"
}
{% endhighlight %}
</details>

### 引用

1. `self` 引用当前对象
2. `$` 引用根对象
3. `['foo'] ` 查找字段
4. `.foo` 同上，如果字段没有空格等
5. `[10]` 查找数组的元素
6. `[10:20:2]` 切片，同 python
7. 字符串也是数组，可以切片或者查找

<details><summary>例子</summary>
{% highlight jsonnet %}
{
    local var_a= 'var a',
    var_array:: [1,2,3,4,5,6,7,8,9,10],
    field_a: 'field a',
    inner_obj: {
        var_a: var_a,
        var_b: $.field_a,
        var_c: $['field_a'],
        var_d: $.var_array[3],
        var_e: $.var_array[3:10:2],
    },
   var_a: self.field_a,
}
# Output:
{
  "field_a": "field a",
  "inner_obj": {
    "var_a": "var a",
    "var_b": "field a",
    "var_c": "field a",
    "var_d": 4,
    "var_e": [ 4, 6, 8, 10 ]
  },
  "var_a": "field a"
}
{% endhighlight %}
</details>

### 运算

1. 浮点运算、二进制运算、位运算
2. + 连接字符串
3. 字符串对比 `<`
4. `==` 相等运算
5. 类似 python 的字符串格式化运算

<details><summary>例子</summary>
{% highlight jsonnet %}
{
  concat_array: [1, 2, 3] + [4],
  concat_string: '123' + 4,
  equality1: 1 == '1',
  equality2: [{}, { x: 3 - 1 }] == [{}, { x: 2 }],
  ex1: 1 + 2 * 3 / (4 + 5),
  // Bitwise operations first cast to int.
  ex2: self.ex1 | 3,
  ex3: self.ex1 % 2,
  ex4: (4 > 3) && (1 <= 3) || false,
  // 合并两个 object
  obj: { a: 1, b: 2 } + { b: 3, c: 4 },
  // 检查 object 是否包含字段
  obj_member: 'foo' in { foo: 1 },
  // String 格式化
  str1: 'The value of self.ex2 is ' + self.ex2 + '.',
  str2: 'The value of self.ex2 is %g.' % self.ex2,
  str3: 'ex1=%0.2f, ex2=%0.2f' % [self.ex1, self.ex2],
  // By passing self, we allow ex1 and ex2 to
  // be extracted internally.
  str4: 'ex1=%(ex1)0.2f, ex2=%(ex2)0.2f' % self,
  // Do textual templating of entire files:
  str5: |||
    ex1=%(ex1)0.2f
    ex2=%(ex2)0.2f
  ||| % self,
}
# Output:
{
  "concat_array": [1, 2, 3, 4],
  "concat_string": "1234",
  "equality1": false,
  "equality2": true,
  "ex1": 1.6666666666666665,
  "ex2": 3,
  "ex3": 1.6666666666666665,
  "ex4": true,
  "obj": { "a": 1, "b": 3, "c": 4 },
  "obj_member": true,
  "str1": "The value of self.ex2 is 3.",
  "str2": "The value of self.ex2 is 3.",
  "str3": "ex1=1.67, ex2=3.00",
  "str4": "ex1=1.67, ex2=3.00",
  "str5": "ex1=1.67\nex2=3.00\n"
}
{% endhighlight %}
</details>

### 函数

<details><summary>定义函数例子</summary>
{% highlight jsonnet %}
// 单行函数，跟python 一样
local my_function(x, y=10) = x + y;
// 多行函数
local multiline_function(x) =
  local temp = x * 2;
  [temp, temp + 1];
// 通过对象引用函数
local object = {
  my_method(x): x * x,
};
{
  // 初始化的时候，执行函数
  call_inline_function: (function(x) x * x)(5),
}
{% endhighlight %}
</details>

### 条件语句

<details><summary>定义条件语句</summary>
{% highlight jsonnet %}
{
    local factor = if large then 2 else 1,
}

[] + (
    if virgin 
    then [] 
    else [ { kind: 'Banks', qty: 1.5 * factor }, ]
)

{
    garnish: if large then 'Lime wedge',
    [if salted then 'garnish']: 'Salt',
}
{% endhighlight %}
</details>

### 数组


## Jsonnet 常用命令

执行 jsonnet 命令行，可以把模版生成到标准输出或者文件。

```shell
jsonnet -e <code> # 从标准输入获取模版
jsonnet <file> # 从文件获取模版
jsonnet <file> -o output.file # 输出到文件
jsonnet -m . <file> # 输出到多个文件
jsonnet -y <file> # 输出 yaml 文件，可以是数组
```

<details><summary>例子：jsonnet -e 'code' </summary>
{% highlight shell %}
$ jsonnet -e '{ x: 1 , y: self.x + 1 } { x: 10 }'
{
   "x": 10,
   "y": 11
}
{% endhighlight %}
</details>

<details><summary>例子：jsonnet file</summary>
{% highlight shell %}
$ jsonnet landingpage.jsonnet
{
   "person1": {
      "name": "Alice",
      "welcome": "Hello Alice!"
   },
   "person2": {
      "name": "Bob",
      "welcome": "Hello Bob!"
   }
}
{% endhighlight %}
</details>

<details><summary>例子：jsonnet -m . file</summary>
{% highlight shell %}
$ jsonnet -m . multiple_output.jsonnet
a.json
b.json
$ cat a.json
Output:
{
   "x": 1,
   "y": 2
}
$ cat b.json
{
   "x": 1,
   "y": 2
}
{% endhighlight %}
</details>
<details><summary>例子：jsonnet -y file</summary>
{% highlight shell %}
$ jsonnet -y yaml_stream.jsonnet

---
{
   "x": 1,
   "y": 2
}

---
{
   "x": 1,
   "y": 2
}
{% endhighlight %}
</details>
