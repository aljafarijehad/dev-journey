# 🧬 Parameterized Constructor of the Base Class in C++

When a base class has a **parameterized constructor**, the derived class must explicitly call it.

---

## 🔹 The Problem

If the base class does NOT have a default constructor:

```cpp
class Base {
public:
    int x;

    Base(int val) {
        x = val;
    }
};
```

And you try this:

```cpp
class Derived : public Base g
public:
    Derived() {
        // ❌ ERROR
    }
};
```

### 💥 Result:

* Compilation Error
* Because C++ tries to call:

  ```cpp
  Base()
  ```

  which does NOT exist

---

## 🔹 The Solution (Constructor Initialization List)

You must call the base constructor manually:

```cpp
class Derived : public Base {
public:
    Derived(int val) : Base(val) {
        // ✅ Correct
    }
};
```

---

## 🔹 Full Example

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    int x;

    Base(int val) {
        x = val;
        cout << "Base Constructor\n";
    }
};

class Derived : public Base {
public:
    int y;

    Derived(int a, int b) : Base(a) {
        y = b;
        cout << "Derived Constructor\n";
    }
};

int main() {
    Derived obj(10, 20);

    cout << "x = " << obj.x << endl;
    cout << "y = " << obj.y << endl;
}
```

---

## 🔥 Output

```text
Base Constructor
Derived Constructor
x = 10
y = 20
```

---

## 🧠 Key Idea

> Base class constructor is ALWAYS called first

Even if you don’t see it.

---

## 🔹 Order of Execution

1. Base constructor
2. Derived constructor

---

## 🔹 What if You Don’t Call It?

### Case 1: Base has default constructor

✅ Works (C++ calls it automatically)

### Case 2: No default constructor

❌ Compilation error

---

## 🔹 Multiple Parameters Example

```cpp
class Base {
public:
    Base(int a, int b) {
        cout << a << " " << b << endl;
    }
};

class Derived : public Base {
public:
    Derived() : Base(10, 20) {
        cout << "Derived\n";
    }
};
```

---

## 🔹 Common Mistake

```cpp
Derived(int a) {
    Base(a); // ❌ WRONG
}
```

### 💥 Why wrong?

* This creates a temporary object
* It does NOT call the base constructor of the current object
md
---

## 🔹 Correct Way

```cpp
Derived(int a) : Base(a) {
}
```

---

## 🔹 With Default + Parameterized Constructors

```cpp
class Base {
public:
    Base() {
        cout << "Default\n";
    }

    Base(int x) {
        cout << "Parameterized\n";
    }
};
```

### Usage:

```cpp
class Derived : public Base {
public:
    Derived() : Base(10) {
        // calls parameterized version
    }
};
```

---

## 🧠 Key Takeaways

* Use **initializer list** to call base constructor
* Base constructor runs **before** derived
* If no default constructor exists → you MUST call it
* Never call base constructor inside body ❌

---

## 🚀 Pro Tip

Always prefer initializer lists:

* More efficient
* Required for:

  * Base classes
  * const members
  * references

---
