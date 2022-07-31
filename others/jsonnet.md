# Jsonnet

Jsonnet 是模版语言，是 Json 的简单拓展。[例子](https://github.com/google/jsonnet/tree/master/examples)  
主要用来为大型复杂的服务，跟编程一样，管理所有的配置。

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

## 标准库
