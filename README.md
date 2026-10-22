<p align="center">
  <img src="https://raw.githubusercontent.com/viniciushnf/StickS3-GPS-GNSS/refs/heads/main/media/cover.webp" alt="Cover" width="100%">
</p>

# StickS3 with GPS and GNSS

Turn your **M5StickS3** into a compact and practical GPS/GNSS device.

This project provides two firmware options for connecting a compatible GPS or GNSS module to the StickS3 and displaying positioning and satellite information directly on its screen.

The main goal is to make GPS/GNSS data easy to access in a portable device, whether for navigation, testing, field monitoring, development, or simply exploring positioning data.

## ✨ What This Project Provides

This repository includes:

* Two firmware options for the StickS3
* Precompiled `.bin` firmware files
* Source code for **GPS & GNSS Monitor**
* Instructions for connecting a GPS/GNSS module
* Compatible module requirements
* Firmware installation instructions
* Configuration instructions
* Hardware assembly information
* Basic usage instructions for both firmware options

The two firmware options are:

| Firmware               | Main Purpose                                                                                                                                                                                |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **GPS & GNSS Monitor** | Dedicated firmware for monitoring GPS/GNSS positioning, satellite, movement, distance, route, and time information                                                                          |
| **Bruce Modified**     | Bruce firmware with all its existing features, enhanced with a new **GPS Info** screen for viewing satellites, HDOP, course, speed, altitude, date, time, timezone, latitude, and longitude |

---

# 📡 GPS vs GNSS

Although the terms **GPS** and **GNSS** are often used interchangeably, they are not exactly the same.

**GPS** is the satellite navigation system operated by the United States.

**GNSS** is the broader term for satellite navigation systems and can include multiple constellations, such as:

* GPS — United States
* GLONASS — Russia
* Galileo — European Union
* BeiDou — China
* QZSS — Japan
* Other regional augmentation systems

A GNSS receiver can potentially use multiple satellite constellations at the same time, depending on the receiver's hardware and configuration.

Therefore, this project is compatible with both **GPS and GNSS modules** as long as the module meets the communication and electrical requirements described below.

A module does not need to be limited to GPS. A multi-constellation GNSS receiver can also be used.

---

# 🔌 Compatible GPS/GNSS Modules

The project is designed for GPS/GNSS modules that provide positioning information through a **UART serial interface**, using a protocol supported by the firmware.

The recommended communication format is:

| Parameter   | Requirement                                |
| ----------- | ------------------------------------------ |
| Interface   | UART                                       |
| Data        | Standard NMEA GPS/GNSS data                |
| Data format | 8 data bits, no parity, 1 stop bit (`8N1`) |
| Baud rate   | Must match the module configuration        |
| Output      | GPS/GNSS positioning data                  |

Common baud rates such as `9600`, `19200`, `38400`, `57600`, and `115200` can be used with the GPS & GNSS Monitor firmware.

Other modules may also work if they provide compatible NMEA data through UART.

> **Important:** Compatibility is not determined only by the communication protocol. Always check the electrical specifications of the GPS/GNSS module before connecting it to the StickS3.

### Examples of Compatible Modules

The following are examples of GPS/GNSS modules that use UART and provide NMEA data:

| Module       | Manufacturer | Type |
| ------------ | ------------ | ---- |
| **RYS352A**  | REYAX        | GNSS |
| **NEO-6M**   | u-blox       | GPS  |
| **NEO-M8N**  | u-blox       | GNSS |
| **NEO-M9N**  | u-blox       | GNSS |
| **MAX-M10S** | u-blox       | GNSS |
| **ATGM336H** | Various      | GNSS |
| **L76K**     | Quectel      | GNSS |

> **⚠️ Important:** Before connecting a GPS/GNSS module to the StickS3, always check the module's datasheet and verify its **power supply voltage, UART logic levels, pinout, and communication settings**. Specifications may vary between manufacturers, module models, and breakout boards. Make sure that the module is electrically compatible with the StickS3 before connecting it.


---

# ⚠️ Voltage and Electrical Compatibility

Pay particular attention to **power supply voltage** and **UART signal voltage**.

Different GPS/GNSS modules can require different supply voltages. Some modules operate at 3.3 V, while others may require different voltages or include voltage regulation on their breakout board.

You must also verify the **TX output voltage of the GPS/GNSS module** before connecting it to the StickS3 RX pin.

### Recommended M5StickS3 Connections

The recommended GPIO configuration depends on the connection interface.

**Hat2-Bus**

- Configure G44 as RX and G43 as TX.
- Connect the GPS/GNSS module's TX to G44.
- Connect the GPS/GNSS module's RX to G43, following the recommended Hat2-Bus wiring.

**HY2.0-4P**

- Configure G10 as RX and G9 as TX.
- Connect the GPS/GNSS module's TX to G10.
- Connect the GPS/GNSS module's RX to G9.

> **⚠️ Check the module's datasheet and the voltage available from your hardware setup first.**

The same applies to the UART signal levels. The module's TX output must be electrically compatible with the StickS3 RX input.

---

# 🛰️ Position Accuracy

The firmware does not determine the physical accuracy of the GPS/GNSS receiver. It receives, displays, and processes the information provided by the module.

Different GPS/GNSS modules can have very different performance characteristics.

Positioning accuracy can be affected by factors such as:

* GPS/GNSS receiver quality
* Antenna quality
* Number of visible satellites
* Satellite geometry
* Signal strength
* Indoor or outdoor environment
* Buildings and other obstructions
* Trees and terrain
* Multipath effects
* Atmospheric conditions
* Receiver configuration
* Update rate
* Constellations supported by the receiver

Therefore, two different modules running the same firmware can produce different results.

A high-quality GNSS receiver with a good antenna and clear view of the sky can provide significantly better results than a low-cost receiver operating in a difficult environment.

### HDOP

Some of the firmware screens also display **HDOP (Horizontal Dilution of Precision)**.

HDOP is an indicator related to the geometry of the satellites being used for the position calculation. In general, a lower HDOP indicates more favorable satellite geometry.

However:

> **HDOP is not a direct measurement of position accuracy in meters.**

A good HDOP value does not guarantee a specific real-world accuracy, and a higher HDOP does not necessarily mean that the receiver is completely unusable.

---

# 🧩 Hardware Assembly

<p align="center">
  <img src="https://raw.githubusercontent.com/viniciushnf/StickS3-GPS-GNSS/refs/heads/main/media/pcb-1.jpg" alt="PCB" width="70%">
</p>
<p align="center">
  <img src="https://raw.githubusercontent.com/viniciushnf/StickS3-GPS-GNSS/refs/heads/main/media/photo-6.jpg" alt="Photo" width="70%">
</p>

For my hardware setup, I soldered the necessary pins to a small PCB and wired the GPS/GNSS module and the StickS3 together.

This creates a compact assembly where the GPS/GNSS module and the StickS3 remain firmly attached to each other.

This type of assembly is especially useful for:

* Portable GPS/GNSS testing
* Field experiments
* Navigation
* Development and prototyping
* Long-term monitoring

The exact mechanical assembly can be adapted according to the GPS/GNSS module being used.

### StickS3 pins

| GPS/GNSS pin | StickS3                     |
| ------------ | --------------------------- |
| TX           | **GPIO 44 (RX)**            |
| RX           | **GPIO 43 (TX)**            |
| GND          | GND                         |
| VCC          | Compatible power supply     |

<p align="center">
  <img src="https://raw.githubusercontent.com/viniciushnf/StickS3-GPS-GNSS/refs/heads/main/media/wiring-diagram.png" alt="Wiring Diagram" width="70%">
</p>

---

# ⭐ Tested GPS/GNSS Module — REYAX RYS352A

During the development and testing of this project, I used the **REYAX RYS352A**, kindly provided by **REYAX**.

I had a very good experience with this module during my tests. It provided excellent overall quality, good positioning precision, and fast FIX acquisition.

The RYS352A is a multi-GNSS module supporting systems such as GPS, GLONASS, Galileo, BeiDou and QZSS, and provides a UART interface with NMEA output.

According to the manufacturer, the module operates from a typical **3.3 V supply**, supports a default baud rate of **115200 bps**, and supports navigation update rates of up to **10 Hz**.

For these reasons, the RYS352A is a module I strongly recommend for this project when looking for good quality, positioning performance, and fast FIX acquisition.

<p align="center">
  <img src="https://raw.githubusercontent.com/viniciushnf/StickS3-GPS-GNSS/refs/heads/main/media/RYS352A.png" alt="REYAX RYS352A" width="70%">
</p>

### Official RYS352A page

[Official Product Page: https://reyax.com/product/GPS-GNSS/RYS352A](https://reyax.com/product/GPS-GNSS/RYS352A)

### Where to buy

* [DigiKey: https://www.digikey.com/en/products/detail/reyax/RYS352A/22206992](https://www.digikey.com/en/products/detail/reyax/RYS352A/22206992)
* [eBay: https://www.ebay.com/itm/187031730034](https://www.ebay.com/itm/187031730034)
* [Amazon: https://www.amazon.com/dp/B0CM5JTJL7](https://www.amazon.com/dp/B0CM5JTJL7?lv=shuf&language=zh_TW&channelId=500&plpRedirect=mhFallback)

> **Disclosure:** The RYS352A used during development and testing was provided by REYAX. The opinions about the module above are based on my own experience using it with this project.

Thank you to **REYAX** for providing the RYS352A for development and testing.

---

# 📍 GPS & GNSS Monitor

**GPS & GNSS Monitor** is a dedicated firmware created specifically for monitoring GPS/GNSS information on the StickS3.

It focuses on making positioning information easy to read and access without requiring the user to navigate through unrelated features.

## Main Features

The GPS & GNSS Monitor firmware provides dedicated screens for monitoring GPS/GNSS positioning, satellite reception, navigation, and trip statistics.

Main features include:

- **Position:** Latitude and longitude.
- **Satellite Information:** Satellite count, HDOP, and positioning quality information.
- **Speed:** Current speed and trip-related speed statistics, with configurable measurement units.
- **Altitude:** Current altitude and altitude statistics, with configurable units.
- **Course:** Direction of travel.
- **Distance:** Straight-line distance from the trip starting position and accumulated route distance.
- **Route Statistics:** Total route distance, average moving speed, minimum and maximum speed, minimum and maximum altitude, and time in motion.
- **Session Information:** Time in Motion, Trip Time, and Fix Time.
- **Date & Time:** GPS/GNSS date and time with configurable timezone and display formats.
- **UART Configuration:** Select the RX GPIO, TX GPIO, and baud rate directly on the device.
- **Theme Color:** Customize the interface color.
- **Background Color:** Select the display background color.
- **Display Brightness:** Adjust screen brightness.
- **Screen Timeout:** Configure the inactivity period before the display turns off, or disable the timeout.
- **Screen Orientation:** Flip the display horizontally or vertically by 180 degrees, or apply an additional 90-degree rotation.
- **Screen Update:** Select automatic display updates or a fixed refresh interval.
- **Module Timeout:** Configure when the GPS/GNSS communication warning appears, or disable the warning.
- **Minimum Trip Speed:** Configure the minimum speed used to record route distance and accumulate time in motion.
- **Measurement & Format Settings:** Configure coordinate format, speed units, altitude units, distance units, timezone, date format, and time format.
- **Persistent Settings:** Configuration values are saved in non-volatile storage (NVS) and retained after restarting the device.
- **Trip Reset:** Reset trip data and route statistics.

The firmware also provides an introductory startup screen displaying the firmware name, version, and developer's GitHub address.

## Main Screens

<p align="center">
  <img src="https://raw.githubusercontent.com/viniciushnf/StickS3-GPS-GNSS/refs/heads/main/media/screens-gps-gnss-monitor.gif" alt="GPS & GNSS Monitor Screens" width="70%">
</p>

The firmware includes the following screens:

| Screen | Information |
|---|---|
| **General** | General GPS/GNSS information and positioning quality. |
| **Position** | Latitude and longitude. |
| **Speed** | Current speed. |
| **Altitude** | Current altitude. |
| **Distance** | Straight-line distance from the trip starting position. |
| **Route Stats** | Accumulated route distance and trip statistics, including time in motion. |
| **Course** | Direction of travel. |
| **Time** | GPS/GNSS date and time. |
| **Session Info** | Time in Motion, Trip Time, and Fix Time. |
| **About** | Firmware information and a second view containing developer and GitHub repository information. |
| **Settings** | Firmware configuration options. |

## Configuration Screens

<p align="center">
  <img src="https://raw.githubusercontent.com/viniciushnf/StickS3-GPS-GNSS/refs/heads/main/media/screens-gps-gnss-monitor-config.gif" alt="GPS & GNSS Monitor Screens" width="70%">
</p>

The Settings menu provides the following configuration options:

| Screen | Description |
|---|---|
| **Theme Color** | Select the color used for interface elements and text. |
| **Background Color** | Select the display background color. |
| **Brightness** | Adjust display brightness. |
| **Screen Timeout** | Configure the inactivity period before the display turns off, or disable the timeout. |
| **Screen Flip H** | Rotate horizontal screens by 180 degrees when enabled. |
| **Screen Flip V** | Rotate vertical screens by 180 degrees when enabled. |
| **Screen Rotate** | Apply an additional 90-degree rotation to the display. |
| **Coord. Format** | Select the coordinate display format. |
| **Speed Unit** | Select the speed measurement unit. |
| **Min. Trip Speed** | Set the minimum speed used to record route distance and time in motion. |
| **Altitude Unit** | Select the altitude measurement unit. |
| **Distance Unit** | Select the distance measurement unit. |
| **Timezone** | Configure the timezone used to display local date and time. |
| **Date Format** | Select the date display format. |
| **Time Format** | Select the time display format. |
| **Screen Update** | Select automatic display updates or a fixed refresh interval. |
| **Module Timeout** | Configure when the GPS/GNSS communication warning appears, or disable it. |
| **Basic Settings** | View and configure the UART RX GPIO, TX GPIO, and baud rate. |
| **Reset Trip** | Reset trip data and route statistics. |
| **Exit** | Leave the Settings menu and return to the General screen. |

### Available Theme and Background Colors

Both `Theme Color` and `Background Color` support the following colors:

`WHITE`, `BLACK`, `RED`, `GREEN`, `BLUE`, `YELLOW`, `CYAN`, `MAGENTA`, `ORANGE`, `PURPLE`, `PINK`, `NAVY`, `BROWN`, `GRAY`

The selected theme color and background color cannot be identical, helping preserve the readability of the interface.

### Screen Update Interval

The `Screen Update` setting provides the following options:

- `Automatic`
- `1 second`
- `5 seconds`
- `15 seconds`
- `30 seconds`
- `60 seconds`

In Automatic mode, the display refreshes when new GPS/GNSS information is received. When a fixed interval is selected, data processing continues independently of the display refresh interval. Button interactions that require a screen change or immediate redraw can still refresh the display.

### Module Timeout

The `Module Timeout` setting controls when the `Communication Warning` screen appears if no new GPS/GNSS data is received.

Available options:

- `Disabled`
- `5 seconds`
- `15 seconds`
- `30 seconds`
- `60 seconds`

When Disabled is selected, the firmware does not display the communication warning, regardless of how long the module remains silent.

### Screen Timeout

The `Screen Timeout` setting controls how long the device can remain without button interaction before the display turns off.

Available options:

- `Disabled`
- `10 seconds`
- `30 seconds`
- `60 seconds`
- `5 minutes`
- `10 minutes`

GPS/GNSS data processing continues while the display is off. Press **Button A** to turn the display back on.

## Button Controls

### Button B

- **Short press:** Go to the next screen.
- **Long press:** Go to the previous screen.

### Button A

The function of Button A depends on the current screen. It can be used to:

- Change display formats or switch between additional views.
- Enter the Settings menu and modify configuration values.
- Switch between the two About views.
- Open the UART configuration workflow from `Basic Settings`.
- Confirm configuration choices.
- Turn the display back on after a screen timeout.
- Dismiss the GPS/GNSS communication warning.

### Inside the Settings Menu

- **Button B:** Navigate between settings.
- **Button A:** Change or confirm the selected setting, depending on the screen.

### Basic Settings

On the `Basic Settings` screen, press **Button A** to configure the UART RX GPIO, TX GPIO, and baud rate.

During configuration:

- **Button B:** Cycle through the available options.
- **Button A:** Confirm the selected option and continue to the next configuration step.

### About

On the About screen, press **Button A** to switch between the two About views. The second view contains the developer information and the firmware's GitHub repository link.

## Main Features

* Dedicated GPS/GNSS interface
* Simple and focused user experience
* Several dedicated information screens
* Route statistics
* Configurable units and formats
* Configurable timezone
* Configurable GNSS baud rate
* Persistent configuration
* Display timeout for better battery usage
* GPS/GNSS communication warning
* Source code is available

### Available Files

This repository provides:

* `GPS_GNSS_Monitor.bin`
* `GPS_GNSS_Monitor.ino`

## M5Burner

The **GPS & GNSS Monitor** firmware is also available directly through **M5Burner**, making it easy to install the firmware on your StickS3 without manually downloading the firmware file.

<p align="center">
  <img src="https://raw.githubusercontent.com/viniciushnf/StickS3-GPS-GNSS/refs/heads/main/media/m5burner-gps-gnss-monitor.webp" alt="GPS & GNSS Monitor Screens" width="70%">
</p>

### Access the Firmware

You can access the firmware in either of the following ways:

* Visit [M5Burner](https://burner.m5stack.com/), select **StickS3**, and search for `GPS & GNSS Monitor`.
* Open the firmware directly through [this link](https://burner.m5stack.com/85KU9L).

> **💡 Recommendation:** For the best experience when using M5Burner, I recommend using **Google Chrome**.

### Installing the Firmware with M5Burner

1. Put the StickS3 into **programming mode** by pressing and holding the **Power** button until the indicator light starts blinking.
2. Connect the **StickS3** to your computer using a **USB cable**.
3. Open [M5Burner](https://burner.m5stack.com/) using **Google Chrome**.
4. Select **StickS3** and search for **GPS & GNSS Monitor**, or open the [direct firmware page](https://burner.m5stack.com/85KU9L).
5. Follow the M5Burner instructions to select the StickS3 and upload the firmware.
6. Wait for the installation to complete. Once finished, the StickS3 will be ready to use with the **GPS & GNSS Monitor** firmware.

## Repository dedicated to the GPS and GNSS Monitor

A dedicated repository with more detailed information about GPS & GNSS Monitor is available here:

[github.com/viniciushnf/M5StickS3-GPS-GNSS-Monitor](https://github.com/viniciushnf/M5StickS3-GPS-GNSS-Monitor)

---

# 🦈 Bruce — Modified Firmware

The second option is a **modified version of Bruce Firmware**.

The original Bruce firmware already provides a large collection of tools and features for the StickS3. I modified it by adding a dedicated screen called **GPS Info**.

The goal is to make GPS/GNSS information available while keeping the rest of the Bruce environment.

Original Bruce Firmware: [Bruce Firmware — GitHub](https://github.com/BruceDevices/firmware)

## Main GPS Info Features

The added **GPS Info** interface provides several screens:

* General GPS information
* GPS Speed
* GPS Altitude
* GPS Time
* GPS Position

The general GPS Info screen provides information such as:

* Number of satellites
* HDOP
* Course
* Speed
* Altitude
* Date and time
* Timezone
* Latitude
* Longitude

## Navigating Between GPS Screens

While inside **GPS Info**, a **short press of Button B** switches between the available GPS screens.

The screens cycle through:

```text
GPS Info
   ↓
GPS Speed
   ↓
GPS Altitude
   ↓
GPS Time
   ↓
GPS Position
   ↓
GPS Info
```

<p align="center">
  <img src="https://raw.githubusercontent.com/viniciushnf/StickS3-GPS-GNSS/refs/heads/main/media/screens-bruce.gif" alt="Bruce GPS Info Screens" width="70%">
</p>

The same navigation can be used in the opposite direction using the corresponding previous/back navigation action supported by Bruce.

Press the A button to access the menu. In the menu, you can save data and change the units of measurement for speed and altitude.

## Speed and Altitude Units

The GPS Info menu allows you to change:

### Speed

* km/h
* mph
* knots
* m/s

### Altitude

* meters
* feet

These units are reflected in the GPS information screens and when GPS data is saved.

## GPS Time

The displayed time comes from the **GPS/GNSS module**.

The module provides UTC time, and the timezone configured in Bruce is applied to display the local date and time.

This means that the displayed time depends on:

1. The date and time received from the GPS/GNSS module.
2. The timezone configured in Bruce.

## Saving GPS/GNSS Data

The modified Bruce firmware can save GPS/GNSS information to:

* **LittleFS**
* **SD Card**

When saving data, you can define:

* The place/location name
* The file name

To access the saved file, open the **Bruce file explorer** and navigate to the `BruceGPS_data` folder.

The saved text file contains information such as:

* Place
* Local date and time
* Timezone
* Satellites
* HDOP
* Speed
* Altitude
* Course
* Decimal coordinates
* Degrees and decimal minutes coordinates
* Degrees, minutes and seconds coordinates
* UTC date/time
* UTC ISO 8601 date/time

## GPS/GNSS Configuration in Bruce

The GPS/GNSS module must be configured through the:

```text
GPS → Config
```

submenu in Bruce.

The **Baudrate** selected in `Config` must match the baud rate used by the connected GPS/GNSS module.

For this project, the StickS3 GPS UART pins are:

| Function |   GPIO |
| -------- | -----: |
| RX       | **44** |
| TX       | **43** |

<p align="center">
  <img src="https://raw.githubusercontent.com/viniciushnf/StickS3-GPS-GNSS/refs/heads/main/media/screen-bruce-gps-pins.jpg" alt="Bruce GPS Pins" width="50%">
</p>

Therefore:

```text
GPS/GNSS TX → StickS3 GPIO 44 (RX)
GPS/GNSS RX → StickS3 GPIO 43 (TX)
```

If the baud rate is incorrect, the firmware may not be able to correctly decode the data received from the module.

## Main Features

* GPS/GNSS information integrated directly into Bruce
* Keeps the other Bruce features available
* Dedicated GPS Info screen
* Multiple GPS information screens
* Speed and altitude unit selection
* GPS/GNSS date and time
* Timezone support
* GPS/GNSS data export
* LittleFS and SD Card support for saved data
* Useful for users who already use Bruce

### Available File

The modified Bruce firmware is provided as:

```text
Bruce-m5stack-sticks3.bin
```

---

# 💾 Firmware Installation

Both firmware options can be installed on the StickS3 using the same flashing procedure with **ESP Tool JS**.

Espressif ESP Tool JS: [https://espressif.github.io/esptool-js/](https://espressif.github.io/esptool-js/)

> **Recommendation:** Use **Google Chrome** when accessing ESP Tool JS, as it generally provides the best Web Serial support for this type of browser-based flashing tool.

## Entering Programming Mode

Before flashing the firmware, the StickS3 must be placed into **download/programming mode**.

1. Press and hold the **Power button**.
2. Keep the button pressed until the indicator LED starts flashing.
3. The StickS3 is now ready to be programmed.

## Flashing Procedure

1. Put the StickS3 into programming mode.
2. Connect the StickS3 to your computer using USB.
3. Download the desired `.bin` file from this repository.
4. Open [ESP Tool JS](https://espressif.github.io/esptool-js/).
5. Set the baud rate to `115200`.
6. Select the StickS3's **COM port**.
7. Select the `.bin` file in ESP Tool JS.
8. Set **Flash Address** to `0x0`.
9. Set **Flash Mode** to `dio`.
10. Set **Flash Frequency** to `80m`.
11. Set **Flash Size** to `8MB`.
12. Start the flashing process.
13. Wait for the process to finish.
14. Restart the StickS3.

## ESP Tool JS screenshots

<p align="center">
  <img src="https://raw.githubusercontent.com/viniciushnf/StickS3-GPS-GNSS/refs/heads/main/media/esptool-1.png" alt="ESPTool 1" width="70%">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/viniciushnf/StickS3-GPS-GNSS/refs/heads/main/media/esptool-2.png" alt="ESPTool 2" width="70%">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/viniciushnf/StickS3-GPS-GNSS/refs/heads/main/media/esptool-3.png" alt="ESPTool 3" width="70%">
</p>

## Required Settings

When flashing either firmware, use the following settings:

| ESP Tool JS Setting | Value    |
| ------------------- | -------- |
| **Baudrate**        | `115200` |
| **Flash Address**   | `0x0`    |
| **Flash Mode**      | `dio`    |
| **Flash Frequency** | `80m`    |
| **Flash Size**      | `8MB`    |


### Firmware Files

| Firmware                  | File                        |
| ------------------------- | --------------------------- |
| GPS & GNSS Monitor        | `GPS_GNSS_Monitor.bin`      |
| Bruce Modified            | `Bruce-m5stack-sticks3.bin` |

---

# 🧪 Testing

I performed extensive testing with both firmware options and the GPS/GNSS hardware used during development.

The tests included:

* GPS/GNSS communication
* Satellite information
* Position
* Speed
* Altitude
* Course
* Date and time
* Timezone conversion
* GPS/GNSS configuration
* Display functions
* Route statistics
* Distance calculation
* GPS/GNSS data saving
* LittleFS storage
* SD Card storage

Both firmware options worked correctly during my tests.

However, GPS/GNSS performance will always depend on the connected receiver, antenna, environment, satellite visibility, and signal conditions.

---

# 👋 Get in touch

If you build this project, I'd love to see the result! 

If you have any questions, suggestions, or run into any issues, feel free to contact me on Instagram. 

I'm always happy to help, receive feedback, and see what the community creates. 

I'm also open to collaborations and partnership opportunities related to electronics, embedded systems, and open-source projects.

* Instagram: **@viniciushnf**
* [instagram.com/viniciushnf](https://www.instagram.com/viniciushnf/)

---

## ⭐ If You Find This Project Useful

If this project helps you turn your StickS3 into a practical GPS/GNSS device, consider giving the repository a ⭐ on GitHub.

Enjoy experimenting with GPS and GNSS!

---

# 🔗 Related Projects

### GPS & GNSS Monitor

For more detailed information about the dedicated GPS & GNSS Monitor firmware, including its source code, features, screens, configuration, and development details:

[GPS & GNSS Monitor — GitHub](https://github.com/viniciushnf/M5StickS3-GPS-GNSS-Monitor)

### Original Bruce Firmware

The modified Bruce firmware is based on the original Bruce project:

[Bruce Firmware — GitHub](https://github.com/BruceDevices/firmware)

---

# 📚 Useful Links

* [ESP Tool JS — Espressif](https://espressif.github.io/esptool-js/)
* [M5Stack StickS3 Documentation](https://docs.m5stack.com/en/core/StickS3)
* [M5Stack StickS3 Arduino Documentation](https://docs.m5stack.com/en/arduino/m5sticks3/program)
* [Bruce Firmware — GitHub](https://github.com/BruceDevices/firmware)
* [REYAX RYS352A — Official Product Page](https://reyax.com/product/GPS-GNSS/RYS352A)

---

# 🙏 Acknowledgments

Special thanks to **REYAX** for providing the **RYS352A GNSS module** used during the development and testing of this project.

Thank you for supporting the project and for providing a module that performed very well during testing.

---

# 📄 License

This repository contains multiple components with different licenses.

### GPS & GNSS Monitor

The dedicated **GPS & GNSS Monitor** firmware is distributed under the **MIT License**.

### Bruce Modified

The modified Bruce firmware is based on the original Bruce Firmware and is distributed according to the **GNU Affero General Public License v3.0 (AGPL-3.0)** and the applicable terms of the original project.

See the license information included with each firmware where applicable.

### Documentation

The documentation and original written content of this repository are provided under the license specified for the repository documentation.

Third-party software, libraries, firmware, trademarks, and other materials remain subject to their respective licenses and terms.