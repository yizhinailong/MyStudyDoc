# C++类和对象

面向对象编程（Object-Oriented Programming，OOP）是一种以对象为核心的编程范式，通过将现实世界的事物抽象为程序中的对象，来解决复杂的问题。这种方法与面向过程的编程方式不同，面向过程更关注流程和步骤的实现，而面向对象则强调对象之间的交互和协作。

---

## 一、面向对象与面向过程

### 1. 什么是面向过程？

**面向过程**：将解决问题的过程视为一系列步骤的集合，按照步骤顺序逐步实现，主要关注的是实现过程和函数调用。

**举例：大象装进冰箱需要几步？**

1. 打开冰箱门
2. 把大象放进去
3. 关闭冰箱门

**面向过程实现：**

```cpp
#include <iostream>

void openFridge() {
    std::cout << "打开冰箱门" << std::endl;
}

void putElephantIn() {
    std::cout << "把大象放进去" << std::endl;
}

void closeFridge() {
    std::cout << "关闭冰箱门" << std::endl;
}

int main() {
    openFridge();
    putElephantIn();
    closeFridge();

    return 0;
}
```

**输出：**

```bash
打开冰箱门
把大象放进去
关闭冰箱门
```

### 2. 什么是面向对象？

**面向对象**：将现实世界的事物抽象为对象，每个对象包含属性和方法，通过对象之间的交互来解决问题。

**面向对象实现大象装进冰箱：**

```cpp
#include <iostream>
#include <string>

// 大象类
class Elephant {
public:
    Elephant(std::string n) : name(n) {}
    std::string getName() const { return name; }
private:
    std::string name;
};

// 冰箱类
class Fridge {
public:
    void open() {
        std::cout << "冰箱门打开了" << std::endl;
    }

    void putIn(const Elephant& elephant) {
        std::cout << "把" << elephant.getName() << "放进冰箱" << std::endl;
    }

    void close() {
        std::cout << "冰箱门关闭了" << std::endl;
    }
};

int main() {
    Elephant elephant("非洲大象");
    Fridge fridge;

    fridge.open();
    fridge.putIn(elephant);
    fridge.close();

    return 0;
}
```

**输出：**

```bash
冰箱门打开了
把非洲大象放进冰箱
冰箱门关闭了
```

**说明：**

- **对象**：`Elephant`和`Fridge`都是类的实例（对象），它们有自己的属性和方法。
- **方法调用**：通过调用对象的方法来完成操作，使程序更加模块化和可扩展。

---

## 二、类与对象的关系

### 1. 基本概念

- **类（Class）**：是对一类具有相同属性和行为的对象的抽象，是创建对象的模板。
- **对象（Object）**：是类的实例化结果，拥有类所定义的属性和方法。

### 2. 类与对象的区别

- **类是抽象的**，不占用内存；**对象是具体的**，占用内存空间。
- **类是对象的模板**；对象是类的实例。

**示例：**

```cpp
#include <iostream>
#include <string>

// 学生类
class Student {
public:
    Student(std::string n, int a) : name(n), age(a) {}

    void study() {
        std::cout << name << " 正在学习" << std::endl;
    }

    // Getter和Setter方法
    std::string getName() const { return name; }
    void setName(std::string n) { name = n; }

    int getAge() const { return age; }
    void setAge(int a) { age = a; }

private:
    std::string name;
    int age;
};

int main() {
    // 创建对象
    Student student1("张三", 20);
    student1.study();  // 输出：张三 正在学习

    Student student2("李四", 22);
    student2.study();  // 输出：李四 正在学习

    return 0;
}
```

---

## 三、基本特征：封装、继承、多态

### 1. 封装

#### （一）基本概念

**封装（Encapsulation）**：将对象的属性和方法封装起来，隐藏内部实现细节，只对外提供必要的接口。

**通俗理解**：在日常生活中，我们使用手机、电脑等设备时，只需关注如何操作，而不必了解其内部的复杂结构。这种对内部细节的隐藏就是封装。

**在编程中**：封装是将对象的属性（数据）和方法（功能）结合在一起，形成一个独立的实体（类）。类对外只暴露必要的接口，隐藏其内部实现细节。

**简而言之**：封装就是将数据和操作数据的方法绑定在一起，对外隐藏内部细节，只提供必要的访问接口。

#### （二）访问控制修饰符

- **public**：公有成员，类外部可访问。
- **private**：私有成员，类外部不可直接访问。
- **protected**：受保护成员，供子类访问。

#### （三）封装的使用

**示例：**

```cpp
#include <iostream>
#include <string>

class Dog {
public:
    // 构造函数
    Dog(std::string n, int a) : name(n), age(a) {}

    // Getter和Setter方法
    std::string getName() const { return name; }
    void setName(std::string n) { name = n; }

    int getAge() const { return age; }
    void setAge(int a) {
        if (a >= 0 && a <= 20) {
            age = a;
        } else {
            std::cout << "年龄不合法" << std::endl;
        }
    }

    // 行为方法
    void bark() {
        std::cout << name << " 正在汪汪叫" << std::endl;
    }

private:
    std::string name;
    int age;
};

int main() {
    Dog dog("小白", 3);
    dog.bark();  // 输出：小白 正在汪汪叫

    dog.setAge(25);  // 输出：年龄不合法

    return 0;
}
```

**说明：**

- **属性私有化**：将属性设置为`private`，防止外部直接访问。
- **提供公共方法**：通过`public`的`get`和`set`方法来访问和修改属性。
- **数据校验**：在`set`方法中添加条件判断，保证数据的合法性。

---

### 2. 继承

#### （一）基本概念

**继承（Inheritance）**：子类继承父类的属性和方法，实现代码的重用。

**通俗理解**：孩子继承父母的特征，如外貌、性格等。

**在编程中**：继承是指一个类（子类）继承另一个类（父类）的属性和方法，从而实现代码的重用和扩展。

- **语法：**

  ```cpp
  class 子类 : public 父类 {
      // 子类特有的属性和方法
  };
  ```

#### （二）继承的使用

**示例：**

```cpp
#include <iostream>
#include <string>

// 动物类（父类）
class Animal {
public:
    Animal(std::string n) : name(n) {}

    void eat() {
        std::cout << name << " 正在吃东西" << std::endl;
    }

protected:
    std::string name;
};

// 狗类（子类）
class Dog : public Animal {
public:
    Dog(std::string n) : Animal(n) {}

    void bark() {
        std::cout << name << " 正在汪汪叫" << std::endl;
    }
};

// 猫类（子类）
class Cat : public Animal {
public:
    Cat(std::string n) : Animal(n) {}

    void meow() {
        std::cout << name << " 正在喵喵叫" << std::endl;
    }
};

int main() {
    Dog dog("小黑");
    dog.eat();   // 输出：小黑 正在吃东西
    dog.bark();  // 输出：小黑 正在汪汪叫

    Cat cat("小花");
    cat.eat();   // 输出：小花 正在吃东西
    cat.meow();  // 输出：小花 正在喵喵叫

    return 0;
}
```

#### （三）方法重写（Override）

子类可以重写父类的方法，以实现不同的功能。

**示例：**

```cpp
#include <iostream>
#include <string>

// 动物类（父类）
class Animal {
public:
    Animal(std::string n) : name(n) {}

    virtual void eat() {
        std::cout << name << " 正在吃东西" << std::endl;
    }

protected:
    std::string name;
};

// 狗类（子类）
class Dog : public Animal {
public:
    Dog(std::string n) : Animal(n) {}

    void eat() override {
        std::cout << name << " 正在啃骨头" << std::endl;
    }
};

int main() {
    Animal* animal = new Dog("小黑");
    animal->eat();   // 输出：小黑 正在啃骨头

    delete animal;
    return 0;
}
```

#### （四）方法重载（Overload）

在同一个类中，函数名相同但参数列表不同。

**示例：**

```cpp
#include <iostream>

class Calculator {
public:
    // 两个参数的加法
    int add(int a, int b) {
        return a + b;
    }

    // 三个参数的加法
    int add(int a, int b, int c) {
        return a + b + c;
    }
};

int main() {
    Calculator calc;
    std::cout << "两个数相加：" << calc.add(1, 2) << std::endl;       // 输出：3
    std::cout << "三个数相加：" << calc.add(1, 2, 3) << std::endl;    // 输出：6

    return 0;
}
```

---

### 3. 多态

#### （一）基本概念

**多态（Polymorphism）**：同一个接口，使用不同的实例而执行不同的操作。

**通俗理解**：同一个操作作用于不同的对象，会产生不同的效果。

**在编程中**：多态是指父类指针或引用指向子类对象，不同的子类对象调用相同的方法，表现出不同的行为。

**多态的条件：**

1. **继承**：必须有父类和子类的继承关系。
2. **虚函数**：父类中声明虚函数，子类中重写该函数。
3. **父类指针或引用指向子类对象**。

#### （二）多态的使用

**示例：**

```cpp
#include <iostream>
#include <string>

// 动物类（父类）
class Animal {
public:
    Animal(std::string n) : name(n) {}

    virtual void makeSound() = 0;  // 纯虚函数，定义为抽象类

protected:
    std::string name;
};

// 狗类（子类）
class Dog : public Animal {
public:
    Dog(std::string n) : Animal(n) {}

    void makeSound() override {
        std::cout << name << "：汪汪汪" << std::endl;
    }
};

// 猫类（子类）
class Cat : public Animal {
public:
    Cat(std::string n) : Animal(n) {}

    void makeSound() override {
        std::cout << name << "：喵喵喵" << std::endl;
    }
};

int main() {
    Animal* animal1 = new Dog("小黑");
    Animal* animal2 = new Cat("小花");

    animal1->makeSound();  // 输出：小黑：汪汪汪
    animal2->makeSound();  // 输出：小花：喵喵喵

    delete animal1;
    delete animal2;

    return 0;
}
```

#### （三）理解多态

- **父类指针指向子类对象**：`Animal* animal = new Dog();`
- **虚函数机制**：通过在父类中声明虚函数，实现运行时多态。

**动态绑定机制：**

在程序运行时，根据对象的实际类型调用对应的函数，而不是编译时确定。

---

**总结：**

面向对象编程通过**封装、继承和多态**三个基本特征，使程序设计更加贴近现实世界的思维方式。

- **封装**：隐藏对象的内部实现，只对外提供公共接口，提高代码的安全性和可维护性。
- **继承**：实现代码的重用，建立类与类之间的层次关系，方便扩展。
- **多态**：提高代码的灵活性，使用统一的接口对不同的对象进行操作。

通过理解和运用这些特征，可以编写出高内聚、低耦合、可扩展、可维护的代码。

## 四、面向对象程序设计的五大基本原则

为了编写高质量、可维护的代码，软件开发中提出了 SOLID 五大原则。

### 1. 单一职责原则（SRP）

**定义**：一个类只负责一项职责，即一个类只有一个引起变化的原因。

单一功能原则规定每一个类都应该有一个单一的功能，并且该功能应该由这个类完全封装起来。所有它的服务都应该严密的和该功能平行（功能平行，意味着没有依赖）。通常意义下的单一功能，就是指类只有一种功能，而不为其实现过多的功能点，从而保证实体对象只有一个引起它变化的原因。

**优点**：

- **降低复杂度**：每个类的职责单一，逻辑简单。
- **提高可读性**：代码清晰明了，易于理解。
- **增强可维护性**：修改影响面小，降低风险。

**示例：**报表编辑与打印的分离

假设有一个报表类 `Report`，其最初设计如下：

```cpp
class Report {
public:
    void editContent(const std::string& content) {
        // 修改报表内容
        this->content = content;
    }

    void printReport() {
        // 打印报表内容
        std::cout << "Printing Report: " << content << std::endl;
    }

private:
    std::string content;
};
```

在这个设计中，`Report` 类既承担了**编辑内容**的责任，也承担了**打印内容**的责任，这违反了单一功能原则，因为修改或打印报表是两种不同的职责，分别可能因不同原因发生变化。

**改进：**将编辑和打印功能拆分

为遵循单一功能原则，我们可以将编辑和打印功能分离到不同的类中：

```cpp
// 负责报表内容的编辑
class ReportEditor {
public:
    void editContent(const std::string& content) {
        this->content = content;
    }

    std::string getContent() const {
        return content;
    }

private:
    std::string content;
};

// 负责报表的打印
class ReportPrinter {
public:
    void printReport(const ReportEditor& editor) {
        std::cout << "Printing Report: " << editor.getContent() << std::endl;
    }
};
```

**使用示例：**

```cpp
int main() {
    ReportEditor editor;
    editor.editContent("Annual Financial Report");

    ReportPrinter printer;
    printer.printReport(editor);

    return 0;
}
```

**优点分析：**

1. **单一职责清晰**：`ReportEditor` 仅负责管理和编辑内容，而 `ReportPrinter` 仅负责打印，职责明确。
2. **降低耦合**：编辑和打印的逻辑相互独立，修改编辑逻辑不会影响打印逻辑，反之亦然。
3. **更易扩展**：如果未来需要更改打印方式，比如打印到 PDF，只需修改或扩展 `ReportPrinter` 类即可。

### 2. 开放封闭原则（OCP）

**定义**：软件实体（类、模块、函数等）应该对扩展开放，对修改封闭。

开闭原则规定**软件**中的对象（类、模块、函数等）对于扩展是开放的，但对于修改是封闭的，这意味着一个实体是允许在不改变它的源代码的前提下变更它的行为。

**原则核心**

1. **对扩展开放**：当需求变化时，可以通过**添加新代码**（扩展）满足需求，而不需要改动已有代码。
2. **对修改封闭**：已有代码不应被修改，以确保稳定性，减少引入新问题的可能性。

**实现核心**
开闭原则通常通过**抽象**和**多态**实现：
- **依赖于抽象编程**：抽象类或接口定义系统的稳定行为，具体实现通过扩展或覆写实现新功能。
- **多态性**：通过多态机制调用子类的新行为，而无需修改原有代码逻辑。

**优点：**

1. **增强代码扩展性**：通过添加新类（扩展），实现功能拓展。
2. **提高代码稳定性**：已有代码不被修改，减少了引入新问题的风险。
3. **提高代码复用性**：抽象类和多态机制支持代码的灵活复用。

---

**示例：**图形绘制

违背开闭原则的设计
以下是一个不符合开闭原则的设计：

```cpp
class Shape {
public:
    int type;  // 1: Circle, 2: Rectangle
};

class GraphicEditor {
public:
    void drawShape(Shape* shape) {
        if (shape->type == 1) {
            drawCircle();
        } else if (shape->type == 2) {
            drawRectangle();
        }
    }

private:
    void drawCircle() {
        std::cout << "Drawing Circle" << std::endl;
    }
    void drawRectangle() {
        std::cout << "Drawing Rectangle" << std::endl;
    }
};
```

当需要支持新形状（如三角形）时，必须修改 `GraphicEditor` 类，违反了“对修改封闭”的原则。

---

遵循开闭原则的设计

通过抽象类和多态机制重构代码：

```cpp
// 抽象类：Shape
class Shape {
public:
    virtual void draw() const = 0;  // 定义抽象方法
    virtual ~Shape() = default;
};

// 具体实现类：Circle
class Circle : public Shape {
public:
    void draw() const override {
        std::cout << "Drawing Circle" << std::endl;
    }
};

// 具体实现类：Rectangle
class Rectangle : public Shape {
public:
    void draw() const override {
        std::cout << "Drawing Rectangle" << std::endl;
    }
};

// 图形编辑器
class GraphicEditor {
public:
    void drawShape(const Shape* shape) {
        shape->draw();  // 调用多态方法
    }
};
```

---

**使用示例**

```cpp
int main() {
    GraphicEditor editor;

    Shape* circle = new Circle();
    Shape* rectangle = new Rectangle();

    editor.drawShape(circle);      // 输出：Drawing Circle
    editor.drawShape(rectangle);   // 输出：Drawing Rectangle

    delete circle;
    delete rectangle;

    return 0;
}
```

如果未来需要支持新形状（如三角形），只需创建一个新的 `Triangle` 类，实现 `Shape` 接口，而不需要修改 `GraphicEditor` 类。

---

开闭原则强调**通过扩展实现变化，通过封闭保证稳定**。这种设计模式适用于变化频繁但结构相对稳定的系统，能够显著提高软件的**可维护性**和**可扩展性**。

### 3. 里氏替换原则（LSP）

**里氏替换原则**是面向对象编程中继承机制的核心规范，强调子类必须能够替代其父类，而不会影响程序的行为和正确性。

---

**原则核心**
1. **子类可替换父类**：程序中的子类对象应该能够无缝替换父类对象，而不会引发错误或行为变化。
2. **约束继承关系**：继承应符合父类的契约，子类扩展功能时不能破坏基类的行为逻辑。
3. **继承复用的基础**：只有遵循里氏替换原则，才能保证继承带来的代码复用是安全可靠的。

---

**实现方式：**

- **抽象父类或接口**：提取通用特性并定义接口，子类通过实现接口或继承抽象类来扩展行为。
- **避免违反父类契约**：子类重写方法时，必须确保行为符合父类预期，不能降低父类方法的适用范围。

---

**示例：**矩形与正方形

以下示例展示了里氏替换原则的遵守与违背：

违背里氏替换原则

```cpp
class Rectangle {
public:
    virtual void setWidth(double w) {
        width = w;
    }
    virtual void setHeight(double h) {
        height = h;
    }
    double getArea() const {
        return width * height;
    }

protected:
    double width;
    double height;
};

class Square : public Rectangle {
public:
    void setWidth(double w) override {
        width = w;
        height = w; // 正方形的宽高相等
    }
    void setHeight(double h) override {
        height = h;
        width = h; // 正方形的宽高相等
    }
};
```

在这里，正方形继承了矩形，但却违背了矩形的逻辑。程序中如果需要对 `Rectangle` 进行扩展，则 `Square` 的行为可能导致意外错误。

遵循里氏替换原则

将矩形和正方形抽象为不同类，避免强行继承：

```cpp
class Shape {
public:
    virtual double getArea() const = 0;
    virtual ~Shape() = default;
};

class Rectangle : public Shape {
public:
    Rectangle(double w, double h) : width(w), height(h) {}
    void setWidth(double w) {
        width = w;
    }
    void setHeight(double h) {
        height = h;
    }
    double getArea() const override {
        return width * height;
    }

private:
    double width;
    double height;
};

class Square : public Shape {
public:
    Square(double side) : sideLength(side) {}
    void setSide(double side) {
        sideLength = side;
    }
    double getArea() const override {
        return sideLength * sideLength;
    }

private:
    double sideLength;
};
```

通过为 `Rectangle` 和 `Square` 分离逻辑并实现 `Shape` 抽象接口，避免了违反里氏替换原则。

---

**优点：**

1. **保证继承复用的可靠性**：遵循里氏替换原则可以确保子类在扩展父类时不会破坏系统的稳定性。
2. **增强代码扩展性**：通过抽象和多态机制，简化了类型判别逻辑。
3. **减少运行期错误**：消除了父类与子类间不一致可能引发的运行期问题。

---

里氏替换原则是继承机制的设计规范，保障了继承复用的正确性，同时为开放封闭原则提供了理论支持。通过遵循该原则，可以提高代码的**可维护性**和**可扩展性**，并显著减少不必要的代码耦合。

### 4. 依赖倒置原则（DIP）

**接口隔离原则**是面向对象设计的五大原则之一，其核心思想是：**客户端不应该被强迫依赖它不需要的接口**。这一原则旨在通过设计更小、更专注的接口，减少类之间的耦合，提高系统的灵活性和可维护性。

---

**原则核心**

1. **避免“胖”接口**：将庞大且职责不单一的接口拆分为多个小型接口，每个接口只包含客户端需要的方法。
2. **接口单一性**：每个接口应针对特定的功能，避免强迫实现类去实现无关的方法。
3. **解耦客户端与接口**：通过设计更小的接口，让客户端仅依赖自己需要的功能，避免接口污染。

---

**胖接口问题**
一个“胖”接口可能会导致以下问题：

1. **实现复杂性**：实现类需要实现许多并不相关的方法，增加开发难度。
2. **低内聚**：接口的职责分散，难以维护和扩展。
3. **高耦合**：接口修改可能影响所有实现类和依赖该接口的客户端，带来维护灾难。

---

**示例：**

**违背接口隔离原则**
以下是一个违反接口隔离原则的设计：

```cpp
// 一个胖接口
class IWorker {
public:
    virtual void work() = 0;
    virtual void eat() = 0;
    virtual void sleep() = 0;
};

// 工厂工人实现
class FactoryWorker : public IWorker {
public:
    void work() override {
        std::cout << "Factory worker is working" << std::endl;
    }
    void eat() override {
        std::cout << "Factory worker is eating" << std::endl;
    }
    void sleep() override {
        std::cout << "Factory worker is sleeping" << std::endl;
    }
};

// 机器人实现（不需要eat和sleep方法）
class Robot : public IWorker {
public:
    void work() override {
        std::cout << "Robot is working" << std::endl;
    }
    void eat() override {
        // 机器人不需要吃饭
        throw std::logic_error("Robot does not eat");
    }
    void sleep() override {
        // 机器人不需要睡觉
        throw std::logic_error("Robot does not sleep");
    }
};
```

这种设计强迫 `Robot` 实现无用的方法，违背了接口隔离原则。

---

**遵循接口隔离原则**
通过将胖接口拆分为多个小型接口：

```cpp
// 定义更小的接口
class IWorkable {
public:
    virtual void work() = 0;
    virtual ~IWorkable() = default;
};

class IEatable {
public:
    virtual void eat() = 0;
    virtual ~IEatable() = default;
};

class ISleepable {
public:
    virtual void sleep() = 0;
    virtual ~ISleepable() = default;
};

// 工厂工人实现多个接口
class FactoryWorker : public IWorkable, public IEatable, public ISleepable {
public:
    void work() override {
        std::cout << "Factory worker is working" << std::endl;
    }
    void eat() override {
        std::cout << "Factory worker is eating" << std::endl;
    }
    void sleep() override {
        std::cout << "Factory worker is sleeping" << std::endl;
    }
};

// 机器人只实现需要的接口
class Robot : public IWorkable {
public:
    void work() override {
        std::cout << "Robot is working" << std::endl;
    }
};
```

---

**优点分析**

1. **降低耦合性**：客户端和实现类只依赖于需要的方法，减少了类间依赖。
2. **增强灵活性**：接口变动对实现类的影响更小，便于系统的扩展和重构。
3. **提升代码内聚性**：更小、更专注的接口确保了接口的职责单一性。

---

**接口隔离的两种实现方式**

1. **委托分离**：将接口职责分离到多个委托类中，通过组合实现接口隔离。例如，将接口职责分配给不同的服务对象。
2. **多重继承分离**：通过接口的多重继承，将胖接口拆分为多个小接口，实现类可以根据需求选择继承特定接口。

---

接口隔离原则强调**接口设计的单一性和精细化**，通过减少不必要的依赖，降低系统耦合度，提升代码灵活性和可维护性。这一原则在复杂系统的设计中尤为重要，能够有效防止“修改连锁反应”的问题。

### 5. 接口隔离原则（ISP）

**依赖反转原则**是面向对象设计的核心原则之一，旨在通过依赖抽象接口而非具体实现，减少高层和低层模块之间的耦合性。它是 **SOLID 原则**中的“D”，强调依赖的稳定性和灵活性。

---

**核心思想**
1. **高层模块不依赖低层模块**：高层模块和低层模块都应该依赖于共同的抽象接口。
2. **抽象接口不依赖具体实现**：接口设计独立于实现，具体实现依赖于抽象接口。
3. **依赖关系颠倒**：传统设计中高层模块依赖于低层模块，而在依赖反转原则中，低层模块反过来依赖于高层的需求抽象。

---

**原则动机**
在软件设计中，高层模块通常是系统的核心业务逻辑部分，低层模块是实现细节。如果高层模块直接依赖于低层模块，修改低层模块可能会破坏高层模块的功能，导致系统难以扩展和维护。通过依赖反转，将这种直接依赖转为依赖抽象接口，可以有效提高系统的稳定性和可扩展性。

---

**示例：**

传统设计（违反依赖反转原则）

```cpp
// 低层模块
class Keyboard {
public:
    std::string getInput() {
        return "Keyboard Input";
    }
};

// 高层模块
class Computer {
private:
    Keyboard keyboard; // 直接依赖具体实现
public:
    void processInput() {
        std::cout << "Processing: " << keyboard.getInput() << std::endl;
    }
};
```

在此设计中：
- 高层模块 `Computer` 直接依赖于低层模块 `Keyboard`。
- 如果需要添加新的输入设备（如 `Mouse`），需要修改 `Computer` 类，这破坏了系统的稳定性。

遵循依赖反转原则的设计

```cpp
// 抽象接口
class InputDevice {
public:
    virtual std::string getInput() = 0;
    virtual ~InputDevice() = default;
};

// 低层模块
class Keyboard : public InputDevice {
public:
    std::string getInput() override {
        return "Keyboard Input";
    }
};

class Mouse : public InputDevice {
public:
    std::string getInput() override {
        return "Mouse Input";
    }
};

// 高层模块
class Computer {
private:
    InputDevice& inputDevice; // 依赖于抽象接口
public:
    Computer(InputDevice& device) : inputDevice(device) {}
    void processInput() {
        std::cout << "Processing: " << inputDevice.getInput() << std::endl;
    }
};
```

在此设计中：
- 高层模块 `Computer` 和低层模块 `Keyboard`/`Mouse` 都依赖于抽象接口 `InputDevice`。
- 新增或替换输入设备时，只需扩展接口的实现，不需要修改 `Computer` 类。

---

**实现方式**
1. **依赖注入（Dependency Injection）**使用构造函数注入、方法注入或属性注入的方式，将依赖的抽象接口传递给高层模块。
   
2. **工厂模式（Factory Pattern）**使用工厂方法生成具体实现，隐藏依赖的创建细节。

3. **服务定位器（Service Locator）**通过服务定位器模式提供依赖的抽象接口，动态分配具体实现。

---

**优点**
1. **降低耦合性**：模块之间通过抽象接口连接，降低直接依赖。
2. **提高扩展性**：新增功能只需扩展接口实现，而无需修改现有代码。
3. **增强测试性**：通过依赖注入可以轻松替换依赖，便于单元测试。
4. **支持模块化开发**：不同团队可以基于共同接口开发各自的模块，提升开发效率。

---

**注意事项**
1. **接口设计的稳定性**：抽象接口需要足够稳定，以避免频繁修改影响整个系统。
2. **权衡抽象与具体实现**：在某些场景下，完全依赖抽象可能增加设计复杂性，需要根据需求权衡设计。
3. **增加的复杂性**：引入抽象接口和依赖注入可能使代码结构更复杂，需避免过度设计。

---

依赖反转原则是面向对象设计中减少耦合的重要手段。通过依赖抽象接口，高层和低层模块之间的依赖关系得以解耦，系统的可维护性和灵活性显著提升。这一原则与**开放封闭原则**、**接口隔离原则**密切相关，共同构成了高质量软件设计的理论基础。

---

## 五、总结

面向对象程序设计通过 **封装、继承、多态** 三大特性，提供了强大的代码复用和扩展能力。遵循 **SOLID** 五大原则，可以编写出高内聚、低耦合、易维护的代码。

**主要收获**：

- 理解了封装的重要性和实现方式。
- 掌握了继承的特点和应用场景。
- 了解了多态的实现条件和优势。
- 学习了五大设计原则，提高代码质量。
- 深入解析了 C++ 类和对象的细节，加深对 OOP 的理解。

---

希望以上内容能够帮助你更理解面向对象程序设计的核心概念和应用。如有疑问，欢迎交流讨论！
