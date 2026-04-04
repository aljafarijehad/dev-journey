# 🧠 Static Members and Methods in C++

Understanding `static` in C++ is essential when you want to share data or behavior across all objects of a class.

---

## 🔹 What is a Static Member?

A **static data member** is a variable that:

* Is **shared among all objects** of a class
* Exists **only once in memory**
* Is not tied to any specific object

---

## 📌 Key Idea

> Normal member → each object has its own copy
> Static member → all objects share one copy

---

## 🔹 Example: Static Data Member

```cpp
#include <iostream>
using namespace std;

class Test {
public:
    static int count;

    Test() {
        count++;
    }
};

// Definition (required)
int Test::count = 0;

int main() {
    Test a;
    Test b;
    Test c;

    cout << Test::count << endl; // Output: 3
}
```

---

## 🧠 Explanation

* `count` is shared across all objects
* Every time an object is created → `count` increases
* Accessed using:

  ```cpp
  Test::count
  ```

---

## 🔹 What is a Static Method?

A **static method (static function)**:

* Belongs to the class, not to objects
* Can be called **without creating an object**
* Can only access:

  * Static members
  * Other static methods

---

## 📌 Example: Static Method

```cpp
#include <iostream>
using namespace std;

class Test {
public:
    static int count;

    Test() {
        count++;
    }

    static void showCount() {
        cout << count << endl;
    }
};

int Test::count = 0;

int main() {
    Test a;
    Test b;

    Test::showCount(); // Output: 2
}
```

---

## 🔥 Important Rules

### 1. Static variables must be defined outside the class

```cpp
int Test::count = 0;
```

---

### 2. Static methods CANNOT access non-static members

❌ Wrong:

```cpp
void show() {
    cout << count; // ERROR
}
```

✅ Correct:

```cpp
static void show() {
    cout << count;
}
```

---

### 3. No `this` pointer in static methods

* Because they are not tied to an object

---

## 🔹 Memory Behavior

| Member Type   | Memory Allocation |
| ------------- | ----------------- |
| Normal member | Per object        |
| Static member | One shared copy   |

---

## 🔹 When to Use Static?

Use `static` when:

* You need a **shared counter**
* You want **class-wide data**
* You don’t need object-specific values
* You want utility/helper functions

---

## 🔹 Real-World Example

### Counter for objects

```cpp
class User {
public:
    static int totalUsers;

    User() {
        totalUsers++;
    }
};

int User::totalUsers = 0;
```

---

## 🔥 Static vs Non-Static

| Feature       | Static            | Non-Static    |
| ------------- | ----------------- | ------------- |
| Ownership     | Class             | Object        |
| Memory        | Shared            | Per object    |
| Access        | ClassName::member | object.member |
| Needs object? | ❌ No              | ✅ Yes         |

---

## 🧠 Key Takeaways

* Static members are **shared across all objects**
* Static methods belong to the **class itself**
* Use `ClassName::member` to access them
* Static methods **cannot access non-static data**

---

## 🚀 Pro Tip

Static is commonly used for:

* Counters
* Configuration values
* Utility/helper functions

---

## ⚠️ Common Mistake

Forgetting to define static variables outside the class:

```cpp
// ❌ This alone is NOT enough
static int count;
```

You must add:

```cpp
// ✅ Required
int Test::count = 0;
```

```cpp
#include <iostream>
using namespace std;
class clsA
{
public:
static int Function1()
{
return 10;
}
int Function2()
{
return 20;
}
};
int main()
{
//The following line calls static function directly via class
not through the object
//At class level you can call only static methods and static
members
cout << clsA::Function1() <<endl;
//static methods can also be called throught the object.
clsA A1, A2;
cout << A1.Function1() << endl;
cout << A1.Function2() << endl;
cout << A2.Function1() << endl;
}
```
---
