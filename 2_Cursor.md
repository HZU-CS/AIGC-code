# 使用 Cursor 进行代码修改

## 实验介绍

在完成某个功能后，可能代码还存在某些问题，如可读性、健壮性都比较低，甚至还存在一些 BUG，在本节实验中，我们将演示如何使用 Cursor 对代码进行修改。

#### 知识点

- 加强可读性
- 加强健壮性
- 拆分代码
- 重构代码
- 修改 BUG

## 使用 Cursor 加强可读性

如下是对两个输入进行数学运算的 Python 代码：

```python
def m(a,b):return a+b,a-b,a*b,a/b
def f(x,y):
    return (x + y)**3 + (x - y)**2 + sum(m(x,y))

if __name__ == '__main__':
    x = int(input('Enter x: '))
    y = int(input('Enter y: '))
    print(f(x, y))
```

此代码可读性较差，我们使用 Cursor 加强可读性：

```
make the code readable
```

<iframe 
    height=450 
    width=800 
    src="./2_Cursor.assets/readable.mp4" 
    frameborder=0 
    allowfullscreen>
</iframe>

可以看到，这段代码被修改成了满足 PEP8 风格的代码。

接下来，我们试试以下已进行过变量混淆的代码：

```python
def func (OO0O000000OO0000O ):
   OO0OO000OOOO0OO0O =len (OO0O000000OO0000O )
   for O0O00OO0O00000000 in range (OO0OO000OOOO0OO0O ):
    for O00OOOO0O00O00000 in range (0 ,OO0OO000OOOO0OO0O -O0O00OO0O00000000 -1 ):
     if OO0O000000OO0000O [O00OOOO0O00O00000 ]>OO0O000000OO0000O [O00OOOO0O00O00000 +1 ]:
        OO0O000000OO0000O [O00OOOO0O00O00000 ],OO0O000000OO0000O [O00OOOO0O00O00000 +1 ]=OO0O000000OO0000O [O00OOOO0O00O00000 +1 ],OO0O000000OO0000O [O00OOOO0O00O00000 ]
   return OO0O000000OO0000O
```

先问 Cursor 这段代码在干什么，在这里我们使用的是对话功能，选中代码内容进行对话，也可以直接对整个文件进行对话：

```
what is this code talk about?
```

<iframe 
    height=450 
    width=800 
    src="./2_Cursor.assets/talkabout.mp4" 
    frameborder=0 
    allowfullscreen>
</iframe>

正确说出了这是一个冒泡排序（bubble sort）的代码，然后继续对话，让 Cursor 生成 PEP8 风格的代码：

```
convert this code to PEP8 style and more readable
```

<iframe 
    height=450 
    width=800 
    src="./2_Cursor.assets/pep8.mp4" 
    frameborder=0 
    allowfullscreen>
</iframe>

## 使用 Cursor 加强健壮性

以下代码是一个使用 `requests` 爬取网页内容的代码：

```python
import requests
from bs4 import BeautifulSoup

def process_urls(url_list):
    results = {}

    for url in url_list:
        response = requests.get(url)
        soup = BeautifulSoup(response.text, "html.parser")
        links = [a.get('href') for a in soup.find_all('a', href=True)]
        results[url] = links

    return results
```

该代码健壮性较差，我们让 Cursor 增强这段代码的健壮性：

```
make this code more stable and robustness
```

<iframe 
    height=450 
    width=800 
    src="./2_Cursor.assets/stable.mp4" 
    frameborder=0 
    allowfullscreen>
</iframe>

可以看到 Cursor 为请求设置了超时时间，并捕获全部的异常。

## 使用 Cursor 拆分代码

以下代码执行了 3 个步骤：请求网页，获取数据，保存数据到本地，这段代码不符合函数设计的高内聚低耦合原则。

```python
import requests
import json

def fetch_and_process_data(url, output_file):
    response = requests.get(url)
    data = response.json()

    processed_data = {}
    for item in data:
        key = item['id']
        value = item['value']
        processed_data[key] = value

    with open(output_file, 'w') as f:
        json.dump(processed_data, f)
```

我们让 Cursor 拆分这个函数，增加可读性：

```
split this function into separate functions for improved readability
```

<iframe 
    height=450 
    width=800 
    src="./2_Cursor.assets/split.mp4" 
    frameborder=0 
    allowfullscreen>
</iframe>

## 使用 Cursor 重构代码

以下是使用 `urllib` 库进行网页请求的代码，但 `urllib` 库现在已经有更好的替代：`requests` 了。

```python
import urllib.request

def get_html_from_url(url):
    # Make the request and store the response in a variable
    response = urllib.request.urlopen(url)

    # Read the response and decode it as UTF-8
    html = response.read().decode("utf-8")

    return html
```

让我们用 `requests` 库重构代码：

```
refactor the code to use the requests lib
```

<iframe 
    height=450 
    width=800 
    src="./2_Cursor.assets/requests.mp4" 
    frameborder=0 
    allowfullscreen>
</iframe>

接下来看一个更高级的用法，以下是一个简单的披萨售卖系统，该代码定义了两个类，`Pizza` 和 `PizzaStore`，`Pizza` 用于制作指定类型的披萨，`Pizzastore` 用于出售指定类型的披萨。

```python
class Pizza:
    def __init__(self, name, toppings):
        self.name = name
        self.toppings = toppings

    def prepare(self):
        print(f"Preparing {self.name} pizza with toppings: {', '.join(self.toppings)}")


class PizzaStore:
    def order_pizza(self, pizza_type):
        if pizza_type == "cheese":
            pizza = Pizza("Cheese", ["mozzarella", "tomato sauce"])
        elif pizza_type == "pepperoni":
            pizza = Pizza("Pepperoni", ["pepperoni", "mozzarella", "tomato sauce"])
        else:
            raise ValueError(f"Unknown pizza type: {pizza_type}")

        pizza.prepare()
        return pizza


store = PizzaStore()
store.order_pizza("cheese")
```

我们让 Cursor 使用工厂模式重构这段代码：

```
refactor the code to use the Factory Pattern
```

<iframe 
    height=450 
    width=800 
    src="./2_Cursor.assets/factory.mp4" 
    frameborder=0 
    allowfullscreen>
</iframe>

## 使用 Cursor 修改 BUG

最后，我们让 Cursor 来修改 BUG。

```python
def binary_search(array, find_num):
    left = 0
    right = len(array) - 1

    while left <= right:
        mid = (left - right) // 2
        if array[mid] == find_num:
            return mid
        elif array[mid] < find_num:
            left = mid + 1
        else:
            right = mid - 1

    return -1
```

上述是一段二分查找的代码，但是 `mid = (left + right) // 2` 被错误地输入成 `mid = (left - right) // 2`。

```
try to fix bug if exists
```

<iframe 
    height=450 
    width=800 
    src="./2_Cursor.assets/fixbug.mp4" 
    frameborder=0 
    allowfullscreen>
</iframe>

## 实验总结

本次实验中，我们详细介绍了如何在编写程序的过程中，使用 Cursor 对代码进行修改，有了 Cursor 这种辅助工具，相信可以大大提高各位的编程效率。

接下来，我们将介绍如何拓展 Cursor，去提升那些你不太熟悉的编程语言的编程效率。