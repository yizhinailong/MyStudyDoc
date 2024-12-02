# C++ 类详解

C++ 是一种支持面向对象编程的强大语言，类是其核心特性，提供了封装、继承、多态等功能。以下是关于 C++ 类的详细解析，涵盖基础概念、成员函数、构造与析构、访问控制、继承、多态、高级特性以及设计实践。

---

## 1. 类与对象的基本概念

类与对象的基本概念

在面向对象编程中，**类** 和 **对象** 是核心概念。以下详细解释它们的定义、特点、以及在程序设计中的作用。

---

### 1. 什么是类？
#### 定义
**类（Class）** 是一种用户定义的数据类型，用于描述一组具有相同属性和行为的对象。它是对象的蓝图或模板，定义了对象的属性（成员变量）和方法（成员函数）。

#### 特点
- **封装性**：类将数据和操作这些数据的函数封装在一起，隐藏实现细节。
- **继承性**：可以通过继承扩展已有类的功能。
- **多态性**：同一操作可以对不同的类实例表现出不同的行为。

#### 类的定义语法
```cpp
class ClassName {
public:
    // 公有成员
protected:
    // 受保护成员
private:
    // 私有成员
};
```

- **ClassName**：类的名称。
- **访问控制符**：`public`、`protected` 和 `private`，用于控制成员的访问权限。

#### 示例：简单的类定义
```cpp
class Car {
public:
    std::string brand; // 公有属性
    int speed;         // 公有属性

    void drive() {     // 公有方法
        std::cout << "The car is driving at speed: " << speed << " km/h" << std::endl;
    }
};
```

---

### 2. 什么是对象？
#### 定义
**对象（Object）** 是类的实例，是程序中实际操作的实体。对象包含类中定义的属性和方法。

#### 特点
- **独立性**：每个对象都有自己独立的数据成员。
- **行为性**：对象可以调用类的方法来操作自己的数据。
- **具体性**：对象是类的具体实现，与类的抽象性相对应。

#### 对象的创建（实例化）
通过声明类的变量或使用 `new` 运算符创建对象。

```cpp
Car car1;              // 创建对象 car1
Car* car2 = new Car(); // 使用指针创建对象 car2
```

#### 示例：对象的使用
```cpp
#include <iostream>
#include <string>

class Car {
public:
    std::string brand; // 公有属性
    int speed;         // 公有属性

    void drive() {     // 公有方法
        std::cout << "The car is driving at speed: " << speed << " km/h" << std::endl;
    }
};

int main() {
    Car car1;              // 创建对象
    car1.brand = "Toyota"; // 设置属性
    car1.speed = 120;

    car1.drive(); // 调用方法
    return 0;
}
```

**输出：**

```
Toyota is driving at speed: 120 km/h
```

---

### 3. 类与对象的关系
- **类是抽象的**：它定义了一组对象的共同特性和行为，但不能直接使用。
- **对象是具体的**：它是类的实例化，拥有实际数据和功能。

---

### 4. 类的组成

#### 4.1 成员变量（属性）
- 数据成员是类的属性，用于存储对象的状态。
- **示例：**
  
  ```cpp
  class Person {
     public:
         string name;  // 成员变量
         int age;
  };
  ```

#### 4.2 成员函数（方法）
- 成员函数是类的方法，用于操作成员变量或执行某些功能。
- **示例：**
  
  ```cpp
  class Person {
     public:
         void introduce() {  // 成员函数
             cout << "Hi, I am " << name << " and I am " << age << " years old." << endl;
         }
  };
  ```

#### 4.3 访问控制符
- 控制成员的访问权限：
  - **`public`**：成员可以被类的外部直接访问。
  - **`protected`**：成员不能被外部访问，但可以被派生类访问。
  - **`private`**：成员只能在类的内部访问。
- **示例：**
  
  ```cpp
  class Person {
     private:
         string ssn;  // 私有成员
  
     public:
         void setSSN(string id) { ssn = id; }  // 提供公有接口
         string getSSN() { return ssn; }
  };
  ```

#### 4.4 构造函数
- 用于初始化对象。
- **示例：**
  
  ```cpp
  class Car {
     public:
         string brand;
         int speed;
  
         // 构造函数
         Car(string b, int s) {
             brand = b;
             speed = s;
         }
  };
  ```

#### 4.5 析构函数
- 用于释放对象资源。
- **示例：**
  ```cpp
  ~Car() {
      cout << "Car object destroyed" << endl;
  }
  ```

---

### 5. 对象的独立性
每个对象拥有自己独立的成员变量，它们互不干扰。

**示例**：对象的独立性

```cpp
#include <iostream>
using namespace std;

class Car {
   public:
       string brand;
       int speed;
};

int main() {
    Car car1, car2;

    car1.brand = "Toyota";
    car1.speed = 120;

    car2.brand = "Ford";
    car2.speed = 100;

    cout << car1.brand << ": " << car1.speed << " km/h" << endl;
    cout << car2.brand << ": " << car2.speed << " km/h" << endl;

    return 0;
}
```

**输出：**

```
Toyota: 120 km/h
Ford: 100 km/h
```

---

### 6. 类的封装性
封装是通过将数据和操作方法结合起来，同时隐藏内部实现细节，提供公有接口供外界访问。

#### 示例：封装的实现
```cpp
#include <iostream>
using namespace std;

class BankAccount {
   private:
       double balance;

   public:
       void deposit(double amount) {
           if (amount > 0) balance +=
```

---

## 2. 类的访问控制符

C++ 提供了三种访问控制符，用于管理类成员的访问权限：`public`、`private` 和 `protected`。它们定义了成员的可见性和访问范围，从而实现类的封装性和安全性。

---

### 1. `public` 公有访问权限
- **范围**：类的外部可以访问。
- **典型用途**：用于定义类的接口（如构造函数、操作函数等）。

**示例**：公有访问权限

```cpp
/**
 * 这段C++代码定义了一个`Box`类。
 * 类中包含三个公共数据成员：`length`、`breadth`和`height`，分别表示盒子的长、宽和高。
 * 类中还定义了一个公共成员函数`getVolume`，用于计算并返回盒子的体积。
 * 在`main`函数中，创建了一个`Box`对象`box1`，并为其三个属性赋值。
 * 然后调用`getVolume`函数计算体积，并输出结果。
 */
#include <iostream>

class Box {
public:
    double length; // 公共数据成员
    double breadth;
    double height;

    double getVolume() { // 公共成员函数
        return length * breadth * height;
    }
};

int main() {
    Box box1; // 创建对象
    box1.length = 5.0;
    box1.breadth = 6.0;
    box1.height = 7.0;

    std::cout << "Volume: " << box1.getVolume() << std::endl;

    return 0;
}
```

**输出：**

```bash
Volume: 210
```

---

### **2. `private` 私有访问权限**
- **范围**：成员只能在类的内部访问，不能在类的外部或派生类中访问。
- **典型用途**：用于定义类的内部实现细节，保护类的数据完整性。

**示例：私有访问权限**
```cpp
#include <iostream>
using namespace std;

class Box {
   private:
      double length;  // 私有成员

   public:
      void setLength(double len) {  // 公有接口操作私有成员
          length = len;
      }

      double getLength() {  // 公有接口访问私有成员
          return length;
      }
};

int main() {
    Box box;
    box.setLength(5.0);  // 设置私有成员的值
    cout << "Length: " << box.getLength() << endl;  // 输出 5.0

    // box.length = 10.0;  // 错误！不能直接访问私有成员
    return 0;
}
```

---

### **3. `protected` 受保护访问权限**
- **范围**：成员不能被类的外部访问，但可以被派生类访问。
- **典型用途**：通常用于继承时，允许派生类操作基类的成员，但隐藏这些成员对类的外部访问。

**示例：受保护访问权限**
```cpp
#include <iostream>
using namespace std;

class Base {
   protected:
      double value;  // 受保护成员

   public:
      void setValue(double val) {
          value = val;
      }
};

class Derived : public Base {
   public:
      void showValue() {  // 派生类可以访问受保护成员
          cout << "Value: " << value << endl;
      }
};

int main() {
    Derived obj;
    obj.setValue(20.5);  // 通过公有接口设置基类成员
    obj.showValue();     // 派生类访问受保护成员

    // cout << obj.value;  // 错误！不能在外部访问受保护成员
    return 0;
}
```

---

### **4. 访问控制符与继承的关系**

访问控制符的作用在继承中会有所变化，派生类对基类成员的访问权限与继承方式有关：

#### 继承方式与访问权限对比表：

| **基类成员**     | **公有继承** | **保护继承** | **私有继承** |
| ---------------- | ------------ | ------------ | ------------ |
| `public` 成员    | 公有         | 受保护       | 私有         |
| `protected` 成员 | 受保护       | 受保护       | 私有         |
| `private` 成员   | 无法访问     | 无法访问     | 无法访问     |

**示例：继承方式与访问权限**
```cpp
#include <iostream>
using namespace std;

class Base {
   public:
      int publicMember = 1;

   protected:
      int protectedMember = 2;

   private:
      int privateMember = 3;
};

class PublicDerived : public Base {
   public:
      void display() {
          cout << "Public: " << publicMember << endl;        // 公有成员保持公有
          cout << "Protected: " << protectedMember << endl; // 受保护成员保持受保护
          // cout << privateMember; // 错误！无法访问私有成员
      }
};

class ProtectedDerived : protected Base {
   public:
      void display() {
          cout << "Public as Protected: " << publicMember << endl;   // 公有成员变为受保护
          cout << "Protected: " << protectedMember << endl;         // 受保护成员保持受保护
      }
};

class PrivateDerived : private Base {
   public:
      void display() {
          cout << "Public as Private: " << publicMember << endl;    // 公有成员变为私有
          cout << "Protected as Private: " << protectedMember << endl; // 受保护成员变为私有
      }
};

int main() {
    PublicDerived obj1;
    obj1.display();
    cout << obj1.publicMember << endl;  // 可以访问公有成员

    // ProtectedDerived obj2;
    // obj2.publicMember;  // 错误！成员在外部不可见

    return 0;
}
```

---

### **5. 常见的访问控制错误与解决方案**

#### 错误 1：尝试在外部访问私有成员
```cpp
class Box {
   private:
      double length;
};

int main() {
    Box box;
    // box.length = 5.0;  // 错误！私有成员不可访问
}
```

**解决方案：** 使用公有接口访问或操作私有成员。

#### 错误 2：继承时访问权限不匹配
```cpp
class Base {
   protected:
      int value;
};

class Derived : public Base {
   public:
      void display() { cout << value << endl; }
};

int main() {
    Derived obj;
    // obj.value = 10;  // 错误！受保护成员不可直接访问
}
```

**解决方案：** 提供公有接口在基类中操作受保护成员。

---

### **总结**

C++ 的访问控制符为类的封装性提供了灵活的控制：
- **`private`**：用于隐藏实现细节，保护数据安全。
- **`public`**：定义类的外部接口，提供访问能力。
- **`protected`**：允许继承类使用，同时隐藏成员对外部的访问。

通过合理使用访问控制符，可以实现数据隐藏、接口封装以及继承中的安全性，从而编写更加健壮和可维护的代码。

---

## **3. 构造函数与析构函数**

### 构造函数
- 构造函数是类的一种特殊成员函数，在对象创建时自动调用。
- 构造函数的名称与类名相同，无返回值。

**示例：构造函数**
```cpp
class Box {
   private:
      double length;
   public:
      Box() { length = 0; }  // 默认构造函数
      Box(double len) { length = len; }  // 带参数的构造函数
      double getLength() { return length; }
};
```

### 析构函数
- 析构函数在对象销毁时自动调用，用于释放资源。
- 析构函数的名称在类名前加 `~`，无参数和返回值。

**示例：析构函数**
```cpp
class Box {
   public:
      ~Box() {
          cout << "Box object is destroyed." << endl;
      }
};
```

---

## **4. 深拷贝与浅拷贝**

浅拷贝只复制指针地址，可能导致多个对象共享同一块内存。深拷贝需要创建一块新的内存并复制内容。

**深拷贝示例：**
```cpp
class Box {
   private:
      double* length;
   public:
      Box(double len) {
          length = new double(len);
      }
      Box(const Box& other) { // 拷贝构造函数
          length = new double(*other.length);
      }
      ~Box() {
          delete length;
      }
};
```

---

## **5. 静态成员与静态函数**

### 静态成员
静态成员在类的所有对象中共享，只存在一个副本。

### 静态函数
静态函数只能访问静态成员。

**示例：静态成员与静态函数**
```cpp
class Box {
   static int count;
   public:
      static void incrementCount() { count++; }
};
int Box::count = 0;
```

---

## **6. 运算符重载**

C++ 支持运算符重载，使类的对象可以像内置类型一样操作。

**示例：重载 `+` 运算符**
```cpp
class Box {
   public:
      double length;
      Box operator+(const Box& other) {
          Box result;
          result.length = this->length + other.length;
          return result;
      }
};
```

---

## **7. 类的继承与多态**

### 继承
- 派生类继承基类的特性，可通过 `public`、`protected` 或 `private` 方式继承。
- 基类的 `private` 成员不能被派生类直接访问。

**继承示例：**
```cpp
class Base {
   protected:
      int value;
   public:
      void setValue(int val) { value = val; }
};

class Derived : public Base {
   public:
      void showValue() { cout << value << endl; }
};
```

### 多态
- 通过基类指针或引用调用派生类的函数。
- 使用 `virtual` 关键字实现运行时多态。

**多态示例：**
```cpp
class Shape {
   public:
      virtual void draw() { cout << "Drawing Shape" << endl; }
};

class Circle : public Shape {
   public:
      void draw() override { cout << "Drawing Circle" << endl; }
};

int main() {
    Shape* shape = new Circle();
    shape->draw();  // 调用 Circle 的 draw
    delete shape;
    return 0;
}
```

---

## **8. 模板类**

模板类允许类支持泛型，适用于多种数据类型。

**模板类示例：**
```cpp
template <typename T>
class Box {
   private:
      T data;
   public:
      Box(T value) : data(value) {}
      T getData() { return data; }
};
```

---

## **9. 高级特性**

### 抽象类
包含纯虚函数的类不能实例化：
```cpp
class Shape {
   public:
      virtual void draw() = 0;  // 纯虚函数
};
```

### 虚函数表
虚函数表（vtable）用于实现多态机制。

### 智能指针
C++11 提供 `std::unique_ptr` 和 `std::shared_ptr`，用于自动管理动态内存，避免内存泄漏：
```cpp
#include <memory>
std::unique_ptr<Box> box = std::make_unique<Box>(10, 20);
```

---

## **10. 类的设计原则**

1. **单一职责原则**：每个类只负责一个功能。
2. **开闭原则**：类应对扩展开放，对修改关闭。
3. **合理封装**：数据成员设置为 `private`，通过公有接口访问。

---

## **总结**

C++ 类提供了强大的面向对象编程能力，包括数据封装、继承与多态、模板支持以及内存管理机制。通过合理使用这些特性，可以设计出高效、健壮、易维护的代码。
