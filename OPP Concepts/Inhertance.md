# 🧬 Inheritance in C++

Inheritance is one of the core concepts of **Object-Oriented Programming (OOP)**.
It allows a class to inherit properties and behavior from another class.

---

## 🔹 What is Inheritance?

> Inheritance allows a class (child/derived) to reuse the code of another class (parent/base).

---

## 📌 Basic Syntax

```cpp
class Base {
public:
    void show() {
        cout << "Hello from Base" << endl;
    }
};

class Derived : public Base {
    // inherits everything from Base
};
```

---

## 🔹 Example

```cpp
#include <iostream>
using namespace std;

class Animal {
public:
    void speak() {
        cout << "Animal makes a sound" << endl;
    }
};

class Dog : public Animal {
public:
    void bark() {
        cout << "Dog barks" << endl;
    }
};

int main() {
    Dog d;

    d.speak(); // inherited
    d.bark();  // own function
}
```

---

## 🧠 Explanation

* `Dog` inherits from `Animal`
* `Dog` can use:

  * `speak()` ✅ (from parent)
  * `bark()` ✅ (its own)

---

## 🔹 Types of Inheritance (Access Specifiers)

### 1. Public Inheritance

```cpp
class Derived : public Base {};
```

| Base Member | In Derived       |
| ----------- | ---------------- |
| public      | public           |
| protected   | protected        |
| private     | ❌ not accessible |

---

### 2. Protected Inheritance

```cpp
class Derived : protected Base {};
```

| Base Member | In Derived |
| ----------- | ---------- |
| public      | protected  |
| protected   | protected  |
| private     | ❌          |

---

### 3. Private Inheritance

```cpp
class Derived : private Base {};
```

| Base Member | In Derived |
| ----------- | ---------- |
| public      | private    |
| protected   | private    |
| private     | ❌          |

---

## 🔹 Access Modifiers Recap

| Modifier  | Accessible in Class | Accessible in Child | Accessible Outside |
| --------- | ------------------- | ------------------- | ------------------ |
| public    | ✅                   | ✅                   | ✅                  |
| protected | ✅                   | ✅                   | ❌                  |
| private   | ✅                   | ❌                   | ❌                  |

---

## 🔹 Constructor Behavior

* Base class constructor runs **first**
* Then derived class constructor

```cpp
class Base {
public:
    Base() {
        cout << "Base Constructor\n";
    }
};

class Derived : public Base {
public:
    Derived() {
        cout << "Derived Constructor\n";
    }
};
```

---

## 🔹 Overriding Functions

```cpp
class Base {
public:
    void show() {
        cout << "Base" << endl;
    }
};

class Derived : public Base {
public:
    void show() {
        cout << "Derived" << endl;
    }
};
```

---

## 🔹 Calling Base Version

```cpp
void show() {
    Base::show(); // call parent version
    cout << "Derived" << endl;
}
```

---

## 🔹 Types of Inheritance (Structure)

### 1. Single Inheritance

One base → one derived

### 2. Multiple Inheritance

```cpp
class A {};
class B {};
class C : public A, public B {};
```

---

### 3. Multilevel Inheritance

```cpp
class A {};
class B : public A {};
class C : public B {};
```

---

### 4. Hierarchical Inheritance

```cpp
class A {};
class B : public A {};
class C : public A {};
```

---

## 🔥 Important Notes

* Private members are **NOT inherited directly**
* Use `protected` if you want child classes to access members
* Always use **public inheritance** for "is-a" relationships

---

## 🧠 Real-World Example

```cpp
class Vehicle {
public:
    void start() {
        cout << "Vehicle started\n";
    }
};

class Car : public Vehicle {
public:
    void drive() {
        cout << "Car driving\n";
    }
};
```

---

## 🔥 Common Mistakes

### ❌ Trying to access private members

```cpp
class Base {
private:
    int x;
};

class Derived : public Base {
    void test() {
        // x = 10; ❌ ERROR
    }
};
```

---

## 🧠 Key Takeaways

* Inheritance = code reuse
* Derived class gets access to base class members
* Access depends on:

  * access modifier
  * inheritance type
* Constructors run from base → derived

---

## 🚀 Pro Tip

Use inheritance when:

* There is a clear **"is-a" relationship**

  * Dog is an Animal
  * Car is a Vehicle

Avoid it when:

* You only want to reuse code → consider composition instead

---
