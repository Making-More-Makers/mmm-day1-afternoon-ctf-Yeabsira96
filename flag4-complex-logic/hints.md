# Flag 4: Hints & Tips
# 关卡4：提示与技巧

Building a complex multi-component system? Here are key strategies!

构建复杂的多组件系统？这里是关键策略！

---

## 🎯 Key Strategies | 关键策略

### Strategy 1: Start Small, Build Up | 从小开始，逐步构建

**DON'T**: Try to build the entire system at once  
**不要**：尝试一次构建整个系统

**DO**: Build incrementally  
**要**：逐步构建

1. Test sensor 1 alone
2. Add sensor 2, test together
3. Add first actuator, test
4. Add logic connecting them
5. Add more components one at a time

---

### Strategy 2: Use State Machines | 使用状态机

**State machine pattern makes complex logic manageable**:

```cpp
enum State {STATE1, STATE2, STATE3};
State currentState = STATE1;

void loop() {
  switch(currentState) {
    case STATE1:
      // State 1 logic
      if (condition) currentState = STATE2;
      break;
    case STATE2:
      // State 2 logic
      break;
  }
}
```

---

### Strategy 3: Organize with Functions | 用函数组织

```cpp
void readAllSensors() {
  sensor1Value = analogRead(SENSOR1);
  sensor2Value = digitalRead(SENSOR2);
}

void evaluateLogic() {
  if (sensor1Value > 500 && sensor2Value == HIGH) {
    triggerAlarm = true;
  }
}

void controlAllActuators() {
  digitalWrite(LED1, state1);
  analogWrite(LED2, brightness);
}

void loop() {
  readAllSensors();
  evaluateLogic();
  controlAllActuators();
}
```

---

## 🐛 Common Issues | 常见问题

### Issue: System Behaves Erratically | 系统行为不稳定

**Solution**: Add Serial.print() everywhere to debug:

```cpp
Serial.println("=== Debug Info ===");
Serial.print("Sensor1: "); Serial.println(s1);
Serial.print("Sensor2: "); Serial.println(s2);
Serial.print("State: "); Serial.println(currentState);
Serial.println("==================");
```

---

### Issue: Too Many Components, Confusing | 组件太多，令人困惑

**Solution**: Create a pin mapping section at the top:

```cpp
// ========== PIN CONFIGURATION ==========
// Sensors (传感器)
const int BUTTON_PIN = 2;
const int LIGHT_SENSOR = A0;
const int TEMP_SENSOR = A1;

// Actuators (执行器)
const int RED_LED = 8;
const int GREEN_LED = 9;
const int BUZZER = 10;
// =======================================
```

---

### Issue: Timing Problems with delay() | delay()的计时问题

**Solution**: Use millis() for non-blocking timing:

```cpp
unsigned long previousMillis = 0;
const long interval = 1000;

void loop() {
  unsigned long currentMillis = millis();
  
  if (currentMillis - previousMillis >= interval) {
    previousMillis = currentMillis;
    // Do something every second
  }
  
  // Rest of code runs without blocking
}
```

---

## 💡 Design Patterns | 设计模式

### Pattern: Multiple Threshold Levels | 多级阈值

```cpp
if (value < 200) {
  level = LOW;
} else if (value < 600) {
  level = MEDIUM;
} else {
  level = HIGH;
}
```

### Pattern: Combining Conditions | 组合条件

```cpp
if ((motion == HIGH || button == HIGH) && !alarmDisabled) {
  triggerAlarm();
}
```

### Pattern: Timed Events | 定时事件

```cpp
if (alarmTriggered && (millis() - alarmStartTime > 30000)) {
  // Alarm has been on for 30 seconds
  autoShutoff();
}
```

---

## 📋 Quick Debugging Checklist | 快速调试清单

- [ ] All pinMode() statements present (所有pinMode语句都有)
- [ ] Pin numbers match physical wiring (引脚号匹配物理接线)
- [ ] Serial output shows sensor values changing (串口输出显示传感器值变化)
- [ ] Each state/condition tested separately (每个状态/条件单独测试)
- [ ] No delay() blocking critical code (没有delay()阻塞关键代码)

---

**Complex systems are just many simple parts working together! Break it down!**

**复杂系统只是许多简单部分协同工作！分解它！**

