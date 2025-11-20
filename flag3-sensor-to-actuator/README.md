# Flag 3: Sensor to Actuator ⭐⭐⭐
# 关卡3：传感器到执行器 ⭐⭐⭐

**Difficulty**: Intermediate | 难度：中级  
**Points**: 10 | 分数：10  
**Estimated Time**: 45-60 minutes | 预计时间：45-60分钟

---

## 🎯 Challenge Mission | 挑战任务

**Your mission**: Create an interactive system where a sensor controls an actuator!

**你的任务**：创建一个交互系统，让传感器控制执行器！

This is where things get exciting - you're building a real interactive system!

这就是事情变得令人兴奋的地方 - 你正在构建一个真实的交互系统！

### Success Criteria | 成功标准

To capture Flag 3, you must:

要捕获Flag 3，你必须：

- ✅ Connect 1 sensor and 1 actuator (连接1个传感器和1个执行器)
- ✅ Sensor input controls actuator output (传感器输入控制执行器输出)
- ✅ Demonstrate clear cause-and-effect (演示清晰的因果关系)
- ✅ Include conditional logic (if/else or map) (包含条件逻辑)
- ✅ Document the interaction (记录交互)

---

## 📚 What You'll Learn | 你将学习

By completing this flag, you'll learn:

完成此关卡后，你将学习：

- Combining input and output (结合输入和输出)
- Conditional logic with if/else (if/else条件逻辑)
- Mapping sensor values to actuator ranges (将传感器值映射到执行器范围)
- Creating interactive behaviors (创建交互行为)
- Real-world applications of Arduino (Arduino的实际应用)

---

## 💡 Project Ideas | 项目想法

### Easy Projects | 简单项目 ⭐⭐⭐

1. **Button-Controlled LED** (按钮控制LED)
   - Button pressed → LED ON
   - Button released → LED OFF

2. **Touch-Activated Buzzer** (触摸激活蜂鸣器)
   - Touch sensor → Buzzer sounds

3. **Motion-Sensing Light** (动作感应灯)
   - PIR sensor detects motion → LED turns ON
   - No motion → LED turns OFF

### Medium Projects | 中等项目 ⭐⭐⭐⭐

4. **Light-Responsive Buzzer** (光响应蜂鸣器)
   - Dark (low light) → Buzzer alarm
   - Bright (high light) → Buzzer off

5. **Distance-Controlled Servo** (距离控制舵机)
   - Close distance → Servo at 0°
   - Far distance → Servo at 180°
   - Distance changes → Servo position changes proportionally

6. **Temperature-Controlled Fan** (温度控制风扇)
   - Hot → Motor/Fan fast
   - Cool → Motor/Fan slow or off

7. **Potentiometer-Controlled LED Brightness** (电位器控制LED亮度)
   - Pot turned low → LED dim
   - Pot turned high → LED bright

### Advanced Projects | 高级项目 ⭐⭐⭐⭐⭐

8. **Smart Parking Assistant** (智能停车助手)
   - Ultrasonic sensor measures distance
   - Close → Buzzer beeps fast, LED red
   - Medium → Buzzer beeps slow, LED yellow
   - Far → No sound, LED green

9. **Interactive Light Show** (交互式灯光秀)
   - Sound sensor detects claps
   - Different clap patterns → Different LED patterns

---

## 🔌 Wiring Guide | 接线指南

### Basic Setup | 基本设置

```
Sensor Input:
  Sensor VCC → 5V
  Sensor GND → GND
  Sensor OUT → Arduino Pin (Digital or Analog)

Actuator Output:
  Actuator Power → 5V (if needed)
  Actuator GND → GND
  Actuator Signal → Arduino Pin (Digital or PWM)
```

**⚠️ Important**: Make sure sensor and actuator share the same GND!

**重要**：确保传感器和执行器共享同一个GND！

---

## 💻 Code Templates | 代码模板

### Template 1: Digital Sensor → Digital Actuator

```cpp
// Flag 3: Button → LED
const int BUTTON_PIN = 2;   // Sensor (input)
const int LED_PIN = 13;     // Actuator (output)

void setup() {
  pinMode(BUTTON_PIN, INPUT_PULLUP);
  pinMode(LED_PIN, OUTPUT);
  Serial.begin(9600);
  Serial.println("=== Button to LED ===");
}

void loop() {
  // Read sensor
  int buttonState = digitalRead(BUTTON_PIN);
  
  // Control actuator based on sensor
  if (buttonState == LOW) {  // Button pressed (INPUT_PULLUP)
    digitalWrite(LED_PIN, HIGH);
    Serial.println("Button pressed - LED ON");
  } else {
    digitalWrite(LED_PIN, LOW);
    Serial.println("Button released - LED OFF");
  }
  
  delay(100);
}
```

### Template 2: Analog Sensor → PWM Actuator (Proportional Control)

```cpp
// Flag 3: Light Sensor → LED Brightness
const int LIGHT_SENSOR_PIN = A0;  // Analog input
const int LED_PIN = 9;            // PWM output

void setup() {
  pinMode(LED_PIN, OUTPUT);
  Serial.begin(9600);
  Serial.println("=== Light to LED Brightness ===");
}

void loop() {
  // Read sensor (0-1023)
  int lightLevel = analogRead(LIGHT_SENSOR_PIN);
  
  // Map sensor value to LED brightness (0-255)
  int brightness = map(lightLevel, 0, 1023, 0, 255);
  
  // Control actuator
  analogWrite(LED_PIN, brightness);
  
  // Debug output
  Serial.print("Light: ");
  Serial.print(lightLevel);
  Serial.print(" → Brightness: ");
  Serial.println(brightness);
  
  delay(100);
}
```

### Template 3: Threshold-Based Control

```cpp
// Flag 3: Distance Sensor → Buzzer Alarm
const int TRIG_PIN = 9;
const int ECHO_PIN = 10;
const int BUZZER_PIN = 8;
const int THRESHOLD_DISTANCE = 20;  // 20cm

void setup() {
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(BUZZER_PIN, OUTPUT);
  Serial.begin(9600);
  Serial.println("=== Distance Alarm ===");
}

void loop() {
  // Measure distance
  long distance = getDistance();
  
  // Control actuator based on threshold
  if (distance < THRESHOLD_DISTANCE) {
    tone(BUZZER_PIN, 1000);  // Alarm ON
    Serial.print("⚠️ WARNING! Distance: ");
    Serial.println(distance);
  } else {
    noTone(BUZZER_PIN);      // Alarm OFF
    Serial.print("✓ Safe. Distance: ");
    Serial.println(distance);
  }
  
  delay(200);
}

long getDistance() {
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);
  
  long duration = pulseIn(ECHO_PIN, HIGH);
  long distance = duration * 0.034 / 2;
  return distance;
}
```

---

## 📝 What to Submit | 提交内容

Use the `solution-template.md` file and fill in:

使用 `solution-template.md` 文件并填写：

1. **System Overview** (系统概述)
   - What sensor-actuator pair you chose (你选择了什么传感器-执行器对)
   - What problem it solves or behavior it creates (它解决什么问题或创建什么行为)

2. **Wiring** (接线)
   - Complete pin connections (完整引脚连接)
   - Wiring photo or diagram (接线照片或图表)

3. **Code** (代码)
   - Complete working code (完整的工作代码)
   - Logic explanation (逻辑解释)

4. **Demonstration** (演示)
   - Video or photos showing the interaction (显示交互的视频或照片)
   - Description of behavior (行为描述)

5. **Reflection** (反思)
   - How sensor and actuator interact (传感器和执行器如何交互)
   - Real-world applications (实际应用)

---

## 🎯 Key Concepts | 关键概念

### Conditional Logic | 条件逻辑

```cpp
if (sensorValue > threshold) {
  // Do something
} else {
  // Do something else
}
```

### Mapping Values | 映射值

```cpp
// Map sensor range (0-1023) to actuator range (0-255)
int output = map(input, 0, 1023, 0, 255);
```

### Constrain Values | 约束值

```cpp
// Keep value within range
int safeValue = constrain(value, 0, 255);
```

---

## ✅ Verification Checklist | 验证清单

Before submitting, make sure:

提交前，确保：

- [ ] Code compiles without errors (代码编译无错误)
- [ ] Sensor reading is visible in Serial Monitor (串口监视器中可见传感器读数)
- [ ] Actuator responds to sensor changes (执行器响应传感器变化)
- [ ] Cause-and-effect relationship is clear (因果关系清晰)
- [ ] Code includes conditional logic or mapping (代码包含条件逻辑或映射)
- [ ] Demo video/photos show working interaction (演示视频/照片显示工作交互)

---

## 🌟 Bonus Challenges | 加分挑战

Want extra credit? Try these:

想要额外学分？试试这些：

1. **Add multiple thresholds** (添加多个阈值)
   - Different sensor ranges trigger different actuator behaviors
   - 不同传感器范围触发不同执行器行为

2. **Add feedback** (添加反馈)
   - Use Serial Monitor to display clear status messages
   - 使用串口监视器显示清晰的状态消息

3. **Smooth transitions** (平滑过渡)
   - Instead of abrupt on/off, create gradual changes
   - 不是突然开关，而是创建渐变

4. **Add hysteresis** (添加滞后)
   - Prevent rapid switching at threshold boundaries
   - 防止在阈值边界快速切换

---

## 🚀 Next Steps | 下一步

Once you capture Flag 3:

捕获Flag 3后：

1. Test your system thoroughly (彻底测试系统)
2. Document the behavior (记录行为)
3. Commit your work to GitHub (将工作提交到GitHub)
4. Move on to **Flag 4: Complex Logic** (进入Flag 4：复杂逻辑)

---

## 🆘 Need Help? | 需要帮助？

- Check `hints.md` for troubleshooting (查看hints.md进行故障排除)
- Review the code templates above (查看上面的代码模板)
- Test sensor and actuator separately first (先分别测试传感器和执行器)
- Ask your TA for guidance (向助教寻求指导)

---

**This is where Arduino becomes truly interactive! You're building real systems!** 🎉

**这就是Arduino真正变得互动的地方！你正在构建真实的系统！** 🎉

Good luck! 加油！ 🚀

