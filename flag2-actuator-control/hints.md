# Flag 2: Hints & Tips
# 关卡2：提示与技巧

Need some help controlling actuators? Here are progressive hints!

需要控制执行器的帮助吗？这里有渐进式提示！

---

## 🤔 General Hints | 一般提示

### Hint 1: Start with LED | 从LED开始

**LED is the easiest actuator!** It's perfect for learning digital output.

**LED是最简单的执行器！**它非常适合学习数字输出。

Just remember:
- Long leg → Positive (+) → Arduino pin (through resistor)
- Short leg → Negative (-) → GND

只需记住：
- 长脚 → 正极 (+) → Arduino引脚（通过电阻）
- 短脚 → 负极 (-) → GND

---

### Hint 2: Always Use Resistors with LEDs | 总是对LED使用电阻

**Without a resistor, you might burn out your LED or Arduino!**

**没有电阻，你可能会烧坏LED或Arduino！**

Recommended resistor values:
- Standard LED: 220Ω - 1kΩ (推荐值：220欧姆 - 1千欧)
- High-brightness LED: 470Ω - 1kΩ (高亮LED：470欧姆 - 1千欧)

---

### Hint 3: Check Pin Capabilities | 检查引脚能力

**Not all pins are the same!**

**不是所有引脚都一样！**

- **Any digital pin**: Can do `digitalWrite()` (HIGH/LOW)
- **PWM pins** (marked with ~): Can do `analogWrite()` (0-255)
  - Arduino Uno PWM pins: 3, 5, 6, 9, 10, 11

---

## 🔌 Actuator-Specific Hints | 执行器特定提示

### For LED | LED

**Problem**: LED doesn't light up  
**问题**：LED不亮

**Solutions**:
1. Check polarity (long leg to pin, short leg to GND) (检查极性)
2. Try flipping the LED around (尝试翻转LED)
3. Test with the onboard LED first (pin 13) (先用板载LED测试)

```cpp
// Test onboard LED
const int LED = 13;  // Built-in LED
void setup() {
  pinMode(LED, OUTPUT);
}
void loop() {
  digitalWrite(LED, HIGH);
  delay(1000);
  digitalWrite(LED, LOW);
  delay(1000);
}
```

---

**Problem**: Want to control brightness, not just ON/OFF  
**问题**：想控制亮度，不只是开/关

**Solution**: Use PWM with `analogWrite()`  
**解决方案**：使用PWM和`analogWrite()`

```cpp
const int LED = 9;  // Must be PWM pin!

void setup() {
  pinMode(LED, OUTPUT);
}

void loop() {
  analogWrite(LED, 50);   // Dim (暗)
  delay(1000);
  analogWrite(LED, 128);  // Medium (中)
  delay(1000);
  analogWrite(LED, 255);  // Bright (亮)
  delay(1000);
}
```

---

### For Buzzer | 蜂鸣器

**Problem**: Buzzer makes sound but I can't control the pitch  
**问题**：蜂鸣器发声但我无法控制音调

**Solution**: You might have a **passive buzzer**. Use `tone()` function:  
**解决方案**：你可能有**无源蜂鸣器**。使用`tone()`函数：

```cpp
const int BUZZER = 9;

void setup() {
  pinMode(BUZZER, OUTPUT);
}

void loop() {
  tone(BUZZER, 1000);  // 1000 Hz
  delay(500);
  tone(BUZZER, 2000);  // 2000 Hz
  delay(500);
  noTone(BUZZER);      // Stop
  delay(500);
}
```

**If you have an active buzzer**, just use `digitalWrite()`:

**如果你有有源蜂鸣器**，只需使用`digitalWrite()`：

```cpp
digitalWrite(BUZZER, HIGH);  // Beep
delay(500);
digitalWrite(BUZZER, LOW);   // Stop
```

---

**Bonus**: Play a melody!  
**加分**：播放旋律！

```cpp
// Note frequencies (音符频率)
#define NOTE_C 262
#define NOTE_D 294
#define NOTE_E 330
#define NOTE_F 349
#define NOTE_G 392

void loop() {
  int melody[] = {NOTE_C, NOTE_D, NOTE_E, NOTE_F, NOTE_G};
  int noteDuration = 500;
  
  for (int i = 0; i < 5; i++) {
    tone(BUZZER, melody[i]);
    delay(noteDuration);
    noTone(BUZZER);
    delay(50);
  }
  delay(2000);
}
```

---

### For Servo Motor | 舵机

**Problem**: Servo won't move / jitters  
**问题**：舵机不动/抖动

**Solutions**:
1. Make sure you included the Servo library (确保包含了Servo库)
   ```cpp
   #include <Servo.h>
   ```

2. Check power supply (检查电源)
   - Servos need good power! (舵机需要良好的电源！)
   - If jittering, try powering servo from external 5V (如果抖动，尝试从外部5V供电)

3. Verify wiring (验证接线)
   ```
   Brown/Black → GND
   Red → 5V
   Orange/Yellow → Signal Pin (PWM)
   ```

---

**Problem**: How to make smooth motion?  
**问题**：如何实现平滑运动？

**Solution**: Move in small increments  
**解决方案**：小增量移动

```cpp
#include <Servo.h>
Servo myServo;

void setup() {
  myServo.attach(9);
}

void loop() {
  // Sweep from 0 to 180
  for (int pos = 0; pos <= 180; pos++) {
    myServo.write(pos);
    delay(15);  // Small delay for smooth motion
  }
  
  // Sweep from 180 to 0
  for (int pos = 180; pos >= 0; pos--) {
    myServo.write(pos);
    delay(15);
  }
}
```

---

### For RGB LED | RGB LED

**Understanding RGB LED**:
- Has 4 pins: R (Red), G (Green), B (Blue), Common (共阴或共阳)
- **Common Cathode** (共阴): Common → GND, R/G/B → Pins
- **Common Anode** (共阳): Common → 5V, R/G/B → Pins (inverted logic)

**理解RGB LED**：
- 有4个引脚：R（红）、G（绿）、B（蓝）、公共端
- **共阴极**：公共端 → GND，R/G/B → 引脚
- **共阳极**：公共端 → 5V，R/G/B → 引脚（反向逻辑）

```cpp
// RGB LED - Common Cathode
const int RED = 9;
const int GREEN = 10;
const int BLUE = 11;

void setup() {
  pinMode(RED, OUTPUT);
  pinMode(GREEN, OUTPUT);
  pinMode(BLUE, OUTPUT);
}

void loop() {
  // Pure colors
  setColor(255, 0, 0);    // Red
  delay(1000);
  setColor(0, 255, 0);    // Green
  delay(1000);
  setColor(0, 0, 255);    // Blue
  delay(1000);
  
  // Mixed colors
  setColor(255, 255, 0);  // Yellow
  delay(1000);
  setColor(255, 0, 255);  // Magenta
  delay(1000);
  setColor(0, 255, 255);  // Cyan
  delay(1000);
}

void setColor(int red, int green, int blue) {
  analogWrite(RED, red);
  analogWrite(GREEN, green);
  analogWrite(BLUE, blue);
}
```

---

## 🐛 Debugging Tips | 调试技巧

### Issue: Nothing Happens | 什么都不发生

**Check**:
1. Is the actuator connected to power? (执行器连接到电源了吗？)
2. Is GND connected? (GND连接了吗？)
3. Did you set the pin as OUTPUT? (你将引脚设置为OUTPUT了吗？)
   ```cpp
   pinMode(PIN, OUTPUT);  // Don't forget this!
   ```

---

### Issue: Code Uploads but Actuator Doesn't Respond | 代码上传但执行器无响应

**Try this debug code**:

```cpp
void setup() {
  Serial.begin(9600);
  pinMode(13, OUTPUT);
  Serial.println("Testing pin 13...");
}

void loop() {
  digitalWrite(13, HIGH);
  Serial.println("HIGH");
  delay(1000);
  
  digitalWrite(13, LOW);
  Serial.println("LOW");
  delay(1000);
}
```

If Serial prints but nothing happens:
- Check your wiring (检查接线)
- Try a different pin (尝试不同引脚)
- Test with the onboard LED (用板载LED测试)

---

### Issue: Servo Library Not Found | 找不到Servo库

**If you get "Servo.h: No such file or directory"**:

**如果你得到"Servo.h: No such file or directory"**：

1. Go to Sketch → Include Library → Servo (进入Sketch → Include Library → Servo)
2. Or install via Library Manager (或通过库管理器安装)
   - Tools → Manage Libraries (工具 → 管理库)
   - Search "Servo" (搜索"Servo")
   - Install "Servo by Arduino"

---

## 💡 Pro Tips | 专业技巧

### Tip 1: Use `for` Loops for Patterns | 使用for循环创建模式

```cpp
// Fade LED in and out
for (int i = 0; i <= 255; i++) {
  analogWrite(LED, i);
  delay(5);
}
for (int i = 255; i >= 0; i--) {
  analogWrite(LED, i);
  delay(5);
}
```

---

### Tip 2: Create Functions for Reusability | 创建函数以重用

```cpp
void blinkLED(int times, int delayMs) {
  for (int i = 0; i < times; i++) {
    digitalWrite(LED, HIGH);
    delay(delayMs);
    digitalWrite(LED, LOW);
    delay(delayMs);
  }
}

void loop() {
  blinkLED(3, 200);  // Blink 3 times, 200ms each
  delay(1000);
}
```

---

### Tip 3: Non-blocking Timing | 非阻塞计时

Instead of `delay()`, use `millis()` for better control:

不用`delay()`，使用`millis()`以获得更好的控制：

```cpp
unsigned long previousMillis = 0;
const long interval = 1000;

void loop() {
  unsigned long currentMillis = millis();
  
  if (currentMillis - previousMillis >= interval) {
    previousMillis = currentMillis;
    
    // Toggle LED
    digitalWrite(LED, !digitalRead(LED));
  }
}
```

---

## 📋 Quick Checklist | 快速检查清单

Before asking for help:

寻求帮助前：

- [ ] Actuator connected to correct pin (执行器连接到正确引脚)
- [ ] GND connected (GND已连接)
- [ ] Power (VCC/5V) connected if needed (如需要，电源已连接)
- [ ] pinMode() set to OUTPUT (pinMode设置为OUTPUT)
- [ ] Using correct function (digitalWrite/analogWrite/tone) (使用正确函数)
- [ ] Pin number in code matches physical connection (代码中的引脚号匹配物理连接)
- [ ] For PWM: Using a PWM-capable pin (对于PWM：使用支持PWM的引脚)

---

## 🆘 Still Need Help? | 还需要帮助？

1. **Swap components** - Try a different LED or buzzer (更换组件 - 尝试不同的LED或蜂鸣器)
2. **Test with examples** - Use File → Examples → Basics (用示例测试)
3. **Ask for help** - Your TA is here to support you! (寻求帮助 - 助教在这里支持你！)

---

**You're doing great! Actuators are the fun part - they make things happen!** 🎉

**你做得很好！执行器是有趣的部分 - 它们让事情发生！** 🎉

