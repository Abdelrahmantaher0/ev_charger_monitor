EV CHARGER BLE MONITOR — ANDROID CHROME INSTALLABLE WEB APP

This is a working Web Bluetooth app rather than a MIT App Inventor .aia project.
It is built for the ESP-IDF ble_uart_service Nordic UART-style GATT service.

TO RUN ON YOUR PHONE:
1. Publish the contents of this folder on an HTTPS web host (e.g. GitHub Pages or Netlify Drop).
2. Open the HTTPS link on Android Chrome (not an in-app browser).
3. Allow Bluetooth permissions; turn Bluetooth on.
4. Power your ESP32-S3 firmware ble_uart_service.
5. Tap Connect BLE, choose BleUart-xxxx, confirm connection.
6. Tap STATUS to send CMD:STATUS, START to send CMD:START, STOP to send CMD:STOP.
7. Incoming ESP32 TX notifications populate metrics and graph.
8. Chrome's Add to Home Screen/Install App provides an app icon.

IMPORTANT:
- BLE UUIDs are editable on the page; default NRF UART-style UUIDs:
  Service 6e400001-b5a3-f393-e0a9-e50e24dcca9e
  RX write 6e400002-b5a3-f393-e0a9-e50e24dcca9e
  TX notify 6e400003-b5a3-f393-e0a9-e50e24dcca9e
- Current ESP-IDF echo firmware only echoes phone messages. For real graphs the ESP32
  must SEND NOTIFICATIONS periodically, e.g.
  STATE=CHARGING,V=398,I=76,SOC=55,E=8.4,FAULT=NONE\n
- Typical 20-byte ATT notification chunks are handled by a short collection interval.
  Add newline delimiters to frames for robust framing in the final firmware.
- The chart can be previewed with Try demo data without connecting to hardware.
- Without HTTPS Web Bluetooth will NOT work. Opening the local file directly is
  sufficient for previewing demo visuals but not real BLE.
- This is not a safety controller. STM32 must validate any commands and independently
  enforce safety and power interlocks.
- Web Bluetooth is intended for Chromium browsers on supported Android devices;
  it is not generally available on iOS Safari.

ALL GRAPHS VERSION: Power, voltage, current and SOC graphs are simultaneously visible. No graph selector.

VERSION 3 FIX:
- Charging Power (kW) is calculated from voltage (V) and current (A) for DC charging: P = V * I / 1000.
- A supplied P= value overrides the calculated result for that particular incoming message.
- Chart history is updated before graphs are redrawn, fixing one-sample delay.
- Offline service-worker cache upgraded. When using an old HTTPS deployment, replace all files and reload the page.
