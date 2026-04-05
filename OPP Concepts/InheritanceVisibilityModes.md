# 🔐 Inheritance Visibility Modes in C++

In C++, **inheritance visibility modes** (also called access modes) determine how base class members are inherited into a derived class.

---

## 🔹 What are Visibility Modes?

When inheriting from a base class, you can use:

```cpp
class Derived : public Base {};
class Derived : protected Base {};
class Derived : private Base {};
```

These modes control how the base class members appear inside the derived class.

---

## 🔹 Base Class Example

```cpp id="g7x2lm"
class Base {
public:
    int pub;
protected:
    int pro;
private:
    int pri;
};
```

---

## 🔹 1. Public Inheritance

```cpp id="u4k9wd"
class Derived : public Base {};
```

### 📊 Behavior

| Base Member | In Derived       |
| ----------- | ---------------- |
| public      | public           |
| protected   | protected        |
| private     | ❌ not accessible |

---

## 🔹 2. Protected Inheritance

```cpp id="r9n3qa"
class Derived : protected Base {};
```

### 📊 Behavior

| Base Member | In Derived |
| ----------- | ---------- |
| public      | protected  |
| protected   | protected  |
| private     | ❌          |

---

## 🔹 3. Private Inheritance

```cpp id="m1z8vy"
class Derived : private Base {};
```

### 📊 Behavior

| Base Member | In Derived |
| ----------- | ---------- |
| public      | private    |
| protected   | private    |
| private     | ❌          |

---

## 🔥 Full Comparison

| Mode      | public →  | protected → | private → |
| --------- | --------- | ----------- | --------- |
| public    | public    | protected   | ❌         |
| protected | protected | protected   | ❌         |
| private   | private   | private     | ❌         |

---

## 🔹 Example

```cpp id="x8v5pl"
#include <iostream>
using namespace std;

class Base {
public:
    int x;
protected:
    int y;
private:
    int z;
};

class Derived : public Base {
public:
    void test() {
        x = 10; // ✅
        y = 20; // ✅
        // z = 30; ❌
    }
};
```

---

## 🔹 Access from Outside

```cpp id="w3k7zs"
int main() {
    Derived d;

    d.x = 10; // ✅ (only in public inheritance)
    // d.y = 20; ❌
}
```

---

## 🧠 Key Idea

> Inheritance mode affects how members are exposed in the derived class — NOT how they exist in the base class.

---

## 🔹 When to Use Each Mode

### ✅ Public Inheritance

* Represents **"is-a" relationship**
* Most commonly used

Example:

```cpp
class Dog : public Animal {};
```

---

### ⚠️ Protected Inheritance

* Rarely used
* When you want to hide public interface from outside but keep it for derived classes

---

### ⚠️ Private Inheritance

* Used when:

  * You want to reuse implementation
  * But NOT expose base class interface

---

## 🔹 Important Notes

* `private` members are NEVER directly accessible in derived classes
* Use `protected` if you want child classes to access data
* Public inheritance keeps interface visible

---

## 🧠 Key Takeaways

* Inheritance mode controls **access transformation**
* Does NOT change base class itself
* Public inheritance = most useful and common
* Private/protected = for controlled access

---

## 🚀 Pro Tip

If your design represents:

> **"Derived IS-A Base"**

👉 Always use:

```cpp
public inheritance
```

Otherwise, consider **composition instead of inheritance**

---
