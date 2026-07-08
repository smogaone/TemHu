# TemHu
✨ Features
📊 Live readings — temperature, humidity & clock on 3 swipeable pages
🎨 Color-coded arc ring — smooth color transitions based on current values
📈 24h history graph — 96 data points × 15 min, auto-scaling Y-axis
🌐 Full web interface — all settings configurable in the browser, no app needed
📡 MQTT + Home Assistant — auto-discovery, no manual entity setup
🔄 OTA updates — firmware updates entirely over Wi-Fi, no USB after first flash
🔧 Static IP support — with automatic gateway derivation
🕐 45 timezones — including DST, fully configurable
📏 Calibration offsets — temperature & humidity correction built in
🖥️ Models at a Glance
Tem(H)u Nano	Tem(H)u Macro
Display	1.43" AMOLED	1.75" AMOLED
Resolution	466 × 466 px	466 × 466 px
Chip	ESP32-S3R8	ESP32-S3
Sensor connection	SH1.0 4-pin I2C connector	8-pin header (no soldering)
GPIO header alternative	✅ GPIO 38/39 (fw 2.0.0+)	—
IMU / RTC	✅ QMI8658 + PCF85063	—
Power management	Direct (USB / battery)	AXP2101
Waveshare	Shop	Shop
Amazon	amazon.de	amazon.de
🚀 Quick Start

1. Wire SHT31 sensor to display
2. Flash factory firmware via web.esphome.io (USB, first time only)
3. Connect to Wi-Fi via Captive Portal
4. Open http://temhu-nano.local  or  http://temhu-macro.local
5. Done — all further updates via OTA in the web interface
📦 1. Required Hardware
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
Model	Required
Tem(H)u Nano	SH1.0 4-pin cable — solder SHT31 to cable
Tem(H)u Macro	Dupont jumper cables Male–Female
🔌 2. Connecting the Sensor
IMPORTANT

Connect the sensor before the first flash. The display does not need to be powered while wiring.

Tem(H)u Nano (1.43") — SH1.0 I2C Connector
SHT31 Pin	GPIO	Function
VCC	3.3V	Power
GND	GND	Ground
SDA	GPIO 47	I2C Data
SCL	GPIO 48	I2C Clock
NOTE

As of firmware 2.0.0, a second I2C bus is available on the 2×14-pin GPIO header: GPIO 38 (SCL) and GPIO 39 (SDA). This allows connecting the SHT31 via jumper cable without soldering.

Tem(H)u Macro (1.75") — 8-Pin Header
Connect via Dupont Male–Female cables (male to board header, female to SHT31):

SHT31 Pin	GPIO	Function
VCC	3.3V	Power
GND	GND	Ground
SDA	GPIO 16	I2C Data (Bus B)
SCL	GPIO 17	I2C Clock (Bus B)
NOTE

Use the dedicated 8-pin header on the back. Do not use Bus A (GPIO14/15) — reserved for touch and AXP2101.

⚡ 3. Flashing the Firmware
IMPORTANT

The first flash must be done once via USB. All subsequent updates run over Wi-Fi.

Required: Chrome or Edge browser · web.esphome.io

Firmware Files
Model	Factory (first flash)	OTA (updates)
Tem(H)u Nano	temhu-nano-firmware.factory(2.0.0).bin	temhu-nano-firmware.ota(2.0.0).bin
Tem(H)u Macro	temhu-macro-firmware.factory(2.0.0).bin	temhu-macro-firmware.ota(2.0.0).bin
NOTE

The version number (e.g. 2.0.0) may change with updates. Always use the latest available version.

Steps
Open web.esphome.io in Chrome or Edge
Connect display via USB-C cable
Click "Connect" → select serial port
Click "Install" → select the Factory .bin for your model
Wait ~2–4 minutes for flashing to complete
Device restarts automatically
CAUTION

Always use the Factory file for the first flash. The OTA file only works on an already-flashed device.

📶 4. Wi-Fi Setup
After first boot without a saved network, the device opens an access point:

Model	AP Name
Tem(H)u Nano	Tem(H)u Nano
Tem(H)u Macro	Tem(H)u Macro
Steps
Connect to Tem(H)u Nano or Tem(H)u Macro — no password required
Captive Portal opens automatically — if not, go to http://192.168.4.1
Select Wi-Fi network → enter password → click "Connect"
Device joins home network and restarts — AP disappears
TIP

If the AP doesn't close: disconnect power briefly and restart.

🌍 5. Web Interface
Model	URL
Tem(H)u Nano	http://temhu-nano.local
Tem(H)u Macro	http://temhu-macro.local
TIP

If .local doesn't resolve (Windows without mDNS): use the IP address from your router's DHCP list directly.

🔄 6. OTA Updates
All updates after the first flash are done entirely via the web interface:

Open http://temhu-nano.local or http://temhu-macro.local
Go to "OTA Update" → upload the matching OTA .bin file
Wait for "OTA Success"
Device restarts — verify in web interface
🖥️ 7. User Interface
Pages
Page	Content
Humidity	Current value in % + 24h graph
Temperature	Current value in °C + 24h graph
Clock	Time · Date · Weekday · Daily min/max
Navigation: Swipe left/right · Auto-cycles every ~15 seconds

24h History Graph
96 data points × 15 minutes = 24 hours. Y-axis auto-scales. Builds up gradually after startup — one point added every 15 minutes.

🎨 Animation Ring Color Coding
⚙️ 8. Settings
All settings at http://temhu-nano.local / http://temhu-macro.local

8.1 Display
Setting	Range	Default	Description
Daytime Brightness	10 – 255	248	Brightness during the day
Auto-Dim Display	On/Off	Off	Auto-dim at night
Auto-Dim Brightness	1 – 100	20	Brightness when dimmed
Auto-Dim Start (Hour)	0 – 23	22	Hour dimming begins
Auto-Dim End (Hour)	0 – 23	7	Hour brightening resumes
Show Time and Date	On/Off	On	Show/hide clock page
Time Format (12h AM-PM)	On/Off	Off	24h or 12h format
8.2 Network — Static IP (optional)
Default is DHCP — no configuration needed.

Setting	Format	Description
Network: Static IP	192.168.x.x	Fixed IP (empty = DHCP)
Network: Gateway	192.168.x.1	Gateway (empty = auto-derived from IP)
Network: Subnet Mask	255.255.255.0	Subnet mask (empty = 255.255.255.0)
NOTE

Auto gateway: Leave gateway empty and it is derived automatically — last octet replaced with .1. Example: 10.20.5.100 → 10.20.5.1

IMPORTANT

Restart required after changing static IP settings.

8.3 Timezone
Setting	Description
Timezone	45 predefined timezones (dropdown)
Timezone Custom (POSIX)	Override with custom POSIX string, e.g. CET-1CEST,M3.5.0,M10.5.0/3
Default: Europe/Berlin (+1) — DST handled automatically.

8.4 Calibration
Setting	Range	Step	Default
Temperature Offset	-10.0 – +10.0 °C	0.1 °C	0.0 °C
Humidity Offset	-20.0 – +20.0 %	0.5 %	0.0 %
TIP

Let the device run for 30 minutes before calibrating — the SHT31 needs a warm-up period.

8.5 MQTT & Home Assistant
Setting	Description
01. MQTT Username	Broker username
02. MQTT Password	Broker password
03. MQTT Discovery Topic	Auto-discovery prefix (default: homeassistant)
04. MQTT Broker IP	Broker IP address
05. MQTT Port	Port (default: 1883)
06. MQTT Auto-Discovery	Enable — restart required after
Topics published every 30 seconds:

Tem(H)u Nano topics
Tem(H)u Macro topics
TIP

Both devices can run on the same MQTT broker simultaneously — topics are fully independent.

Home Assistant setup:

Enter broker IP, port, username and password in the web interface
Enable "06. MQTT Auto-Discovery"
Restart the device
All sensors appear under Settings → Devices & Services → MQTT
NOTE

MQTT is entirely optional. Tem(H)u works as a standalone display without any MQTT configuration.

🔧 9. Maintenance & Troubleshooting
Controls
Action	Tem(H)u Nano	Tem(H)u Macro
Restart	http://temhu-nano.local → "Restart"	http://temhu-macro.local → "Restart"
Factory Reset	http://temhu-nano.local → "Reset Factory Settings"	http://temhu-macro.local → "Reset Factory Settings"
CAUTION

Factory Reset erases all saved settings (Wi-Fi, IP, MQTT, offsets, brightness). The firmware remains intact. The device reopens the Captive Portal after reset.

Diagnostic Sensors
Available in the web interface and Home Assistant (when MQTT is active):

WiFi Signal · ESP Temperature · Uptime · IP Address · MAC Address · ESPHome Version

🩺 Common Issues
Problem	Solution
No Wi-Fi AP after flash	Restart — AP appears when no network is saved
Captive Portal doesn't open	Go to http://192.168.4.1 manually
.local not reachable	Use IP from router DHCP list directly
Sensor shows ---	Check I2C wiring — SHT31 address = 0x44
Wrong temperature readings	Adjust offset under "Calibration" in web interface
Static IP not working	Restart after entering IP; leave gateway empty = auto
OTA update fails	Repeat factory flash via USB
Display stays black	Disconnect power, wait 10 s, reconnect
Graph shows only one point	Normal — builds every 15 min, full after 24 h
