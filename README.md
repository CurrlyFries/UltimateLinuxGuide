# Ultimate Linux Guide
### A guide I'm making to solve problems I have had setting up linux for Gaming and productivity

Welcome to the guide :)

I've been using ubuntu since october 2024 and plan on using it forever, but a lot of that time has been spent fixing weird issuses I've had.

This guide will aim to make solving these issues easier for everyone else who may encounter them.

I will keep updating it with solutions as I find them, as I remember them, or if somebody ask for a solution to something (My discord is CurrlyFries_ and I fix linux things for fun so feel free to ask is you have a problem :) )

MOST OF THESE FIXES WERE FOUND BY SOMEBODY ELSE, I AM JUST COMPILING THEM INTO A BIG FILE TO BE EASY.<br>
I will credit everyone if I can.

## IMPORTANT

I have exclusively been using use ubuntu, which means I will be downloading packages with `apt`. If you are on an arch-based distro, you will have to use different package managers such as `pacman`. If you need to know the command to install a package, I recommend just googling "Install (package name) (your distro)"

In linux, the tidle(~) key is shorthand for your home directory, /home/(user)/

for the sake on concistency, I will be doing all generic linux things with the command line (e.g. I will not use the files app to make files, i will use `mkdir`)

This guide also assumes that you are using bash, idk if people use other shells but this is all bash

# Contents
[General](#General)<br>

- [Using an ntfs drive with steam](#Using-an-NTFS-drive-to-play-steam-games)<br>
- [Using Multiple python versions](#Multiple-Python-versions)<br>
  
[Video](#Video)<br>
[Audio](#Audio)<br>
[Gaming](#Gaming)<br>
[Peripherals](#Peripherals)<br>

- [Audio interface shows up as surround sound even though it is stereo](#My-audio-interface-shows-up-as-surround-sound-even-though-it-is-stereo)

# General

## Using an NTFS drive to play steam games.

This is more of a gaming problem but it changes how your drive will be mounted so I thought it'd be more of a general thing.

This applies if you are switching from windows, and you either want to share a drive across a dual boot or just dont want to reinstall games.

It is recommended to just reformat the drive, but if you are dual booting with windows or really just don't want to, then follow the guide linked below:

(https://github.com/ValveSoftware/Proton/wiki/Using-a-NTFS-disk-with-Linux-and-Windows)

## Multiple Python versions

For some reason, the version of python that comes with ubuntu doesn't work all that well.

It comes from the fact that pip (or pipx) has changed and doesn't work, now if you want to install something with pip, you are meant to create a virtual python environment, and even then I've never got it to work.

This also includes dependencies, which is where I believe most of my issues come from (mainly just python scripts not running at all)

### <ins>The Solution</ins>

The solution to this is a tool called [pyenv](https://github.com/pyenv/pyenv), which lets you change python verions.

- To install pyenv, you can run the automatic installer with `curl -fsSL https://pyenv.run | bash`

- Then run `pyenv install -l` to see a list of versions

-  To install a version use `pyenv install (version)`
   (I've been mainly using 3.8.0)

-  To set a global python version use `pyenv global (version)`

-  If you want to check your global pyenv version, use `pyenv global`

<br>

But then I ran into another problem.

<br>


I was installing the [thcrap](https://github.com/major-gnuisance/thcrap-linux-ez) touhou translation mod and it wasn't working.

Naturally, this was becuase it uses the version of python that the system uses, so you have to use multiple python versions.

You can also do this with pyenv.

  - move into the directory where you want to change with `cd (directory)`

  - then run `pyenv local (version)`

The problem with this is that you have to be in the directory with the python script, or it will use the global version.<br>
For example (using [bcml](https://github.com/NiceneNerd/BCML)):

 ```
 cd ~/bcml
 python3 bcml.py
 ```
 Will work, but
 ```
 python3 ~/bcml/bcml.py
 ```
 Will not work

<br>

This is mainly a problem if you have a desktop file which runs a python script, which I do for convenience.

To circumvent this, instead of setting `exec=(~/bcml/bcml.py)` in your desktop file, use `exec=bash -c 'cd ~/bcml && python3 bcml.py`

  
# Video
  tbd
# Audio
  tbd
# Gaming
  tbd
# Peripherals

## Audio interface shows up as surround sound even though it is stereo

Out of all the problems I've had, this was the biggest pain in the ass.

Say that your playing spider-man miles morales. This problem would make it so you couldnt hear anything that wasn't infront of you, which also includes the calls you get throughout the game. On windows, you can just go into settings and set your audio interface to stereo, but on linux It's not that easy

### <ins>The solution</ins>

I believe this will need alsa, pipewire, pulse and wireplumber

(credit to reddit.com/user/khiron)

  - Create the folder `~/.config/wireplumber/wireplumber.conf.d/` if it does not already exist with `mkdir ~/.config/wireplumber/wireplumber.conf.d)` You may need to make `~/.config/wireplumber` first.

  - Create a .conf file with the name of your audio interface in that folder with touch (I don't think the name of this file actually matters but it'll make it memorable), for example `touch ~/.config/wiremplumber/wireplumber.d/Focusrite.conf`

  - Use `wpctl status` to get the sink ID of your audio interface (For example my scarlett 18i8 gen 1 shows up as ` Audio/Sink alsa_output.usb-Focusrite_Scarlett_18i8_USB_1000112B-00.analog-surround-71`) make a note of it (or just leave the terminal window open to copy from)
  
  - Open the .conf file we made earlier and copy the following into it:

    ```
    monitor.alsa.rules = [
	{
		matches = [
    			{
    				node.name = "(Audio Interface ID)"
    			}
    		]
    		actions = {
    			update-props = {
    				node.description = "(Audio interface name) Stereo"
    				node.nick = "Main"						
    				api.alsa.use-acp = true
    				audio.channels = 2
    				audio.position = "FL, FR"
    			}
    		}
	    }
    ]
    
    ```

    Replace `(Audio interface ID)` with the one we got earlier. The audio interface name is just for you to remember it by.

  - Reboot

To check if it worked, open sytem settings and test the audio. There should only be 2 directions - Front left and front right


    

  
