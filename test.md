<a id="arabic"></a>
[English ↙](#english)

<div dir="rtl" style="text-align: right;">

# 📘 الفرق بين Class و Structure

<p align="center">
  <img src="https://img.shields.io/badge/Language-C++-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/Level-Beginner-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/Topic-OOP-orange?style=for-the-badge">
</p>

---

## 🕰️ السياق التاريخي

### ❓ لماذا يتشابه Class و Structure؟

**🔹 C++ هي امتداد للغة C**

---

### 🔸 في لغة C:

- **Structure** موجودة فقط لتجميع البيانات  
- لا يوجد داخل Structure **Functions أو Methods**  
- لا يوجد مفهوم **Object Oriented Programming**  
- الهدف: **تجميع البيانات المرتبطة**  
  *(مثال: First Name + Last Name + E-mail للطالب)*  

---

### 🔸 في لغة C++:

- تم تطوير **Structure** لتدعم:
  - Functions (Methods)
  - Encapsulation (جزئياً)

- تم إضافة **Class**:
  - تدعم OOP بشكل كامل
  - تستخدم لبناء أنظمة معقدة

---

## ⚡ الفرق الأساسي

| الميزة            | Class 🧱        | Struct 📦       |
|------------------|----------------|----------------|
| Default Access   | Private        | Public         |
| الاستخدام        | أنظمة معقدة     | بيانات بسيطة   |
| Encapsulation    | قوي            | ضعيف افتراضياً |
| OOP              | كامل           | جزئي           |

---

## 💻 مثال عملي

```cpp
class Person {
private:
    string name;

public:
    void setName(string n) {
        name = n;
    }
};
