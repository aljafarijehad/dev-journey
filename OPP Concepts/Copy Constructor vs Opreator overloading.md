# Copy Constructor vs Assignment Operator in C++

## When is the Copy Constructor Called?

The copy constructor is called when a new object is created from an existing object.

### Common Cases

#### 1. Initialization from another object

```cpp
MyClass a;
MyClass b = a;   // copy constructor
```

#### 2. Passing object by value

```cpp
void func(MyClass obj) { }
func(a);   // copy constructor
```

#### 3. Returning object by value

```cpp
MyClass func() {
    MyClass temp;
    return temp;   // copy constructor (may be optimized)
}
```

#### 4. Direct initialization

```cpp
MyClass b(a);   // copy constructor
```

---

## When is the Assignment Operator (=) Called?

The assignment operator is called when the object is already created, and then assigned a value.

### Example

```cpp
MyClass a;
MyClass b;

b = a;   // assignment operator
```

---

## Key Difference

| Case             | What Happens        |
| ---------------- | ------------------- |
| `MyClass b = a;` | Copy Constructor    |
| `b = a;`         | Assignment Operator |

### Rule

* Object creation → Copy Constructor
* Already exists → Assignment Operator

---

## How to Define Them

### Copy Constructor

```cpp
class MyClass {
public:
    MyClass(const MyClass& other) {
        cout << "Copy Constructor Called\n";
    }
};
```

---

### Assignment Operator Overloading

```cpp
class MyClass {
public:
    MyClass& operator=(const MyClass& other) {
        cout << "Assignment Operator Called\n";
        return *this;
    }
};
```

---

## Ways to Call Each

### Copy Constructor Calls

```cpp
MyClass a;
MyClass b = a;
MyClass c(a);
func(a);
return a;
```

---

### Assignment Operator Calls

```cpp
MyClass a, b, c;
b = a;
a = b = c;
```

---

## Full Example

```cpp
#include <iostream>
using namespace std;

class MyClass {
public:
    MyClass() {}

    MyClass(const MyClass& other) {
        cout << "Copy Constructor\n";
    }

    MyClass& operator=(const MyClass& other) {
        cout << "Assignment Operator\n";
        return *this;
    }
};

int main() {
    MyClass a;

    MyClass b = a; // Copy constructor
    MyClass c(a);  // Copy constructor

    MyClass d;
    d = a;         // Assignment operator
}
```

---

## Summary

* New object → Copy Constructor
* Existing object → Assignment Operator

---

## Important Note

If you don’t define them:

* C++ provides default versions
* If your class uses dynamic memory (pointers), you should implement them yourself

This relates to the Rule of Three.
