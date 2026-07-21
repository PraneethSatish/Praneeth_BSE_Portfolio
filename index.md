# IOT Plant Watering Monitor
Forget to water your plants or having fun on vacation, don't worry about your plants. With this futuristic plant monitor, your plants stay healthy with an auto watering system, that can detect when the soil is dry. With a 3d printed case and a screen showing moisture level and a diagram of the soil, everything will be ok. 


| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Praneeth S | Valley Christiain High School| Mechanical Engineering | Incoming Freshman

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

- For my 3rd milestone, I was able to complete many new things. I have created a 3d print enclosure. This will house all my components, and has holes for the USB - C, and a platform for the arduino where you can see the expressions being relayed on soil and water moisture. I hae also taken a few days to work and debug code for the expressions, so that depending on the moisture the sensor is reading, the expressions will be happy, sad, or neutral. I have also been able to setup thr BLYNK App where I can control the water sensor and watering machine remotely. 
- My biggest challenge was trying to keep the code working while making different modifications. It also took a lot of researching to learn how to set up the BLYNK App. 
- I learned how to really apply my skills on ONSHAPE, how to code different pieces of engineering on Arduino IDE, and I even learned how to make sure my components are stable without my help. 
- I hope to learn how to make a working screen, and get this idea out into the real world of innovation and entreprenuership. 



# Second Milestone
<iframe width="560" height="315" src="https://www.youtube.com/embed/InGHRm_oWCo?si=Tfs3ni-HGRzLjzwi" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
- The code was designed to make the soil moisture sensor work. This code will be able to tell me when a plant is ok or in need of water. It took just one day, of looking through diagrams and past work, to find and connec the right code. After an hour of debugging, the code worked, and now I am able to calibrate soil moisture. 
- The code being so easy to finish was very surprising, especially in C#, because the syntax and indentation being very complex. I was able to find the source code, and easily ge the base code for my sensor. 
- I overcame my fear of coding, and while it may sound childish, I always believed I am not able to code, and this was very empowering for me, because I was able to learn a lot more on the language, and I was able to calibrate soil sensors and their inner - workings. 
- I need to connect the water pump, and I need to be able to relay expressions. 

# First Milestone
<iframe width="560" height="315" src="https://www.youtube.com/embed/LAsJ_gsJFeg?si=NwBSCBkvz6XWBHNg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
For your first milestone, describe what your project is and how you plan to build it. You can include:
- My project includes a 5V Relay Module, a capacitive soil moisture sensor, a water pump, and an Arduino UNO R4. These components work perfectly together with my laptop (the external power source), to monitor soil moisture. When the water pump is connected, it will mtor water from a bowl or bucket into the plant when needed and will perfectly add the certain amount of water needed. The relay module is like the messenger, packaging messages and data between the arduino and laptop and the soil sensor and the water pump. With everything working otgether, a plant will be rightfully taken care of. 
- I have finished the code for the soil moisture sensor and the relay module to tell accurate information to the laptoo. I am able to understand soil moisture. 
- The water pump requires mutiple layers of soldering to fuly connect, and the motor must be perfectly screwed in to fix. I am still working on fixing the code for the water pump also. 
- I am planning to finish my main project by the 3rd week. Modifications will be tough, and will take at least 2 weeks to complete. 

# Schematics 
<img width="1562" height="500" alt="image" src="https://github.com/user-attachments/assets/49f7b9c0-5fda-4124-a5d6-da3216c4634e" />
<img width="410" height="405" alt="Screenshot 2026-07-09 at 4 07 17 PM" src="https://github.com/user-attachments/assets/8a3e47f8-7629-4d64-8fce-e74664d25a7b" />
<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/49232e0e-5db5-4dd8-85e1-0ae113b99997" />


This diagram at the top shows the inner workings of my plant monitoring and self watering system and how it will look. This wiring diagram taught me how to connect the wires in the right place. 
This screenshot shows my CAD design for my 3d print. 



# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
#define BLYNK_TEMPLATE_ID "TMPL2D3vwtsqU"
#define BLYNK_TEMPLATE_NAME "plant watering updated"
#define BLYNK_AUTH_TOKEN "z4wL7XeK3TLpwUoy5LRbItaJMjz4lidk"

#include <BlynkSimpleWifi.h>
#include <EEPROM.h>
#include "Arduino_LED_Matrix.h" // Required library for the Uno R4 LED matrix

#define moisture_sensor A0 
#define relay 7 

// 1. CALIBRATION VALUES: Change these based on your specific sensor tests
const int DRY_VALUE = 3800;  // Value in open air (dry)
const int WET_VALUE = 1800;  // Value in water (wet)

BlynkTimer timer; 
ArduinoLEDMatrix matrix; 

char ssid[] = "J11"; 
char pass[] = "Blue@J11"; 

int eeprom_addr = 0; 
int sensorValue = 0; 
int prev_pump_status = 0; 
int pump_status = 0; 
float moist_percent = 0.00; 

// LED Frames
const uint32_t HAPPY_LED[] = { 0x3fc48a95, 0x58019fd9, 0x5889871 }; 
const uint32_t NORMAL_LED[] = { 0x3fc40298, 0xd98d8019, 0x5889871 }; 
const uint32_t SAD_LED[] = { 0x3fc48a9d, 0xd8898018, 0x71889905 }; 

BLYNK_WRITE(V1){ 
  pump_status = param.asInt(); 
  EEPROM.write(eeprom_addr, pump_status); 
  prev_pump_status = EEPROM.read(eeprom_addr); 
  Serial.println(prev_pump_status); 
  Serial.println(pump_status); 
} 

void sendSensor(){ 
  Blynk.virtualWrite(V0, moist_percent); 
} 

void init_renesas_MCU_IO(){ 
  pinMode(relay, OUTPUT); 
  pinMode(moisture_sensor, INPUT); 
  analogReadResolution(12); // Sets 12-bit resolution (0-4095 range)
  matrix.begin(); 
} 

void track_soil_moisture(){ 
  sensorValue = analogRead(moisture_sensor); 
  
  // Maps the 12-bit input value directly to a 0-100 percentage scale
  moist_percent = map(sensorValue, DRY_VALUE, WET_VALUE, 0, 100); 
  moist_percent = constrain(moist_percent, 0, 100); 

  Serial.print("Raw Sensor Value: "); 
  Serial.print(sensorValue); 
  Serial.print(" | Moisture: "); 
  Serial.print(moist_percent); 
  Serial.println("%"); 

  if(moist_percent >= 0 && moist_percent < 33.33){ 
    Serial.println("DRY"); 
    matrix.loadFrame(SAD_LED); 
  } 
  else if(moist_percent >= 33.33 && moist_percent < 66.66){ 
    Serial.println("MODERATE"); 
    matrix.loadFrame(NORMAL_LED); 
  } 
  else if(moist_percent >= 66.66 && moist_percent <= 100){ 
    Serial.println("WET"); 
    matrix.loadFrame(HAPPY_LED); 
  } 
} 

void setup() { 
  Serial.begin(9600); 
  init_renesas_MCU_IO(); 
  
  // Populates data variables right away before loops fire
  track_soil_moisture(); 
  
  Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass); 
  timer.setInterval(1000L, sendSensor); 
  
  prev_pump_status = EEPROM.read(eeprom_addr); 
  pump_status = prev_pump_status; 
} 

void loop() { 
  Blynk.run(); 
  timer.run(); 
  track_soil_moisture(); 
  
  if(pump_status == 0){ 
    Serial.println("Water pump is off"); 
    digitalWrite(relay, LOW); 
  } 
  else if(pump_status == 1){ 
    Serial.println("Water pump is on"); 
    digitalWrite(relay, HIGH); 
  } 
  delay(500); 
}



```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| 5V Relay Module | Packages Information through sources | $1.01 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Capacitive Soil Sensor | Monitors Soil Moisture | $3.47 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Arduino UNO R4 Wifi | To relay expressions to me on how the plant is feeling, connect to laptop code, connect all components together | $27.50 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| 5V Water Pump | To pump water from bowl to plant | $1.12 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |

# Other Resources/Examples
- [DIY Plant Watering Setup]([https://trashytuber.github.io/YimingJiaBlueStamp/](https://circuitdigest.com/microcontroller-projects/build-a-simple-plant-watering-system-using-arduino#how-to-make-an-automatic-plant-watering-system))
- [OnShape]([https://sviatil0.github.io/Sviatoslav_BSE/](https://cad.onshape.com/documents?resourceType=resourcecompanyowner&nodeId=6a4587586d2bd086b9c24146))
- [Blynk Setup]([https://blynk.cloud/dashboard/336066/templates/edit/744946/dashboard](url)

