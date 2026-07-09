# IOT Plant Watering Monitor
Forget to water your plants or having fun on vacation, don't worry about your plants. With this futuristic plant monitor, your plants stay healthy with an auto watering system, that can detect when the soil is dry. With a 3d printed case and a screen showing moisture level and a diagram of the soil, everything will be ok. 


| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Praneeth S | Valley Christiain High School| Mechanical Engineering | Incoming Freshman

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



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
<img width="682" height="517" alt="Screenshot 2026-07-08 at 2 50 32 PM" src="https://github.com/user-attachments/assets/22209b84-deec-4a88-ad50-ed21b7c02eab" />

This diagram at the top shows the inner workings of my plant monitoring and self watering system and how it will look. This wiring diagram taught me how to connect the wires in the right place. 
This screenshot shows my CAD design for my 3d print. 



# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
/*
 * This Arduino UNO R4 code was developed by newbiely.com
 *
 * This Arduino UNO R4 code is made available for public use without any restriction
 *
 * For comprehensive instructions and wiring diagrams, please visit:
 * https://newbiely.com/tutorials/arduino-uno-r4/arduino-uno-r4-soil-moisture-sensor
 */

#define AOUT_PIN A0 // Defines pin A0 to read from the moisture sensor

void setup() {
  Serial.begin(9600); // Initializes serial communication at 9600 bps
}

void loop() {
  int value = analogRead(AOUT_PIN); // Reads the moisture level from the sensor

  Serial.print("Moisture: "); // Sends the text 'Moisture: ' to the serial monitor
  Serial.println(value); // Prints the moisture level to the serial monitor

  delay(500); // Pauses the loop for 500 milliseconds
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


