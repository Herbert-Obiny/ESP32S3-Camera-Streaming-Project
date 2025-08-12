# ESP32S3-Camera-Streaming-Project
ESP32S3 Camera Streaming Project
This project streams video from a Seeed Studio XIAO ESP32S3 camera module over Wi-Fi, allowing real-time viewing in a browser.
Features
- Streams live video over Wi-Fi.
- Compatible with Seeed Studio XIAO ESP32S3.
- Simple browser-based viewing.
- Works on Linux, Windows, and Mac.
Hardware Requirements
- Seeed Studio XIAO ESP32S3 camera module
- USB-C cable
- Wi-Fi network (2.4GHz)
Software Requirements
- Arduino IDE 2.x
- ESP32 board support installed
- Required libraries: esp32-camera, WiFi
Download and install arduino if not already.
1. Install Arduino IDE (if not already)
   Download from: https://www.arduino.cc/en/software
2. Install the ESP32 board support
    Open Arduino IDE.
    Go to File > Preferences.
    In “Additional Board Manager URLs”, paste:
https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
Click OK.
Go to Tools > Board > Boards Manager.
Search for esp32, click Install on “ESP32 by Espressif Systems”.
3. Select the XIAO ESP32S3 Board
    Go to Tools > Board > ESP32 Arduino > XIAO_ESP32S3 (if not available, use ESP32S3 Dev Module).
    Under Tools, set the following:
        USB CDC On Boot: Enabled
        Upload Mode: UART0 / Hardware CDC
        PSRAM: Enabled
        Partition Scheme: Huge APP (3MB No OTA)
        Flash Mode: QIO
        Flash Frequency: 80 MHz
        Core Debug Level: None
        Erase All Flash: Disabled
4. Connect Your Device
    Use a data-capable USB-C cable.
    Your board should show as something like /dev/ttyACM0 or /dev/ttyUSB0.
If nothing appears, double-tap the reset button to enter bootloader mode.
5. Set Wi-Fi Credentials
Update these lines in your sketch:
const char *ssid = "YourNetworkName(WIFI)";
const char *password = "YourPassword";

6. Create camera_pins.h
Create a new tab in Arduino IDE:
Sketch > Add File > New Tab, name it: camera_pins.h
Paste the following pin definitions:

<pre>
   #ifndef CAMERA_PINS_H 
   #define CAMERA_PINS_H 
   #define PWDN_GPIO_NUM -1 
   #define RESET_GPIO_NUM -1 
   #define XCLK_GPIO_NUM 10 
   #define SIOD_GPIO_NUM 40 
   #define SIOC_GPIO_NUM 39 
   #define Y9_GPIO_NUM 48 
   #define Y8_GPIO_NUM 11 
   #define Y7_GPIO_NUM 12 
   #define Y6_GPIO_NUM 14 
   #define Y5_GPIO_NUM 16 
   #define Y4_GPIO_NUM 18 
   #define Y3_GPIO_NUM 17 
   #define Y2_GPIO_NUM 15 
   #define VSYNC_GPIO_NUM 38 
   #define HREF_GPIO_NUM 47 
   #define PCLK_GPIO_NUM 13 
   #define LED_GPIO_NUM -1 // Set to real pin if LED exists eg 21 #endif  </pre>

7. Upload the Sketch
    Go to Tools > Port and select the correct /dev/ttyACM* or COM* port.
    Click the Upload button (right arrow).
If it fails:
    Double-tap the reset button to enter bootloader mode.
    Re-select the port and upload again.
   
 8. Open Serial Monitor
    Go to Tools > Serial Monitor
    Set baud rate to 115200
    You should see:
    WiFi connected
    Camera server started (dummy)
    Camera Ready! Use 'http://192.168.x.x' to connect
9. Access the Stream
Open your browser and go to the IP address shown in the serial monitor:
http://192.168.x.x

#OPTION TWO
File > Examples > ESP32 > Camera > CameraWebServer
