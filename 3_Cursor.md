# 使用 Cursor 进行代码转换

## 实验介绍

假设你对某种编程语言的掌握程度比较低，在本节实验中，我们将通过 Cursor 辅助生成对应的编程语言，以及进行相应的优化。

#### 知识点

- 语言转换
- 风格转换
- 前端生成
- 代码优化

## 使用 Cursor 进行语言转换

以下是使用 OpenCV-Python 进行视频读取的代码：

```python
import cv2 as cv
cap = cv.VideoCapture('vtest.avi')
while cap.isOpened():
    ret, frame = cap.read()
    if not ret:
        break
    gray = cv.cvtColor(frame, cv.COLOR_BGR2GRAY)
    if cv.waitKey(1) == ord('q'):
        break
cap.release()
cv.destroyAllWindows()
```

假设要将此代码部署到边缘设备（无法安装 Python 环境），但你不懂 C/C++，就可以使用 Cursor 对其进行转换：

```
convert to C/C++
```

<iframe 
    height=450 
    width=800 
    src="./3_Cursor.assets/convert.mp4" 
    frameborder=0 
    allowfullscreen>
</iframe>

## 使用 Cursor 进行风格转换

以下是对学生成绩进行分级的代码，这段代码是一位从 C/C++ 刚转行到 Python 的程序员写的，不够 Pythonic。

```python
def get_grade(score: int) -> str:
    if score >= 90:
        grade = "A"
    elif score >= 80:
        grade = "B"
    elif score >= 70:
        grade = "C"
    elif score >= 60:
        grade = "D"
    else:
        grade = "E"
    return grade
```

使用 Cursor 对其进行转换，变得更加 Pythonic：

```
simplify this code pythonically
```

<iframe 
    height=450 
    width=800 
    src="./3_Cursor.assets/pythonic.mp4" 
    frameborder=0 
    allowfullscreen>
</iframe>

## 使用 Cursor 生成前端

假设你只会 Python，但需要开发一个问答聊天的网页，就可以让 Cursor 辅助你生成前端：

```
generate a html q-a chat page, inculde backend request
```

<iframe 
    height=450 
    width=800 
    src="./3_Cursor.assets/html.mp4" 
    frameborder=0 
    allowfullscreen>
</iframe>

继续对话，让 Cursor 生成 CSS 样式：

```
generate css
```

<iframe 
    height=450 
    width=800 
    src="./3_Cursor.assets/css.mp4" 
    frameborder=0 
    allowfullscreen>
</iframe>

## 使用 Cursor 代码优化

以下是一个列表去重，并返回去重结果的代码示例：

```python
def process_data(data):
    unique_list = []
    for elem in data:
        if elem not in unique_list:
            unique_list.append(elem)

    return unique_list
```

该代码存在性能问题，对 Cursor 进行提问：

```
why this code run so slow?
```

<iframe 
    height=450 
    width=800 
    src="./3_Cursor.assets/faster.mp4" 
    frameborder=0 
    allowfullscreen>
</iframe>

可以看到 Cursor 解释了是使用 `list` 导致查找会比较慢，并给出了使用 `set` 对代码进行优化的方案。

## 实验总结

在本实验中，我们学习了如何使用 Cursor 辅助生成编程语言以及进行相应的优化，这样即使对某种编程语言不熟悉的开发者也能在短时间内快速掌握其用法，并在实际项目中实现高效的代码编写。

本课程是一个对于使用 AIGC 功能生成代码的演示课程，相信学完本课程之后，开发者们能够在各自的生产领域使用 AIGC 更加高效地进行代码开发。