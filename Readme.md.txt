# Water Monitoring and Purification System 🌊💧

This project is a **smart water monitoring and purification system** built using a **Raspberry Pi**.  
It monitors **water level, pH, turbidity, and temperature** while automatically controlling a **water pump** and **filtering system** (activated carbon, UV, etc.) through relays.  

---

## 🚀 Features
- Real-time monitoring of:
  - Water level
  - pH
  - Turbidity
  - Temperature
- Automatic **pump control** based on water level
- Automatic **filtering system control** based on water quality
- Data output to console
- Easy threshold customization
- Extendable for:
  - Wi-Fi connectivity for remote monitoring
  - Data logging
  - Alerts for abnormal water quality

---

## 🛠️ Hardware Requirements
1. **Raspberry Pi** (any model with GPIO support)
2. **Water level sensor** (e.g., HC-SR04 ultrasonic sensor)
3. **Water quality sensors**:
   - pH sensor  
   - Turbidity sensor  
   - Temperature sensor  
4. **Water pump**
5. **Filtering system** (activated carbon / UV)
6. **Relays** (to control pump & filter system)
7. **Wires & Breadboard**

---

## 💻 Software Requirements
- Raspbian OS (on Raspberry Pi)  
- Python 3.x  
- Libraries:  
  - `RPi.GPIO` (for GPIO control)  
  - `Adafruit_ADS1x15` (for analog sensor readings)  

### Install dependencies:
```bash
sudo apt-get update
sudo apt-get install python3-pip
pip3 install adafruit-ads1x15
