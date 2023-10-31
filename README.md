# LYH-s-plant
1. ESP8266 link to WIFI and MQTT and sent data to MQTT
   According to the workshop step 2 to 7, the ESP8266 module would be linked to the wifi in lab and sent data to MQTT every minute. The first step is link to wifi. After set the name and password of wifi in the lab and the command of WiFi.begin & WiFiClient, the ESP6288 could through WIFI touch the Internet and return the IP and time to Serial monitor with the library of ESP8266WiFi.h and ezTime.h.

   After ensuring that the ESP8266 is successfully linked to the network, the module will link with the MQTT server through the MQTT user name, password, images, and callback function, and publish the information to the MQTT server using the sendMQTT function. The code already upload to file of "code". The results of successful operation are as follows:
<img width="213" alt="db8bf08a6c5cb95a36ae0d32736e350" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/926df38d-ea6c-491f-8658-adef8d50a8a1">
<img width="262" alt="image" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/c2ec9b6b-0ef1-431f-aab5-4e2198d78b70">


2. The sensor is used on the ESP8266 and the measured values are sent to the MQTT
   I connected the ESP8266 module to the sensor of the dht series through the DHT.h and DHT-U.h libraries and set the corresponding pin to input mode. To measure ambient temperature, humidity and moisture. The serial port plotter displays the following measurement results:
   <img width="618" alt="image" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/0a9e1e09-81d3-4aab-b096-3ed79dd5b4bf">
   
   After verifying that the measurement was successful. The code in the sensor measurement section will be combined with the code in the previous section MQTT. To upload the measurement value to a specific topic in the MQTT server. Finally, on the serial port monitor side, and MQTT browser side. All the measured values were detected successfully, which proved that this part of the experiment was successful and the combined code is uploaded to the code file.
   
   <img width="215" alt="ec4286a0f30143c0cf2b718006abfe1" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/70b7afc8-671f-4a0f-9b06-c729be1c0dd9">
<img width="270" alt="d3a71c4efc587d854a4998c3c1995fc" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/b4c79f90-773f-4141-a16e-5202fc7e0f22">

3. Configure Raspberry PI to be a cloud server and gateway

   According to the instructions of workshop 9-15, I used SSH to access Raspberry PI after flashing the SD card, installed InflusxDB and other software on it. To realize the operation of data visualization on web page with the Raspberry PI which as the gateway. After obtaining the API token of Raspberry PI in the InflusxDB software and completing the related Settings in Raspberry PI. The page could access data of PI through this token and display it on the web.

   <img width="1167" alt="90ee7bda15e5f003f9a954fc95877bf" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/340e24e3-e256-4493-bd43-5c865d45794a">

   Similarly, after the configuration file of Telegraf is completed in PI, the web page can use the Raspberry PI as a springboard to read the data which uploaded by ESP to MQTT and display it

  <img width="1173" alt="ec138ef47de70f71466b254060d0ba8" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/853d6ba2-0781-4112-af13-b825bdfc35a6">
  
   Under Grafana, the data can be displayed more intuitively.

  <img width="509" alt="9083b44bc4e6cb810ed6d632cbb82d4" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/877e4b72-1032-4934-89a6-f3aa521296f3">  
  
   The configuration of related files has been uploaded to the code file.

4. Usse I2C to realize the communication between ESP8266 and Arduino

   I wanted to show the data measured by the ESP8266 in a physical way in the real world. However, the ESP does not have enough PIN connection for the output, such as the LCD screen. Therefore, I transmit the data of ESP8266 to Arduino through I2C wired connection to get enough output pin.

   After connecting the ESP to the Arduino with SCL and SDA PINs of them. The Esp was set as the sending end and transmited the measured value to the Arduino which as the receiving end. The Arduino would store the received data in different addresses to achieve signal transmission between the two. The result is shown as follows:

  <img width="925" alt="image" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/b3d66691-beba-419f-b8a2-081e93b56e1b">

  The code to implement the I2C communication has been uploaded to the code file.
