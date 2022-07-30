# Markdown 收起内容

## 收起 content

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

注意：代码的上分需要一个空行。

```markdown
<details><summary>Show</summary>

```cpp
int main() {
	printf("Hello World!");
	return 0;
}
```
</details>
```

<details><summary>Show</summary>

```cpp
int main() {
	printf("Hello World!");
	return 0;
}
```
</details>

## 缩进并收起代码

1. 缩进之后收藏代码
	<details>
	<summary>Show</summary>
	A nice Hello world!

	```javascript
	int main() {
		printf("Hello World!");
		return 0;
	}
	```
	</details>
