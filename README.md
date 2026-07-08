# TemHu
Tem(H)u stands for Temperature + Humidity — a compact ambient sensor display
showing temperature, humidity and a clock, based on ESPHome +
Waveshare ESP32-S3 AMOLED Touch Display

License: GPL v3
Version
ESPHome

Table of Contents
Required Hardware
Connecting the Sensor
Flashing the Firmware
Wi-Fi Setup
Accessing the Web Interface
Updates (OTA)
User Interface
Settings
Maintenance & Troubleshooting
1. Required Hardware
Display
Choose one of the following displays:

Model	Waveshare Shop	Amazon
Tem(H)u Nano — Waveshare ESP32-S3 Touch AMOLED 1.43"	waveshare.com	amazon.de
Tem(H)u Macro — Waveshare ESP32-S3 Touch AMOLED 1.75"	waveshare.com	amazon.de
Sensor
Component	Link
SHT31 Temperature & Humidity Sensor	amazon.de
USB Cable & Power Supply
Component	Link
USB-C Extension (angled)	amazon.de
IMPORTANT

The Amazon link leads to an angled USB-C extension. When using this extension, power can only be supplied via a USB-C to USB-A cable — USB-C to USB-C in combination with the extension does not work.

Alternatively, a directly angled USB-C cable may be used (untested).

Additional Accessories
Dupont jumper cables (Male–Female) for the SHT31 on the 8-pin header of the Tem(H)u Macro
SH1.0 4-pin cable for the I2C connector of the Tem(H)u Nano (solder SHT31 to cable)
2. Connecting the Sensor (SHT31 → Display)
IMPORTANT

Connect the sensor before the first flash. The display does not need to be powered while connecting the cables.

Connection — Tem(H)u Nano (1.43")
The Tem(H)u Nano has a SH1.0 4-pin I2C connector (JST SH1.0, 1mm pitch). The SHT31 must be soldered to a matching SH1.0 cable. Pin assignment:

SHT31 Pin	GPIO	Function
VCC	3.3V	Power supply
GND	GND	Ground
SDA	GPIO 47	I2C Data
SCL	GPIO 48	I2C Clock
NOTE

The board also features a 2×14-pin GPIO header (1.27mm) with GPIO 38 (SCL) and GPIO 39 (SDA). This connection option via jumper cable is supported as a second I2C bus from firmware 2.0.0 onwards — no soldering required.

Connection — Tem(H)u Macro (1.75")
The Tem(H)u Macro has a dedicated 8-pin header for external sensors (Bus B). Connect via Dupont jumper cable (Male–Female: male side to the board header, female side to the SHT31):

SHT31 Pin	GPIO	Function
VCC	3.3V	Power supply
GND	GND	Ground
SDA	GPIO 16	I2C Data (Bus B)
SCL	GPIO 17	I2C Clock (Bus B)
NOTE

Use the 8-pin header on the back of the Tem(H)u Macro. Do not use the internal I2C bus (Bus A, GPIO14/15) — it is reserved for touch and AXP2101.

3. Flashing the Firmware (once via USB — Factory Flash)
IMPORTANT

The first flash must be done once via USB using the factory firmware. All subsequent updates run over Wi-Fi (OTA) — the USB cable is only needed for power afterwards.

Required: Chrome or Edge browser (other browsers are not supported)

Firmware Files
Model	First Flash (Factory)	OTA Update (after first flash)
Tem(H)u Nano	temhu-nano-firmware.factory(2.0.0).bin	temhu-nano-firmware.ota(2.0.0).bin
Tem(H)u Macro	temhu-macro-firmware.factory(2.0.0).bin	temhu-macro-firmware.ota(2.0.0).bin
NOTE

The version number in the file names (e.g. 2.0.0) may change with updates. Always use the currently available version.

Step-by-Step (First Flash)
Open Chrome or Edge and go to web.esphome.io
Connect the display to the computer via USB-C cable
Click "Connect" → select the serial port from the list
Click "Install" → select the matching Factory .bin file:
temhu-nano-firmware.factory(2.0.0).bin for Tem(H)u Nano
temhu-macro-firmware.factory(2.0.0).bin for Tem(H)u Macro
Wait for the flash process to complete (approx. 2–4 minutes)
The device restarts automatically
CAUTION

Always use the Factory file for the first flash. The OTA file only works as an update on an already-flashed device.

4. Wi-Fi Setup (Captive Portal)
After the first boot without a saved Wi-Fi network, the device automatically opens a Wi-Fi Access Point:

Model	AP Name
Tem(H)u Nano	Tem(H)u Nano
Tem(H)u Macro	Tem(H)u Macro
Step-by-Step
Connect your smartphone or computer to the Wi-Fi network Tem(H)u Nano (or Tem(H)u Macro) — no password required
The Captive Portal opens automatically (if not: open browser → http://192.168.4.1)
In the Captive Portal:
Select your Wi-Fi network from the list
Enter your Wi-Fi password
Click "Connect"
The device connects to the home network and restarts
The AP disappears — the device is now on the home network
TIP

If the AP does not close automatically after connecting: briefly disconnect the device from power and restart.

5. Accessing the Web Interface
After Wi-Fi setup, the device is accessible via browser:

Model	URL
Tem(H)u Nano	http://temhu-nano.local
Tem(H)u Macro	http://temhu-macro.local
TIP

If .local does not work (Windows without mDNS): find the IP address in your router's interface / DHCP list and access it directly (e.g. http://192.168.1.42).

All settings and OTA updates are accessible via the web interface.

6. Updates (OTA — without USB)
After the first flash, all further updates run directly via the web interface — no USB cable, no browser flasher:

Open the web interface:
Tem(H)u Nano: http://temhu-nano.local
Tem(H)u Macro: http://temhu-macro.local
Navigate to the "OTA Update" section → upload the matching OTA .bin file:
temhu-nano-firmware.ota(2.0.0).bin for Tem(H)u Nano
temhu-macro-firmware.ota(2.0.0).bin for Tem(H)u Macro
Wait until "OTA Success" appears
The device restarts automatically → reopen the web interface and verify
7. User Interface
The 3 Display Pages
The display shows 3 swipeable pages:

Page	Content
Humidity	Current value in % + 24h history graph
Temperature	Current value in °C + 24h history graph
Clock	Time, date, weekday + daily min/max values
Navigation
Swipe (left/right): switch page
Automatic: the outer animation ring cycles pages approximately every 15 seconds (unless swiped manually)
Animation Ring Color Coding
The rotating arc ring displays the current reading as a color. The color transitions smoothly based on the value:

Humidity (Page 1):

Range	Color	Meaning
< 30%	🔵 Light blue (#8BC5E8)	Too dry
30 – 40%	Light blue → Mint green	Transition
40 – 60%	🟢 Mint green (#7EDCB5) → Sage green (#A8D8A8)	Optimal range
60 – 70%	Sage green → 🟡 Amber (#F5C77E)	Transition
> 70%	🔴 Coral red (#E88B8B)	Too humid
Temperature (Page 2):

Range	Color	Meaning
< 16°C	🔵 Light blue (#8BC5E8)	Too cold
16 – 18°C	Light blue → Mint green	Transition
18 – 22°C	🟢 Mint green (#7EDCB5) → Sage green (#A8D8A8)	Optimal range
22 – 26°C	Sage green → 🟡 Amber (#F5C77E)	Transition
> 26°C	🟣 Lavender (#B39DDB)	Too warm
Clock (Page 3): Ring always in 🟢 Mint green (#7EDCB5)

24h History Graph
Each page shows a line graph at the bottom with the last 24 hours (96 data points × 15 minutes). The Y-axis scales automatically to the current value range.

NOTE

The graph builds up gradually — a new data point is added every 15 minutes. The full 24 hours are only visible after a complete day. Immediately after startup, the current value is shown as the starting point.

8. Settings (Web Interface)
All settings are accessible via the web interface:

Tem(H)u Nano: http://temhu-nano.local
Tem(H)u Macro: http://temhu-macro.local
When MQTT is active, settings are also accessible via Home Assistant.

8.1 Display
Setting	Range	Default	Description
Daytime Brightness	10 – 255	248	Display brightness during the day
Auto-Dim Display	On/Off	Off	Automatically dim at night
Auto-Dim Brightness	1 – 100	20	Brightness when dimmed
Auto-Dim Start (Hour)	0 – 23	22	Dimming starts at this hour
Auto-Dim End (Hour)	0 – 23	7	Brightening resumes at this hour
Show Time and Date	On/Off	On	Show/hide the clock page
Time Format (12h AM-PM)	On/Off	Off	24h or 12h format
8.2 Network (Static IP — optional)
By default the device uses DHCP — no configuration needed.

To set a fixed IP, fill in the following fields in the web interface:

Setting	Format	Description
Network: Static IP	192.168.x.x	Desired fixed IP (leave empty = DHCP)
Network: Gateway	192.168.x.1	Default gateway (empty = automatically derived from static IP)
Network: Subnet Mask	255.255.255.0	Subnet mask (empty = 255.255.255.0)
NOTE

Gateway auto-detection: If the gateway field is left empty, the device automatically derives the gateway from the static IP (last octet → .1). Example: Static IP 10.20.5.100 → Gateway 10.20.5.1. Works with any router subnet.

IMPORTANT

After setting a static IP, the device must be restarted (http://temhu-nano.local / http://temhu-macro.local → "Restart").

8.3 Timezone
Setting	Description
Timezone	Select from 45 predefined timezones (dropdown)
Timezone Custom (POSIX)	Custom POSIX timezone (overrides dropdown, e.g. CET-1CEST,M3.5.0,M10.5.0/3)
Default: Europe/Berlin (+1) — daylight saving time is handled automatically.

8.4 Calibration (Offset)
The SHT31 sensor may report slightly inaccurate values due to self-heating of the ESP32 or mounting conditions. Corrections can be applied:

Setting	Range	Step	Default
Calibration: Temperature Offset	-10.0 – +10.0 °C	0.1 °C	0.0 °C
Calibration: Humidity Offset	-20.0 – +20.0 %	0.5 %	0.0 %
Example: Device reads 23.5°C but a reference thermometer shows 22.0°C → set offset to -1.5°C.

TIP

For accurate calibration, let the device run for 30 minutes before comparing readings. The SHT31 needs a warm-up period.

8.5 MQTT & Home Assistant Integration
The device publishes readings via MQTT to any MQTT broker (Mosquitto, EMQX, HiveMQ, etc.). Home Assistant is integrated — if desired — exclusively via MQTT Auto-Discovery.

Setting	Description
01. MQTT Username	MQTT broker username
02. MQTT Password	MQTT broker password
03. MQTT Discovery Topic	Prefix for auto-discovery (default: homeassistant)
04. MQTT Broker IP	IP address of the MQTT broker
05. MQTT Port	Port (default: 1883)
06. MQTT Auto-Discovery	Enable auto-discovery — restart required
MQTT topics (published automatically every 30 seconds):

Tem(H)u Nano:


temhu-nano/sensor/humidity/state       → Humidity in %
temhu-nano/sensor/temperature/state    → Temperature in °C
temhu-nano/sensor/esp_temp/state       → ESP32 chip temperature
temhu-nano/sensor/wifi_signal/state    → Wi-Fi signal strength in dBm
temhu-nano/sensor/uptime/state         → Formatted uptime
Tem(H)u Macro:


temhu-macro/sensor/humidity/state       → Humidity in %
temhu-macro/sensor/temperature/state    → Temperature in °C
temhu-macro/sensor/esp_temp/state       → ESP32 chip temperature
temhu-macro/sensor/wifi_signal/state    → Wi-Fi signal strength in dBm
temhu-macro/sensor/uptime/state         → Formatted uptime
TIP

Both variants can run simultaneously on the same MQTT broker — the topics are separate and there are no conflicts.

Integrating Home Assistant:

Enter the MQTT broker IP, port, username and password in the web interface
http://temhu-nano.local (Nano) / http://temhu-macro.local (Macro)
Enable "06. MQTT Auto-Discovery"
Restart the device
All sensors appear automatically in HA under Settings → Devices & Services → MQTT
NOTE

MQTT is entirely optional. The device works as a standalone display without any MQTT configuration.

9. Maintenance & Troubleshooting
Restart Device
Tem(H)u Nano: http://temhu-nano.local → button "Restart"
Tem(H)u Macro: http://temhu-macro.local → button "Restart"
Factory Reset
Tem(H)u Nano: http://temhu-nano.local → button "Reset Factory Settings"
Tem(H)u Macro: http://temhu-macro.local → button "Reset Factory Settings"
NOTE

Restart and Reset are only available via the web interface. These buttons are not present in Home Assistant via MQTT, as the MQTT interface only sends data (no command reception).

CAUTION

Factory Reset deletes all saved settings (IP, MQTT, offsets, brightness, Wi-Fi). The device then opens the Captive Portal AP again. The firmware remains intact.

Diagnostic Sensors
Accessible via the web interface or, when MQTT is active, also in Home Assistant:

Sensor	Description
WiFi Signal Strength	Signal in % and dBm
ESP Temperature	Internal chip temperature
Uptime	Time since last restart
IP Address	Current IP
MAC Address	Hardware address
ESPHome Version	Firmware version
Common Issues
Problem	Solution
No Wi-Fi AP after flash	Restart device — AP appears when no Wi-Fi is saved
Captive Portal does not open	Navigate browser manually to http://192.168.4.1
temhu-nano.local / temhu-macro.local not reachable	Find IP address in router interface and access directly
Sensor shows ---	Check I2C wiring — SHT31 address = 0x44
Incorrect temperature readings	Adjust offset under "Calibration" in the web interface
Static IP not working	Restart device after entering IP; leave gateway empty = auto
OTA update fails	Repeat factory flash via USB
Display stays black	Disconnect power, wait 10 seconds, reconnect
Graph shows only one point	Normal — builds up every 15 minutes, full after 24 hours
License
This project is licensed under the GNU General Public License v3.0.
See the 
LICENSE
 file for details.

Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
When submitting changes, please ensure all modifications are clearly documented.
