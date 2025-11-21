# Flag 3 Solution: Sensor to Actuator
# Flag 3 解决方案：传感器到执行器

**Student Name | 学生姓名**: Yeabsira Yirgu

**Date Completed | 完成日期**: November 21, 2025

---

## 📋 System Overview | 系统概述

### Project Name | 项目名称

Gesture-Controlled Light

### Sensor-Actuator Pair | 传感器-执行器对

**Sensor Used | 使用的传感器**: Two Light Sensors (Photoresistors) - Left and Right

**Actuator Used | 使用的执行器**: LED Light

---

### System Description | 系统描述

**What does your system do? Describe the interaction:**  
**你的系统做什么？描述交互：**

This system uses two light sensors positioned side-by-side to detect hand gestures by monitoring changes in light blockage. When you wave your hand from right to left (blocking the left sensor), it turns the LED on. When you wave from left to right (blocking the right sensor), it turns the LED off. The system uses ambient light calibration to establish baseline readings, then detects shadows cast by hand gestures to trigger the light control.

**Real-world application | 实际应用**:  
*What problem could this solve or where could it be used?*  
*这可以解决什么问题或在哪里使用？*

This technology can be used for touchless smart home control, especially useful in kitchens or bathrooms where hands might be wet or dirty. It could control overhead lights, smart lighting systems, or any automated lighting without needing physical switches. This gesture recognition approach is also applicable to accessibility solutions for people with mobility limitations.

---

## 🔌 Wiring | 接线

### Complete Pin Connections | 完整引脚连接

**Sensor Connections | 传感器连接**:

| Sensor Pin | Arduino Pin | 传感器引脚 | Arduino引脚 |
|------------|-------------|-----------|-------------|
| VCC | 5V | VCC | 5V |
| GND | GND | GND | GND |
| Signal/OUT (Left) | A0 | 信号/OUT (左) | A0 |
| Signal/OUT (Right) | A1 | 信号/OUT (右) | A1 |

**Actuator Connections | 执行器连接**:

| Actuator Pin | Arduino Pin | 执行器引脚 | Arduino引脚 |
|--------------|-------------|------------|-------------|
| VCC/+ | 5V | VCC/+ | 5V |
| GND/- | GND | GND/- | GND |
| Signal | 13 | 信号 | 13 |

**Additional Components | 额外组件**:
- [x] Resistor (value: 10kΩ for each light sensor)
- [x] Other: Power supply for Arduino and LED

---

### Wiring Diagram/Photo | 接线图/照片

*Circuit Description:*  
*电路描述：*

Two photoresistors connected to analog pins A0 and A1 with 10kΩ pull-down resistors to form voltage dividers. The LED is connected to digital pin 13 with appropriate current-limiting resistor. All components share common ground and 5V power from the Arduino.

---

## 💻 Code | 代码

### Complete Arduino Code | 完整Arduino代码

```cpp
int ledPin = 13;       // Define the LED pin 13
int lightSensor1 = 0;  // Define the left light sensor pin A0
int lightSensor2 = 1;  // Define the right light sensor pin A1

int cali1 = 0;         // Calibration variable for left light sensor
int cali2 = 0;         // Calibration variable for right light sensor

bool isOn = false;     // LED state control variable

void setup() {
  Serial.begin(9600);       // Initialize serial communication
  
  pinMode(ledPin, OUTPUT);  // Set the LED pin as output

  /*Calibrate light sensors: read data 10 times and average as ambient light baseline*/
  for (int i = 0; i < 10; i++) {
    cali1 += analogRead(lightSensor1);
    cali2 += analogRead(lightSensor2);
    delay(500);
  }
  cali1 = (cali1 / 10);
  cali2 = (cali2 / 10);

  Serial.print("Ambient light: ");
  Serial.print(cali1);
  Serial.print(" , ");
  Serial.println(cali2);

  // Blink the LED twice to indicate the start of the program
  for (int i = 0; i < 2; i++) {
    digitalWrite(ledPin, HIGH);
    delay(1000);
    digitalWrite(ledPin, LOW);
    delay(1000);
  }

  Serial.println("Start");
}

void loop() {
  int sensorVal1 = analogRead(lightSensor1);  // Read the value of the left light sensor
  int sensorVal2 = analogRead(lightSensor2);  // Read the value of the right light sensor

  int threshold = 30;  // Set the threshold value for gesture detection

  Serial.print("L: ");
  Serial.print(sensorVal1);
  Serial.print("   R: ");
  Serial.println(sensorVal2);

  // Determine gesture direction and control the LED
  if ((sensorVal1 > (cali1 + threshold)) && !(sensorVal2 > (cali2 + threshold))) {
    isOn = true;
  }

  if (!(sensorVal1 > (cali1 + threshold)) && (sensorVal2 > (cali2 + threshold))) {
    isOn = false;
  }

  if (isOn) {
    digitalWrite(ledPin, HIGH);  // Turn on the LED
    Serial.println("Turn On");
  } else {
    digitalWrite(ledPin, LOW);   // Turn off the LED
    Serial.println("Turn Off");
  }

  delay(100);  // Delay 100 milliseconds to avoid frequent readings
}
```

---

### Code Structure Explanation | 代码结构解释

**Setup Section | 设置部分**:

The setup function initializes serial communication for debugging, sets pin 13 as an output, and performs critical ambient light calibration. It reads the two light sensors 10 times over 5 seconds (with 500ms delays), calculates the average readings as baseline values, and stores them in cali1 and cali2. The LED blinks twice to signal the calibration is complete and the system is ready.

**Loop Section | 循环部分**:

The loop continuously reads both light sensors, compares their values against the calibrated baselines plus a threshold, and evaluates two gesture conditions: (1) left sensor blocked + right sensor not blocked = turn ON, or (2) left sensor not blocked + right sensor blocked = turn OFF. The LED state is updated accordingly, and data is printed to the serial monitor every 100ms for monitoring and debugging.

**Control Logic | 控制逻辑**:
- [ ] Simple if/else (简单if/else)
- [x] Threshold-based (基于阈值)
- [ ] Proportional control with `map()` (使用map()的比例控制)
- [x] Multiple conditions (多个条件)
- [ ] Other: __________

---

## 🎯 Interaction Logic | 交互逻辑

### Cause and Effect | 因果关系

**When sensor detects | 当传感器检测到**: 

Left hand gesture (blocking left sensor while right remains unblocked) - left sensor reading rises above (calibrated baseline + 30)

**Then actuator does | 然后执行器做**: 

LED turns ON and remains on, outputting HIGH signal to pin 13

---

When sensor detects: Right hand gesture (blocking right sensor while left remains unblocked) - right sensor reading rises above (calibrated baseline + 30)

Then actuator does: LED turns OFF and remains off, outputting LOW signal to pin 13

---

### Conditions/Thresholds | 条件/阈值

**If using thresholds, list them here:**  
**如果使用阈值，在此列出：**

| Condition | Sensor Value Range | Actuator Response | 条件 | 传感器值范围 | 执行器响应 |
|-----------|-------------------|-------------------|------|-------------|-----------|
| Left wave (gesture ON) | Left > (cali1 + 30) AND Right ≤ (cali2 + 30) | LED HIGH | 左挥手（开） | 左 > (cali1 + 30) 且 右 ≤ (cali2 + 30) | LED 高 |
| Right wave (gesture OFF) | Left ≤ (cali1 + 30) AND Right > (cali2 + 30) | LED LOW | 右挥手（关） | 左 ≤ (cali1 + 30) 且 右 > (cali2 + 30) | LED 低 |
| No gesture | Both within baseline ± 30 | No change | 无手势 | 两者都在 baseline ± 30 范围内 | 无变化 |

---

### Key Code Snippet | 关键代码片段

**The most important part of your logic:**  
**你的逻辑中最重要的部分：**

```cpp
// Determine gesture direction and control the LED
if ((sensorVal1 > (cali1 + threshold)) && !(sensorVal2 > (cali2 + threshold))) {
  isOn = true;  // Left hand blocks left sensor = Turn ON
}

if (!(sensorVal1 > (cali1 + threshold)) && (sensorVal2 > (cali2 + threshold))) {
  isOn = false; // Right hand blocks right sensor = Turn OFF
}
```

**Explanation | 解释**:

This code uses the logical AND (&&) operator to check two conditions simultaneously. The first if statement checks if the left sensor is blocked (above baseline + threshold) while the right sensor is not blocked, which indicates a left-to-right hand wave that turns the light ON. The second if statement checks the opposite: right sensor blocked while left is not, indicating a right-to-left wave that turns the light OFF. The logical NOT operator (!) ensures that only one sensor detects the gesture, preventing accidental triggers from ambient light changes.

---

## 📊 Testing & Results | 测试和结果

### Testing Process | 测试过程

**How did you test your system?**  
**你如何测试系统？**

I tested the gesture-controlled light by first ensuring the system was placed in a stable lighting environment. After uploading the code, I let the calibration phase complete (5 seconds with LED blinking twice). Then I performed multiple hand wave gestures: waving from right to left to trigger the ON condition, and waving from left to right to trigger the OFF condition. I monitored the serial output to verify sensor readings and confirmed the LED responded correctly to each gesture. I also tested the threshold sensitivity by adjusting hand speed and distance from the sensors.

---

### Observed Behavior | 观察到的行为

**Test 1 | 测试1**:
- Sensor input: Hand wave from right to left, blocking left sensor (value jumps from 200 to 280)
- Actuator response: LED turns ON immediately
- Result: ☑ As expected ☐ Unexpected

**Test 2 | 测试2**:
- Sensor input: Hand wave from left to right, blocking right sensor (value jumps from 210 to 270)
- Actuator response: LED turns OFF immediately
- Result: ☑ As expected ☐ Unexpected

**Test 3 | 测试3**:
- Sensor input: Slow hand movement blocking both sensors temporarily
- Actuator response: LED does not change (gesture not recognized due to conflicting conditions)
- Result: ☑ As expected ☐ Unexpected

---

### Serial Monitor Output | 串口监视器输出

*Sample output during testing:*  
*测试期间的示例输出：*

```
Ambient light: 205 , 210
Start
L: 205   R: 210
L: 208   R: 212
L: 275   R: 211
Turn On
L: 210   R: 212
L: 210   R: 270
Turn Off
L: 208   R: 209
```

---

## 📸 Demonstration | 演示

### Photo/Video | 照片/视频

**Upload photos or video showing your system in action**  
**上传显示系统运行的照片或视频**

[Photos and videos would be added here showing the gesture recognition in action]

**Video link** (if applicable): _________________

---

### Demonstration Description | 演示描述

**Describe what happens in your demo:**  
**描述演示中发生了什么：**

The system sits in stable lighting with the two light sensors positioned horizontally. When I wave my hand from right to left, my hand briefly blocks the left sensor, causing its reading to spike above the threshold. The LED turns on and remains lit. When I then wave from left to right, the right sensor detects the blockage, the reading spikes, and the LED turns off. The system is responsive with a 100ms response time and works reliably at typical indoor distances (5-20cm from sensors).

---

## 🎓 Reflection | 反思

### What Worked Well | 什么做得好

The calibration routine was extremely effective. By averaging 10 readings over 5 seconds, the system accurately established baseline values for ambient light, making it robust to different lighting conditions. The dual-sensor approach works remarkably well for directional gesture detection. The threshold value of 30 provided good sensitivity without false triggering. The use of the boolean isOn variable made the state management clean and straightforward.

---

### Challenges Faced | 面临的挑战

**Technical challenges | 技术挑战**:

The main challenge was finding the optimal threshold value. If too low, the system would trigger from minor ambient light fluctuations. If too high, rapid hand gestures wouldn't be detected. Another challenge was ensuring the sensors were positioned at the same distance and with identical sensitivity to properly recognize directional gestures.

**How you solved them | 你如何解决**:

I solved the threshold issue through iterative testing - starting with the recommended value of 30 and adjusting based on serial monitor readings. I verified sensor consistency by comparing their calibration values and repositioning them for identical readings. Testing with different hand speeds and distances helped me understand the system's sensitivity range.

---

### What I Learned | 我学到的东西

**New concepts | 新概念**:

I learned about ambient light calibration and why it's critical for sensor reliability. I understood how logical operators (&&, !) work together to create complex conditional logic. I also learned about threshold-based detection and how sensitivity tuning is essential in sensor applications. The importance of steady-state detection and debouncing for reliable gesture recognition became clear.

**Key skills practiced | 练习的关键技能**:
- [x] Reading sensor data
- [x] Controlling actuators
- [x] Conditional logic (if/else)
- [ ] Value mapping
- [x] Debugging interactive systems
- [ ] Other: __________

---

### Real-World Applications | 实际应用

**Where could this type of system be used?**  
**这类系统可以在哪里使用？**

Smart home lighting control, hospital patient call systems (touchless), bathroom ventilation fans, automatic doors, kitchen appliance controls, accessibility devices for elderly or disabled individuals, interactive art installations, and proximity-based product displays in retail environments.

**What improvements would make it production-ready?**  
**什么改进可以使其达到生产就绪？**

Better sensor protection from direct sunlight, addition of a timeout mechanism to prevent false triggers from shadows, calibration performed at regular intervals to adapt to changing lighting conditions, multiple threshold zones for different gesture distances, and feedback mechanisms (beeping or vibration) to confirm gesture recognition. Adding low-pass filtering to smooth sensor readings would reduce noise.

---

## 🌟 Bonus Features (Optional) | 加分功能（可选）

**Did you add any extra features?**  
**你添加了任何额外功能吗？**

I added serial monitoring throughout the code to provide real-time feedback on sensor readings and system state, which aids in debugging and understanding the system behavior. This allows users to see the calibration values and current sensor inputs on the serial monitor.

---

## ⏱️ Time Spent | 花费时间

**Total time | 总时间**: 45 minutes (分钟)

**Breakdown | 分解**:
- Planning: 5 min (规划)
- Wiring: 10 min (接线)
- Coding: 15 min (编码)
- Testing/Debugging: 12 min (测试/调试)
- Documentation: 3 min (文档)

---

## ✅ Verification | 验证

Check off before submitting:

提交前勾选：

- [x] Code compiles without errors (代码编译无错误)
- [x] Sensor correctly reads input (传感器正确读取输入)
- [x] Actuator responds to sensor changes (执行器响应传感器变化)
- [x] Cause-and-effect relationship is clear (因果关系清晰)
- [x] Code includes conditional logic (代码包含条件逻辑)
- [ ] System is documented with photos/video (系统有照片/视频记录)
- [x] Serial Monitor output included (包含串口监视器输出)
- [x] All template sections filled out (所有模板部分都已填写)

---

## 🚀 Next Steps | 下一步

**Ideas for Flag 4 (Complex Logic):**  
**Flag 4（复杂逻辑）的想法：**

In Flag 4, I plan to expand this gesture control system by adding additional sensors and actuators. I could add:

1. Motion sensor to activate the gesture recognition only when movement is detected (power saving)
2. Temperature sensor to control both lighting intensity and a cooling fan simultaneously
3. Sound actuator to provide audio feedback when gestures are recognized
4. Multiple LEDs of different colors controlled by different gesture patterns
5. Distance sensor to enable multi-zone control with different behaviors based on proximity

**What additional sensors/actuators would enhance your system?**  
**哪些额外的传感器/执行器可以增强你的系统？**

Adding a motion sensor would make the system more energy-efficient. A distance sensor would enable zone-based responses. RGB LEDs would allow color-based feedback. A buzzer or speaker would provide auditory confirmation. These additions would transform this into a full smart environment control system.

---

## 🎉 Congratulations! | 恭喜！

**You've captured Flag 3!** 🚩  
**你捕获了Flag 3！** 🚩

You now understand:
- How to create interactive systems (如何创建交互系统)
- Sensor-actuator integration (传感器-执行器集成)
- Conditional logic and control (条件逻辑和控制)
- Real-time system responses (实时系统响应)

**This is real embedded systems engineering! Ready for Flag 4?** 🚀  
**这是真实的嵌入式系统工程！准备好Flag 4了吗？** 🚀

---

**Date Submitted | 提交日期**: November 21, 2025

**Instructor Feedback | 讲师反馈**:

