## Uno (Atmega328PU) - Raspberry Pi 5 and older models for communication

### Testing Platform
- The MCU chip **Atmega328P** is well known and the price is affordable as well as most of the robotic hardware that is described here. The Arduino Uno board comes with a removable MCU.
- **PlatformIO** is a cross-platform, cross-architecture, multiple framework, professional tool for embedded systems engineers and for software developers who write applications for embedded products. 
- **Visual Studio Code** is a streamlined code editor and it runs on macOS, Linux, and Windows. The best thing about VSCode, it is free.

### Raspberry Pi 5 as a computer
- I used Samsung SSD for fast processing with the Raspberry Pi 5 for testing circuits and code connected by USB to the Uno (atmega328PU) while debugging with a serial monitor.
  - Raspberry Pi 5 with 8GB [Hardware](https://www.raspberrypi.com/products/raspberry-pi-5/)
  - GeeekPi Metal Case for Raspberry Pi 5 [Å](https://www.amazon.com/GeeekPi-Raspberry-Active-Support-Peripheral/dp/B0CMZ84GM8?ref_=ast_sto_dp)
  - 52.PI M.2 MVNE SSD Adapter - NO4 for RP|5 [Å](https://www.amazon.com/GeeekPi-NVMe-Adapter-Raspberry-Support/dp/B0CRK4YB4C?ref_=ast_sto_dp)
  - SAMSUNG 990 EVO SSD [Å](https://www.amazon.com/Samsung-Internal-Computer-MZ-V9E1T0B-AM/dp/B0CRCC9863?th=1)
- Raspberry Pi OS
  - Use **Raspberry Pi Imager** to install of the [Raspberry Pi OS](https://www.raspberrypi.com/software/) onto the SD card.
  - Insert the card into RPi5, power up the board and follow the installation instructions.
- 52Pi - N04 M.2 2280 PCIe to NVMe
  - N04 is compatible with the standard HAT size of Raspberry Pi 5  [52Pi Wiki EP-0210](https://wiki.52pi.com/index.php?title=EP-0210)
    - 52Pi GPIO connects to the two rows of five pins as shown in the images. This is to power and to communicate to the SSD.]
- [Instructions](https://www.youtube.com/watch?v=kUBHWhdpbco)

### Boot Order
- The boot order among the **USB**, the **SD Card** and the **SSD card** might be puzzling and frustrating.
- Boot Order in Hexidecimal Values
  - **f** = **start again**  - *bits 1111*
  - **1** = check **SD Card**  - *bits 0001*
  - **4** = check **USB drive**  - *bits 0100*
  - **6** = check **PCie NVME**  - *bits 0110*
- The boot order might look like **0xf416** (*bits 1111 0100 0001 0110*) and will execute the following in the order listed...
  - RPi will start again first
  - RPi will then check the USB (usually for the OS)
  - RPi will then check the SD Card (usually for the OS)
  - RPi will finally check the PCie NVME (SSD card -  (usually for the OS)
- How to boot the RPi5 with the SD Card first (which is the default)
  - Use the boot order **0xf416**
  - This is is most likely accompilished while using the OS in the SD card...
- How to boot the RPi5 with the PCie NVME (SSD card) first before the CD Card
  - Use the boot order **0xf461**
  - This is is most likely accompilished while using the OS in the SSD card...
- How to change the boot order
  - (1) open a terminal panel
  - (2) Type in the following command
     - ***sudo rpi-eeprom-config --edit*** (see link below for more information
       - You might see the following:
       ```
         [all]
         BOOT_UART=1
         POWER_OFF_ON_HALT=0
         BOOT_ORDER=0xf416
       ```
  - (3) The statement ***BOOT_ORDER=0xf416*** is where the boot order can be changed...
  - Update the bootloader configuration [Raspberry Pi Documentation](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#update-the-bootloader-configuration)

### Using other Raspberry Pi for Atmega328PU communication
- Under development
