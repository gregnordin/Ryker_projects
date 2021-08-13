# 2021-07-04

Create [How To Build A Simple Raspberry Pi Pico Robot](https://www.tomshardware.com/how-to/raspberry-pi-pico-robot).

- Put together robot car chasis, wiring, and connect to RPi Pico on Kitronick's motor driver board
- Try to use Thonny but have problems
    - Have to set up Thonny correctly for RPi Pico. Use [Getting Started with Thonny MicroPython IDE for ESP32 and ESP8266](https://microcontrollerslab.com/getting-started-thonny-micropython-ide-esp32-esp8266/) to learn how to select RPI Pico from within Thonny and connect to it.
- Once connected to RPi Pico, have to let Thonny download and install updated micropython version.
- Notice that the RPi Pico is connected at `/dev/cu.usbmodem14401` on my mac.
- Can't get LED to flash with RPi Pico connected to motor driver board so pull it out and connect by itself to my mac laptop
- Use the Step 2 code at [Raspberry Pi Pico LED Blink](https://www.instructables.com/Raspberry-Pi-Pico-LED-Blink/) to get LED to blink.
- Also learn how to use Thonny better. Key commands:
    - When change `main.py` file on the RPi Pico:
        - Save file
        - Hit Stop button in Thonny
        - Hit Play button in Thonny and newly saved program will start operating

## Resources

- [Micropython Quick reference for the RP2](https://docs.micropython.org/en/latest/rp2/quickref.html)
- [Raspberry Pi P2040 getting started](https://www.raspberrypi.org/documentation/rp2040/getting-started/)
- [Raspberry Pi Pico Python SDK - A MicroPython environment for RP2040 microcontrollers](https://datasheets.raspberrypi.org/pico/raspberry-pi-pico-python-sdk.pdf) - Look at Sect. 3.1 to blink LED with a Timer interrupt class
- Download free book [Get Started with MicroPython on Raspberry Pi Pico](https://hackspace.raspberrypi.org/books/micropython-pico/pdf)