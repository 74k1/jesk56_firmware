# Panda パンダ, a JESK56 (Swiss-Layout) Keymap

> The JESK56 keyboard is a single-board keyboard with 4x6 column staggered keys and 5 thumb keys. It utilises a new type of circuit design stemming from graph theory and mathematical design theory.
> [T. G. Marbach](https://github.com/triliu)

<img alt="Static Badge" src="https://qmk.fm/badge-dark.svg" style="width:200px;">

## ToDo's

- [ ] new 3D Printed Case + open source it (currently on it)
- [ ] take pic
- [ ] update readme.md

## Intro

// add spicy image

I initially was on the hunt for a new 56-Key Keyboard since the Lotus58 was so perfect already, except for portability.
Finding the JESK56 was like a dream come true -- a single-board 56-Key Keyboard, that is coincidentally also very cheap and easy to build, since it doesnt require any diodes

// add build-guide 4 noobs

This is my first built-from-scratch keyboard. :)

## Specs

| Component | Quantity |
|-----------|----------|
| JESK56 PCB | 5x (minimum Order of JLCPCB, guide above) |
| [TTC Silent Bluish White Switches Tactile](https://aliexpress.com/item/1005008451623861.html) | 1x Pack of 60 Switches |

// add rp2040 controller
// add keycaps

## How do I flash this?

1. Install [QMK](https://docs.qmk.fm/#/newbs) and git
2. do a

   `git clone https://github.com/vial-kb/vial-qmk ~/qmk`
3. then a

   `mkdir -p ~/qmk/keyboards/triliu`
4. then do a

   `git clone https://github.com/triliu/jesk56 ~/qmk/keyboards/triliu/jesk56`

5. finally a

   `git clone https://github.com/74k1/jesk56_firmware ~/qmk/keyboards/triliu/jesk56/keymaps/74k1`
6. now you should be able to compile it with a simple:

   `qmk compile -kb triliu/jesk56/rp2040 -km 74k1`
8. then flash your boards with the qmk command: (to put your board into boot-mode, press the top soldered button twice 😉)

   `qmk flash -kb triliu/jesk56/rp2040 -km 74k1`

## Credits

| Name | Remarks |
|------|---------|
| [T.G. Marbach](https://github.com/triliu) | For making the keyboard (and also helping me out a lot with the firmware in the beginning) |
| [laosteven](https://github.com/laosteven/fluffy-octo-eureka) | For the readme inspiration. |

