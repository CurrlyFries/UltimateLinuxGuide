# Ultimate Linux Guide
A guide I'm making to solve problems I have had setting up linux for Gaming and productivity

Welcome to the guide :)

I've been using ubuntu since october 2024 and plan on using it forever, but a lot of that time has been spent fixing weird issuses I've had.

This guide will aim to make solving these issues easier for everyone else who may encounter them.

I will keep updating it with solutions as I find them, as I remember them, or if somebody ask for a solution to something (My discord is CurrlyFries_ and I fix linux things for fun so feel free to ask is you have a problem :) )

## IMPORTANT

In linux, the tidle(~) key is shorthand for your home directory, /home/(user)/

# Contents
## [General](#General)
## [Video](#Video)
## [Audio](#Audio)
## [Gaming](#Gaming)
## [Peripherals](#Peripherals)

# General
  tbd
# Video
  tbd
# Audio
  tbd
# Gaming
  tbd
# Peripherals

## 1. My audio interface shows up as surround sound even though it is stereo

Out of all the problems I've had, this was the biggest pain in the ass.

Say that your playing spider-man miles morales. This problem would make it so you couldnt hear anything that wasn't infront of you, which also includes the calls you get throughout the game. On windows, you can just go into settings and set your audio interface to stereo, but on linux It's not that easy

### <ins>The solution</ins>

(credit to reddit.com/user/khiron)

  Create the file `~/.config/wireplumber/wireplumber.conf.d/(your audio interface name, doesn't really matter).conf`
