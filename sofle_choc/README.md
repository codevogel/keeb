# What is this?

This directory holds the QMK files that I use to flash my keyboard. This guide mainly serves as a reminder to myself on how to flash my keyboard, and how to set up the firmware, but if you stumble upon this and find it useful, then I'm glad to have helped. Feel free to use my keymap. (If you do, please let me know! I'd love to hear about it.) 

## The keeb

I use a [Sofle Choc](https://josefadamcik.github.io/SofleKeyboard/build_guide_choc.html). I put in a custom print order for the PCB at [jlcpcb](https://jlcpcb.com), and sourced the parts from [SplitKB](https://splitkb.com/).

## The firmware

There are two components in this directory:

   - `codevogel` is a directory that holds the QMK firmware for my keyboard. Explanation for the containing files can be found at [QMK's repo](https://github.com/qmk/qmk_firmware/blob/master/docs/config_options.md)
   - `sofle_choc_codevogel_qmk_keymap.json` holds the keybinds in JSON format. This is handy for when you want to use the [QMK Configurator](https://config.qmk.fm/#/sofle_choc/LAYOUT) to edit the keymap. (We can then run `qmk json2c` to convert the exported JSON to a C file, and nab the keymap array from there to re-use in `codevogel/keymap.c`.)

## Get started

1. Clone (optionally a personal fork of) the QMK firmware repository:
   
   ```bash
   git clone git@github.com:qmk/qmk_firmware.git
   ```

2. Copy the `codevogel` directory to `qmk_firmware/keyboards/sofle_choc/keymaps/`

3. Follow the instructions in the [QMK documentation](https://docs.qmk.fm/newbs_getting_started) to set up your environment.

4. (Optional:) Compile the firmware with the following command:

   ```bash
   qmk compile -kb sofle_choc -km codevogel
   ```
5. Unplug the Keeb. Remove the TRSS cable from both sides. Plug the USB cable back into one half of the Keeb. 

6. Compile and flash the firmware to your Keeb. When asked, short the ground pins to enter bootloader mode. (If things don't work, read step 7 to make sure you are using the right flasher) 

   ```bash
   qmk flash -kb sofle_choc -km codevogel
   ```

7. Update the `BOOTLOADDER` variable in `qmk_firmware/keyboards/sofle_choc/keymaps/codevogel/rules.mk`. The Elite-C (USB-C) controller needs the atmel-dfu bootloader, while the Pro Micro (USB-Mini) controller needs the caterina bootloader.

8. Repeat for the other half of the Keeb.

9. Enjoy your new keymap!
