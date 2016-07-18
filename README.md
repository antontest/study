## Markdown --- 入门使用

### 目录
* [列表](#列表)
	* [无序列表](#无序列表)
	* [有序列表](#有序列表)
* [引用](#引用)
* [内容块](#内容块)
* [粗体、斜体与删除线](#粗体斜体与删除线)
* [表格](#表格)
* [代码](#代码)
* [分割线](#分割线)
* [流程图](#流程图)
* [时序图](#时序图)
* [链接](#链接)
* [图片](#图片)

#### 列表
##### 无序列表
- iphone
- ipad
- ipod

##### 有序列表
1. iphone
2. ipad
3. ipod

#### 引用
下面是引用内容：

> 我是引用部分

#### 内容块
~~~
我是内容块
~~~

#### 粗体、斜体与删除线
我是**粗体**,我是斜体**斜体  
~~我是删除线~~

#### 表格
|name|age|sex|
|----|---|---|
|anton|26|male|
|antonio|27|male|
|lee|23|female|

#### 代码
    int main(int argc, int argv[])  
    {
        printf("hello, world\n");
        return 0;
    }
```c
int main(int argc, int argv[])
{
    printf("hi\n");
    return 0;
}
```
这是也是代码 `printf("hello\n")`。

#### 分割线
***
- - -

#### 流程图

```flow
st=>start: Start
op=>operation: Your Operation
cond=>condition: Yes or No?
e=>end

st->op->cond
cond(yes)->e
cond(no)->op
```

#### 时序图

```sequence
A->B: how are you?
B-->>A: fine.
```

#### 链接
我是[百度] [baidu]的链接

 [baidu]: http://www.baidu.com

#### 图片
下面是一张ubuntu的桌面壁纸:  
![ubuntu] [ubuntu]

 [ubuntu]: http://images.forwallpaper.com/files/images/6/60ae/60ae2d6e/594646/ubuntu.jpg "ubuntu壁纸"

* <font color="red">**高级特性**</font>
  - 小节

# markdown-study
