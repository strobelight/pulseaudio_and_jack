# PulseAudio and Jack

## Overview

[Pulseaudio](https://www.freedesktop.org/wiki/Software/PulseAudio/) is now the standard audio system on linux. It has several [modules](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Modules/) that can direct or manipulate the audio in some way. It supports the Linux simple plugin API ([LADSPA](http://www.ladspa.org/)). You can find plugins for EQ, compression, gate, effects, guitar simulators, noise generators, etc, some of which you have to compile yourself. I haven't found a way to use Jack to play back videos from the web for example, without using pulseaudio. Until browsers or other non-jack-aware apps playing some form of audio start supporting the jack api for audio, pulseaudio will still be necessary.

[Jack](https://jackaudio.org/) is a way to get audio anywhere, in jack-aware apps. These apps could be DAWs, OBS, Synths, whatever. Jack is one patchbay to route signals to places. Using qjackctl, you can visually see what's patched to where, but it gets convoluted pretty quickly when lots of connections are made. I use "carla" to view my patchbay, and "calf" for plugins. There are many apps that support jack found [here](https://jackaudio.org/applications/).

## This repo
The scripts here mostly get Jack running after you log in. I say mostly, because every now and then, the jack daemon, jackd, won't start due to some race condition I have yet to track down.

### ~/bin/checkjack
Does a `ps` command with `grep` to show the pulseaudio and jackd processes. If no jackd processes appear, log out/in, and check again. *Of course this presumes you have the autostart set to run `startJack`.*

### ~/bin/startJack

This scripts starts the jack daemon, and runs `setupjack` to connect to jack to pulseaudio.

*You'll need to edit this for your environment.*

### ~/bin/setupJack

This script creates a jack sink and source to pulseaudio (you'll need the pulseaudio jack connection kit installed). It also establishes some alsa devices if you so choose.

*You'll need to edit this for your environment.*

### ~/.config/autostart/startjack.desktop

This is a desktop file that is put in your autostart directory to start jack. Edit according to where you've placed the scripts.

### ~/.config/pulse/daemon.conf

`daemon.conf.diff` contains the changes made from `/etc/pulse/daemon.conf`.

### ~/.config/pulse/default.pa

`default.pa.diff` contains the changes made from `/etc/pulse/default.pa`.