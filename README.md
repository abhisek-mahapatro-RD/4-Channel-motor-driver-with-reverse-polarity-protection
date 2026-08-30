# 4-Channel DRV8871 Motor Driver



A compact, highly reliable 4-channel brushed DC motor driver designed around four Texas Instruments **DRV8871** H-bridge ICs. 

Developed as part of the hardware initiative, this board underwent multiple PCB layout revisions and hands-on prototype testing in the lab to achieve production-grade stability for ESP32 and micro-controller-based robotics.

---

## Features

- **Quad Motor Control**: 4 independent brushed DC motor channels (1 × dedicated DRV8871 IC per motor).
- **Flexible Digital Interface**: 8 total digital control inputs compatible with 3.3V and 5V microcontrollers (ideal for ESP32 PWM control).
- **Dedicated Outputs**: Separate A/B output pairs for clean routing to each motor.
- **Power Safety & Protection**:
  - Reverse-polarity protection on the main high-current power input rail.
  - Onboard input fuse provision for overcurrent safety.
  - Bulk storage capacitance onboard to handle high motor transient currents and prevent voltage dips.
- **Diagnostic LEDs**: Dedicated **ON** (Power) and **ERR** (Fault Status) visual indicators.
- **Industrial Terminal Connections**: Heavy-duty screw-terminal blocks for motor connections (introduced in Rev 3).

---

## System Specs & Pinout Overview

| Specification | Details |
| :--- | :--- |
| **Motor Driver IC** | 4× TI DRV8871 H-Bridge Drivers |
| **Logic Supply Voltage** | 3.3V to 5V (ESP32, STM32, Arduino compatible) |
| **Motor Input Voltage ($V_{IN}$)** | 6.5V – 45V DC |
| **Max Peak Output Current** | Up to 3.6A per channel |
| **Current Limits** | Hardware set via $R_{ILIM}$ resistors |
| **Connectors** | Screw terminals (Rev 3) for power & motors, pin headers for logic |


## Quick Start (ESP32 Code Example)

```cpp
// Example code for driving Motor 1 using ESP32 PWM pins
const int MOTOR1_IN1 = 18; 
const int MOTOR1_IN2 = 19; 

void setup() {
  pinMode(MOTOR1_IN1, OUTPUT);
  pinMode(MOTOR1_IN2, OUTPUT);
}

void loop() {
  // Drive Motor 1 Forward at ~75% Speed
  analogWrite(MOTOR1_IN1, 190);
  digitalWrite(MOTOR1_IN2, LOW);
  delay(2000);

  // Coast / Stop
  digitalWrite(MOTOR1_IN1, LOW);
  digitalWrite(MOTOR1_IN2, LOW);
  delay(1000);
}
