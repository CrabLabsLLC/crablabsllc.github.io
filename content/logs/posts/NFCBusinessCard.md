---
author: Orion Serup
title: Designing your Own NFC Business Cards
cover:
  image: /images/BusinessCardFront.jpg
  alt: Crab Labs NFC PCB Business Card
  relative: false
---

An NFC PCB business card can be a fun and unique way to promote yourself or your business.

Crab Labs designed and built these NFC PCB Business cards, the source files are [here](https://github.com/CrabLabsLLC/BusinessCard)

![Business Card Back](/images/BusinessCardBack.jpg)

I will show you how to design and build one using [KiCad](https://www.kicad.org/) and [JLCPCB](https://jlcpcb.com/)

## Primer on NFC (Near Field Communication)

Near Field Communication is a standardized series of protocols which define communication between two devices utilizing a 13.56 MHz carrier frequency ([reference](https://nfc-forum.org/learn/nfc-technology/)).

NFC devices need to be within several centimeters to communicate with each other.

Common NFC protocols are [ISO 14443](https://www.thalesgroup.com/en/markets/digital-identity-and-security/technology/iso14443) (Most Common) and [ISO 15693](https://www.rfidlabel.com/understanding-the-iso15693-protocol-an-in-depth-look/) (Newer, faster, more range). Most devices, including smartphones, natively support ISO 14443 communication; support for ISO15693 is not as widespread.

## Designing the Circuit

The following circuit is what was designed and used by Crab Labs

![Schematic](/images/CardSchematic.jpg)

The circuit is relatively simple, it revolves around a NFC IC which handles all of the NFC communication. More circuitry can be added as desired. For a detailed breakdown of the schematic see the docs portion of the source repository located [here](https://github.com/CrabLabsLLC/BusinessCard/blob/develop/docs/Specification.md).

### Selecting NFC IC

The most crucial decision in designing an NFC business card if the choice of NFC transponder or tag IC. It is generally recommended to chose a ISO 14443 chip as it is the most compatible.

If you are comfortable hand soldering components you can look for components from any source, if you are looking for fully assembled PCBAs from JLCPCB it is recommended to look for components on [LCSC](https://lcsc.com). LCSC has relatively limited inventory

There are a number of popular ISO 14443 NFC Tag ICs, such as:

- 