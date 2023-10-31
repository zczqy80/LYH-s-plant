# LYH-s-plant
1. ESP8266 link to WIFI and MQTT and sent data to MQTT
   According to the workshop step 2 to 7, the ESP8266 module would be linked to the wifi in lab and sent data to MQTT every minute. The first step is link to wifi. After set the name and password of wifi in the lab and the command of WiFi.begin & WiFiClient, the ESP6288 could through WIFI touch the Internet and return the IP and time to Serial monitor with the library of ESP8266WiFi.h and ezTime.h.

   After ensuring that the ESP8266 is successfully linked to the network, the module will link with the MQTT server through the MQTT user name, password, images, and callback function, and publish the information to the MQTT server using the sendMQTT function. The code already upload to file of "code". The results of successful operation are as follows:
<img width="213" alt="db8bf08a6c5cb95a36ae0d32736e350" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/926df38d-ea6c-491f-8658-adef8d50a8a1">
<img width="262" alt="image" src="https://github.com/zczqy80/LYH-s-plant/assets/146266229/c2ec9b6b-0ef1-431f-aab5-4e2198d78b70">

