# 🌬️ Mini Mobile Air Monitoring System

<div align="center">

![Arduino](https://img.shields.io/badge/Arduino-00979D?style=for-the-badge&logo=Arduino&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)
![Hardware](https://img.shields.io/badge/Hardware-FF6B35?style=for-the-badge&logo=arduino&logoColor=white)
![Environmental](https://img.shields.io/badge/Environmental-4CAF50?style=for-the-badge&logo=leaf&logoColor=white)

**A compact and affordable air quality monitoring system for real-time environmental sensing**

</div>

---

## 🎯 Project Overview

The **Mini Mobile Air Monitoring System** is an Arduino-based environmental monitoring solution that provides real-time air quality measurements. This portable device continuously monitors air pollution levels, displays the data in parts per million (PPM), and alerts users when pollution exceeds safe thresholds.

### ✨ Key Features

- **📊 Real-time Monitoring**: Continuous air quality measurement in PPM
- **🖥️ LCD Display**: Clear, easy-to-read 16x2 LCD showing current readings
- **🚨 Smart Alerts**: LED/Buzzer notifications when pollution levels are dangerous
- **💰 Cost-Effective**: Built with affordable, readily available components
- **🔋 Portable**: Compact design for mobile environmental monitoring
- **⚡ Low Power**: Efficient power consumption for extended operation

---

## 🛠️ Hardware Components

### Essential Components

| Component | Quantity | Purpose |
|-----------|----------|---------|
| **Arduino Uno R3** | 1 | Main microcontroller |
| **MQ-135 Gas Sensor** | 1 | Air quality detection |
| **16x2 LCD Display** | 1 | Data visualization |
| **LED (Red/Green)** | 2 | Visual status indicators |
| **Buzzer** | 1 | Audio alert system |
| **Resistors** | 3-5 | Current limiting (220Ω, 10kΩ) |
| **Breadboard** | 1 | Circuit prototyping |
| **Jumper Wires** | 15-20 | Connections |
| **Potentiometer 10kΩ** | 1 | LCD contrast adjustment |

### Optional Components
- **9V Battery + Connector**: For portable operation
- **Enclosure Case**: Protection and professional look
- **Push Button**: Manual reset/calibration

---

## 🔌 Circuit Diagram & Connections

### Arduino Pin Connections

#### MQ-135 Gas Sensor
```
MQ-135 VCC  → Arduino 5V
MQ-135 GND  → Arduino GND
MQ-135 A0   → Arduino A0 (Analog Pin)
MQ-135 D0   → Arduino Pin 7 (Digital Pin)
```

#### 16x2 LCD Display (I2C or Standard)
```
LCD VSS → Arduino GND
LCD VDD → Arduino 5V
LCD V0  → Potentiometer (10kΩ)
LCD RS  → Arduino Pin 12
LCD EN  → Arduino Pin 11
LCD D4  → Arduino Pin 5
LCD D5  → Arduino Pin 4
LCD D6  → Arduino Pin 3
LCD D7  → Arduino Pin 2
```

#### Alert System
```
Green LED (+) → Arduino Pin 8 → 220Ω Resistor → GND
Red LED (+)   → Arduino Pin 9 → 220Ω Resistor → GND
Buzzer (+)    → Arduino Pin 10
Buzzer (-)    → Arduino GND
```

---

## 💻 Software Setup

### Prerequisites
- **Arduino IDE** (Version 1.8.0 or higher)
- **LiquidCrystal Library** (Usually pre-installed)

### Installation Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/p1ll3chan/Mini-Mobile-Air-Monitoring-System.git
   cd Mini-Mobile-Air-Monitoring-System
   ```

2. **Open Arduino IDE**
   - Launch Arduino IDE
   - Open the main `.ino` file from the project directory

3. **Select Board & Port**
   ```
   Tools → Board → Arduino Uno
   Tools → Port → [Select your Arduino's COM port]
   ```

4. **Upload Code**
   - Click the Upload button (→) or press `Ctrl+U`

---

## ⚙️ Configuration & Calibration

### Sensor Calibration
The MQ-135 sensor requires a **24-48 hour burn-in period** for accurate readings:

1. **Initial Burn-in**: Power the sensor for 24-48 hours in clean air
2. **Baseline Calibration**: Record readings in known clean environment
3. **Threshold Setting**: Adjust alert levels based on your requirements

### Air Quality Thresholds (PPM)
```cpp
// Recommended threshold values
#define CLEAN_AIR_THRESHOLD    50   // Good air quality
#define MODERATE_THRESHOLD     100  // Moderate air quality  
#define UNHEALTHY_THRESHOLD    200  // Unhealthy air quality
#define HAZARDOUS_THRESHOLD    300  // Hazardous air quality
```

---

## 🚀 Usage Instructions

### Basic Operation

1. **Power On**: Connect Arduino via USB or battery
2. **Initialization**: Wait 2-3 minutes for sensor warm-up
3. **Monitoring**: LCD displays current PPM readings
4. **Alert Response**: 
   - **Green LED**: Air quality is good (< 100 PPM)
   - **Red LED + Buzzer**: Poor air quality detected (> 200 PPM)

### Display Information
```
Line 1: Air Quality: XXX PPM
Line 2: Status: GOOD/MODERATE/POOR
```

### Interpreting Readings

| PPM Range | Air Quality | Status | Action |
|-----------|------------|--------|---------|
| 0-50 | Excellent | 🟢 Good | Normal operation |
| 51-100 | Good | 🟡 Moderate | Monitor closely |
| 101-200 | Moderate | 🟠 Caution | Consider ventilation |
| 201-300 | Poor | 🔴 Alert | Immediate action needed |
| 300+ | Hazardous | 🚨 Emergency | Evacuate area |

---

## 📊 Features & Functionality

### Core Functions

#### Real-Time Monitoring
- Continuous analog reading from MQ-135 sensor
- PPM conversion using calibration formula
- 1-second update interval for responsive monitoring

#### Smart Alert System
```cpp
void checkAirQuality(int ppm) {
    if (ppm < MODERATE_THRESHOLD) {
        digitalWrite(GREEN_LED, HIGH);
        digitalWrite(RED_LED, LOW);
        noTone(BUZZER_PIN);
    } else if (ppm > UNHEALTHY_THRESHOLD) {
        digitalWrite(GREEN_LED, LOW);
        digitalWrite(RED_LED, HIGH);
        tone(BUZZER_PIN, 1000); // 1kHz alarm
    }
}
```

#### Data Logging (Future Enhancement)
- SD card logging capability
- Timestamp recording
- Data export functionality

---

## 🔧 Troubleshooting

### Common Issues & Solutions

#### Sensor Not Responding
- **Check Connections**: Verify all wiring matches the diagram
- **Power Supply**: Ensure stable 5V power to sensor
- **Warm-up Time**: Allow 2-3 minutes for sensor initialization

#### Inaccurate Readings
- **Calibration**: Recalibrate sensor in known clean air
- **Placement**: Avoid direct sunlight or heat sources
- **Interference**: Keep away from strong electrical fields

#### LCD Display Issues
- **Contrast**: Adjust potentiometer for optimal contrast
- **Connections**: Check all data and power connections
- **Library**: Ensure LiquidCrystal library is properly installed

#### False Alarms
- **Threshold Adjustment**: Fine-tune PPM thresholds for your environment
- **Sensor Stability**: Ensure sensor has completed burn-in period
- **Environmental Factors**: Consider temperature and humidity effects

---

## 🌟 Future Enhancements

### Planned Features
- [ ] **WiFi Connectivity**: IoT integration for remote monitoring
- [ ] **Mobile App**: Smartphone interface and notifications
- [ ] **Data Logging**: SD card storage for historical data
- [ ] **Multi-Gas Detection**: Additional sensors (CO, CO2, PM2.5)
- [ ] **Weather Integration**: Temperature and humidity sensors
- [ ] **Solar Power**: Renewable energy operation
- [ ] **GPS Tracking**: Location-based air quality mapping

### Advanced Modifications
- **Sensor Array**: Multiple MQ sensors for comprehensive analysis
- **Machine Learning**: Predictive air quality algorithms
- **Cloud Integration**: Real-time data streaming to cloud platforms
- **Solar Charging**: Self-sustaining power system

---

## 🤝 Contributing

We welcome contributions to improve this air monitoring system! Here's how you can help:

### How to Contribute

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'Add AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request

### Contribution Areas
- 🐛 Bug fixes and improvements
- ✨ New sensor integrations
- 📖 Documentation enhancements
- 🎨 UI/UX improvements
- 🧪 Testing and validation

### Code Guidelines
- Follow Arduino coding standards
- Add comments for complex functions
- Test thoroughly before submitting
- Update documentation for new features

---

## 📚 Technical Resources

### Datasheets & References
- [MQ-135 Sensor Datasheet](https://www.electronicoscaldas.com/datasheet/MQ-135_Hanwei.pdf)
- [Arduino Uno R3 Specifications](https://docs.arduino.cc/hardware/uno-rev3)
- [16x2 LCD Display Guide](https://www.arduino.cc/en/Tutorial/LibraryExamples/LiquidCrystalDisplay)

### Learning Resources
- [Air Quality Index (AQI) Standards](https://www.airnow.gov/aqi/aqi-basics/)
- [Arduino Programming Tutorial](https://www.arduino.cc/en/Tutorial/HomePage)
- [Environmental Monitoring Best Practices](https://www.epa.gov/air-quality-management-process)

---

## ⚖️ License & Legal

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

### Disclaimer
- This device is for **educational and monitoring purposes only**
- **Not certified** for professional environmental assessment
- Always consult professional equipment for critical applications
- Users assume responsibility for proper calibration and interpretation

---

## 👨‍💻 Author & Contact

**Abhijith R Pillai** (@p1ll3chan)
- 🏫 Amrita Vishwa Vidyapeetham, Amritapuri Campus
- 📧 Email: [am.en.u4mee23002@am.students.amrita.edu](mailto:am.en.u4mee23002@am.students.amrita.edu)
- 💼 LinkedIn: [abhijith-r-pillai-p1ll3chan](https://www.linkedin.com/in/abhijith-r-pillai-p1ll3chan/)
- 🐙 GitHub: [p1ll3chan](https://github.com/p1ll3chan)

---

## 🙏 Acknowledgments

- **Arduino Community**: For extensive libraries and support
- **Amrita University**: For providing resources and guidance  
- **Environmental Engineers**: For air quality standards and best practices
- **Open Source Community**: For inspiration and collaborative development

---

<div align="center">

### 🌱 "Monitoring air quality today for a cleaner tomorrow!" 🌱

![GitHub stars](https://img.shields.io/github/stars/p1ll3chan/Mini-Mobile-Air-Monitoring-System?style=social)
![GitHub forks](https://img.shields.io/github/forks/p1ll3chan/Mini-Mobile-Air-Monitoring-System?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/p1ll3chan/Mini-Mobile-Air-Monitoring-System?style=social)

**⭐ If this project helped you, please give it a star! ⭐**

</div>
