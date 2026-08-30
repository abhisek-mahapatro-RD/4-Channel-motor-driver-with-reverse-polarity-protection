# 4-Channel DRV8871 Motor Driver

A compact, highly reliable 4-channel brushed DC motor driver designed around four Texas Instruments **DRV8871** H-bridge ICs. 

This board underwent iterative PCB engineering and real-world lab testing to achieve production-grade performance for ESP32 and microcontroller-based robotics.

---

## Features

- **Quad Motor Control**: 4 independent brushed DC motor channels (1 × dedicated DRV8871 IC per motor).
- **Flexible Digital Interface**: 8 digital control inputs (IN1–IN8) compatible with 3.3V and 5V microcontrollers via a keyed box header (ideal for ESP32 PWM control).
- **Dedicated Outputs**: Separate A/B output pairs for clean routing to each motor load.
- **Power Safety & Protection**:
  - P-Channel MOSFET (SI2371EDS) reverse-polarity protection on main power input ($V_+$).
  - Onboard input fuse provision for main overcurrent protection.
  - Dual $220\mu\text{F}$ bulk storage capacitors ($C1$, $C10$) onboard to handle motor startup transients and prevent power supply dips.
- **Diagnostic LEDs**: Onboard **ON** (Power status) and **ERR** (Fault condition) visual indicators.
- **High-Current Terminal Connections**: Upgraded heavy-duty screw terminals (Rev 2) for reliable power delivery under heavy motor load.

---

## Hardware Revisions

- **Rev 1.0**: Initial breadboard validation and PCB prototype utilizing standard 2.54mm pin headers. Real-world testing revealed 2.54mm pins suffered excessive voltage drop and current constraints at continuous 2.5A loads.
- **Rev 2.0 (Current)**: Upgraded motor outputs and main power input rails to heavy-duty screw terminal blocks to safely handle high-current transients up to 2.5A+. Optimized thermal dissipation vias directly beneath DRV8871 exposed thermal pads.

---

## System Specs & Hardware Parameters

| Parameter | Value / Detail |
| :--- | :--- |
| **Driver IC** | 4× TI DRV8871DDA (H-Bridge Driver) |
| **Logic Supply Voltage** | 3.3V to 5V (ESP32, STM32, Arduino compatible) |
| **Motor Input Voltage ($V_{IN}$)** | 6.5V – 45V DC |
| **Max Peak Output Current** | Up to 3.6A per channel |
| **Current Limit Resistors** | $R1-R4 = 30\text{k}\Omega$ ($R_{ILIM}$) |
| **Bulk Capacitance** | $2 \times 220\mu\text{F}$ High-Capacitance Electrolytic Rail Filters |
| **Connectors** | Screw terminals (Rev 2) for motor/power; 8-pin keyed header for logic |

---

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
