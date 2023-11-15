# LYH-s-plant
1. ESP8266 link to WIFI and MQTT and sent data to MQTT
   
   According to the workshop step 2 to 7, the ESP8266 module would be linked to the wifi in lab and sent data to MQTT every minute. The first step is link to wifi. After set the name and password of wifi in the lab and the command of WiFi.begin & WiFiClient, the ESP6288 could through WIFI touch the Internet and return the IP and time to Serial monitor with the library of ESP8266WiFi.h and ezTime.h.

   After ensuring that the ESP8266 is successfully linked to the network, the module will link with the MQTT server through the MQTT user name, password, images, and callback function, and publish the information to the MQTT server using the sendMQTT function. The code already upload to file of "code". The results of successful operation are as follows:
   <img width="450" alt="db8bf08a6c5cb95a36ae0d32736e350" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/926df38d-ea6c-491f-8658-adef8d50a8a1">
   <img width="450" alt="image" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/c2ec9b6b-0ef1-431f-aab5-4e2198d78b70">


2. The sensor is used on the ESP8266 and the measured values are sent to the MQTT
   
   I connected the ESP8266 module to the sensor of the dht series through the DHT.h and DHT-U.h libraries and set the corresponding pin to input mode. To measure ambient temperature, humidity and moisture. The serial port plotter displays the following measurement results:
   <img width="900" alt="image" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/0a9e1e09-81d3-4aab-b096-3ed79dd5b4bf">
   
   After verifying that the measurement was successful. The code in the sensor measurement section will be combined with the code in the previous section MQTT. To upload the measurement value to a specific topic in the MQTT server. Finally, on the serial port monitor side, and MQTT browser side. All the measured values were detected successfully, which proved that this part of the experiment was successful and the combined code is uploaded to the code file.
   
   <img width="450" alt="ec4286a0f30143c0cf2b718006abfe1" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/70b7afc8-671f-4a0f-9b06-c729be1c0dd9">
   <img width="450" alt="d3a71c4efc587d854a4998c3c1995fc" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/b4c79f90-773f-4141-a16e-5202fc7e0f22">


3. Configure Raspberry PI to be a cloud server and gateway

   According to the instructions of workshop 9-15, I used SSH to access Raspberry PI after flashing the SD card, installed InflusxDB and other software on it. To realize the operation of data visualization on web page with the Raspberry PI which as the gateway. After obtaining the API token of Raspberry PI in the InflusxDB software and completing the related Settings in Raspberry PI. The page could access data of PI through this token and display it on the web.

   <img width="900" alt="90ee7bda15e5f003f9a954fc95877bf" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/340e24e3-e256-4493-bd43-5c865d45794a">

   Similarly, after the configuration file of Telegraf is completed in PI, the web page can use the Raspberry PI as a springboard to read the data which uploaded by ESP to MQTT and display it.

   <img width="900" alt="ec138ef47de70f71466b254060d0ba8" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/853d6ba2-0781-4112-af13-b825bdfc35a6">
  
   Under Grafana, the data can be displayed more intuitively.

   <img width="900" alt="9083b44bc4e6cb810ed6d632cbb82d4" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/877e4b72-1032-4934-89a6-f3aa521296f3">  
  
   The configuration of related files has been uploaded to the code file.
   

4. Usse I2C to realize the communication between ESP8266 and Arduino

   I wanted to show the data measured by the ESP8266 in a physical way in the real world. However, the ESP does not have enough PIN connection for the output, such as the LCD screen. Therefore, I transmit the data of ESP8266 to Arduino through I2C wired connection to get enough output pin.

   After connecting the ESP to the Arduino with SCL and SDA PINs of them. The Esp was set as the sending end and transmited the measured value to the Arduino which as the receiving end. The Arduino would store the received data in different addresses to achieve signal transmission between the two. The result is shown as follows:

   <img width="900" alt="image" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/b3d66691-beba-419f-b8a2-081e93b56e1b">

   The code to implement the I2C communication has been uploaded to the code file.


5. LCD display on Arduino

   After the information is passed to the Arduino, I need to display it through the LCD1602. An LCD can display 16 by 2 characters. The LCD has multiple pins, each PIN has the following functions:

   <img width="900" alt="image" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/cf587a05-bed8-449d-8508-fe383cf9b1fc">

   The LCD has 4-bit and 8-bit operating modes, and in 4-bit operating mode, only four pins need to be connected as inputs. And set the other two pins to set the read/write status and Register selection bits respectively. The connection between the LCD and Arduino is as follows:

   <img width="900" alt="image" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/e4639220-7bf6-4a3a-9f9e-9c1221c2d477">

   After the relevant codes are load into Arduino, the display results are shown in the following figure (code already upload to github):

   ![639d4d6e9eeb816c7bca4bed9d75ad0](https://github.com/zczqy80/LYH-s-plant/assets/146266229/7423f8a4-e2e7-488e-b8d0-a63645509539)


6. Final part: Display measure value on LCD

   The goal of the project is to use the ESP8266 and the sensor to collect data and upload it to the MQTT server and display it simultaneously on the LCD screen. So the project can be divided into two parts.

   The first part is ESP8266 and includes the code for Parts 2 and 4. The ESP continuously measures the data and connects to WiFi to upload the measured values to a specific topic on the MQTT server. At the same time, the measurement data is transmitted to the Arduino via I2C.

   The second part is Arduino and includes the code for Parts 4 and 5. Once the Arduino receives the data, it will display the data on the LCD screen. The result is as follows:

![ed4160109b36ff833e37327adcda3eb](https://github.com/zczqy80/LYH-s-plant/assets/146266229/c4432ffb-22f0-486c-9346-93a6aa0bd136)


   The code for this section has been uploaded. Hopefully, more output can be added in the future. Such as the use of LEDs to indicate changes in temperature, and the addition of buzzers to remind the addition of water. That's all, thanks for your reading.
