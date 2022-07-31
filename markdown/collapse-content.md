# Markdown 收起内容

## 收起 content

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
.box-rowr {
    flex-direction: row-reverse;
}
</style>

```markdown
<details><summary>Show</summary>
<div class="box box-rowr">
    <div class="box-item">1</div>
    <div class="box-item">2</div>
    <div class="box-item">3</div>
</div>
</details>
```

<details><summary>Show</summary>
<div class="box box-rowr">
    <div class="box-item">1</div>
    <div class="box-item">2</div>
    <div class="box-item">3</div>
</div>
</details>

## 收起代码

注意：不能缩进。

```markdown
{% raw %}
<details><summary>Show</summary>
{% highlight cpp %}
int main() {
    printf("Hello World!");
    return 0;
}
{% endhighlight %}
</details>
{% endraw %}
```

<details><summary>Show</summary>

{% highlight cpp %}
int main() {
    printf("Hello World!");
    return 0;
}
{% endhighlight %}
</details>
