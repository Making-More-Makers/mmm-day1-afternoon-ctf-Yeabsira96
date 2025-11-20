# Flag 2: Actuator Control ⭐⭐
# 关卡2：执行器控制 ⭐⭐

**Difficulty**: Beginner | 难度：初级  
**Points**: 5 | 分数：5  
**Estimated Time**: 30-45 minutes | 预计时间：30-45分钟

---

## 🎯 Challenge Mission | 挑战任务

**Your mission**: Control an actuator (output device) using your Arduino.

**你的任务**：使用Arduino控制执行器（输出设备）。

### Success Criteria | 成功标准

To capture Flag 2, you must:

要捕获Flag 2，你必须：

- ✅ Choose one actuator from your kit (从套件中选择一个执行器)
- ✅ Connect it properly to your Arduino (正确连接到Arduino)
- ✅ Write code to control the actuator (编写代码控制执行器)
- ✅ Demonstrate at least 2 different states/behaviors (演示至少2种不同的状态/行为)
- ✅ Document your work (记录你的工作)

---

## 📚 What You'll Learn | 你将学习

By completing this flag, you'll learn:

完成此关卡后，你将学习：

- How to connect actuators to Arduino (如何将执行器连接到Arduino)
- Digital output control (数字输出控制)
- PWM (Pulse Width Modulation) for analog control (PWM脉宽调制用于模拟控制)
- Timing and delays (计时和延迟)

---

## 🛠️ Available Actuators | 可用执行器

Choose **ONE** of these actuators to complete the challenge:

选择**其中一个**执行器来完成挑战：

### Basic Actuators | 基础执行器

1. **LED** (发光二极管)
   - Difficulty: ⭐
   - Control: ON/OFF, brightness, blinking patterns
   - 控制：开/关、亮度、闪烁模式

2. **Buzzer** (蜂鸣器)
   - Difficulty: ⭐
   - Control: ON/OFF, different tones/melodies
   - 控制：开/关、不同音调/旋律

3. **RGB LED** (RGB LED)
   - Difficulty: ⭐⭐
   - Control: Different colors, color mixing
   - 控制：不同颜色、颜色混合

### Intermediate Actuators | 中级执行器

4. **Servo Motor** (舵机)
   - Difficulty: ⭐⭐
   - Control: Position from 0-180 degrees
   - 控制：0-180度的位置

5. **DC Motor (with L298N driver)** (直流电机)
   - Difficulty: ⭐⭐⭐
   - Control: Speed, direction
   - 控制：速度、方向

6. **Relay Module** (继电器模块)
   - Difficulty: ⭐⭐
   - Control: Switch high-power devices ON/OFF
   - 控制：开关大功率设备

---

## 🔌 Basic Wiring Guide | 基本接线指南

### For LED | LED

```
LED Long Leg (+)  →  220Ω Resistor  →  Arduino Pin 13
LED Short Leg (-)  →  Arduino GND
```

**⚠️ Important**: Always use a resistor with LEDs! (LED总是使用电阻！)

### For Buzzer | 蜂鸣器

```
Buzzer (+)  →  Arduino Pin 9
Buzzer (-)  →  Arduino GND
```

### For Servo Motor | 舵机

```
Servo Brown/Black  →  Arduino GND
Servo Red          →  Arduino 5V
Servo Orange/Yellow →  Arduino Pin 9 (PWM)
```

---

## 💻 Code Templates | 代码模板

### For LED - Blinking Pattern | LED闪烁模式

```cpp
// Flag 2: LED Control
const int LED_PIN = 13;

void setup() {
  pinMode(LED_PIN, OUTPUT);
  Serial.begin(9600);
  Serial.println("=== LED Control Demo ===");
}

void loop() {
  // Pattern 1: Fast blink
  digitalWrite(LED_PIN, HIGH);
  delay(200);
  digitalWrite(LED_PIN, LOW);
  delay(200);
  
  // Pattern 2: Slow blink
  digitalWrite(LED_PIN, HIGH);
  delay(1000);
  digitalWrite(LED_PIN, LOW);
  delay(1000);
}
```

### For LED - PWM Brightness | LED PWM亮度

```cpp
// Flag 2: LED Brightness Control
const int LED_PIN = 9;  // Must be PWM pin!

void setup() {
  pinMode(LED_PIN, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  // Fade in
  for (int brightness = 0; brightness <= 255; brightness++) {
    analogWrite(LED_PIN, brightness);
    delay(10);
  }
  
  // Fade out
  for (int brightness = 255; brightness >= 0; brightness--) {
    analogWrite(LED_PIN, brightness);
    delay(10);
  }
}
```

### For Buzzer - Tone | 蜂鸣器音调

```cpp
// Flag 2: Buzzer Control
const int BUZZER_PIN = 9;

void setup() {
  pinMode(BUZZER_PIN, OUTPUT);
  Serial.begin(9600);
  Serial.println("=== Buzzer Demo ===");
}

void loop() {
  // Play different tones
  tone(BUZZER_PIN, 262);  // C note
  delay(500);
  tone(BUZZER_PIN, 294);  // D note
  delay(500);
  tone(BUZZER_PIN, 330);  // E note
  delay(500);
  noTone(BUZZER_PIN);     // Stop
  delay(1000);
}
```

### For Servo Motor | 舵机

```cpp
// Flag 2: Servo Control
#include <Servo.h>

Servo myServo;
const int SERVO_PIN = 9;

void setup() {
  myServo.attach(SERVO_PIN);
  Serial.begin(9600);
  Serial.println("=== Servo Demo ===");
}

void loop() {
  // Move to 0 degrees
  myServo.write(0);
  Serial.println("Position: 0°");
  delay(1000);
  
  // Move to 90 degrees
  myServo.write(90);
  Serial.println("Position: 90°");
  delay(1000);
  
  // Move to 180 degrees
  myServo.write(180);
  Serial.println("Position: 180°");
  delay(1000);
}
```

---

## 📝 What to Submit | 提交内容

Use the `solution-template.md` file and fill in:

使用 `solution-template.md` 文件并填写：

1. **Actuator Information** (执行器信息)
   - Which actuator you chose (你选择了哪个执行器)
   - What it controls/does (它控制/做什么)

2. **Wiring** (接线)
   - Pin connections (引脚连接)
   - Photo or diagram (照片或图表)

3. **Code** (代码)
   - Your complete Arduino code (你的完整Arduino代码)
   - Explanation of control logic (控制逻辑解释)

4. **Demonstration** (演示)
   - Description of behaviors/patterns (行为/模式描述)
   - Video or photo showing it working (显示工作的视频或照片)

5. **Reflection** (反思)
   - What you learned (学到的东西)
   - Any creative additions (任何创意添加)

---

## ✅ Verification Checklist | 验证清单

Before submitting, make sure:

提交前，确保：

- [ ] Code compiles without errors (代码编译无错误)
- [ ] Actuator performs at least 2 different behaviors (执行器执行至少2种不同行为)
- [ ] Code demonstrates control (not just ON/OFF) (代码演示控制，不只是开/关)
- [ ] Code is commented and clean (代码有注释且整洁)
- [ ] Solution template is complete (解决方案模板完整)

---

## 🌟 Bonus Challenges | 加分挑战

Want to go further? Try these:

想走得更远？试试这些：

- **LED**: Create a traffic light pattern (创建交通灯模式)
- **Buzzer**: Play a simple melody (播放简单旋律)
- **Servo**: Make it sweep smoothly (使其平滑扫描)
- **RGB LED**: Cycle through rainbow colors (循环彩虹颜色)

---

## 🚀 Next Steps | 下一步

Once you capture Flag 2:

捕获Flag 2后：

1. Commit your work to GitHub (将工作提交到GitHub)
2. Celebrate! 🎉 (庆祝！)
3. Move on to **Flag 3: Sensor to Actuator** (进入Flag 3：传感器到执行器)

---

## 🆘 Need Help? | 需要帮助？

- Check `hints.md` for tips (查看hints.md获取提示)
- Review the code examples above (查看上面的代码示例)
- Ask your TA for assistance (请助教帮忙)

---

**Great job on Flag 1! Now let's make things move and light up!** 💡

**Flag 1做得很好！现在让我们让东西移动和发光！** 💡

Good luck! 加油！ 🚀

