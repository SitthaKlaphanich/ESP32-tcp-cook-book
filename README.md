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

3.2 เพิ่ม #include "driver/gpio.h" และกำหนดขา LED #define LED  23

![image](https://github.com/user-attachments/assets/b59e9ee6-4e50-47e9-9f1e-b2fb174be501)


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

3.4 เพิ่มการทำงานเงื่อนไข LED ใช้ strstr ไว้ใช้ค้นหาสตริงหรืออักขระในสตริงที่กำหนด เพิ่ม code ใน case MQTT_EVENT_DATA
```
if (strncmp(event->topic, "KMITL/Sittha/LED", event->topic_len) == 0) {
            printf("Topic matched\r\n" );
            if (strstr(event->data, "ON") != NULL) {
                printf("LED ON\r\n" );
                gpio_set_level(LED, 1); // Turn ON LED
            } else if (strstr(event->data, "OFF") != NULL) {
                printf("LED OFF\r\n" );
                gpio_set_level(LED, 0); // Turn OFF LED
            }
        }
```
![image](https://github.com/user-attachments/assets/9467f1af-87af-45c1-9852-ba18f39939a1)

3.5 เพิ่มลงในฟังชั่น void app_main เพื่อให้กำหนด LED ได้ หลังจากนั้น build flash 
```
gpio_set_direction(LED, GPIO_MODE_OUTPUT); 
```
![image](https://github.com/user-attachments/assets/5212e95a-b5d7-4f6d-9ffe-4d41b665812b)

3.5 โหลด mqtt ผ่านเว็บ และเข้า mqtt ที่ได้กำหนดไว้ตั้งแต่ตอนต้น 

https://mqtt-explorer.com/

![image](https://github.com/user-attachments/assets/419cab91-3d34-4ab2-8eb3-1a3b90927231)

3.6 กำหนด path ของ Topic ให้ตรวตามที่กำหนดไว้ใน code 

![image](https://github.com/user-attachments/assets/a6cb69e1-9d57-46e9-b117-061842a2c738)


3.7 จากนั้นกด Pubilsh จะได้ตามภาพ

![image](https://github.com/user-attachments/assets/a1ae0bde-a42b-4851-89a8-163598393d60)

4.ผลลัพธ์การทำงาน 

ON

![image](https://github.com/user-attachments/assets/a1ae0bde-a42b-4851-89a8-163598393d60)

![image](https://github.com/user-attachments/assets/154e9d5e-b124-4083-9b3a-01275e1db52a)

OFF

![image](https://github.com/user-attachments/assets/13f4ce25-25d2-4afb-91c7-c87198fbecf1)

![image](https://github.com/user-attachments/assets/c96f4415-70ee-4886-9e1d-1733d0a64cfb)

5.ESP32 สามารถเชื่อมต่อไปยัง MQTT ได้สามารถส่งข้อมูลการทำงานไปยัง MQTT ได้อีกทั้ง MQTT ยังสามารถ สั่งการ
   ทำงาน ESP32 ได้อีกด้วย
