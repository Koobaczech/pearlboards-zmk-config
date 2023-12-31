# Pearlboards ZMK Firmware (ZeusPad, Pearl 40% R2, Atlas65, Zeus TKL)

This is the ZMK firmware for all Pearlboards boards.
You can find more info on our projets here [Pearlboards](https://pearlboards.net/) here [Discord](https://discord.gg/SMuBMmPY) and here [CadlabCNC](https://cadlabcnc.com).
  <br>
  <br>
A huge thanks to the entire ZMK team and my keyboard friends Hedgey, Flawmenco, etc for making all of this possible.
## Getting Started
### Overview
- By leveraging ZMk and GitHub Actions, this repository will automatically build a flashable firmware file for your PCB whenever a commit is pushed to it.
- For example, if you edit and change your keymap and commit your changes, this repo will build your new firmware file which you can then download and flash.
### Setup
- If you have not already done so, create a GitHub account (simple).
- Fork this repository (top right button usually above the ABOUT section), [More about Forking](https://github.com/orgs/community/discussions/35849).
- Enable GitHub Actions on your forked repo [More about Github Actions](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository).
- NOT NEEDED, BUT HERE IF YOU WANT TO READ MORE [ZMK Setup Instructions](https://zmk.dev/docs/user-setup#summary).
  <br>
  <br>
## Modifying your keyboards keymap
- You can edit the keymap in '/zmk-config/config/boards/arm/<keyboard>/<keyboard>.keymap' to suit your needs, and then build it with the instructions below.
    - For example, if you wanted to modify Pearls keymap, edit '/zmk-config/config/boards/arm/pearl/pearl.keymap'.
    - The encoder functionality (if supported on that PCB) can be changed in the keymap file as well.
- All ZMK Keycodes found [here](https://zmk.dev/docs/codes).
  <br>
  <br>
## Building the firmware with GitHub Actions on your forked Repo
- Simply push a commit to trigger the build.
- Notice a 'firmware.zip' artifact from your latest (and hopefully successful) Github Actions run for the build.
  <br>
  <br>
## Flashing the firmware
- Download the 'firmware.zip' artifact from your latest successful Github Actions run for the build.
- Unzip it and you should see a .uf2 file named after your specific PCB.
- Plug the PCB into your computer.
    - Double press in quick succession the physical RESET button on your pcb.
    - Right after ou should see the board mount as a USB device 'NRF52BOOT' (or similar if using a different controller) on your computer.
    - Open that USB device in your file explorer, and copy or drag and drop the .uf2 for the right side into it.
    - DO NOT WORRY IF IT FAILS WITH a '1 Interrupted Action' dialog popping up, asking you to Try Again, Skip or Cancel, as it has most likely been flashed at this point.
    - Once copied the devie will automatically disconnect and flash itself, most likely displaying the message above.
  <br>
  <br>
## Specifying how many keyboards firmwares get built
- You can edit '/zmk-config/build.yaml' to include or exclude whichever keyboards you want.
- By default, all of the Pearlboards keyboards are set to build at once whenever a commit is pushed.
  <br>
  <br>
## Other ZMK configurations
- Feel free to poke around all the other board files and enable or disable whatever things you want.
    - This can be things such as underglow, debug logging, sleep timeouts etc..
 - If your build is not successfull at this point please do not blame me xD.
 - More help can be found [here](https://discord.gg/jFzBGF6u5Q).
  
## Working with different Bluetooth profiles
- [ZMK Docs](https://zmk.dev/docs/behaviors/bluetooth)
- Please note there are five (0, 1, 2, 3, 4) available Bluetooth profiles by default. If you need to adjust the number of available profiles, set CONFIG_BT_MAX_CONN and CONFIG_BT_MAX_PAIRED to the desired number of profiles ,n, in your zmk-config.conf file.
- If you would like to pair to another device, but still maintain the previous pairing, use a keycode ('BT_NXT or BT_PRV or BT_SEL <number>')to move to a new profile and then pair to your device.
- If you would like to use the current profile to connect to a new device, you have to clear it first with this keycode 'BT_CLR', and then pair to the new device.
- For example you would like to use the third (aka profile 2 since its indexed by 0) profile to connect to a new device, you have to switch to it first ('BT_SEL 2') and then clear it with the same keycode 'BT_CLR', and then pair to the new device.
  <br>
  <br>
## Switching between Bluetooth and wired modes
- [ZMK Docs](https://zmk.dev/docs/behaviors/outputs)
- No matter what profile you are in, to switch between whats paired there and wired mode (if connected), simply use the keycode 'OUT_TOG'.
- To favor a wired connection use the keycode "OUT_USB".
    - This means that if you select a paired profile, or pair a new device, the keyboard will remain in wired mode until you use the keycode 'OUT_TOG'.
- To favor a wireless connection use the keycode 'OUT_BLE'.
    - This means that if you are wired in, and select a paired profile, or pair a new device, the keyboard will start working in bluetooth mode until you use the keycode "OUT_TOG".
<br>
<br>
  Enjoy! For all other information please join our [Discord](https://discord.gg/SMuBMmPY)
