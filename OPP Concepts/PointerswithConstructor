# 🧠 Shallow Copy vs Deep Copy in C++

This topic is very important because it distinguishes between code that merely "works" and code that is **correct and safe** in C++.

---

## 🔹 What Happens If You Don't Define a Copy Constructor?

If you don’t define your own Copy Constructor, C++ automatically provides:

> **Default Copy Constructor**

### 📌 What does it do?

* Performs a **Shallow Copy**

### 💡 Meaning:

* Copies values as they are
* If there is a **pointer** → it copies the **address only** ❌

---

## ⚠️ Problem Example

```cpp
#include <iostream>
using namespace std;

class Test {
public:
    int* ptr;

    Test(int value) {
        ptr = new int(value);
    }
};

int main() {
    Test a(10);
    Test b = a;   // Default Copy Constructor (Shallow Copy)

    *b.ptr = 50;

    cout << *a.ptr << endl; // 🔥 Output?
}
```

### ❗ Output:

```
50
```

### 🧠 Why?

* `a.ptr` and `b.ptr` point to the **same memory location**
* Modifying one affects the other

---

## 🔥 The Bigger Problem (Danger)

If you add a destructor:

```cpp
~Test() {
    delete ptr;
}
```

### 💥 What happens?

* The same pointer gets deleted twice!
* Result:

  * Crash
  * Undefined Behavior

---

## 🔹 What is Shallow Copy?

### 📌 Definition:

> Copying values without duplicating the actual memory

### 🧠 Visualization:

```
Pointer A ──► [Data]
Pointer B ──► [Same Data]
```

### ❌ Problems:

* Changing one object affects another
* Double deletion
* Hard-to-debug bugs

---

## 🔹 What is Deep Copy?

### 📌 Definition:

> Copying values **and** creating a separate copy in memory

### 🧠 Visualization:

```
Pointer A ──► [Data]
Pointer B ──► [New Copy of Data]
```

---

## ✅ How to Implement Deep Copy (Copy Constructor)

```cpp
class Test {
public:
    int* ptr;

    Test(int value) {
        ptr = new int(value);
    }

    // Deep Copy Constructor
    Test(const Test& other) {
        ptr = new int(*other.ptr);  // 🔥 Copy value, not address
    }

    ~Test() {
        delete ptr;
    }
};
```

---

## 🔹 Result After Deep Copy

```cpp
Test a(10);
Test b = a;

*b.ptr = 50;

cout << *a.ptr << endl; // ✅ 10
```

### ✅ Now:

* Each object is independent
* No side effects

---

## 🔹 When Do You Need Deep Copy?

If your class contains:

* Pointers 🔥
* Dynamic memory (`new`)
* Dynamic arrays
* Resources (files, sockets, etc.)

---

## 🔹 Relation to the Rule of Three

If your class defines:

* Destructor
* Copy Constructor
* Copy Assignment Operator

### ✅ You must define all three

> Because they manage memory together

---

## 🔥 Final Comparison

| Feature     | Shallow Copy ❌ | Deep Copy ✅     |
| ----------- | -------------- | --------------- |
| Copy Type   | Address        | Value           |
| Memory      | Shared         | Independent     |
| Safety      | Unsafe         | Safe            |
| Performance | Faster         | Slightly slower |

---

## 🧠 Key Takeaways

* Default Copy Constructor = **Shallow Copy** ❌
* If your class uses pointers → use **Deep Copy** ✅

### ⚠️ Otherwise, you may face:

* Strange bugs
* Crashes
* Memory issues

---

## 🔹 What Happens After Deleting a Pointer?

```cpp
int* ptr = new int(10);
delete ptr;
```

### 📌 Notes:

* The value in the heap is deleted
* The pointer still exists ⚠️ (dangling pointer)

### ✅ Best Practice:

```cpp
ptr = nullptr;
```

---

## 🔹 Pointer vs No Pointer

| Case                    | Risk         |
| ----------------------- | ------------ |
| No pointers             | ❌ Safe       |
| Pointers + Shallow Copy | ⚠️ High risk |
| Pointers + Deep Copy    | ✅ Safe       |

---

## 🔹 The `*` in Pointers

* `ptr` → holds the **address**
* `*ptr` → accesses the **value at that address**

### 📌 Example:

```cpp
int* p = new int(5);

cout << p << endl;   // address
cout << *p << endl;  // value = 5

*p = 20;             // modify value

cout << *p << endl;  // 20
```

---

## 💡 Final Note

When working with manual memory management in C++, understanding:

* Shallow Copy
* Deep Copy

is **essential**, not optional.

---

## 🚀 Next Step (Recommended)

Consider using:

* Smart Pointers (`unique_ptr`, `shared_ptr`)
* Rule of Five (modern C++)

for safer and cleaner code.

---
