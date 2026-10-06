# Panda パンダ, a JESK56 (Swiss-Layout) Keymap

Vanilla QMK firmware for the RP2040-based [JESK56](https://github.com/triliu/jesk56), with VIA support, a Swiss German QWERTZ keymap, four compiled combos, and key overrides. Set your operating system's keyboard layout to **Swiss German**.

<img alt="Static Badge" src="https://qmk.fm/badge-dark.svg" style="width:200px;">

## ToDo's

- [ ] new 3D Printed Case + open source it (currently on it)
- [ ] take pic

## Intro

// add spicy image

I initially was on the hunt for a new 56-Key Keyboard since the Lotus58 was so perfect already, except for portability.
Finding the JESK56 was like a dream come true -- a single-board 56-Key Keyboard, that is coincidentally also very cheap and easy to build, since it doesnt require any diodes.

// add build-guide 4 noobs

This is my first built-from-scratch keyboard. :)

## Specs

| Component | Quantity |
|-----------|----------|
| JESK56 PCB | 5x (minimum Order of JLCPCB, guide above) |
| [TTC Silent Bluish White Switches Tactile](https://aliexpress.com/item/1005008451623861.html) | 1x Pack of 60 Switches |

// add rp2040 controller
// add keycaps

## Build

Install [QMK and its build dependencies](https://docs.qmk.fm/newbs_getting_started) and Git. On NixOS: `nix shell nixpkgs#{qmk,git}`.

Use **vanilla QMK**, the hardware definition from upstream's **`QMK-vial/jesk56`** directory, and this keymap. Despite that directory's name, Vial is not required.

For fresh checkouts, run in Bash (revisions pinned to the tested sources):

```bash
mkdir -p "$HOME/dev"
git clone https://github.com/qmk/qmk_firmware.git "$HOME/dev/qmk"
git clone --filter=blob:none --sparse https://github.com/triliu/JESK56.git "$HOME/dev/JESK56"
git -C "$HOME/dev/JESK56" sparse-checkout set QMK-vial/jesk56
git -C "$HOME/dev/JESK56" checkout --detach eaf9473933c5bae33cda3221874a6308ade19f83

cd "$HOME/dev/qmk"
git checkout --detach 7a1bbf37c5c07da4ea0a162bb139083a46ef40a1
git submodule update --init --recursive
mkdir -p keyboards/triliu
cp -R "$HOME/dev/JESK56/QMK-vial/jesk56" keyboards/triliu/
git clone https://github.com/74k1/jesk56_firmware.git keyboards/triliu/jesk56/keymaps/74k1
git apply keyboards/triliu/jesk56/keymaps/74k1/qmk-compatibility.patch
qmk compile -c -kb triliu/jesk56/rp2040 -km 74k1
```

The patch updates upstream's scanner for current QMK GPIO and initialization APIs. Apply it once per fresh keyboard copy. For an existing setup, skip cloning and back up the old keyboard directory before replacing it, rather than merging the definitions. Edit `keyboards/triliu/jesk56/keymaps/74k1/keymap.c` and rerun the compile command to rebuild.

## Flash

1. Double-tap **RESET**. A USB drive named **RPI-RP2** should appear.
2. Copy `~/dev/qmk/triliu_jesk56_rp2040_74k1.uf2` onto it.
3. The keyboard reboots automatically.

If double-tap fails: hold **BOOT**, press and release **RESET**, then release **BOOT**.

## VIA

Open [VIA](https://usevia.app/) in Chromium, enable **Show Design tab** in Settings, and load [`via.json`](via.json) in Design using V3 mode. Authorize the keyboard to configure it. VIA GUI operation still needs hardware verification.

Combos remain compiled into the firmware: **Tab+1 → Escape**, **E+A/O/U → ä/ö/ü**. VIA remappings may survive reflashing; export them before resetting EEPROM.

## Credits

| Name | Remarks |
|------|---------|
| [T.G. Marbach](https://github.com/triliu) | For making the keyboard (and also helping me out a lot with the firmware in the beginning) |
| [laosteven](https://github.com/laosteven/fluffy-octo-eureka) | For the readme inspiration. |
