# ⚡ Virtual Functions in Inheritance (C++)

Virtual functions are the foundation of **runtime polymorphism** in C++ when using inheritance.

---

## 🔹 What is a Virtual Function?

> A virtual function is a member function declared in the base class using the `virtual` keyword, and it can be **overridden** in a derived class.

---

## 🔹 Why Do We Need Virtual Functions?

Without `virtual`:

* The function call is decided at **compile-time**
* Based on the **pointer type** ❌

With `virtual`:

* The function call is decided at **runtime**
* Based on the **actual object type** ✅

---

## 🔹 Basic Example (Without Virtual)

```cpp id="k3m9qp"
#include <iostream>
using namespace std;

class Base {
public:
    void show() {
        cout << "Base show()" << endl;
    }
};

class Derived : public Base {
public:
    void show() {
        cout << "Derived show()" << endl;
    }
};

int main() {
    Base* ptr;
    Derived d;

    ptr = &d;
    ptr->show(); // ❌ Calls Base version
}
```

---

## 🔹 Using Virtual (Correct Way)

```cpp id="t6x1nv"
#include <iostream>
using namespace std;

class Base {
public:
    virtual void show() {
        cout << "Base show()" << endl;
    }
};

class Derived : public Base {
public:
    void show() override {
        cout << "Derived show()" << endl;
    }
};

int main() {
    Base* ptr;
    Derived d;

    ptr = &d;
    ptr->show(); // ✅ Calls Derived version
}
```

---

## 🔥 Output

```text id="f4b7ke"
Derived show()
```

---

## 🧠 Key Idea

> The function that gets called depends on the **actual object**, not the pointer type

---

## 🔹 How It Works Internally

* C++ uses something called:

  > **vtable (virtual table)**

* Each object keeps a pointer to a table of virtual functions

* At runtime → correct function is selected

---

## 🔹 Rules for Virtual Functions

* Must be declared in base class
* Should be overridden in derived class
* Called using base pointer/reference

---

## 🔹 Using Base Pointer

```cpp id="h9w2qs"
Base* ptr = new Derived();
ptr->show(); // calls Derived version
```

---

## 🔹 Virtual Destructor (VERY IMPORTANT)

```cpp id="m8z3xa"
class Base {
public:
    virtual ~Base() {
        cout << "Base destructor\n";
    }
};
```

### 💡 Why?

```cpp id="n7k1zd"
Base* ptr = new Derived();
delete ptr; // ensures proper cleanup
```

Without virtual destructor → memory issues ⚠️

---

## 🔹 Pure Virtual Function (Abstract Class)

```cpp id="y5q8rm"
class Base {
public:
    virtual void show() = 0; // pure virtual
};
```

### 📌 Meaning:

* Base class becomes **abstract**
* Cannot create objects from it

---

## 🔹 Derived Must Implement

```cpp id="c2x9vb"
class Derived : public Base {
public:
    void show() override {
        cout << "Implemented!" << endl;
    }
};
```

---

## 🔥 Summary Table

| Feature      | Without Virtual ❌ | With Virtual ✅ |
| ------------ | ----------------- | -------------- |
| Binding      | Compile-time      | Runtime        |
| Behavior     | Static            | Dynamic        |
| Polymorphism | ❌                 | ✅              |

---

## 🧠 Key Takeaways

* Virtual functions enable **runtime polymorphism**
* Always use `override` in derived classes
* Use base pointers to get dynamic behavior
* Always make destructor virtual in polymorphic classes

---

## 🚀 Pro Tip

Use virtual functions when:

* You have a base class pointer/reference
* You expect different behavior in derived classes

---

## ⚠️ Common Mistake

```cpp id="d4r6zx"
Base obj = Derived(); // ❌ object slicing
```

### 💥 Problem:

* Derived part is lost
* Virtual behavior breaks

---

## ✅ Correct Way

```cpp id="p8t3kw"
Base* ptr = new Derived();
```

---

## 🎯 Real-World Idea

Think of:

* Base → Shape
* Derived → Circle, Rectangle

Each has its own `draw()` implementation

---
