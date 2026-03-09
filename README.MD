# Maker Coin PCB
The Maker Coin PCB is a MakerCoin sized breakout board featuring an STM32 Microcontroller compatible with Klipper & Kalico

It should be noted that V1.0, which was handed out at SMRRF2026, has two Silkscreen errors listed below.
> Boot0 & RESET are Flipped
> The "PA8" LED & Breakout Pin is actually pin PA0

To start with flashing, we will begin by installing katapult on your pi if you haven't already.

Firstly run the below, to make sure everything is uptodate and what we need is installed
``sudo apt update``
``sudo apt upgrade``
``sudo apt install python3 python3-serial``

Next, install katapult
``test -e ~/katapult && (cd ~/katapult && git pull) || (cd ~ && git clone https://github.com/Arksine/katapult) ; cd ~``

After installation has complete, run:
``cd ~/katapult``
and then
``make menuconfig``

Copy the config below and then hit Q to quit and then Y to save
<p align="center">
	<img src="images/Katapult_Config.png"/>
</p>


Next we will put the STM32 into DFU mode by holding "RESET" and single pressing "BOOT0"
You can check if the STM32 is in DFU mode by entering ``lsusb`` in the terminal
You should see something similar to the below image
<p align="center">
	<img src="images/DFU.png"/>
</p>
After confirming it is in dfu mode you can run
``make flash FLASH_DEVICE=0483:df11``
this will flash katapult to the STM32

after this is done, its likely it will still be in DFU mode as there is no Klipper/Kalico to boot to
You can once again check with lsusb, and if its not in DFU mode, make sure to enter it into DFU mode
