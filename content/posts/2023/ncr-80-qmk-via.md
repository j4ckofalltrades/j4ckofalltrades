--- 
date: 2023-04-25T17:16:02+08:00
title: "NCR-80 QMK/VIA firmware"
description: "QMK/VIA firmware for the NCR-80 keyboard"
draft: false
categories:
- keyboards
tags:
- qmk
- via
images:
- https://res.cloudinary.com/j4ckofalltrades/image/upload//c_limit,w_900,g_face/v1676107180/keebs/ncr80/ncr-80-via_hlgb5c.png
---

Built the [NCR-80](https://jduabe.dev/posts/2022/ncr-80) last year, great-looking board especially if you like the
retro aesthetic, and is a pleasure to type on.

One thing I did notice was that the product listing points to a Google Drive link to the pre-compiled [QMK and VIA firmware](https://drive.google.com/drive/folders/1e3mjUg-N15SFVrExlBiI01-XOKpPm9ry?usp=sharing),
but it hasn't been added to the QMK and VIA repositories. I thought this would be a good weekend project (**Spoiler**: it took longer than a weekend).

I wrote the steps of how I got it done (the steps also apply to any keyboard firmware).

## Converting KBFirmware JSON to QMK

The starting point is to convert the KBFirmware JSON from the provided "QMK" files from the product listing, and then
converting them to QMK formatted files.

There are a couple of tools that can be used for this purpose:

- Recommended: [KBFirmware JSON to QMK Parser](https://noroadsleft.github.io/kbf_qmk_converter)
- Deprecated: [Keyboard Firmware Builder](https://kbfirmware.com)

The resulting files will be the base of the QMK firmware for the keyboard.

## Creating a QMK pull request

Make sure to read the [contribution guide](https://docs.qmk.fm/#/contributing?id=keyboards) as a first step.
It is also a good idea to check out other supported keyboard firmware to get a feel for the directory structure, and conventions in use.

A keyboard firmware folder (simplified example) should look something like:

```sh
mt
|-- ncr80
|   |-- keymaps
|       |-- default
|           |-- keymap.c
|-- info.json
|-- readme.md
`-- rules.mk
```

In cases where keyboards have multiple versions or revisions e.g. rev1, rev2 or hotswap/soldered, the directory structure
will look different; refer to QMK's contribution guide linked above.

Link to the pull request on GitHub for reference: [[Keyboard] Add NCR-80](https://github.com/qmk/qmk_firmware/pull/19130)

## Creating a VIA pull request

In order to add VIA support for a keyboard, it is required to enable the VIA feature in QMK, and adding a `via`-compatible
keymap for the keyboard. You can check out the QMK pull request linked above; look for the `keymaps/via` directory.

Read the VIA docs for [configuring QMK](https://www.caniusevia.com/docs/configuring_qmk) for a more in-depth guide.
I also recommend reading about the [VIA spec](https://www.caniusevia.com/docs/specification).

It is also required to have the QMK pull request merged in before contributing to the VIA repository.

## VIA V2 vs V3 definitions

It is basically just a matter of copying the VIA `json` files from the Drive link referenced at the start of this post.
The main difference here is the location of the definitions depend on the version; `V2` definitions are located in the
`src/<manufacturer>/<keyboard>` directory while the `V3` definitions are in the `v3/<manufacturer>/<keyboard>`.

If you have a `V2` definition, you can convert it a `V3` definition by running the `scripts/build-all.ts` file in the
[via keyboards](https://github.com/the-via/keyboards) repository.

Link to the pull request on GitHub for reference: [Add support for NCR-80](https://github.com/the-via/keyboards/pull/1548)

That's it, once the pull request gets merged VIA should be able to detect your keyboard.

![VIA NCR-80](https://res.cloudinary.com/j4ckofalltrades/image/upload/v1676107180/keebs/ncr80/ncr-80-via_hlgb5c.png)