# Equipment


Adafruit [ItsyBitsy M4 Express](https://www.adafruit.com/product/3800).


# Log

## 8/1/21

With Ryker.

### Preliminaries

Install Mu editor and choose CircuitPython application with the ItsyBitsy plugged into my laptop. Opening the editor automatically connects to the ItsyBitsy.

Open the serial terminal.

### Board setup

#### Update software

Go to circuitpython.org [ItsyBitsy M4 Express by Adafruit](https://circuitpython.org/board/itsybitsy_m4_express/).

##### Current CircuitPython version

`boot_out.txt`:

    Adafruit CircuitPython 3.1.1 on 2018-11-02; Adafruit ItsyBitsy M4 Express with samd51g19

##### Update Bootloader

Follow [updating your bootloader](https://learn.adafruit.com/introducing-adafruit-itsybitsy-m4/update-the-uf2-bootloader#updating-your-bootloader-3061298-2). Double click reset button while ItsyBitsy is plugged into my laptop (*Once successful, the RGB LED on the board will flash red and then stay green. A new drive will show up on your computer*) to get to the `ITSYM4BOOT` drive and go to Finder and look at `INFO_UF2.TXT`:

    UF2 Bootloader v2.0.0-adafruit.7 SFHWRO
    Model: ItsyBitsy M4 Express
    Board-ID: SAMD51G19A-Itsy-v0

Download `update-bootloader-itsybitsy_m4-v3.13.0.uf2` from [ItsyBitsy M4 Express by Adafruit](https://circuitpython.org/board/itsybitsy_m4_express/) and drag to `ITSYM4BOOT`. Wait for bootloader to install and `ITSYM4BOOT` to become available in the Finder again. Examine `INFO_UF2.TXT` and confirm that the bootloader is updated:

    UF2 Bootloader v3.13.0 SFHWRO
    Model: ItsyBitsy M4 Express
    Board-ID: SAMD51G19A-Itsy-v0

##### Update CircuitPython

Download `adafruit-circuitpython-itsybitsy_m4_express-en_US-6.3.0.uf2` from [ItsyBitsy M4 Express by Adafruit](https://circuitpython.org/board/itsybitsy_m4_express/). Drag file in Finder to `ITSYM4BOOT` drive. Board will reboot and come back as `CIRCUITPY` drive. See [Installing CircuitPython](https://learn.adafruit.com/welcome-to-circuitpython/installing-circuitpython) for description of complete process.

Now boot_out.txt contains:

    Adafruit CircuitPython 6.3.0 on 2021-06-01; Adafruit ItsyBitsy M4 Express with samd51g19


### Blink onboard LED

Use the following code to blink the red LED and get help for `board`:

    import board
    import digitalio
    import time
    
    print("Hello world again")
    print(help(board))
    
    red_led = digitalio.DigitalInOut(board.LED)
    red_led.direction = digitalio.Direction.OUTPUT
    
    while True:
        red_led.value = True
        time.sleep(0.5)
        red_led.value = False
        time.sleep(0.5)
        
Output in serial terminal:

    main.py output:
    Hello world again
    object <module ''> is of type module
      A0 -- board.A0
      A1 -- board.A1
      A2 -- board.A2
      A3 -- board.A3
      A4 -- board.A4
      A5 -- board.A5
      D0 -- board.D0
      RX -- board.D0
      D1 -- board.D1
      TX -- board.D1
      D2 -- board.D2
      D3 -- board.D3
      D4 -- board.D4
      D5 -- board.D5
      D7 -- board.D7
      D9 -- board.D9
      D10 -- board.D10
      D11 -- board.D11
      D12 -- board.D12
      LED -- board.LED
      D13 -- board.LED
      SDA -- board.SDA
      SCL -- board.SCL
      SCK -- board.SCK
      MOSI -- board.MOSI
      MISO -- board.MISO
      APA102_MOSI -- board.APA102_MOSI
      APA102_SCK -- board.APA102_SCK
      I2C -- <function>
      SPI -- <function>
      UART -- <function>
    None

### RGB LED

- Read through [ItsyBitsy M0 CircuitPython Libraries](https://learn.adafruit.com/introducing-itsy-bitsy-m0/circuitpython-libraries).
- Download `adafruit-circuitpython-bundle-6.x-mpy-20210731.zip` from [July 31, 2021 release](https://github.com/adafruit/Adafruit_CircuitPython_Bundle/releases/tag/20210731) and unzip. Note that it has the following directories:
    - `examples`
    - `lib`
    - `requirements`
- Create a `lib` directory on the ItsyBitsy.
- Copy `adafruit_dotstar.mpy` in `lib` in the downloaded bundle to `lib` on the ItsyBitsy. Now the needed RGB LED python package is installed.
- From [CircuitPython Internal RGB LED](https://learn.adafruit.com/introducing-itsy-bitsy-m0/circuitpython-internal-rgb-led), get first code and modify brightness:
        
        """CircuitPython Essentials Internal RGB LED red, green, blue example"""
        import time
        import board
        
        # For Trinket M0, Gemma M0, ItsyBitsy M0 Express, and ItsyBitsy M4 Express
        import adafruit_dotstar
        led = adafruit_dotstar.DotStar(board.APA102_SCK, board.APA102_MOSI, 1)
        # For Feather M0 Express, Metro M0 Express, Metro M4 Express, Circuit Playground Express, QT Py M0
        # import neopixel
        # led = neopixel.NeoPixel(board.NEOPIXEL, 1)
        
        led.brightness = 0.03
        
        while True:
            led[0] = (255, 0, 0)
            time.sleep(0.5)
            led[0] = (0, 255, 0)
            time.sleep(0.5)
            led[0] = (0, 0, 255)
            time.sleep(0.5)
            led[0] = (0, 0, 0)
            time.sleep(0.5)
    
- Next, do the colorwheel code with modified brightness:

        """CircuitPython Essentials Internal RGB LED rainbow example"""
        import time
        import board
        
        # For Trinket M0, Gemma M0, ItsyBitsy M0 Express and ItsyBitsy M4 Express
        import adafruit_dotstar
        led = adafruit_dotstar.DotStar(board.APA102_SCK, board.APA102_MOSI, 1)
        # For Feather M0 Express, Metro M0 Express, Metro M4 Express, Circuit Playground Express, QT Py M0
        # import neopixel
        # led = neopixel.NeoPixel(board.NEOPIXEL, 1)
        
        
        def colorwheel(pos):
            # Input a value 0 to 255 to get a color value.
            # The colours are a transition r - g - b - back to r.
            if pos < 0 or pos > 255:
                return 0, 0, 0
            if pos < 85:
                return int(255 - pos * 3), int(pos * 3), 0
            if pos < 170:
                pos -= 85
                return 0, int(255 - pos * 3), int(pos * 3)
            pos -= 170
            return int(pos * 3), 0, int(255 - (pos * 3))
        
        
        led.brightness = 0.03
        
        i = 0
        while True:
            i = (i + 1) % 256  # run from 0 to 255
            led.fill(colorwheel(i))
            time.sleep(0.01)
    
## 8/29/21

### Objective

Get the ultrasonic distance sensor to work.

### Parts

- [CircuitPython Starter Kit with Adafruit Itsy Bitsy M4](https://www.adafruit.com/product/4028), $24.95
    - [ItsyBitsy M4 Express](https://www.adafruit.com/product/3800)
    - Small breadboard
    - Wires
- [Ultrasonic Distance Sensor - 3V or 5V - HC-SR04 compatible - RCWL-1601](https://www.adafruit.com/product/4007#technical-details), $3.95

### Info

- [Pinouts](https://learn.adafruit.com/introducing-adafruit-itsybitsy-m4/pinouts)
- Tutorials
    - [Adafruit - Ultrasonic Distance Sensors](https://learn.adafruit.com/ultrasonic-sonar-distance-sensors)
    - [Ultrasonic Sonar Distance Sensor](https://www.youtube.com/watch?v=opes_7Uf49U&t=2752s) in Youtube [CircuitPython Tutorial by Derek Banas](https://www.youtube.com/watch?v=opes_7Uf49U)

### Preparation

- Copy `adafruit_hcsr04.mpy` to `lib/` on microcontroller using Mac OS Finder.
- Wire up microcontroller and sensor
    - Vcc &rarr; 3.3V on microcontroller
    - Trigger &rarr; D9
    - Echo &rarr; D10
    - GND &rarr; G

### Code

See 48:31 from [Ultrasonic Sonar Distance Sensor](https://www.youtube.com/watch?v=opes_7Uf49U), which comes from [this Adafruit tutorial](https://learn.adafruit.com/ultrasonic-sonar-distance-sensors/python-circuitpython).

    """https://www.youtube.com/watch?v=opes_7Uf49U at 48:13"""
    import time
    import board
    import adafruit_hcsr04
    
    sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D9, echo_pin=board.D10)
    
    while True:
        try:
            print(sonar.distance)
        except RuntimeError:
            print("Retrying...")
        time.sleep(0.1)

Output: continuous stream of distance in cm in the terminal.

### Next

- See 50:55 [Ultrasonic Sonar Distance Sensor](https://www.youtube.com/watch?v=opes_7Uf49U) for code to run 2 wheel car with [Adafruit Crickit](https://learn.adafruit.com/make-it-move-with-crickit).
    - [Adafruit CRICKIT for Circuit Playground Express](https://www.adafruit.com/product/3093), $29.95
    - [Circuit Playground Express](https://www.adafruit.com/product/3333), $24.95
- See 51:18 [Ultrasonic Sonar Distance Sensor](https://www.youtube.com/watch?v=opes_7Uf49U) for IR remote controlled car.

