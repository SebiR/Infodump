# Objective

The goal was to control an ePaper display connected to a Raspberry Pi in Node-RED on this very Raspberry Pi.

# Prerequisites
## Hardware

## Software
### Node-RED

### Python/Waveshare
Install Python3 and the Waveshare ePaper display examples as described [in this Waveshare tutorial](https://www.waveshare.com/wiki/2.13inch_e-Paper_HAT_Manual#Working_With_Raspberry_Pi)

```# Create subfolder in /home/pi for Python projects
mkdir python
cd python/
mkdir epaper
cd ..

# Copy ePaper libary into new project folder
cp -r e-Paper/RaspberryPi_JetsonNano/python/lib/ python/epaper/
```

