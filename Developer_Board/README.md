Welcome, and thank you for your support.

This document is intended to help advanced users and hardware enthusiasts with research and technical discussions. It is primarily written for users of the **Developer Board** version. By following this guide, you will be able to assemble your Developer Board and gain a clear understanding of its hardware design.

It is recommended that you read through the entire guide first to familiarize yourself with the assembly process and its difficulty before beginning.

> [!TIP]
> By choosing this kit, I assume that you already have some hands-on experience and technical knowledge. Therefore, the following sections focus primarily on the technical aspects rather than basic assembly skills.

### Before You Begin Assembly

1. Assembly involves certain risks. Please read this guide carefully and make sure you have a soldering iron and steady hands.
2. The entire process requires practical skills. Before you begin, make sure you are confident that you can complete the assembly successfully. Avoid damaging your device. Any damage caused by improper operation is your own responsibility.
3. Make sure your 3D printer's build plate is clean and has good adhesion. Printing the front shell with embossed text requires excellent first-layer adhesion. (When I printed the first prototypes, a dirty build plate caused many failed prints.)

### 3D Printing

You can print the enclosure you need from the [Shell_Model](../Shell_Model) directory. The folder with the highest version number contains the latest design.

![Step_1](./Step/3DPrint.jpg)

### Assembly Instructions

> [!TIP]
> Before handling the PCB, touch a grounded metal object nearby or wear an anti-static wrist strap to prevent electrostatic discharge (ESD) from damaging the board.

**1. Install the Heat-Set Inserts**

Take the four included heat-set brass inserts. Heat them using a soldering iron or another suitable heat source, then press them into the four mounting holes in the enclosure.

The inserts must **not protrude above** the surrounding surface. This means they should be fully pressed into the plastic, or even slightly deeper.

![Step_2](./Step/IMG_1079.jpg)

On the side of the enclosure, there are three small windows for the status LEDs. It is recommended to fill these openings with a small amount of white or transparent glue, or even melted plastic. Their purpose is simply to keep dust out.

![Step_6](./Step/IMG_1080.jpg)

**2. Install the PCB**

Insert the USB connector side into the enclosure first, then gently press down the antenna side until the PCB is fully seated.

![Step_1](./Step/IMG_1078.jpg)

**3. Install the Battery**

You will need to provide your own battery. The recommended specifications are:

| Item | Specification | Acceptable Range |
|--------------|---------|---------|
| **Dimensions** | 60 × 40 × 6.5 mm | The battery should be smaller than or close to the recommended dimensions in order to fit inside the enclosure. |
| **Capacity** | Approximately 2000 mAh | Use a battery with **at least 2000 mAh** capacity for safe charging operation. |
| **Connector** | JST 1.25 mm, 2-pin |

***Battery Capacity***

The PCB is configured with a maximum charging current of **1 A**. Most lithium batteries recommend a charging current of approximately **0.5C**, so a battery capacity of at least **2000 mAh** is recommended.

If you choose a smaller battery, you **must** reduce the charging current to ensure safe operation.

See the appendix: [Charging Current](#appendix-charging-current)

***Battery Mounting***

You can use thin double-sided adhesive tape to secure the battery inside the enclosure.

***Battery Connection***

If you cannot use a JST 1.25 connector, you may solder the battery directly to the PCB.

**Be extremely careful with the polarity.** The board does **not** include reverse-polarity protection, so you must ensure the positive and negative terminals are connected correctly.

![Step_2](./Step/IMG_1077.jpg)

Optionally, you may also solder a backup battery for the GNSS positioning module. Installing the backup battery can reduce the time required for satellite acquisition after power-up, but it is **not required**. Whether to install it depends on your own needs.

The backup battery model is **ML414H-IV01E**.

The schematic and installation location are shown below:

![Step_3](./Step/Back_Battery.jpg)

**4. Final Assembly**

Use the four included screws to fasten the rear cover.

![Step_4](./Step/IMG_1076.jpg)

Finally, thread the included lanyard through the hole at the lower-right corner of the enclosure for more convenient carrying.

![Step_8](./Step/rope.jpg)

### Firmware Flashing and Debugging

**1. Connect the Device to Your Computer**

The board includes an onboard **CH340 USB-to-UART** chip and is powered through USB.

Whether the device is powered on or off, connecting it to your computer with a USB cable will create a new **COM port**. This port can be used for firmware flashing, development, and serial debugging.

If no COM port appears:

- Make sure your USB cable supports data transfer (not charging only).
- Verify that the CH340 driver is installed on your computer.

CH340 Driver Download:

[Driver](https://www.wch-ic.com/downloads/CH341SER_ZIP.html)

**2. Flash the Firmware**

You can flash firmware using the **ESP32 Download Tool**.

Prepare the firmware files you want to flash, then open **ESP32DownloadTool**.

Set:

- **ChipType:** ESP32C5
- Leave all other options at their default values.

![Step_5](./Step/ChipType.jpg)

Select the required firmware files (bootloader, firmware, etc.) in the file selection area and configure their corresponding flash addresses.

Select the newly created COM port in the lower-right corner.

Set the **BAUD** rate to the **highest available value**. **Be sure to select the highest baud rate—this is important.**

![Step_6](./Step/download.jpg)

ESP32 Download Tool:

[DownloadTool](https://docs.espressif.com/projects/esp-test-tools/en/latest/esp32/production_stage/tools/flash_download_tool.html)

Keep the device powered **off**.

Click **START** in ESP32DownloadTool. The software will enter a waiting state.

Now press the device's power button **once**. Flashing will begin automatically and typically takes around **10 seconds**.

After flashing is complete:

1. Disconnect the USB cable.
2. Power the device off.
3. Power it on again.

The newly flashed firmware should now start running.

### Appendix: Charging Current

To adjust the charging current, refer to the schematic and image below.

The maximum charging current is determined by **R35**, using the following formula:

**I(bat) = 1000 / R35**

![Step_7](./Step/Current_Adjust.jpg)