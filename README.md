# pisugar-faux-upsmon

![my faux-upsmon](docs/img/pisugar.png?raw=true)

Silly project where I attempt to replace upsmon w/ an RPi Zero 2W hooked up to a pisugar battery + surge protector 🤣🤪😂😀😁🤔

Use at your own discretion or if you're desparate 😅🫡🫠

# DEAR LORD(s) WHY?

I installed UPSMon. And NUT utils. I hated the entire experience. And then my one UPS that supported it started to emit gasses that hurt my lungs so I scrapped that entire project and whipped this up with extra hardware that I had.

# Requirements

1. A raspberry pi that can have a [pisugar battery installed](https://github.com/PiSugar/PiSugar/wiki/PiSugar-Power-Manager-(Software)).
2. make sure that you have one of the battery models specified in the link above ☝️
3. make sure to plug in your RPi battery INTO A SURGE PROTECTOR that is NOT backed by a UPS or battery
4. RPi needs to be running a distro w/ `systemctl`

I have [THIS PiSugar batter](https://www.amazon.com/dp/B08D678XPR)

# Installation

1. Clone this repo - `git clone https://github.com/chr0n1x/pisugar-faux-upsmon /etc/pisugar-server`
    - note that we're cloning into `/etc/pisugar-server` here - to keep everything in a single dir
1. Make sure that you can unplug the power cable from your RPi while it's running.
1. Install pisugar server ([instructions here](https://github.com/PiSugar/PiSugar/wiki/PiSugar-Power-Manager-(Software)))
1. Verify pisugar-server installation by running `/etc/pisugar-server/pisugar-util.bash info` -- should print out a bunch of info on your battery.
1. `systemctl enable /etc/pisugar-server/pisugar-faux-upsmon.*`
1. `systemctl start /etc/pisugar-server/pisugar-faux-upsmon.*`

# Misc

The `pisugar-util.bash check` script will run with each timer in the service. When it detects that your RPi is running on the battery and not charging, it will start a timer. After the timer runs out, the `check` command will run the `shutdown` command, which will then reference commands in `/etc/pisugar-server/pisugar-shutdown-commands`.

Note that for some models of the pisugar, you have access to a button that can trigger a custom shell script here!

![server](docs/img/server.png?raw=true)

You can then configure any button taps to trigger the shutdown script like so
![server](docs/img/custom-script.png?raw=true)

_note the custom script pipes the script output into `/var/log`_

# TODO

Shutdown mechanism is super jank, like the rest of this project so I should probably fix that lul.
Also it would be cool to get WoL working at some point.
