# ESP32-tcp-cook-book

1.ESP-IDF Example

เลือก tcp ที่หัวข้อ mqtt หลังจากนั้นกด Create project

![image](https://github.com/user-attachments/assets/a473f80d-6b3d-4ff6-b2e2-958fd2c642a6)

2.ตั้งค่า ESP-IDF: SDK configuration editor (menuconfig) ให้เชื่อมกับ broker และแก้ในส่วนชื่อ
MQTT_EVENT_CONNECTED เพื่อให้รู้ว่าเป็นข้อมูลของเรา และ เพิ่มการ sub จาก led เพื่อสั่งการ ให้ led
ทำตาม sub mqtt 

![image](https://github.com/user-attachments/assets/d6f2592b-f2e0-4c0a-a390-47ecff95a9d2)

3.กำหนด ESP-IDF: SDK configuration editor (menuconfig) ตรวจสอบการตั้งค่าในส่วน Example Configuration 

3.1 กำหนด Broker URL ตามในภาพ และ WiFi SSID WiFi Password ของผู้ใช้

![image](https://github.com/user-attachments/assets/29bed324-96ad-4b9f-8f4f-dd63f96e76ce)

3.2 กำหนดชื่อของตัวเองใน MQTT_EVENT_CONNECTED

![image](https://github.com/user-attachments/assets/c1aa5390-e93a-4e8a-8bc2-e70a560bf17d)

3.3 copy code เและเปลี่ยนชื่อเป็น KMITL/Sittha/LED ตามที่ตัวเองกำหนด อยู่ในฟังก์ชัน mqtt_event_handler
```
msg_id = esp_mqtt_client_subscribe(client, "KMITL/Sittha", 1);
ESP_LOGI(TAG, "sent subscribe successful, msg_id=%d", msg_id);
```

```
msg_id = esp_mqtt_client_subscribe(client, "KMITL/Sittha/LED", 1);
ESP_LOGI(TAG, "sent subscribe successful, msg_id=%d", msg_id);
```

![image](https://github.com/user-attachments/assets/c32ab21a-d4be-4037-974b-8016d55656eb)


