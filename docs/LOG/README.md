# LOG Storage

All activity logs of projects goes here.

## Random Notes

----

Software engineering job openings hit five-year low? `2025-02-21 Fri 08:46.11`

<https://blog.pragmaticengineer.com/software-engineer-jobs-five-year-low/>

Downfall with rise of AI and LLMs.

----

How browsers REALLY load Web pages

<https://fosdem.org/2025/schedule/event/fosdem-2025-4852-how-browsers-really-load-web-pages/>

Strange priories of loading resources and each one unique.
There are some ways around it but hope it improves.

The hilarious last part how HTTP3/Works.

----

The Belfry OpenScad Library, v2.0. An OpenSCAD library of shapes, masks, and manipulators to make working with OpenSCAD easier. BETA

<https://github.com/BelfrySCAD/BOSL2>

WiKi

<https://github.com/BelfrySCAD/BOSL2/wiki>

-----

XOR

<https://www.chiark.greenend.org.uk/~sgtatham/quasiblog/xor/>

Mathematical and useful features

-----

Raspberry Pi Zero USB/Ethernet Gadget Tutorial

<https://www.youtube.com/watch?v=aL1pWI2K60w>

![type:video](https://www.youtube.com/embed/aL1pWI2K60w)

Right Instructions on the CLI Configuration but windows is outdated

Companion Website

<https://www.circuitbasics.com/raspberry-pi-zero-ethernet-gadget/>

-----

Raspberry pi 3 A+ ethernet/ssh over USB! Gadget Mode tutorial

<https://www.youtube.com/watch?v=7nDJPidKSPA>

![type:video](https://www.youtube.com/embed/7nDJPidKSPA)

```
cmdline.txt (after rootwait)
modules-load=dwc2,g_ether
config.txt
dtoverlay=dwc2,dr_mode=peripheral
ssh file at root
```

-----

How to connect Raspberry Pi to Laptop: USB Gadget Mode(Works for Raspberry Pi4)

<https://www.youtube.com/watch?v=FiplDBoaWek>

![type:video](https://www.youtube.com/embed/FiplDBoaWek)

Companion

<https://www.thequantizer.com/access-raspberry-pi-remotely/#gadget-mode-ssh-over-usb>

----

One Port To Rule Them All // Serial, Ethernet, USB OTG, Raspberry Pi, OpenWrt
<https://www.youtube.com/watch?v=BYPsi10kavk>

![type:video](https://www.youtube.com/embed/BYPsi10kavk)

Works for Raspberry Pi 4B

Software

- OpenWrt USB Guest configuration

    <https://openwrt.org/docs/guide-user/hardware/usb_gadget>

- OpenWrt OTG Serial Config

    <https://gist.github.com/odevodyssey/d330b9253cc34bcc978dbe415e041f54>

- OpenWrt OTG Serial And Ethernet Config

    <https://gist.github.com/odevodyssey/5b14d3105dc20fbb55120ad2b3731937>

- OpenWrt OTG Ethernet Config

    <https://gist.github.com/odevodyssey/37d4bdaa89a29d40f760ea44c6a12e59>

OpenWrt Packages Used

```
# Serial Only
kmod-usb-dwc2
kmod-usb-gadget-serial

# Serial and Ethernet
kmod-usb-dwc2
kmod-usb-gadget-cdc-composite

# Ethernet Only
kmod-usb-dwc2
kmod-usb-gadget-eth
```

----

Apache Kafka Fundamentals | Apache Kafka Fundamentals

<https://www.youtube.com/watch?v=B5j3uNBH8X4>

![type:video](https://www.youtube.com/embed/B5j3uNBH8X4)

Conceptual Understanding for the Event Architecture.

----

What is Kafka?

<https://www.youtube.com/watch?v=aj9CDZm0Glc>

![type:video](https://www.youtube.com/embed/aj9CDZm0Glc)

Use-cases and Examples

----

Event-Driven Architecture (EDA) vs Request/Response (RR)

<https://www.youtube.com/watch?v=7fkS-18KBlw>

![type:video](https://www.youtube.com/embed/7fkS-18KBlw)

Why to use and Why not to use either.

----

Kafka vs. RabbitMQ vs. Messaging Middleware vs. Pulsar

<https://www.youtube.com/watch?v=x4k1XEjNzYQ>

![type:video](https://www.youtube.com/embed/x4k1XEjNzYQ)

History and insights of the **MessageQueues** and their evolution.

-----

What does it mean to listen on a port?

<https://paulbutler.org/2022/what-does-it-mean-to-listen-on-a-port/>

Nicely done in a Story mode.

----

The hater’s guide to Kubernetes

<https://paulbutler.org/2024/the-haters-guide-to-kubernetes/>

Where it make sense and where not.

----

Smuggling arbitrary data through an emoji

<https://paulbutler.org/2025/smuggling-arbitrary-data-through-an-emoji/>

Live

<https://emoji.paulbutler.org/>

Source Code

<https://github.com/paulgb/emoji-encoder>


A good hack of the UNICODE format to add data into an Emoji.

----

C can do this too and it's faster than Python

<https://www.youtube.com/watch?v=uFET2vifHh4>

![type:video](https://www.youtube.com/embed/uFET2vifHh4)

This is 2 hour Video for C Story

----

Header only library for writing build recipes in C.

Its a full build tool for code but build into the code.

<https://github.com/tsoding/nob.h>

----

Libmill is a library that introduces Go-style concurrency to C.


<https://libmill.org/>

This Library Turns C into Go

<https://www.youtube.com/watch?v=z1joHmzpoAc>

![type:video](https://www.youtube.com/embed/z1joHmzpoAc)

----

**8 Google Pixel Settings You Need To Turn Off Now**

https://www.youtube.com/watch?v=Uvg7-5q06sA


## Interesting Articles to Read Later

https://hackaday.com/2025/01/06/turns-out-humans-are-terrible-at-intuiting-knot-strength/

https://hackaday.com/2025/01/07/the-helicone-toy-or-mathematical-oddity/

https://hackaday.com/2025/01/07/gaze-upon-this-omni-directional-treadmills-clever-lego-construction/

https://hackaday.com/2025/01/07/bending-light-bending-time-a-diy-polarizer-clock/

https://hackaday.com/2025/01/08/tech-in-plain-sight-security-envelopes/

https://operating-system-in-1000-lines.vercel.app/en

https://hackaday.com/2025/02/22/the-perfect-pi-pico-portable-computer/
----
<!-- Footer Begins Here -->
## Links

- [Back to Root Document](../README.md)
