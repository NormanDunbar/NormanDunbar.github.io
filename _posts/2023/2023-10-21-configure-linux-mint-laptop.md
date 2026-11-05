---
title: "Configuring Linux Mint to use my UHD Laptop Display"
layout: post
date: 2023-10-21 15:30:07+01:00
---

My Linux Mint installation on my laptop has a wee problem with the extreme resolution of the laptop display. This is 3072 by 1920 (16:10) and when an application is opened on the laptop screen, it is tiny. I need to fix it, so this is what I do when I install a new release.

### Display Properties

* LM -> Preferences -> Display.
* Settings tab:
  * Make sure "Enable fractional scaling controls" is on.
  * Set "Scale content up" for "Fractional scaling mode".
* Layout Tab:
  * Make sure "Monitor Scale" is 100% for the laptop screen. I use 75% for the second screen.

Repeat for all monitors. I have two.


### Fonts

* LM -> Preferences -> System Settings
* Font Selection:
  * Choose your preferred font and sizes. Mine are the default, "Ubuntu Regular 10" for most of the options; Monospace is "DejaVu Sans Mono Book"; and Window title is "Ubuntu Medium 10".
* Font Settings:
  * Set "Text scaling factor" to 1.3, 1.4 or 1.5 as you prefer. Mine is 1.4.


### Desktop Panel

Next, the desktop panel (the task bar if you want the Windows terminology!) might need adjusting. My primary monitor is the UHD laptop, so the panel is a wee bit thin for my eyes these days! 

* Right-click the panel.
* Choose "Panel Settings"
* Click "Left Zone"
  * Adjust the panel height, mine is 44 pixies tall. (Affects all zones)
  * Set the "Font size" to "Allow theme to determine font size".
  * Set "Coloured icon size" to "Scale to panel size optimally", or, "Scale to panel size exactly" if you prefer.
* Click "Right Zone"
  * Set the "Font size" to "Allow theme to determine font size".
  * Set "Coloured icon -> Preferences -> System Settings size" to **Scale to panel size optimally**, or, **Scale to panel size exactly** if you prefer.
  * Adjust "Symbolic icon size" to 32 pixies or to match any coloured icons you have on the right side. I have HPLIP over on the right so that sizes automagically, but the symbolic icons (monocolour) look tiny next to it.

I don't have anything to worry about in the "Centre Zone" but if I ever do, I can adjust accordingly.


### Mouse

The mouse pointer looks ridiculously tiny on the UHD monitor, so:

* LM -> Preferences -> Mouse and Touchpad
  * Adjust the pointer size on the UHD monitor until it looks a bit more visible. I ended up at a position 65% of the way along the slider.


### Reboot, Now!

Reboot the laptop even though it *appears* to have all been changed correctly, you get "funnies" if you don't do a reboot.


### Second Monitor

As my second monitor is only a 1920 by 1080 (16:9 HD) one, the fonts appear to be quite large when an application is moved onto that monitor. Nothing too onerous, but if the standard settings don't look right, we need to go back to scaling.

This saves mucking about with the scaling, however, if the two monitors were too far apart in terms of size, it might be a better plan to:

* Set the font scaling back to 1.0.
* Turn on fractional scaling again and set it to 75%
* Set each monitor's scaling individually. 

I did try this, but wasn't too happy with 125% for the laptop and 100% for the HD monitor. Your mileage, as they say. may vary.

