**Pycharm2021.2破解**

https://mp.weixin.qq.com/s/4TWpEl26waFyJ10fgCzbsQ



**Python虚拟环境管理**

```shell
# 在本路径下创建myvenv的虚拟环境
python -m venv myvenv
# 激活虚拟环境
~/myvenv/Script/active.bat

# 导出虚拟环境清单
pip freeze > requirements.txt
# 导入虚拟环境清单
pip install -r requirements.txt
```



**清华大学博士讲解Python数据结构与算法**

https://www.bilibili.com/video/BV1uA411N7c5?p=2



# 时间复杂度与空间复杂度

## **时间复杂度**

- <u>估算</u>程序运行完成的时间

- 常见时间复杂度效率：1>nlogn>n>nlogn>n2>n2logn>n3>....

```python
# ==空间复杂度，依次递增== #
import math


# 1，长度
def one():
    print('hello')
    print('hello')
    print('hello')


# log_n
# 循环减半
def log_n1(n: int = 64):
    while n > 2:
        n = n // 2


count = 0


def log_n2(find, arg):
    """顺序列表，二分法查找
    """
    low = 0
    high = len(arg) - 1
    mid = math.ceil((high - low) / 2)  # 中位序列
    mid_value = arg[mid]  # 中位数
    global count
    try:
        if find == mid_value:
            count += 1
            result = find
        elif find < mid_value:
            count += 1
            result = log_n2(find, arg[:mid])
        else:
            count += 1
            result = log_n2(find, arg[mid + 1:])
        print('Found it, count {}, it is {}'.format(count, result))
        return result
    except:
        print('Not found.')


# n
def n_():
    for i in range(6):
        print('hello')


# n_log_n

# n2，层数
def n2_():
    for i in range(6):
        for j in range(6):
            print('hello')


if __name__ == '__main__':
    log_n2(1, [1, 2, 3, 4, 5, 6])
```



## **空间复杂度**

- 概念：内存占用

- 表现：
  - O(1)：几个变量
  - O(n)：长度为n的一维列表
  - O(mn)：m行n列的二维列表
- 空间换时间
  - 分布式
  - 增加硬件配置



# **递归**

- 特点：

  - 调用自身
  - 结束条件

- ```python
  # 递归
  def func1(x):
      while x > 0:
          func1(x - 1)
          print(x, end='')
          return x
  
  
  def func2(x):
      while x > 0:
          print(x, end='')
          func2(x - 1)
          return x
  
  
  if __name__ == '__main__':
      func1(4)
      func2(4)
  ```

  > 12344321
  >
  > <img src="https://raw.githubusercontent.com/freshman118/ImageRepository/master/image-20210826212939140.png" alt="image-20210826212939140" style="zoom:50%;" />


- 汉诺塔问题

  - 描述：

    - 64个盘子按照从上到下、从小到大的顺序放在一根柱子上，还有另外两根柱子，分别为ABC三根柱子
    - 要求将其移动到另一根柱子，任何时候大盘子不得在小盘子上方

  - 思路

    - n-1个盘子从A经过C柱子移动到B柱子
    - 第n个盘子，从A移动到C柱子
    - n-1个盘子从B经过A柱子移动到C柱子

  - 递推式：h(x) = 2h(x-1) + 1

  - ```python
    def hannoi(n, a, b, c):
        if n > 0:
            # n-1个盘子从A经过C柱子移动到B柱子
            hannoi(n - 1, a, c, b)
            # 第n个盘子，从A移动到C柱子
            print('move {} to {}'.format(a, c))
            # n-1个盘子从B经过A柱子移动到C柱子
            hannoi(n - 1, b, a, c)
    ```

    > move A to C
    > move A to B
    > move C to B
    > move A to C
    > move B to A
    > move B to C
    > move A to C



# 列表查找

## 顺序查找

别称线性查找（Linear search）

```python
def linear_search(data: list, target: int):
    for index, value in enumerate(data):
        if target == value:
            print('Found target')
            return
    else:
        return None
```

## 二分查找

逐次切分成两部分，只适用于有顺序的列表

```python
count = 0

# 方法一：递归
def binary_search(data: list, target: int):
    low = 0
    high = len(data) - 1
    mid = (low + high) // 2
    global count  # 修改函数外的变量
    
    if target == data[mid]:
        count += 1
        print('Found it')
    elif target < data[mid]:
        binary_search(data[:mid], target)
        count += 1
    elif target > data[mid]:
        binary_search(data[mid + 1:], target)
        count += 1
    else:
        print('Can not found it')
    print('Look for it {} time'.format(count))
    
    
# 方法二：循环
def binary_search2(data: list, target: int):
    low = 0
    high = len(data) - 1
    global count

    while low <= high:
        mid = (low + high) // 2
        count += 1
        if target == data[mid]:
            print('Found it')
            print('Look for it {} times'.format(count))
            return data[mid]
        if target > data[mid]:
            low = mid + 1
        else:
            high = mid - 1
    else:
        return None
    
    
#统计时间装饰器
import time

def cal_time(func):
    def wrapper(*args, **kwargs):
        t1 = time.time()
        result = func(*args, **kwargs)
        t2 = time.time()
        print("%s running time: %s secs." % (func.__name__, t2 - t1))
        return result

    return wrapper
```

