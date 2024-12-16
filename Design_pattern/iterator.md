Python中创建迭代器的几种方式：

1. 使用iter()函数：

```python
my_list = [1, 2, 3, 4, 5]
my_iter = iter(my_list)
```

2. 使用__iter__()方法：

```python
class MyClass:
    def __init__(self, data):
        self.data = data

    def __iter__(self):
        return iter(self.data)

    def __next__(self):
        return next(self.data)

    def __getitem__(self, index):
        return self.data[index]

myobj = MyClass([1, 2, 3, 4, 5])
my_iter = iter(myobj)
```

