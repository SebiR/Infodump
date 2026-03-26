# Objective

The goal was to control an ePaper display connected to a Raspberry Pi in Node-RED on this very Raspberry Pi.

# Prerequisites
## Hardware

## Software
### Node-RED

To run Python3 scripts in Node-RED, I used the node [node-red-contrib-python3-function](https://flows.nodered.org/node/node-red-contrib-python3-function).
This enables us to put our Python code directly into Node-RED and pass JSON objects easily into and out of Python.

There might be better ways to do this (like [node-red-contrib-python-venv](https://flows.nodered.org/node/@background404/node-red-contrib-python-venv)), bzut for now this works just fine.

### Python/Waveshare
Install Python3 and the Waveshare ePaper display examples as described [in this Waveshare tutorial](https://www.waveshare.com/wiki/2.13inch_e-Paper_HAT_Manual#Working_With_Raspberry_Pi)

```bash
# Create subfolder in /home/pi for Python projects
mkdir python
cd python/
mkdir epaper
cd ..

# Copy ePaper libary and pic folder into new project folder
cp -r e-Paper/RaspberryPi_JetsonNano/python/lib/ python/epaper/
cp -r e-Paper/RaspberryPi_JetsonNano/python/pic/ python/epaper/
```

# Using the display
```python
import os
import sys
os.chdir("/home/pi/python/epaper/")

import json

picdir = 'pic'
libdir = 'lib'
if os.path.exists(libdir):
    sys.path.append(libdir)

import logging
from waveshare_epd import epd2in13_V4
import time
from PIL import Image,ImageDraw,ImageFont
import traceback

logging.basicConfig(level=logging.DEBUG)

pload = msg['payload']
```