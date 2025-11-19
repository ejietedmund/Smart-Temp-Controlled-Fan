# Smart Temperature-Controlled Fan with ESP32 :fire::thermometer:

### Automatic IoT Fan System using LM35 Sensor, DFRobot 130 DC Motor, LCD Display & Node-RED Dashboard

An intelligent temperature-controlled cooling fan that automatically adjusts speed based on room temperature. Features real-time monitoring and manual override via a stunning Node-RED web dashboard.  
Perfect university-level IoT project (includes **sensor + actuator + communication + dashboard**).



## :rocket: Features
- Real-time temperature reading using **LM35** analog sensor
- Proportional fan speed control (Off → Low → Medium → High)
- Local feedback via **16×2 I2C LCD** and two status LEDs
- Full-speed motor control using **DFRobot 130 DC Motor + Driver Module**
- Live data streaming over **Serial (USB)** to **Node-RED**
- Beautiful web dashboard with gauge, chart, status, and **manual fan override slider**
- Clean JSON communication protocol
- Easy to extend (Wi-Fi/MQTT, alerts, etc.)

## :toolbox: Components Used
| Component                          | Quantity | Notes                                      |
|------------------------------------|----------|--------------------------------------------|
| ESP32 DevKit (any variant)         | 1        | 3.3V logic – works perfectly with driver  |
| LM35 Temperature Sensor            | 1        | Analog output                              |
| DFRobot 130-size DC Motor          | 1        | Comes with fan blade                       |
| DFRobot Motor Driver Module V1.0   | 1        | DIR + PWM control                          |
| 16×2 LCD Display with I2C backpack | 1        | Address usually 0x27                       |
| Red LED + Green LED + 1kΩ resistors| 2        | Status indicators                          |
| Breadboard & jumper wires          | -        |                                            |
| 5V Power Supply (USB/adapter)      | 1        | Powers motor driver (do NOT use ESP32 5V pin for high current) |
## 🔌 Wiring Diagram & Pinout

### Connection Table (ESP32 ↔ Components)

| ESP32 Pin       | Component                  | Connection Notes                          |
|-----------------|----------------------------|-------------------------------------------|
| GPIO34 (ADC)    | LM35                       | Vout → Temperature signal                 |
| 3.3V            | LM35                       | VCC                                       |
| GND             | LM35                       | GND                                       |
| GPIO26          | DFRobot Motor Driver       | PWM pin                                   |
| GPIO27          | DFRobot Motor Driver       | DIR pin                                   |
| VIN or External 5V | DFRobot Motor Driver    | VCC (use external 5V for motor power!)    |
| GND             | DFRobot Motor Driver       | GND (common ground)                       |
| GPIO15          | Red LED                    | Via 1kΩ resistor → GND                    |
| GPIO13          | Green LED                  | Via 1kΩ resistor → GND                    |
| GPIO21 (SDA)    | I2C LCD (backpack)         | SDA                                       |
| GPIO22 (SCL)    | I2C LCD (backpack)         | SCL                                       |
| 5V              | I2C LCD                    | VCC                                       |
| GND             | I2C LCD                    | GND                                       |




## :computer: How to Run
1. Wire everything according to the schematic
2. Open `ESP32_Code/Smart_Fan_ESP32.ino` → Upload to ESP32
3. Install Node-RED + Dashboard nodes
4. Import `Node-RED/smart_fan_flow.json`
5. Change the serial port node to your ESP32 COM port (e.g., COM10)
6. Deploy → Open dashboard at `http://YOUR_IP:1880/ui`
7. Enjoy automatic cooling + manual control!

## :trophy: Project Requirements Met
- [x] At least one sensor (LM35)
- [x] At least one actuator (DC motor with speed control)
- [x] IoT communication (Serial → Node-RED)
- [x] Real-time dashboard with visualization & control

## :bulb: Future Enhancements
- Wi-Fi + Blynk/MQTT (no USB needed)
- DHT22 for temperature + humidity
- Over-temperature email/SMS alert
- 3D-printed enclosure
- OLED display instead of LCD

## :heart: Credits
Created by **EJIET EDMUND**  
Special thanks to DFRobot for the excellent motor driver module.

## :page_facing_up: License
MIT License – feel free to use, modify, and share!

---

**Star :star: this repo if it helped you ace your IoT project!**  
Questions? Open an issue – happy to help!

Made with ❤️ in 2025
