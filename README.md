<h1 align="center">pico-ducky</h1>

<div align="center">
  <strong>Turn your Raspberry Pi Pico into a USB Rubber Ducky</strong>
</div>
<br/>
<img src="images/logo.png" align="center">
<br/>

<div align="center">
  <img alt="GitHub code size in bytes" src="https://img.shields.io/github/languages/code-size/coder12341/pico-ducky">
  <img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/coder12341/pico-ducky">
</div>


<br />

## Install

## **Requirements**

------

 [CircuitPython for the Raspberry Pi Pico](https://circuitpython.org/board/raspberry_pi_pico/)

[adafruit-circuitpython-bundle-7.x-mpy-YYYYMMDD.zip](https://github.com/adafruit/Adafruit_CircuitPython_Bundle/releases/latest)

------

## **Setup**

1. Plug the Pico into your computer. It will show up as a removable media device named `RPI-RP2`.

2. Copy the downloaded `.uf2` file to the root of the Pico (`RPI-RP2`). The device will reboot and after a second or so, it will reconnect as `CIRCUITPY`.
3. Navigate to `lib` in the recently extracted folder and copy `adafruit_hid` to the `lib` folder in your Raspberry Pi Pico.

4. Clone this repository (`git clone https://github.com/coder12341/pico-ducky.git`) and copy the file `code.py` to the root folder of your Raspberry Pi Pico.

5. Create your payload and save it as `payload.dd` in the root folder of your Raspberry Pi Pico.

1. Be careful, if your device isn't in [setup mode](#setup-mode), the device will reboot and after a very short period of time, the script will run.

### Setup mode

To edit the payload, enter setup mode by connecting the pin 1 (`GP0`) to pin 3 (`GND`), this will stop the pico-ducky from injecting the payload in your own machine.
The easiest way to so is by using a jumper wire between those pins as seen bellow. The LED on your Raspberry Pi Pico will start blinking to indicate that it has successfully entered setup mode.

![Setup mode with a jumper](images/setup-mode.png)

### USB enable/disable mode

If you need the pico-ducky to not show up as a USB mass storage device for stealth, follow these instructions.  
Enter setup mode.  
Copy boot.py to the root of the pico-ducky.  
Copy your payload script to the pico-ducky.  
Disconnect the pico from your host PC.
Connect a jumper wire between pin 18 and pin 20.
This will prevent the pico-ducky from showing up as a USB drive when plugged into the target computer.  
Remove the jumper and reconnect to your PC to reprogram.
The default mode is USB mass storage enabled.   

![USB enable/disable mode](images/usb-boot-mode.png)

### Changing Keyboard Layouts

Copied from [Neradoc/Circuitpython_Keyboard_Layouts](https://github.com/Neradoc/Circuitpython_Keyboard_Layouts/blob/main/PICODUCKY.md)  

#### How to use one of these layouts with the pico-ducky repository.

**Go to the [latest release page](https://github.com/Neradoc/Circuitpython_Keyboard_Layouts/releases/latest), look if your language is in the list.**

#### If your language/layout is in the bundle

Download the `py` zip, named `circuitpython-keyboard-layouts-py-XXXXXXXX.zip`

**NOTE: You can use the mpy version targetting the version of Circuitpython that is on the device, but on Raspberry Pi Pico you don't need it - they only reduce file size and memory use on load, which the pico has plenty of.**

#### If your language/layout is not in the bundle

Try the online generator, it should get you a zip file with the bundles for yout language

https://www.neradoc.me/layouts/

#### Now you have a zip file

#### Find your language/layout in the lib directory

For a language `LANG`, copy the following files from the zip's `lib` folder to the `lib` directory of the board.  
**DO NOT** modify the adafruit_hid directory. Your files go directly in `lib`.  
**DO NOT** change the names or extensions of the files. Just pick the right ones.  
Replace `LANG` with the letters for your language of choice.

- `keyboard_layout.py`
- `keyboard_layout_win_LANG.py`
- `keycode_win_LANG.py`

Don't forget to get [the adafruit_hid library](https://github.com/adafruit/Adafruit_CircuitPython_HID/releases/latest).

This is what it should look like **if your language is French for example**.

![CIRCUITPY drive screenshot](https://github.com/Neradoc/Circuitpython_Keyboard_Layouts/raw/main/docs/drive_pico_ducky.png)

#### Modify the pico-ducky code to use your language file:

At the start of the file comment out these lines:

```py
from adafruit_hid.keyboard_layout_us import KeyboardLayoutUS as KeyboardLayout
from adafruit_hid.keycode import Keycode
```

Uncomment these lines:  
*Replace `LANG` with the letters for your language of choice. The name must match the file (without the py or mpy extension).*
```py
from keyboard_layout_win_LANG import KeyboardLayout
from keycode_win_LANG import Keycode
```

## Useful links and resources

### Docs

[CircuitPython](https://circuitpython.readthedocs.io/en/6.3.x/README.html)

[CircuitPython HID](https://learn.adafruit.com/circuitpython-essentials/circuitpython-hid-keyboard-and-mouse)

[Ducky Script](https://github.com/hak5darren/USB-Rubber-Ducky/wiki/Duckyscript)

[Ducky Payload Examples](https://github.com/hak5darren/USB-Rubber-Ducky/wiki/Payloads)
