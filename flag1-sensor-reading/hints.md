# Flag 1: Hints & Tips
# 关卡1：提示与技巧

Need some help? Here are progressive hints to guide you!

需要帮助吗？这里有渐进式提示来指导你！

---

## 🤔 General Hints | 一般提示

### Hint 1: Start Simple | 从简单开始

**If you're new to Arduino**, start with a **button** or **potentiometer**. These are the easiest sensors to work with!

**如果你是Arduino新手**，从**按钮**或**电位器**开始。这些是最容易使用的传感器！

- Button: Just read HIGH or LOW (按钮：只需读取HIGH或LOW)
- Potentiometer: Read a value between 0-1023 (电位器：读取0-1023之间的值)

---

### Hint 2: Check Your Wiring | 检查接线

**Most problems are wiring issues!** (大多数问题都是接线问题！)

Common mistakes | 常见错误:
- GND not connected (GND未连接)
- VCC connected to wrong voltage (VCC连接到错误的电压)
- Signal pin in wrong Arduino pin (信号引脚插在错误的Arduino引脚)

**Tip**: Take a photo of your wiring and compare it to examples online!

**提示**：给接线拍照并与在线示例比较！

---

### Hint 3: Open Serial Monitor | 打开串口监视器

After uploading code:

上传代码后：

1. Tools → Serial Monitor (工具 → 串口监视器)
2. Set baud rate to **9600** (设置波特率为**9600**)
3. You should see sensor values appear! (你应该看到传感器值出现！)

**Not seeing anything?** (什么都看不到？)
- Check if `Serial.begin(9600);` is in your `setup()` function
- Make sure you're using `Serial.println()` in your `loop()`

---

## 🔌 Sensor-Specific Hints | 传感器特定提示

### For Button / Switch | 按钮/开关

**Problem**: Button always reads the same value  
**问题**：按钮总是读取相同的值

**Solution**: Add a pull-down resistor OR use `INPUT_PULLUP` mode:  
**解决方案**：添加下拉电阻或使用`INPUT_PULLUP`模式：

```cpp
pinMode(BUTTON_PIN, INPUT_PULLUP);
// Now: Pressed = LOW, Not Pressed = HIGH
// 现在：按下 = LOW，未按下 = HIGH
```

---

### For Photoresistor | 光敏电阻

**Problem**: Values don't change much  
**问题**：值变化不大

**Solution**: You need a voltage divider circuit:  
**解决方案**：你需要分压电路：

```
5V → Photoresistor → A0 → 10kΩ Resistor → GND
```

**Tip**: Cover the sensor with your hand to see values change!  
**提示**：用手遮住传感器看值变化！

---

### For Temperature Sensor (LM35) | 温度传感器

**Problem**: Getting weird numbers  
**问题**：得到奇怪的数字

**Solution**: You need to convert the reading:  
**解决方案**：你需要转换读数：

```cpp
int reading = analogRead(TEMP_PIN);
float voltage = reading * (5.0 / 1023.0);
float temperatureC = voltage * 100;  // LM35: 10mV per degree

Serial.print("Temperature: ");
Serial.print(temperatureC);
Serial.println(" °C");
```

---

### For Ultrasonic Sensor (HC-SR04) | 超声波传感器

**This is more complex!** Need TWO pins:  
**这个更复杂！**需要两个引脚：

```cpp
const int TRIG_PIN = 9;
const int ECHO_PIN = 10;

void setup() {
  Serial.begin(9600);
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
}

void loop() {
  // Send pulse
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);
  
  // Read echo
  long duration = pulseIn(ECHO_PIN, HIGH);
  long distance = duration * 0.034 / 2;
  
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");
  
  delay(500);
}
```

---

## 🐛 Debugging Tips | 调试技巧

### Issue: Code Won't Compile | 代码不能编译

**Check for**:
- Missing semicolons `;` (缺少分号)
- Mismatched curly braces `{}` (花括号不匹配)
- Typos in variable names (变量名拼写错误)

**Tip**: Read the error message carefully! It usually tells you the line number.  
**提示**：仔细阅读错误消息！它通常会告诉你行号。

---

### Issue: Serial Monitor Shows Nothing | 串口监视器什么都不显示

**Check**:
1. Correct COM port selected? (选择了正确的COM端口吗？)
2. Baud rate set to 9600? (波特率设置为9600了吗？)
3. Is `Serial.begin(9600);` in setup? (setup中有Serial.begin(9600)吗？)
4. Are you using `Serial.print()` or `Serial.println()`? (使用了Serial.print()或Serial.println()吗？)

---

### Issue: Sensor Values Don't Change | 传感器值不变化

**Try this**:
1. Check physical connection (检查物理连接)
2. Try a different pin (尝试不同的引脚)
3. Add debug prints: (添加调试打印：)
   ```cpp
   Serial.println("Reading sensor...");
   int value = analogRead(A0);
   Serial.print("Got value: ");
   Serial.println(value);
   ```

---

## 💡 Pro Tips | 专业技巧

### Tip 1: Format Your Output | 格式化输出

Make your Serial Monitor output easy to read:

让串口监视器输出易于阅读：

```cpp
Serial.println("====================");
Serial.print("Sensor: ");
Serial.println("Photoresistor");
Serial.print("Value: ");
Serial.println(sensorValue);
Serial.println("====================");
```

---

### Tip 2: Add a Delay | 添加延迟

Don't flood the Serial Monitor! Add a delay:

不要淹没串口监视器！添加延迟：

```cpp
delay(500);  // Wait 500ms = 0.5 seconds
```

---

### Tip 3: Map Values | 映射值

For better readability, map 0-1023 to a different range:

为了更好的可读性，将0-1023映射到不同范围：

```cpp
int sensorValue = analogRead(A0);
int percentage = map(sensorValue, 0, 1023, 0, 100);

Serial.print("Light Level: ");
Serial.print(percentage);
Serial.println("%");
```

---

## 📋 Quick Checklist | 快速检查清单

Still stuck? Go through this checklist:

还卡住了？检查这个清单：

- [ ] Arduino is powered on (LED lit) (Arduino已开机，LED亮着)
- [ ] Correct board selected in Arduino IDE (Arduino IDE中选择了正确的板)
- [ ] Correct port selected (选择了正确的端口)
- [ ] Sensor connected to 5V or 3.3V (传感器连接到5V或3.3V)
- [ ] Sensor GND connected to Arduino GND (传感器GND连接到Arduino GND)
- [ ] Signal pin connected to correct Arduino pin (信号引脚连接到正确的Arduino引脚)
- [ ] Pin number in code matches physical connection (代码中的引脚号匹配物理连接)
- [ ] Serial.begin(9600) in setup() (setup()中有Serial.begin(9600))
- [ ] Serial Monitor baud rate set to 9600 (串口监视器波特率设置为9600)
- [ ] Delay added in loop() (loop()中添加了延迟)

---

## 🆘 Still Need Help? | 还需要帮助？

**Don't give up!** (不要放弃！)

1. **Ask a classmate** - Two heads are better than one! (问同学 - 两个人比一个人强！)
2. **Raise your hand** - TAs are here to help! (举手 - 助教在这里帮忙！)
3. **Try a different sensor** - Some are easier than others! (尝试不同的传感器 - 有些比其他的更容易！)

---

**Remember**: Every expert was once a beginner. You've got this! 💪

**记住**：每个专家都曾是初学者。你可以的！💪

