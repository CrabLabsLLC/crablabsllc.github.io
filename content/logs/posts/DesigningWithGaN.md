---
author: Orion Serup
date: "2024-07-12T16:49:48-07:00"
draft: true
title: Designing With GaN
---

Gallium Nitride based semiconductor devices are the future of power and high frequency electronics and are only just now starting to become economically viable for everyday projects. Here is an interesting [post](https://epc-co.com/epc/gallium-nitride/why-gan) by EPC (One of the largest designers of GaN technology) which breaks down the main benefits and applications of GaN.

GaN devices a better in almost every way compared to current technology. They are able to handle more power in the same area as well as turn on and off faster than comparable silicon-based devices. This combination  of speed and power density leads to vast increases in efficiency as well as significant decreases in the size of circuitry.

## Driving GaN Devices

The goal when driving a GaN device is to switch it on and off as fast a possible. The faster you can switch the device on and off the more efficient it will operate.

GaN devices generally have a low Gate Threshold Voltage (Turn On Voltage) of less than 2V or so, which makes turning them on significantly easier than their Si-based counterparts which typically require 10 volts or more

![Threshold Voltage](/images/GaNVgsth.png)

This image shows the threshold voltage on a very high power GaN FET, the [EPC2302](https://epc-co.com/epc/products/gan-fets-and-ics/epc2302)

Note: _It is not advisable to drive a GaN device with GPIO in most cases due to the relatively high output impedance delivered by the GPIO pins, doing so will result in poor switching performance and possible damage to the MCU in a fault scenario_

### GaN Gate Drivers

The best way to drive the Gate of a GaN device is to use a specialized chip. EPC has a list of Gate Drivers for every application [here](https://epc-co.com/epc/products/gan-drivers-and-controllers).

When choosing a Gate Driver there are several factors to keep in mind, the most important of which are as follows:

1. Current Source and Sink Ability: The higher the better generally
2. Propagation Delay: The lower the better generally
3. Isolation: Not strictly necessary but significantly increases system safety

## Protecting GaN Devices

## Additional Resources