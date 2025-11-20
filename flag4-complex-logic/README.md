# Flag 4: Complex Logic ⭐⭐⭐⭐
# 关卡4：复杂逻辑 ⭐⭐⭐⭐

**Difficulty**: Advanced | 难度：高级  
**Points**: 10 | 分数：10  
**Estimated Time**: 60-90 minutes | 预计时间：60-90分钟

---

## 🎯 Challenge Mission | 挑战任务

**Your mission**: Build a complex system with multiple sensors and actuators working together!

**你的任务**：构建一个多个传感器和执行器协同工作的复杂系统！

This is where you combine everything you've learned into a sophisticated interactive system.

这是你将所学的一切结合成复杂交互系统的地方。

### Success Criteria | 成功标准

To capture Flag 4, you must:

要捕获Flag 4，你必须：

- ✅ Use at least **3 sensors** or **3 actuators** (or 2+2) (使用至少3个传感器或3个执行器或2+2)
- ✅ Implement complex logic (state machines, multiple conditions, timing) (实现复杂逻辑)
- ✅ Components interact in meaningful ways (组件以有意义的方式交互)
- ✅ System has a clear purpose or solves a problem (系统有明确目的或解决问题)
- ✅ Code is well-organized and documented (代码组织良好且有文档)

---

## 📚 What You'll Learn | 你将学习

By completing this flag, you'll learn:

完成此关卡后，你将学习：

- Managing multiple inputs and outputs (管理多个输入和输出)
- State machine programming (状态机编程)
- Complex conditional logic (复杂条件逻辑)
- System design and architecture (系统设计和架构)
- Debugging multi-component systems (调试多组件系统)

---

## 💡 Project Ideas | 项目想法

### Smart Home Systems | 智能家居系统 ⭐⭐⭐⭐

1. **Smart Parking Assistant** (智能停车助手)
   - **Inputs**: Ultrasonic distance sensor
   - **Outputs**: 3 LEDs (green/yellow/red), Buzzer
   - **Logic**: 
     - Far: Green LED, no sound
     - Medium: Yellow LED, slow beep
     - Close: Red LED, fast beep
     - Very close: Red LED flashing, continuous alarm

2. **Smart Room Lighting** (智能房间照明)
   - **Inputs**: PIR motion sensor, Photoresistor
   - **Outputs**: LED strips or multiple LEDs
   - **Logic**: 
     - If dark AND motion detected → Lights ON
     - If bright OR no motion for 30s → Lights OFF
     - Adjustable brightness based on ambient light

3. **Temperature Control System** (温度控制系统)
   - **Inputs**: Temperature sensor, Humidity sensor
   - **Outputs**: Fan (motor), Heater (relay/LED), Status LEDs
   - **Logic**:
     - Too hot → Fan ON
     - Too cold → Heater ON
     - Comfortable → Both OFF, Green LED
     - Display status on LEDs

### Safety & Security | 安全与保安 ⭐⭐⭐⭐⭐

4. **Home Security System** (家庭安全系统)
   - **Inputs**: PIR sensor, Door switch, Touch/Button
   - **Outputs**: Buzzer, RGB LED, Servo (lock)
   - **Logic**:
     - Armed mode vs Disarmed mode
     - Motion detected when armed → Alarm
     - Correct code → Disarm
     - Door opened when armed → Alert

5. **Fire Detection System** (火灾检测系统)
   - **Inputs**: Temperature sensor, Smoke sensor (analog), Button
   - **Outputs**: Buzzer, Red LED, Servo (sprinkler simulation)
   - **Logic**:
     - High temp OR smoke → Alarm + Activate sprinkler
     - Button press → System test
     - Status indicators

### Interactive Games | 互动游戏 ⭐⭐⭐⭐

6. **Reaction Time Game** (反应时间游戏)
   - **Inputs**: 3 Buttons
   - **Outputs**: 3 LEDs, Buzzer
   - **Logic**:
     - Random LED lights up
     - Player must press corresponding button
     - Buzzer for correct/wrong
     - Track score

7. **Simon Says** (西蒙说)
   - **Inputs**: 4 Buttons
   - **Outputs**: 4 LEDs, 4 Tones (buzzer)
   - **Logic**:
     - System plays sequence
     - Player repeats sequence
     - Sequence gets longer
     - Game over on mistake

---

## 🔌 System Design Tips | 系统设计技巧

### 1. Plan Before You Code | 编码前规划

**Create a diagram**:
```
INPUTS          PROCESSING        OUTPUTS
[Button 1]  →                 →  [LED 1]
[Sensor 2]  →   Arduino       →  [Buzzer]
[Sensor 3]  →   Logic         →  [Servo]
```

**Define states**:
- What states can your system be in? (系统可以处于什么状态？)
- What triggers state transitions? (什么触发状态转换？)
- What does each state do? (每个状态做什么？)

---

### 2. Use Functions | 使用函数

**Break code into manageable pieces**:

```cpp
void checkSensors() {
  // Read all sensors
}

void updateActuators() {
  // Control all outputs
}

void checkAlarmConditions() {
  // Evaluate logic
}
```

---

### 3. State Machine Pattern | 状态机模式

```cpp
enum SystemState {
  IDLE,
  ACTIVE,
  ALARM,
  RESET
};

SystemState currentState = IDLE;

void loop() {
  switch(currentState) {
    case IDLE:
      // Handle idle state
      if (condition) currentState = ACTIVE;
      break;
    
    case ACTIVE:
      // Handle active state
      if (alarmCondition) currentState = ALARM;
      break;
    
    case ALARM:
      // Handle alarm state
      break;
  }
}
```

---

## 💻 Code Example: Smart Parking Assistant | 代码示例：智能停车助手

```cpp
// Flag 4: Smart Parking Assistant
// Sensors: Ultrasonic Distance
// Actuators: 3 LEDs (Green/Yellow/Red), Buzzer

const int TRIG_PIN = 9;
const int ECHO_PIN = 10;
const int GREEN_LED = 2;
const int YELLOW_LED = 3;
const int RED_LED = 4;
const int BUZZER = 5;

// Distance thresholds (cm)
const int SAFE_DISTANCE = 50;
const int WARNING_DISTANCE = 30;
const int DANGER_DISTANCE = 15;

enum ParkingState {
  FAR,      // Far away - safe
  MEDIUM,   // Getting closer - caution
  CLOSE,    // Close - danger
  TOO_CLOSE // Too close - critical
};

ParkingState currentState = FAR;

void setup() {
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(GREEN_LED, OUTPUT);
  pinMode(YELLOW_LED, OUTPUT);
  pinMode(RED_LED, OUTPUT);
  pinMode(BUZZER, OUTPUT);
  
  Serial.begin(9600);
  Serial.println("=== Smart Parking Assistant ===");
}

void loop() {
  // Read distance
  long distance = getDistance();
  
  // Update state based on distance
  updateState(distance);
  
  // Control LEDs and buzzer based on state
  controlOutputs();
  
  delay(100);
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

void updateState(long distance) {
  if (distance > SAFE_DISTANCE) {
    currentState = FAR;
  } else if (distance > WARNING_DISTANCE) {
    currentState = MEDIUM;
  } else if (distance > DANGER_DISTANCE) {
    currentState = CLOSE;
  } else {
    currentState = TOO_CLOSE;
  }
}

void controlOutputs() {
  // Turn off all first
  digitalWrite(GREEN_LED, LOW);
  digitalWrite(YELLOW_LED, LOW);
  digitalWrite(RED_LED, LOW);
  noTone(BUZZER);
  
  switch(currentState) {
    case FAR:
      digitalWrite(GREEN_LED, HIGH);
      Serial.println("✓ Safe distance - Green");
      break;
    
    case MEDIUM:
      digitalWrite(YELLOW_LED, HIGH);
      tone(BUZZER, 1000);
      delay(100);
      noTone(BUZZER);
      Serial.println("⚠ Caution - Yellow");
      break;
    
    case CLOSE:
      digitalWrite(RED_LED, HIGH);
      tone(BUZZER, 1500);
      delay(150);
      noTone(BUZZER);
      delay(150);
      Serial.println("⛔ Danger - Red");
      break;
    
    case TOO_CLOSE:
      // Flash red LED
      digitalWrite(RED_LED, !digitalRead(RED_LED));
      tone(BUZZER, 2000);
      Serial.println("🚨 TOO CLOSE! STOP!");
      break;
  }
}
```

---

## 📝 What to Submit | 提交内容

Use the `solution-template.md` file and fill in:

使用 `solution-template.md` 文件并填写：

1. **System Design** (系统设计)
   - Block diagram of your system (系统框图)
   - Component list and roles (组件列表和角色)
   - State machine or logic flow (状态机或逻辑流程)

2. **Complete Documentation** (完整文档)
   - All pin connections (所有引脚连接)
   - Wiring photos (接线照片)
   - Code with detailed comments (有详细注释的代码)

3. **Demonstration** (演示)
   - Video showing full functionality (显示完整功能的视频)
   - Multiple test scenarios (多个测试场景)

4. **Reflection** (反思)
   - Design decisions (设计决策)
   - Challenges and solutions (挑战和解决方案)
   - How it could be improved (如何改进)

---

## ✅ Verification Checklist | 验证清单

Before submitting:

提交前：

- [ ] System uses 3+ sensors/actuators (系统使用3+个传感器/执行器)
- [ ] Complex logic implemented (state machine or multiple conditions) (实现复杂逻辑)
- [ ] All components tested and working (所有组件测试并工作)
- [ ] Code is organized with functions (代码用函数组织)
- [ ] Comprehensive comments explain logic (全面的注释解释逻辑)
- [ ] Video demonstrates full system behavior (视频演示完整系统行为)
- [ ] System has clear purpose/solves problem (系统有明确目的/解决问题)

---

## 🌟 Bonus Challenges | 加分挑战

- **Add LCD display** for status messages (添加LCD显示状态消息)
- **Implement data logging** via Serial (通过串口实现数据记录)
- **Add adjustable settings** with potentiometer (用电位器添加可调设置)
- **Non-blocking timing** with `millis()` instead of `delay()` (用millis()而不是delay()实现非阻塞计时)

---

## 🚀 Next Steps | 下一步

Once you capture Flag 4:

捕获Flag 4后：

1. Test your system thoroughly (彻底测试系统)
2. Document everything clearly (清晰记录一切)
3. Commit your work (提交你的工作)
4. Move on to **Flag 5: Creative Project** - The final challenge! (进入Flag 5：创意项目 - 最终挑战！)

---

## 🆘 Need Help? | 需要帮助？

- Check `hints.md` for design patterns (查看hints.md获取设计模式)
- Start simple, add complexity gradually (从简单开始，逐渐增加复杂性)
- Test each component separately first (先分别测试每个组件)
- Ask your TA for system design guidance (向助教寻求系统设计指导)

---

**This is advanced embedded systems! You're building real products!** 🚀

**这是高级嵌入式系统！你正在构建真实产品！** 🚀

Good luck! 加油！ 💪

