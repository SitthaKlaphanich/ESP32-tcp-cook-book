# ESP32-tcp-cook-book

1.ESP-IDF Example

เลือก tcp ที่หัวข้อ mqtt หลังจากนั้นกด Create project

![image](https://github.com/user-attachments/assets/a473f80d-6b3d-4ff6-b2e2-958fd2c642a6)

2.ตั้งค่า ESP-IDF: SDK configuration editor (menuconfig) ให้เชื่อมกับ broker และแก้ในส่วนชื่อ
MQTT_EVENT_CONNECTED เพื่อให้รู้ว่าเป็นข้อมูลของเรา และ เพิ่มการ sub จาก led เพื่อสั่งการ ให้ led
ทำตาม sub mqtt 

![image](https://github.com/user-attachments/assets/d6f2592b-f2e0-4c0a-a390-47ecff95a9d2)

