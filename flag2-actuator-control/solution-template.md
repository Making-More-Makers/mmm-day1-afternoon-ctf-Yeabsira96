# Flag 2 Solution: Actuator Control
# Flag 2 解决方案：执行器控制

**Student Name | 学生姓名**: _________________

**Date Completed | 完成日期**: _________________

---

## 📋 Actuator Information | 执行器信息

### Which actuator did you choose? | 你选择了哪个执行器？

**Actuator Name | 执行器名称**: 

**Actuator Type | 执行器类型**: 
- [ ] LED
- [ ] Buzzer (蜂鸣器)
- [ ] Servo Motor (舵机)
- [ ] DC Motor (直流电机)
- [ ] RGB LED
- [ ] Other: __________

---

### What does this actuator do? | 这个执行器做什么？

*Describe what the actuator controls or produces*  
*描述执行器控制或产生什么*




---

## 🔌 Wiring | 接线

### Pin Connections | 引脚连接

Fill in how you connected your actuator:

填写你如何连接执行器：

| Actuator Pin | Arduino Pin | Connection Type | 执行器引脚 | Arduino引脚 | 连接类型 |
|--------------|-------------|-----------------|-----------|-------------|---------|
| | | ☐ Digital ☐ PWM | | | |
| | | | | | |
| | | | | | |

**Additional components used | 使用的额外组件**:
- [ ] Resistor (value: _______Ω) - for LED
- [ ] Motor driver (specify: _______) - for motors
- [ ] None / No additional components

---

### Wiring Photo | 接线照片

*Upload a photo and link it here*  
*上传照片并在此链接*

![Wiring Photo](./wiring.jpg)

*Or describe your wiring setup:*  
*或描述你的接线设置：*




---

## 💻 Code | 代码

### Complete Arduino Code | 完整Arduino代码

*Paste your complete, working code here with comments!*  
*在此粘贴你完整的、能工作的代码并加注释！*

```cpp
// Paste your code here
// 在此粘贴代码






```

---

### Code Explanation | 代码解释

**Describe your control logic:**  
**描述你的控制逻辑：**

**Setup Section | 设置部分**:




**Loop Section | 循环部分**:




**Control Method Used | 使用的控制方法**:
- [ ] `digitalWrite()` - Digital ON/OFF
- [ ] `analogWrite()` - PWM control (brightness/speed)
- [ ] `tone()` / `noTone()` - Sound frequency
- [ ] Servo library - Position control
- [ ] Other: __________

---

## 🎯 Behaviors Demonstrated | 演示的行为

### Behavior 1 | 行为1

**Description | 描述**:




**Parameters | 参数**:
- Delay/Timing: _______ms
- Value/Position: _______
- Other settings: _______

---

### Behavior 2 | 行为2

**Description | 描述**:




**Parameters | 参数**:
- Delay/Timing: _______ms
- Value/Position: _______
- Other settings: _______

---

### Additional Behaviors (Optional) | 额外行为（可选）

**Behavior 3+**:




---

## 📸 Demonstration | 演示

### Photo/Video | 照片/视频

*Upload a photo or video showing your actuator in action*  
*上传显示执行器运行的照片或视频*

![Demo Photo/Video](./demo.jpg)

---

### Observed Behavior | 观察到的行为

**What happened when you ran your code?**  
**运行代码时发生了什么？**




**Did it work as expected?**  
**按预期工作了吗？**

☐ Yes, perfectly! (是的，完美！)  
☐ Yes, with some adjustments (是的，经过一些调整)  
☐ Partially - needs improvement (部分 - 需要改进)

---

## 🎓 Reflection | 反思

### What Worked Well | 什么做得好




---

### Challenges Faced | 面临的挑战

**Did you encounter any problems? How did you solve them?**  
**遇到任何问题了吗？你如何解决的？**




---

### What I Learned | 我学到的东西

**What new concepts did you learn?**  
**你学到了什么新概念？**




**Key functions or techniques:**  
**关键函数或技术：**




---

### Creative Additions (Bonus) | 创意添加（加分）

**Did you add any extra features or patterns?**  
**你添加了任何额外功能或模式吗？**




---

## 🔄 Comparison with Flag 1 | 与Flag 1的比较

**How is controlling an actuator different from reading a sensor?**  
**控制执行器与读取传感器有何不同？**

| Aspect | Sensor (Flag 1) | Actuator (Flag 2) | 方面 |
|--------|----------------|-------------------|------|
| Direction | Input | Output | 方向 |
| Function | Read data | Control device | 功能 |
| Pin Mode | INPUT | OUTPUT | 引脚模式 |
| Main Functions | `digitalRead()`, `analogRead()` | `digitalWrite()`, `analogWrite()` | 主要函数 |

---

## ⏱️ Time Spent | 花费时间

**Estimated time spent | 估计花费时间**: _______ minutes (分钟)

**Breakdown | 分解**:
- Wiring: _____min (接线)
- Coding: _____min (编码)
- Testing/Debugging: _____min (测试/调试)
- Documentation: _____min (文档)

---

## ✅ Verification | 验证

Check off these items before submitting:

提交前勾选这些项目：

- [ ] Code compiles without errors (代码编译无错误)
- [ ] Actuator responds correctly to code (执行器正确响应代码)
- [ ] At least 2 different behaviors demonstrated (演示了至少2种不同行为)
- [ ] Code is well-commented (代码有良好注释)
- [ ] All sections of this template filled out (模板的所有部分都已填写)
- [ ] Photo or video of working demo included (包含工作演示的照片或视频)

---

## 🚀 Next Steps | 下一步

**Reflections for Flag 3:**  
**Flag 3的思考：**

In Flag 3, you'll combine sensors and actuators. Based on what you learned:

在Flag 3中，你将结合传感器和执行器。基于你学到的：

**What sensor-actuator combination would you like to try?**  
**你想尝试什么传感器-执行器组合？**

Examples:
- Button → LED (按钮 → LED)
- Light sensor → Buzzer (光线传感器 → 蜂鸣器)
- Distance sensor → Servo (距离传感器 → 舵机)

**Your idea | 你的想法**:




---

## 🎉 Congratulations! | 恭喜！

**You've captured Flag 2!** 🚩  
**你捕获了Flag 2！** 🚩

You now understand how to:
- Control output devices (控制输出设备)
- Use digital and PWM signals (使用数字和PWM信号)
- Create patterns and behaviors (创建模式和行为)
- Time events with delays (用延迟计时事件)

**Ready for the next challenge? Let's connect sensors to actuators!** 🚀  
**准备好下一个挑战了吗？让我们将传感器连接到执行器！** 🚀

---

**Date Submitted | 提交日期**: _________________

**Instructor Feedback | 讲师反馈**:

