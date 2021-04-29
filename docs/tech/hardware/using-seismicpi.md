# Using the SeismicPi board

The SeismicPi board is a custom-made Raspberry Pi hat that can also be used as a standalone datalogger for recording data from a seismometer. It can do this by saving data to a microSD card or while tethered to a PC  by a USB cable, as well as attached to a Raspberry Pi. For measurements, there are 4 external inputs on screw terminals, as well as a built-in 3-axis accelerometer. It has a Real Time Clock (RTC) with battery backup (CR1225 - included), an RGB indicator LED, a button, a latching microSD holder and a microUSB connector for power and PC serial connection, as well as the usual Raspberry Pi 40-pin GPIO connector. There is also space on the board to solder a 20-pin header, but this is unlabelled and apparently undocumented, so I'm not sure what you can do with it. A [datasheet](https://www.mindsetsonline.co.uk/Downloads/SeismicPi_Datasheet_27-10-18.pdf) is available from the Mindsets UK website.

I was really excited by the potential of this board. The fact that it could be used as a standalone device as well as on a Raspberry Pi made it tremendously flexible. It meant that I could position the Legomometer in the best place for recording without worrying about having it tethered to a computer. At it's heart the board is just a sensitive and high quality 4-channel Analogue-to-Digital converter, so it could potentially be used for other measurement projects in future.

Rather irritatingly, the [jAmaSeis](www.iris.edu/hq/jamaseis/) software download links and instructions are hidden behind a sign-up page, so once you've downloaded the software make sure you keep the web page open or read through and keep a copy of the instructions before closing your browser!

I am using a computer running Ubuntu Linux, so all the instructions below are for that operating system. Details will vary for Windows/Mac, but follow the instructions on the jAmaSeis website and the guide included with the kit and it should be pretty simple.

The Linux install of jAmaSeis requires some additional libraries first:

```shell
    sudo apt install openjdk-11-jre
    sudo apt install libcanberra-gtk-module
    sudo apt install librxtx-java
    sudo ln -s /usr/lib/jni/librxtxSerial.so /usr/lib/
    sudo usermod -a -G dialout $USER
```

The last line adds your user to the `dialout` group, which is essential for serial communications with the SeismicPi board. For the permissions change to take effect you need to completely logout and login again, and the easiest way to do this is to **reboot your computer**. *Don't* do as I did and spend ages thinking "why the [*expletive*] isn't this working?!?" before realising that.

Once the computer's rebooted, you can download the jAmaSeis Linux installer and run:

```shell
sh jAmaSeis_1_11_8_097.sh
```

  Change to the directory where it installed the program and finally run the following to start jAmaSeis:

```shell
sh run.sh
```

After that, you can follow the guide included with the kit to set up jAmaSeis and start recording a trace. Spend a bit of time adjusting the startup string to explore the different sampling rates and gain levels and see how they affect the sensitivity and resolution of the recorded trace before moving on:

```text
Startup string: 4ase
                ||||
       gain_____||||____input
                 ||
   sample rate___||___channel mode

'4ase' = gain × 4, 32 samples per second, single channel mode, external input

Possible values are:

gain:                        input:
  1  ×1 = 0.64μV/count         e  use external inputs
  2  ×2 = 0.32μV/count         i  use internal accelerometer
  4  ×4 = 0.16μV/count
  8  ×8 = 0.08μV/count
  
sample rate:                 channel mode:
  a  32 samples per second     s  single channel mode
  b  64 samples per second     m  multi channel mode
  c  128 samples per second
```

## Installing and testing the datalogging firmware

As I said, I wanted to use the SeismicPi board as a standalone datalogger without it being tethered to a computer. I eventually discovered that this required a change of firmware on the board.

When it is delivered, the board contains the [streaming firmware](http://www.mindsetsonline.co.uk/Downloads/SeismicPi_Streaming_Firmware_27-10-18.zip) that can be downloaded from the Mindsets UK website. This continually sends out data over the serial connection, and accepts the limited, single character commands shown above, to change its behaviour. While this helps you get up and running quickly with the jAmaSeis software, it doesn't let you exploit all the board's features. In particular, it has no method of logging data to the microSD card instead.

A bit of Googling turned up this [GitHub site for SeismicPi](https://github.com/SeismicPi/SeismicPi) which looked much more promising, but I noted that the last commit was 22nd September 2015, more than 6 years ago, so it was definitely not being actively developed any more. Anyway, I started exploring and, eventually, found what I was after.

An alternative firmware for the board is in the GitHub repository as `Firmware/SeismicPi_Firmware/Debug/SeismicPi_Firmware.bin`. [Download it](https://github.com/SeismicPi/SeismicPi/blob/master/Firmware/SeismicPi_Firmware/Debug/SeismicPi_Firmware.bin) and save it to a microSD card as a file called `firmware.bin`. Put the card into the SeismicPi's microSD card holder, and hold down the button while connecting it to a USB power supply. If all goes well, you should see the LED flash a couple of different colours and then rapidly flicker green as it copies the firmware to the flash memory on the board. It will then automatically reboot and the LED will settle on a steady dim red to show it is ready. If you press the button now, you should see the LED start flashing to show that it is logging data. It flashes green once a second, with a blue flash every minute. Press the button again to stop datalogging, and the flashing will stop.

Unplug the board, eject the microSD card and put it back into your computer. You should see that there is new file on the card called `LOG.BIN` that contains the logged data. If you've got this far, **well done!** It took me the best part of a day to figure all that out.

## Using the datalogger

The firmware appeared to be built using a very expensive tool called [Processor Expert](https://www.nxp.com/design/software/development-software/processor-expert-software:PEX_DEV_TOOLS), so it didn't look like I would be able to modify it in any way. But as well as the firmware, and the source code to build it, the SeismicPi repository also contained various bits of documentation and a Python module, tools and demo scripts for using with the board. This was more useful, if rather outdated. Some of the Python scripts were built for Python 2, which is [no longer being developed](https://www.python.org/doc/sunset-python-2/), so I wanted to update things to the more current Python 3. I initially forked a copy of SeismicPi into my own GitHub account, but since most of the repository is to do with the firmware itself (which I can't change), I eventually decided to create my own separate and much simpler GitHub repository instead, just for the updated tools and documentation that I was using:

[https://github.com/scripsi/legomometer](https://github.com/scripsi/legomometer)

You should find all you need there to work with the Legomometer in datalogging mode.