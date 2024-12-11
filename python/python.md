# 代码规范
----------
* 遵守PEP8风格和其他内部代码规范（可使用自动格式化插件进行定义和修改如yapf或者flake８）：
    - 缩进是２个空格（或者４个空格），不要使用tab
    - 注意最大行长度
    - 函数以及类之间两个空行
    - 类内部的方法间一个空行
* 一个模块modules只做一类事情，相关的类放到一个模块中。模块文件的命名用复数，除了main.py, core.py or config.py。例如`elements.py`, `materials.py`等。
* import要按照如下顺序：标准库，相关第三方，本地lib
* 变量和常数用名词命名（常数大写）

## Python 语法新特性
* 海象运算符（valrus operator）`:=`:变量赋值+条件表达
```python
# case 1
l = [1, 2, 3]
if (lenght:=len(l))>0:
    print(f"The length of the list is {lenght}")
# case 2
l = [2,4,6,8]
is_even = all((num:=i)%2==0 for i in l)
print(f"All numbers in the list are even: {is_even} and the number is {num}")
```
* `match-case`表达式（比的`if-elif-else`更更灵活）：
```python
match x:
    case 0:
        print("x is zero")
    case 1:
        print("x is one")
    case _:
        print("x is neither zero nor one")
```
* 异步编程（async/await）（适用于ＩＯ密集型应用）：
```python
async def my_coroutine():
    await asyncio.sleep(1)
    print("Hello, world!")
    loop = asyncio.get_event_loop()
loop.run_until_complete(my_coroutine())
```


## General Tips
* 一定要做开发环境的隔离和包管理（conda, pipenv）
    * `conda create -n myenv python=3.11` 创建环境
    * `conda env list` 查看环境列表
    * `conda activate myenv` 激活环境
    * `pip/conda install -r requirements.txt` 安装依赖
* 方便使用类型标注（typing hint）的地方请使用类型标注
* 使用`breakpoint()`或者`import pdb;pdb.set_trace()`函数来调试代码
* **修改API形参位置的时候要注意修改所有使用该API的地方**
* UI和非UI相关的函数/代码一定要分开
* 在使用`try－except`的时候
    * 避免对大块代码使用
    * 一定要写清楚具体catch的错误是什么
* 尽量使用‘f－string’  
```python
name = 'John'
age = 25
print(f'My name is {name} and I am {age} years old.')
```
* 尽量避免`if－else`，尝试使用字典`dict`或者`match`去做条件判断
* 使用`defaultdict`对于需要初始化的字典
```python
from collections import defaultdict
d = defaultdict(set)
d['a'].add(1)
d['a'].add(2)
```
* `assert`用于对内debugging（不该出现的情况），`raise`对内（还没有考虑到的情况）
* 多用iterable迭代器和生成器，少用循环
* 当你需要在某个数据容器中查找元素时，使用 `set()` 而不是 `list()` （速度更快）
* 修改代码使记得修改相对应的注释（注释并不总是必要的）
* Python有自己的的垃圾回收机制（garbage collection），不需要手动回收内存。引用计数（reference counting）的垃圾回收机制会导致循环引用的问题。
* 多用列表推导式，少用显示循环
* 多用生成器表达式，少用列表生成式

## 函数与方法
* 函数命名用**动词＿名词**（小写）组合例如 **def get_elements()**
* 函数的标签和变量名要清晰易懂。
* 仅在模块内部使用（internal）函数用　`_`开头
* 私有函数（private function）用两个`__`开头
* 一个函数只做一件事情，其他公用功能可以写进helper函数
* Generic函数的开始要做sanity check提前return不满足条件的输入
* API（接口）函数和他的形参一定要可理解。comment一定要写，且清楚和简洁，可以采用如图所示。注释中语法可以采用sphinx风格。

```python
def my_function(arg1, arg2):
    """
    This is a function that does something.
    :param arg1: The first argument.
    :param arg2: The second argument.
    :return: The result of the function.
    """
    # do something
    return result
```

## 类与对象
* 类名用名词（首字母大写），采用驼峰命名法例如：`class FiniteElementCollector`
* 实例变量用名词（小写）
* 数据类的class可以用`@dataclass`装饰器，去简化类的创建和定义
* 学会重载（定义）magic methods:`__init__`, `__new__`, `__del__`, `__str__`, `__repr＿`, `__eq__`, `__hash__`, `__len__`, `__getitem__`, `__setitem__`, `__delitem__`, `__iter__`, `__contains__`, `__add__`, `__sub__`, `__mul__`, , `__mod__`, `__pow__`, `__and__`,`__imul__`, `__itruediv__`, `__neg__`, `__pos__`, `__abs__`, `__invert__`, etc.  
其中`__str__`和`__repr__`是python中两个比较特殊的magic methods，`__str__`返回用户看到的字符串，`__repr__`返回程序员看到的字符串，一般来说，`__str__`返回的字符串应该是用户可以读懂的，`__repr__`返回的字符串应该是程序员可以读懂的。`print()`命令会调用`__str__`方法，`str()`函数会调用`__repr__`方法。
* 使用built-in函数`dir()`去查看对象(object)的所有属性和方法（魔法方法）
* operator on the property of objects by characters
```python
isinstance(obj, type) # check if the object is an instance of the type
getattr(obj, 'attr') # get the attribute of the object
setattr(obj, 'attr', value) # set the attribute of the object
hasattr(obj, 'attr') # check if the object has the attribute
```
* 类方法（classmethod）用`@classmethod`装饰器，类方法只能访问类变量和类方法，不能访问实例变量和实例方法。
* 静态方法（staticmethod）用`@staticmethod`装饰器，静态方法可以访问类变量和类方法，不能访问实例变量和实例方法。









