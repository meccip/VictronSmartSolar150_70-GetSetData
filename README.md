# Node-Red Victron SmartSolar 150/70 - serial or MQTT connection

Receive/SET/GET data from **Victron SmartSolar 150/70** using Node-Red Serial or mqtt.

Install **[node-red-node-serialport](https://flows.nodered.org/node/node-red-node-serialport)**

Import j.son file into Node-Red.

You will receive data every second until you stop the serial port. You can chose for mqtt node to connect with mppt.<br>
Any way you will need a cable ve.direct from mppt and serial or esp device if you chose for mqtt. You can buy or make one, there is some photo into file area. Use ADUM1201 as isolator between mppt and device. There is an yaml file for esp s2mini if you use esphome, but you can modify it for esp01, d1 mini or any...

You ca **SET** some values:

If you send a payload **[0....70]** with topic **set_charge_current** you can set charge current<br>
You can set Absortion Voltage if you send payload **[55.4....]** with topic **set_absorption_voltage**<br>
You can set Float Voltage if you send payload **[55.4....]** with topic **set_float_voltage**<br>
You can control mppt ON/OFF if you send a payload **[1 for ON and 4 for OFF]** with topic **set_device_mode**<br>

You can **GET** values state if you inject a node with topic:

**get_charge_current** for charge current value<br>
**get_float_voltage** for float voltage value<br>
**get_absorption_voltage** for absorb voltage<br>
**get_device_mode** for device mode state<br>

For MQTT to send command to mppt add mqtt node and replace serial node IN/OUT and set topic to **victron_esp32/command/send_raw**<br>
To receive data add mqttIN node and replace serial node and set topic to **victron_esp32/telemetry/raw**

![serial](https://github.com/user-attachments/assets/e15672b2-0e73-4b19-bd79-4d2ba6b8bd39)

**Data that you will receive:**
- Product ID
- Firmware Version
- Serial Number
- Battery Voltage
- Battery Current
- Solar Voltage
- Solar Current calculated by function not received from controller
- Solar Power
- Charging Mode
- Tracking Mode
- Errors
- Running Days
- Max Solar Power Today
- Max Solar Power Yesterday
- Yield Today
- Yield Yesterday
- Yield Total
- Max charge current state [after GET command]
- Absorb voltage value [after GET command]
- Float voltage value [after GET command]
- Device Mode ON/OFF [after GET command]
- and you can add more if you read **[ve.direct protocol](https://www.victronenergy.com/upload/documents/VE.Direct-Protocol-3.33.pdf)**
