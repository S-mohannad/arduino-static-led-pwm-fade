# 💡 Static LED + PWM Fade LED

> **Arduino Project #08** — LED ثابت يضيء بشكل دائم (Pin 8) + LED ثاني يزيد سطوعه تدريجياً ثم يطفي فجأة (Pin 10)

[![Arduino](https://img.shields.io/badge/Arduino-00979D?style=for-the-badge&logo=arduino&logoColor=white)](https://www.arduino.cc/)
[![Language](https://img.shields.io/badge/Language-C%2B%2B-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)](https://isocpp.org/)
[![Level](https://img.shields.io/badge/Level-Beginner-green?style=for-the-badge)](https://github.com/S-mohannad)

---

## 📋 Description

يتحكم في LEDين بطريقتين مختلفتين في نفس الوقت:
- **Pin 8** — LED ثابت يضيء بشكل دائم منذ `setup()`
- **Pin 10** — LED يزيد سطوعه تدريجياً من 0 إلى 255 بخطوات 5، ثم يطفي فجأة ويتوقف 3 ثواني قبل التكرار

---

## 🔌 Circuit

```
Arduino UNO
┌─────────────────┐
│             8 ●─┼──[220Ω]──💡 LED 1 (ثابت) ── GND
│            10 ●─┼──[220Ω]──💡 LED 2 (Fade)  ── GND
│           GND ●─┼──────────────────────────────GND
└─────────────────┘
```

- 💡 LED 1 على Pin 8 (Digital) — يضيء بشكل ثابت
- 💡 LED 2 على Pin 10 (PWM) — يتحكم بسطوعه تدريجياً
- مقاومة 220Ω لكل LED

---

## 💡 Concepts Used

- `digitalWrite()` — تشغيل LED بشكل ثابت في `setup()`
- `analogWrite()` — التحكم في سطوع LED عبر PWM
- **التحكم بمكونين مختلفين** — Digital و PWM في نفس الوقت
- **التزايد التدريجي** — `x = x + 5` لزيادة السطوع بشكل ناعم
- `if / else` — للتحقق من الوصول لأقصى قيمة

---

## 📊 Behavior

| المكوّن | الحالة | التفاصيل |
|---------|--------|----------|
| LED 1 (Pin 8) | ثابت ON | يضيء منذ البداية ولا يتغير |
| LED 2 (Pin 10) | Fade In | يزيد من 0 → 255 بخطوات 5 كل 150ms |
| LED 2 (Pin 10) | إطفاء فجائي | يطفي فوراً عند وصوله 255 |
| LED 2 (Pin 10) | توقف | يبقى مطفياً 3 ثواني ثم يكرر |

---

## 🔗 Code

```cpp
int x = 0;

void setup() {
  pinMode(8, OUTPUT);
  pinMode(10, OUTPUT);
  digitalWrite(8, 1);  // LED 1 ثابت يضيء دائماً
}

void loop() {
  analogWrite(10, x);  // LED 2 يزيد سطوعه
  delay(150);

  if (x < 255) {
    x = x + 5;
  } else {
    x = 0;
    delay(300);
    analogWrite(10, x);  // إطفاء فجائي
    delay(3000);         // توقف 3 ثواني
  }
}
```
## 🔧 How to Run

1. افتح **Arduino IDE**
2. وصّل الدائرة كما في الرسم
3. انسخ الكود والصقه
4. اختر **Board:** Arduino UNO
5. اختر **Port** الصحيح
6. اضغط ⬆️ **Upload**
7. شاهد LED 1 يضيء بشكل ثابت بينما LED 2 يزيد سطوعه تدريجياً

---

## 👨‍💻 Author

**S-mohannad** — [@S-mohannad](https://github.com/S-mohannad)
