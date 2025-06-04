# 🤖 Arduino Wet Object Detection & Sorting System

An Arduino-powered system that detects passing objects and determines if they're **wet or dry** using an **IR sensor** and a **rain/moisture sensor**. It controls a **stepper motor** and **servo motor** to sort or handle the object accordingly.

## 🧰 Hardware Components

- Arduino Uno or compatible board  
- IR Sensor (object detection)  
- Rain Sensor (to detect wet surface on objects)  
- 28BYJ-48 Stepper Motor + ULN2003 driver  
- Servo Motor (e.g., SG90)  
- Jumper wires, breadboard  

## 🗂️ Pin Configuration

| Component      | Arduino Pin |
|----------------|-------------|
| Servo Motor    | 7           |
| Rain Sensor    | A0          |
| IR Sensor      | A1          |
| Stepper IN1    | 8           |
| Stepper IN3    | 9           |
| Stepper IN2    | 10          |
| Stepper IN4    | 11          |

> ⚠️ **Important:** The stepper pin order (IN1, IN2, IN3, IN4) must follow the order required by the `AccelStepper` library.

## 📦 Libraries Used

- [`AccelStepper`](https://www.airspayce.com/mikem/arduino/AccelStepper/)
- `Servo` (built-in)

Install via Arduino Library Manager if needed.

## 🚀 How It Works

1. **IR Sensor** detects if an object is present.
2. **Rain Sensor** checks if the object's surface is wet.
3. Based on the condition:
   - 🟥 **Wet Object** → Stepper rotates **clockwise**, servo opens.
   - 🟩 **Dry Object** → Stepper rotates **counterclockwise**, servo opens.
   - ⚪ **No Object** → Stepper returns to **home**, servo resets.

## 🧪 Sensor Thresholds

These lines define detection logic — tune the values if your sensor behaves differently:

```cpp
bool objectDetected = irValue < 500;
bool isWet = rainValue < 500;
