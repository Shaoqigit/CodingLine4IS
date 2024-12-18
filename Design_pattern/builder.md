## Builder模式

Builder模式是创建型模式之一，它可以将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示。

Builder模式包含四个角色：

1. Builder（建造者）：它是一个抽象类，提供了创建产品的各个部件的接口。
2. ConcreteBuilder（具体建造者）：它实现了Builder接口，并提供了创建产品各个部件的具体实现。
3. Product（产品）：它是被构建的复杂对象，包含多个组成部件。
4. Director（指挥者）：它负责安排Builder的工作流程，指导建造者如何一步步构建产品。

Builder模式的优点：

1. 它可以使创建产品的过程和产品的表示分离开来，使得同样的构建过程可以创建不同的表示。
2. 它可以更加精细地控制产品的创建过程，提供更好的灵活性。
3. 它可以简化对象的创建过程，并使得创建过程易于扩展。

Builder模式的使用场景：

1. 相同的方法，不同的执行顺序，产生不同的结果。
2. 多个部件或属性，都可以装配到一个对象中。
3. 产品的创建过程相对复杂，其中的一些步骤可以按顺序执行，而其他步骤可以按需执行。

```python
class Director:
    def __init__(self, builder):
        self.builder = builder
    def construct(self):
        self.builder.build_part1()
        self.builder.build_part2()
        self.builder.build_part3()

class Builder:
    def build_part1(self):
        pass
    def build_part2(self):
        pass
    def build_part3(self):
        pass

class ConcreteBuilder(Builder):
    def __init__(self):
        self.product = Product()
    def build_part1(self):
        self.product.add_part1('part1')
    def build_part2(self):
        self.product.add_part2('part2')
    def build_part3(self):
        self.product.add_part3('part3')

class Product:
    def __init__(self):
        self.part1 = None
        self.part2 = None
        self.part3 = None
    def add_part1(self, part1):
        self.part1 = part1
    def add_part2(self, part2):
        self.part2 = part2
    def add_part3(self, part3):
        self.part3 = part3
    def __str__(self):
        return 'Product: part1={}, part2={}, part3={}'.format(self.part1, self.part2, self.part3)

director = Director(ConcreteBuilder())
director.construct()
print(director.builder.product)
```
与template方法模式相比:
- 在template模式中，父类决定子类方法的调用顺序
- 在builder模式中，Director类决定Builder类的方法调用顺序
