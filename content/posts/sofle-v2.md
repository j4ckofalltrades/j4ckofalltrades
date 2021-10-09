---
title: "Sofle v2"
date: 2021-09-27T20:24:42+08:00
description: Sofle v2 keyboard build
draft: false
categories:
- keyboards
tags:
- ortholinear
- sofle
- split
- qmk
- via
images: 
- https://res.cloudinary.com/j4ckofalltrades/image/upload/c_thumb,w_200,g_face/v1631712479/keebs/sofle/sofle_t9qeaa.jpg
---

![keeb](https://res.cloudinary.com/j4ckofalltrades/image/upload/c_limit,w_900/v1631712479/keebs/sofle/sofle_t9qeaa.jpg)

The [SofleKeyboard](https://josef-adamcik.cz/electronics/let-me-introduce-you-sofle-keyboard-split-keyboard-based-on-lily58.html)
is a 6×4+5 keys column-staggered split keyboard with encoder support. Based on
the Lily58, Corne, and Helix keyboards.

## Build components

**Switches**: AEBoard Naevy v1 (lubed Krytox 205g0)

**Keycaps**:  Katha Baybayin (KAT)

<a>
  <img align="center"
    class="projects"
    src="https://res.cloudinary.com/j4ckofalltrades/image/upload/c_limit,w_900/v1632745785/keebs/sofle/pcb_lks6a4.jpg" />
  <img align="center"
    class="projects"
    src="https://res.cloudinary.com/j4ckofalltrades/image/upload/c_limit,w_900/v1632745779/keebs/sofle/keycap3_iplas8.jpg" />
</a>
<a>
  <img align="center"
    class="projects"
    src="https://res.cloudinary.com/j4ckofalltrades/image/upload/c_limit,w_900/v1632745779/keebs/sofle/keycap1_hvcq0v.jpg" />
</a>
<a>
  <img align="center"
    class="projects"
    src="https://res.cloudinary.com/j4ckofalltrades/image/upload/c_limit,w_900/v1632745781/keebs/sofle/keycap2_l7acwc.jpg" />
</a>

## Firmware

QMK and Via compatible [keymap](https://github.com/j4ckofalltrades/keebs/tree/master/sofle)
with focus on adding a standard navigation cluster layer plus some Vim-inspired
features e.g. soft escape (`Esc` when held, `Ctrl` when tapped), using `h`, `j`, `k`, `l`
as arrow keys.

**Layout**

View in [Keyboard Layout Editor](http://www.keyboard-layout-editor.com/#/gists/a1f6519e723ad81ca151741b53a28b80)

![SofleKeyboard custom keymap](https://raw.githubusercontent.com/j4ckofalltrades/keebs/master/sofle/assets/soflekeyboard.png)

**Features**

- Via support
- Mode for soft escape (`Esc` when tapped, `Ctrl` when held) 
- Vim-style navigation (`h` `j` `k` `l` as arrow keys)
- Mode for standard navigation cluster
- Toggling between layers when encoders are pressed
- Encoder controls (additional layer/s when `Ctrl` or `Shift` is held)

**Encoder controls**

| modifier | encoder | action             |
| -------- | ------- | ------------------ |
| N/A      | Left    | Mouse wheel L/R    |
| N/A      | Right   | PgUp/PgDn          |
| Ctrl     | Left    | VolUp/VolUp        |
| Ctrl     | Right   | Brightness Up/Dn   |
| Shift    | Left    | Mouse cursor L/R   |
| Shift    | Right   | Mouse cursor Up/Dn |
