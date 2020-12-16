---
title: 'Python json的运用'
subtitle: 'Python json的运用'
summary: Python json的运用.
authors:
- admin
tags:
- python
categories:
- code
math: true
diagram: true
# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Placement options: 1 = Full column width, 2 = Out-set, 3 = Screen-width
# Focal point options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
image:
  placement: 1
  focal_point: ""
  preview_only: false
---

Json(javascript object Notation)是为了Javascript运用。模块Json让Python数据结构转存到文件中，并在程序再次运行时加载该文件。

1. 使用json.dump()和json.load()

   - json.dump() 存储数组

     ```python
     #number_writer.py
     import json
     numbers = [2,3,4]
     filename = 'numbers.json'
     with open(filename,'w') as f_obj:
         json.dump(numbers,f_obj)
     ```

   - json.load() 读取文件

     ```python
     import json
     filename = 'numbers.json'
     with opne(filename) as f_obj:
         numbers = json.load(f_obj)
     print(numbers)
     ```

   2. 保存和读取用户生成的数据

      对于用户生成的数据，使用json保存它们，因为如果不以某种方式进行存储，等程序停止运行时用户信息将丢失。用户首次运行程序时就记住他了。

   3. 重构
      - 将代码划分为一系列完成具体工作的函数
      - 要编写出清晰而易于维护和拓展的代码，这种划分工作必不可少