---
draft: false
date: 2023-06-16T21:00:00+08:00
title: "Playing around with the Badger2040"
description: "Creating a digital lanyard / badge with the Badger2040"
categories:
- tech
tags:
- badger2040
- rp2040
externalLink: ""
---

[Badger2040](https://shop.pimoroni.com/products/badger-2040) is a programmable E Paper/eInk/EPD badge, powered by
the [RP2040](https://www.raspberrypi.com/products/rp2040).

Some of its features:

- _2.9" black and white E Ink® display (296 x 128 pixels)_
- _Powered by RP2040 (Dual Arm Cortex M0+ running at up to 133Mhz with 264kB of SRAM)_
- _2MB of QSPI flash supporting XiP_
- _Five front user buttons_
- _Reset and boot buttons (the boot button can also be used as a user button)_
- _USB-C connector for power and programming_
- _JST-PH connector for attaching a battery (input range 2.7V - 6V)_

I got one to play around with and to use when attending meetups.

## Programming

The Badger2040 ships with a custom [MicroPython](https://micropython.org/) build and a graphics library
[PicoGraphics](https://github.com/pimoroni/pimoroni-pico/blob/main/micropython/modules/picographics/README.md) that
contains useful utilities for drawing on the screen. There are also a couple of examples loaded on the device by
default.

In order to write code or update / run the existing  code samples, you'll need to connect it to your computer and open
up an IDE with MicroPython support i.e. [Thonny](https://thonny.org/).

One thing to note is you opt to use a different IDE is to make sure to name the file as `main.py` as it will be
automatically run once uploaded to the device (this is the default behavior of the RP2040), otherwise your code will not
be executed.

I ended up using [PyCharm](https://www.jetbrains.com/pycharm/) with the [MicroPython](https://plugins.jetbrains.com/plugin/9777-micropython)
plugin, one extra step I needed to do was to point the plugin to the device which was located at `/dev/ttyACM0`
(if you're on a Unix environment).

## Drawing

With the following built-in functions, we can draw text and shapes on the screen.  

### Constants

The screen dimensions are provided as constants.

```python
import badger2040

WIDTH = badger2040.WIDTH    # 296
HEIGHT = badger2040.HEIGHT  # 128
```

### Pen

There are 16 pen colours - or "shades of grey" - to choose, from 0 (black) to 15 (white).

```python
import badger2040

display = badger2040.Badger2040()

display.set_pen(
  colour  # int: color from 0 to 15
)
```

The thickness of the lines drawn on the screen can be also be configured.

```python
import badger2040

display = badger2040.Badger2040()

display.set_thickness(
  value  # int: thickness in pixels
)
```

### Text

The font can be changed with the `set_font` method and write using the `text` function.

```python
import badger2040

display = badger2040.Badger2040()

# Available fonts
#
# Bitmap
# - bitmap6
# - bitmap8
# - bitmap14_outline
#
# Vector
# - sans
# - gothic
# - cursive
# - serif_italic
# - serif
display.set_font(font)

display.text(
  text,       # the text string to draw 
  x,          # the destination X coordinate
  y,          # the destination Y coordinate
  wordwrap,   # number of pixels width before trying to break text into multiple lines
  scale,      # size
  angle,      # rotation angle (Vector only!)
  spacing     # letter spacing
)
```

### Shapes

There are quite a few functions available here, I just included the ones I used. You can check out the full list in the
[Pico Graphics function reference](https://github.com/pimoroni/pimoroni-pico/tree/main/micropython/modules/picographics).

__Line__ 

```python
import badger2040

display = badger2040.Badger2040()

display.line(x1, y1, x2, y2)
```

__Rectangle__

```python
import badger2040

display = badger2040.Badger2040()

display.rectangle(x, y, width, height)
```

## Putting it all together

<figure>
  <img src="https://res.cloudinary.com/j4ckofalltrades/image/upload/v1688813596/blog/badger2040_x9iaec.jpg" />
  <figcaption style="font-style:italic; text-align: center; font-size: 16px; padding-bottom: 20px;">
    Badger2040 running the full "badge" code
  </figcaption>
</figure>

<script src="https://gist.github.com/j4ckofalltrades/a4ec95b3e077fd7c294d20ef8095f480.js"></script>
