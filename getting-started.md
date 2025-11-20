# Getting Started with Hardware CTF
# 硬件CTF入门指南

**Welcome to Day 1 Afternoon!** | 欢迎来到第1天下午！

---

## 📋 What is Hardware CTF? | 什么是硬件CTF？

**CTF** stands for "Capture The Flag" - a challenge-based learning approach where you progress through levels by completing tasks.

**CTF** 代表"Capture The Flag"（夺旗） - 一种基于挑战的学习方法，你通过完成任务来逐级进阶。

In **Hardware CTF**, each "flag" represents a hardware skill milestone:

在**硬件CTF**中，每个"旗帜"代表一个硬件技能里程碑：

- **Flag 1**: Read sensor data (读取传感器数据)
- **Flag 2**: Control actuators (控制执行器)
- **Flag 3**: Connect sensors to actuators (连接传感器和执行器)
- **Flag 4**: Build complex logic systems (构建复杂逻辑系统)
- **Flag 5**: Create your own project (创建你自己的项目)

---

## 🎯 Learning Objectives | 学习目标

By completing this CTF, you will:

完成此CTF后，你将：

- ✅ Understand how Arduino works (理解Arduino工作原理)
- ✅ Read data from various sensors (从各种传感器读取数据)
- ✅ Control LEDs, motors, buzzers, and more (控制LED、电机、蜂鸣器等)
- ✅ Build interactive systems (构建交互系统)
- ✅ Write clean, documented code (编写干净、有文档的代码)
- ✅ Debug hardware and software issues (调试硬件和软件问题)

---

## 🛠️ Prerequisites | 前置要求

### Hardware | 硬件

- Arduino Uno / ESP32 / Other compatible board (Arduino Uno / ESP32 / 其他兼容板)
- Breadboard and jumper wires (面包板和跳线)
- Sensors and actuators from your kit (套件中的传感器和执行器)
- USB cable (USB线)

### Software | 软件

- Arduino IDE installed (已安装Arduino IDE)
- USB drivers (CH340 or similar) (USB驱动程序)
- Code editor (VS Code, Cursor, etc.) (代码编辑器)

### Skills | 技能

- Basic understanding of programming (基础编程理解)
- Willingness to experiment and fail! (愿意实验和失败！)

---

## 🚦 How to Progress | 如何进阶

### Step-by-Step Approach | 逐步方法

1. **Start with Flag 1** (从Flag 1开始)
   - Don't skip ahead! Each flag builds on the previous one.
   - 不要跳过！每个旗帜都建立在前一个基础上。

2. **Read the challenge** (阅读挑战)
   - Understand what's required (理解要求)
   - Check the hints if you're stuck (如果卡住查看提示)

3. **Build and test** (构建和测试)
   - Connect your hardware (连接硬件)
   - Write your code (编写代码)
   - Upload and test (上传和测试)

4. **Document your work** (记录你的工作)
   - Use the provided templates (使用提供的模板)
   - Take photos of your wiring (给接线拍照)
   - Explain what you did (解释你做了什么)

5. **Submit your flag** (提交你的旗帜)
   - Complete the solution template (完成解决方案模板)
   - Commit to GitHub (提交到GitHub)
   - Move to the next flag! (进入下一个旗帜！)

---

## 📚 Arduino Basics Refresher | Arduino基础回顾

### Arduino Pins | Arduino引脚

```
Digital Pins (数字引脚): 0-13
- Can be INPUT or OUTPUT (可以是输入或输出)
- Read/write HIGH (5V) or LOW (0V) (读/写高电平或低电平)
- Pins 3, 5, 6, 9, 10, 11 support PWM (支持PWM)

Analog Input Pins (模拟输入引脚): A0-A5
- Read values from 0-1023 (读取0-1023的值)
- For sensors like photoresistors, potentiometers (用于光敏电阻、电位器等传感器)

Power Pins (电源引脚):
- 5V: 5 volt power (5伏电源)
- 3.3V: 3.3 volt power (3.3伏电源)
- GND: Ground (接地)
```

### Basic Code Structure | 基本代码结构

```cpp
// 1. Define constants and variables
const int LED_PIN = 13;

// 2. Setup function - runs once at start
void setup() {
  pinMode(LED_PIN, OUTPUT);
  Serial.begin(9600);
}

// 3. Loop function - runs repeatedly
void loop() {
  digitalWrite(LED_PIN, HIGH);
  delay(1000);
  digitalWrite(LED_PIN, LOW);
  delay(1000);
}
```

### Essential Functions | 基本函数

```cpp
// Pin configuration (引脚配置)
pinMode(pin, MODE);  // MODE: INPUT, OUTPUT, INPUT_PULLUP

// Digital (数字)
digitalWrite(pin, VALUE);  // VALUE: HIGH or LOW
int value = digitalRead(pin);

// Analog (模拟)
analogWrite(pin, value);  // value: 0-255 (PWM)
int value = analogRead(pin);  // returns: 0-1023

// Serial Monitor (串口监视器)
Serial.begin(9600);
Serial.print("text");
Serial.println("text with newline");

// Timing (计时)
delay(milliseconds);  // pause for milliseconds
unsigned long time = millis();  // time since program started
```

---

## 🔧 Common Hardware Components | 常见硬件组件

### Sensors | 传感器

| Type | Purpose | Pin Type | 类型 | 用途 |
|------|---------|----------|------|------|
| Button | Detect press | Digital Input | 按钮 | 检测按压 |
| Photoresistor | Measure light | Analog Input | 光敏电阻 | 测量光线 |
| Temperature | Measure temp | Analog Input | 温度 | 测量温度 |
| Ultrasonic | Measure distance | Digital I/O | 超声波 | 测量距离 |
| Motion (PIR) | Detect movement | Digital Input | 人体红外 | 检测运动 |

### Actuators | 执行器

| Type | Purpose | Pin Type | 类型 | 用途 |
|------|---------|----------|------|------|
| LED | Light indicator | Digital Output | LED | 指示灯 |
| Buzzer | Sound alert | Digital Output | 蜂鸣器 | 声音警报 |
| Servo Motor | Precise rotation | PWM Output | 舵机 | 精确旋转 |
| DC Motor | Continuous rotation | PWM Output | 直流电机 | 连续旋转 |
| Relay | Switch high power | Digital Output | 继电器 | 开关大功率 |

---

## 🆘 Getting Help | 获取帮助

### When You're Stuck | 当你卡住时

1. **Check the hints** (查看提示)
   - Each flag has a `hints.md` file (每个旗帜都有hints.md文件)

2. **Review Arduino basics** (复习Arduino基础)
   - Look at the code examples in this guide (查看本指南中的代码示例)

3. **Search online** (在线搜索)
   - Arduino documentation: arduino.cc/reference (Arduino文档)
   - Example projects: Hackster.io, Instructables (示例项目)

4. **Ask for help** (寻求帮助)
   - Raise your hand for TA support (举手找助教)
   - Post in the course forum (在课程论坛发帖)
   - Work with classmates (与同学合作)

### Debugging Tips | 调试技巧

**Hardware not working? | 硬件不工作？**

1. Check your wiring (检查接线)
   - Are wires connected firmly? (线连接牢固吗？)
   - Is power connected? (电源连接了吗？)
   - Are polarities correct? (极性正确吗？)

2. Check your board (检查板子)
   - Is the Arduino powered on? (Arduino开机了吗？)
   - Does the power LED light up? (电源LED亮了吗？)

**Code not working? | 代码不工作？**

1. Check Serial Monitor (检查串口监视器)
   - Tools → Serial Monitor (工具 → 串口监视器)
   - Set baud rate to 9600 (设置波特率为9600)
   - Look for error messages (查找错误消息)

2. Add debug prints (添加调试打印)
   ```cpp
   Serial.println("Reached this point");
   Serial.print("Sensor value: ");
   Serial.println(sensorValue);
   ```

3. Simplify your code (简化代码)
   - Start with basic examples (从基本示例开始)
   - Add complexity gradually (逐渐增加复杂性)

---

## 🎯 Success Criteria | 成功标准

### To Capture a Flag | 捕获一个旗帜

You must:

你必须：

- ✅ Complete the required tasks (完成必需任务)
- ✅ Fill out the solution template (填写解决方案模板)
- ✅ Include working code (包含工作代码)
- ✅ Add documentation (添加文档)
- ✅ Commit and push to GitHub (提交并推送到GitHub)

---

## 📝 Documentation Tips | 文档技巧

### Write Good Explanations | 写好的解释

**Bad example | 坏例子**:
```
I connected the LED to pin 13 and it worked.
```

**Good example | 好例子**:
```
I connected the LED's positive leg (longer leg) to Arduino pin 13 
through a 220Ω resistor, and the negative leg to GND. When pin 13 
is set HIGH, current flows through the LED, making it light up.
```

### Take Clear Photos | 拍清晰的照片

- Good lighting (良好的光线)
- Show the full circuit (显示完整电路)
- Wires should be visible (线应该可见)
- Focus on connections (聚焦在连接上)

---

## 🏆 Scoring | 评分

Each flag is worth points:

每个旗帜值一定分数：

- **Flag 1**: 5 points (5分) - Basic sensor reading
- **Flag 2**: 5 points (5分) - Basic actuator control
- **Flag 3**: 10 points (10分) - Sensor-to-actuator logic
- **Flag 4**: 10 points (10分) - Complex multi-sensor system
- **Flag 5**: 10 points (10分) - Creative final project

**Total**: 40 points | 总分：40分

---

## 🎉 Ready to Start? | 准备开始？

1. **Make sure your Arduino IDE is working** (确保Arduino IDE工作)
   - Tools → Board → Select your board (选择板子)
   - Tools → Port → Select COM port (选择COM端口)

2. **Test with Blink** (用Blink测试)
   - File → Examples → 01.Basics → Blink
   - Upload and check if onboard LED blinks (上传并检查板载LED是否闪烁)

3. **Go to Flag 1!** (前往Flag 1！)
   - Navigate to `/flag1-sensor-reading/` folder
   - Read the `README.md`
   - Start the challenge!

---

**Good luck! Remember: Every maker was once a beginner. The only way to learn is to try!**

**祝好运！记住：每个创客都曾是初学者。学习的唯一方法就是尝试！**

---

*If you have questions, raise your hand! We're here to help you succeed.* 🚀

*如果有问题，举手！我们在这里帮助你成功。* 🚀

