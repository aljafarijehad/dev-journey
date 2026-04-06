# ⚡ Static (Early) Binding vs Dynamic (Late) Binding in C++

Binding refers to how a function call is connected to its definition.

---

## 🔹 What is Binding?

> Binding is the process of deciding **which function to call** when a function is invoked.

---

## 🔹 1. Static Binding (Early Binding)

### 📌 Definition:

> The function call is resolved at **compile-time**

---

## 🧠 Key Characteristics

* Happens **before program execution**
* Based on **pointer/reference type**
* Faster ✅
* No polymorphism ❌

---

## 📌 Example

```cpp
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

## 🔥 Output

```text
Base show()
```

---

## 🧠 Why?

* No `virtual` keyword
* Compiler decides using pointer type (`Base*`)

---

## 🔹 2. Dynamic Binding (Late Binding)

### 📌 Definition:

> The function call is resolved at **runtime**

---

## 🧠 Key Characteristics

* Happens **during execution**
* Based on **actual object type**
* Supports polymorphism ✅
* Slightly slower (due to runtime lookup)

---

## 📌 Example

```cpp
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

```text
Derived show()
```

---

## 🔹 Comparison

| Feature           | Static Binding ⚡ | Dynamic Binding 🔁 |
| ----------------- | ---------------- | ------------------ |
| Time              | Compile-time     | Runtime            |
| Keyword           | None             | `virtual`          |
| Decision Based On | Pointer type     | Object type        |
| Speed             | Faster           | Slightly slower    |
| Polymorphism      | ❌ No             | ✅ Yes              |

---

## 🔹 Visualization

### Static Binding:

```text
Base* ptr ──► Derived object
        |
        └── calls Base::show()
```

---

### Dynamic Binding:

```text
Base* ptr ──► Derived object
        |
        └── calls Derived::show()
```

---

## 🔹 When to Use Each?

### ✅ Use Static Binding When:

* You don’t need polymorphism
* Performance is critical
* Behavior is fixed

---

### ✅ Use Dynamic Binding When:

* You need flexibility
* You use inheritance
* You want runtime behavior changes

---

## 🔹 Important Rule

> Dynamic binding ONLY works with:

* `virtual` functions
* Base class pointer/reference

---

## ⚠️ Common Mistake

```cpp
Base obj = Derived(); // ❌ Object slicing
```

### 💥 Result:

* Derived part is lost
* No dynamic binding

---

## ✅ Correct Approach

```cpp
Base* ptr = new Derived();
```

---

## 🧠 Key Takeaways

* Static = fast but limited
* Dynamic = flexible but slightly slower
* `virtual` enables runtime polymorphism
* Always use base pointers for dynamic behavior

---

## 🚀 Pro Tip

If you see:

```cpp
Base* ptr = new Derived();
```

👉 You probably need `virtual`

---
