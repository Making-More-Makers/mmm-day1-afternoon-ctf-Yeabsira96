# Flag 1: Sensor Reading ⭐
# 关卡1：传感器读取 ⭐

**Difficulty**: Beginner | 难度：初级  
**Points**: 5 | 分数：5  
**Estimated Time**: 30-45 minutes | 预计时间：30-45分钟

---

## 🎯 Challenge Mission | 挑战任务

**Your mission**: Successfully read data from a sensor and display it in the Serial Monitor.

**你的任务**：成功从传感器读取数据并在串口监视器中显示。

### Success Criteria | 成功标准

To capture Flag 1, you must:

要捕获Flag 1，你必须：

- ✅ Choose one sensor from your kit (从套件中选择一个传感器)
- ✅ Connect it properly to your Arduino (正确连接到Arduino)
- ✅ Write code to read sensor data (编写代码读取传感器数据)
- ✅ Display values in Serial Monitor (在串口监视器中显示数值)
- ✅ Document your work (记录你的工作)

---

## 📚 What You'll Learn | 你将学习

By completing this flag, you'll learn:

完成此关卡后，你将学习：

- How to connect sensors to Arduino (如何将传感器连接到Arduino)
- Reading digital and analog inputs (读取数字和模拟输入)
- Using the Serial Monitor for debugging (使用串口监视器进行调试)
- Basic Arduino programming structure (基础Arduino编程结构)

---

## 🛠️ Available Sensors | 可用传感器

Choose **ONE** of these sensors to complete the challenge:

选择**其中一个**传感器来完成挑战：

### Digital Sensors | 数字传感器

1. **Button / Switch** (按钮/开关)
   - Difficulty: ⭐
   - Reads: Pressed (HIGH) or Not Pressed (LOW)

2. **PIR Motion Sensor** (人体红外传感器)
   - Difficulty: ⭐
   - Reads: Motion Detected (HIGH) or No Motion (LOW)

3. **Touch Sensor** (触摸传感器)
   - Difficulty: ⭐
   - Reads: Touched (HIGH) or Not Touched (LOW)

### Analog Sensors | 模拟传感器

4. **Photoresistor** (光敏电阻)
   - Difficulty: ⭐⭐
   - Reads: Light level (0-1023)

5. **Potentiometer** (电位器)
   - Difficulty: ⭐
   - Reads: Rotation position (0-1023)

6. **Temperature Sensor (LM35 / DHT11)** (温度传感器)
   - Difficulty: ⭐⭐
   - Reads: Temperature value (varies by sensor)

7. **Ultrasonic Distance Sensor (HC-SR04)** (超声波距离传感器)
   - Difficulty: ⭐⭐⭐
   - Reads: Distance in cm

---

## 🔌 Basic Wiring Guide | 基本接线指南

### For Digital Sensors | 数字传感器

```
Sensor VCC  →  Arduino 5V
Sensor GND  →  Arduino GND
Sensor OUT  →  Arduino Digital Pin (e.g., Pin 2)
```

### For Analog Sensors | 模拟传感器

```
Sensor VCC  →  Arduino 5V
Sensor GND  →  Arduino GND
Sensor OUT  →  Arduino Analog Pin (e.g., A0)
```

**⚠️ Important | 重要**: Always connect GND first, then VCC, then signal pins!

总是先连接GND，然后VCC，最后信号引脚！

---

## 💻 Code Template | 代码模板

### For Digital Sensor | 数字传感器

```cpp
// Flag 1: Digital Sensor Reading
// Replace SENSOR_NAME with your actual sensor name

const int SENSOR_PIN = 2;  // Digital pin

void setup() {
  // Initialize serial communication
  Serial.begin(9600);
  
  // Set pin as input
  pinMode(SENSOR_PIN, INPUT);
  
  Serial.println("=== Digital Sensor Reading ===");
  Serial.println("Sensor: [YOUR SENSOR NAME]");
  Serial.println("==============================");
}

void loop() {
  // Read digital value (HIGH or LOW)
  int sensorValue = digitalRead(SENSOR_PIN);
  
  // Print to Serial Monitor
  Serial.print("Sensor Status: ");
  if (sensorValue == HIGH) {
    Serial.println("DETECTED / ON");
  } else {
    Serial.println("NOT DETECTED / OFF");
  }
  
  delay(500);  // Wait 500ms between readings
}
```

### For Analog Sensor | 模拟传感器

```cpp
// Flag 1: Analog Sensor Reading
// Replace SENSOR_NAME with your actual sensor name

const int SENSOR_PIN = A0;  // Analog pin

void setup() {
  // Initialize serial communication
  Serial.begin(9600);
  
  Serial.println("=== Analog Sensor Reading ===");
  Serial.println("Sensor: [YOUR SENSOR NAME]");
  Serial.println("=============================");
}

void loop() {
  // Read analog value (0-1023)
  int sensorValue = analogRead(SENSOR_PIN);
  
  // Print to Serial Monitor
  Serial.print("Sensor Value: ");
  Serial.println(sensorValue);
  
  delay(500);  // Wait 500ms between readings
}
```

---

## 📝 What to Submit | 提交内容

Use the `solution-template.md` file and fill in:

使用 `solution-template.md` 文件并填写：

1. **Sensor Information** (传感器信息)
   - Which sensor you chose (你选择了哪个传感器)
   - What it measures (它测量什么)

2. **Wiring** (接线)
   - Pin connections (引脚连接)
   - Optional: Photo of your wiring (可选：接线照片)

3. **Code** (代码)
   - Your complete Arduino code (你的完整Arduino代码)
   - Comments explaining key parts (注释解释关键部分)

4. **Test Results** (测试结果)
   - Screenshot of Serial Monitor output (串口监视器输出截图)
   - Description of what you observed (描述你观察到的内容)

5. **Reflection** (反思)
   - What worked well (什么做得好)
   - Any challenges you faced (遇到的任何挑战)
   - What you learned (学到的东西)

---

## ✅ Verification Checklist | 验证清单

Before submitting, make sure:

提交前，确保：

- [ ] Code compiles without errors (代码编译无错误)
- [ ] Serial Monitor shows changing sensor values (串口监视器显示变化的传感器值)
- [ ] Values make sense for your sensor (值对你的传感器有意义)
- [ ] Code is commented and clean (代码有注释且整洁)
- [ ] Solution template is complete (解决方案模板完整)

---

## 🚀 Next Steps | 下一步

Once you capture Flag 1:

捕获Flag 1后：

1. Commit your work to GitHub (将工作提交到GitHub)
2. Celebrate! 🎉 (庆祝！)
3. Move on to **Flag 2: Actuator Control** (进入Flag 2：执行器控制)

---

## 🆘 Need Help? | 需要帮助？

- Check `hints.md` for tips (查看hints.md获取提示)
- Review the `getting-started.md` guide (查看getting-started.md指南)
- Ask your TA for assistance (请助教帮忙)
- Work with a classmate (与同学合作)

---

**Remember**: The goal is to learn, not to be perfect! Try, fail, learn, and try again.

**记住**：目标是学习，而不是完美！尝试、失败、学习、再尝试。

Good luck! 加油！ 🚀

