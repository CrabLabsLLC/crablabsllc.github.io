---
author: Orion Serup
title: Designing your Own NFC Business Cards
date: "2024-07-12T16:49:48-07:00"
cover:
  image: /images/BusinessCardFront.jpg
  alt: Crab Labs NFC PCB Business Card
  relative: false
tags: ["nfc", "pcb", "rfid", "kicad"]
categories: ["tutorial"]
---

An NFC PCB business card can be a fun and unique way to promote yourself or your business.

Crab Labs designed and built these NFC PCB Business cards, the source files are [here](https://github.com/CrabLabsLLC/BusinessCard)

![Business Card Back](/images/BusinessCardBack.jpg)

I will show you how to design and build one using [KiCad](https://www.kicad.org/) and [JLCPCB](https://jlcpcb.com/)

## Prerequisites

- Understanding of basic circuit theory and electronics (video [here](https://youtu.be/uXr4lXYjXuU?si=g8Fv1T-dVMoQe0k7))
- Working knowledge of KiCad (Tutorial [here](https://youtube.com/playlist?list=PLZNH6jlLeFXsg9ohRMbJ0qqSfUrRyAn7b&si=z17BisQiM9Pfdlvw))

## Primer on NFC (Near Field Communication)

Near Field Communication is a standardized series of protocols which define communication between two devices utilizing a 13.56 MHz carrier frequency ([reference](https://nfc-forum.org/learn/nfc-technology/)).

NFC devices need to be within several centimeters to communicate with each other.

Common NFC protocols are [ISO 14443](https://www.thalesgroup.com/en/markets/digital-identity-and-security/technology/iso14443) (Most Common) and [ISO 15693](https://www.rfidlabel.com/understanding-the-iso15693-protocol-an-in-depth-look/) (Newer, faster, more range). Most devices, including smartphones, natively support ISO 14443 communication; support for ISO15693 is not as widespread.

There are two main classes of NFC devices, Tags and Readers. This business card will be a tag and a smartphone or other device will be a reader.

NFC Tags store information that is procedurally read by a reader device when it gets close enough to be powered by it. The format and type of data that is read and interpreted is standardized but may or may not be supported based on the reader.

## Preliminary Design

The first step in the design is deciding the big picture details of the design such the general shape of the card and what it will contain.

NFC Tags can have a large amount of data stored on then, some reader devices have less compatibility than others in regards to acting on the data in the tag. For example, contact cards (vCards) can be stored on NFC Tags but Apple IPhones are not able to automatically import or read them in to your contacts while most Android devices have native support.

The most universal data form is a simple url, it is recommended to store either a URL or phone number. If you or your company has a website or landing page that would be ideal.

As for the size and shape of the card there are very few limitations, the main limitation is in regards to the antenna. There should be an unbroken area of at least 2cm x 2cm which is dedicated for the NFC antenna. You can and should create an interesting outline using tools such as Adobe Illustrator, Inkscape, or other Vector Graphics tools.

Crab Labs designed our version as a circle in order to use them as coasters or decor as well as to stand out.

## Creating the Schematic

The following circuit is what was designed and used by Crab Labs

![Schematic](/images/CardSchematic.jpg)

The circuit is relatively simple, it revolves around a NFC IC which handles all of the NFC communication.

More circuitry can be added as desired.

For a detailed breakdown of the schematic see the docs portion of the source repository located [here](https://github.com/CrabLabsLLC/BusinessCard/blob/develop/docs/Specification.md).

Open KiCad and create a new project using Command+N or Ctrl+N

Find a location to create the project and name it something appropriate, such as "BusinessCard"

Once the project has been created, navigate to and open the schematic (the file called *.kicad_sch), it will look like this:

### Selecting an NFC Tag IC

The most crucial decision in designing an NFC business card if the choice of NFC transponder or tag IC. It is generally recommended to chose a ISO 14443 chip as it is the most compatible.

There are a number of popular ISO 14443 NFC Tag ICs, such as:

- [NT2H1x](https://octopart.com/datasheet/nt2h1311f0dtlh-nxp+semiconductors-30332213) by NXP (x = 3, 6)
- M24SRx by ST Microelectronics (x = [02](https://octopart.com/datasheet/m24sr02-ymn6t%2F2-stmicroelectronics-31443741), [04](https://octopart.com/datasheet/m24sr04-ydw6t%2F2-stmicroelectronics-31443742), [16](https://octopart.com/datasheet/m24sr16-ymn6t%2F2-stmicroelectronics-31443747), [64](https://octopart.com/datasheet/m24sr64-ymn6t%2F2-stmicroelectronics-31443750))

Some of the most popular ISO 15693 NFC Tag ICs are:

- [ST25DVx](https://octopart.com/datasheet/st25dv04k-ier6t3-stmicroelectronics-80826716) by ST Microelectronics (x = 04K, 16K, 64K)
- M24LRx by ST Microelectronics (x = [04](https://octopart.com/datasheet/m24lr04e-rmc6t%2F2-stmicroelectronics-22275304), [16](https://octopart.com/datasheet/m24lr16e-rmc6t%2F2-stmicroelectronics-20571336), [64](https://octopart.com/datasheet/m24lr64e-rmc6t%2F2-stmicroelectronics-24437452))
- N24RFx by onsemi (x = [04](https://octopart.com/datasheet/n24rf04edwpt3g-onsemi-96588362), [16](https://octopart.com/datasheet/n24rf16edtpt3g-onsemi-96588363), [64](https://octopart.com/datasheet/n24rf64edwpt3g-onsemi-96588366))

The most important factor in finding the right transponder chip is the memory size, you generally want as much memory as you can afford.

Note: _Crab Labs recommends using the M24S or ST25DV series of transponders, they are plentiful, affordable, and easy to work with._

#### Sourcing NFC Tag ICs

If you are comfortable hand soldering components you can look for components from any source ([Octopart](https://octopart.com) searches multiple sources around the web at once)

If you can't or don't want to hand assemble PCBAs, then it is recommended to look for components on [LCSC](https://lcsc.com). If the component is available on LCSC then your design can be fully built and assembled at JLCPCB in a timely manner. If you do not chose a component that is available on LCSC you will either have to hand assemble that component or have the part be ordered on the side (this is more expensive, takes longer, and is more difficult).

Open KiCad and create a new project using Command+N or Ctrl+N

Find a location to create the project and name it something appropriate, such as "BusinessCard"

Once the project has been created, navigate to and open the schematic (the file called *.kicad_sch), it will look like this:

### Placing the Components

![Empty Schematic](/images/EmptySchematic.jpg)

Press "A" to add a symbol, this menu will appear. If you chose the ST25DV, then the component will be available, else you will need to add the component library to use it (see [here](#optional-importing-external-libraries) for tutorial)

![Symbol Adder](/images/SymbolAdder.jpg)

Search for the component you want to add:

![ST25 Selection](/images/ST25Selection.jpg)

Make sure that you __play close attention to the full name and that the symbol and footprint line up with that is on the datasheet__ of the part that you selected. Double click the item and click somewhere to place it, preferably in the middle of the schematic.

![ST25 Placed](/images/ST25Placed.jpg)

Next is to add any supporting circuitry, namely the antenna and storage capacitors.

Add a loop antenna symbol by pressing "A" and searching for "Antenna_Loop".

![Antenna Placed](/images/LoopAntennaPlaced.jpg)

Add a tuning capacitor by pressing "A" and searching for "C_Small"

![Antenna Circuit Placed](/images/CAntTag.jpg)

These three components are technically all that is required to make this device work as intended. _If you don't care about adding additional niceties such as test points or status LEDs then proceed to [here](#assigning-component-footprints)_

If the device contains an external voltage supply pin (i.e. VDD or VCC), then a capacitor should be added. This capacitor should have a value of 100nF or more. Press "A" and look for "C". Once placed, click on it and press "E" in the "Value" field enter "100nF".

![VCC Capacitor Added](/images/VCCCapAdded.jpg)

![Component Properties Menu](/images/ChangeSymbolProps.jpg)

![Component Value Modified](/images/ComponentValueModified.jpg)

If the device has energy harvesting capabilities, then a capacitor should be added for the energy harvesting voltage (search the data sheet for this information). Press "A" and look for "C". A recommended capacitance by Crab Labs is 100nF, if the datasheet suggests a different value, use that value instead

![EH Capacitor Added](/images/EHCapAdded.jpg)

It is recommended to add test points to all of the pins in order to properly test and debug the functionality of the device. This is entirely optional but highly recommended in the first revision of a design. Press "A" and search for "TestPoint", __it is recommended to use the "TestPoint" symbol but "TestPoint_Small" works just as well__.

![All Components Placed](/images/AllComponentsPlaced.jpg)

If you would like a status LED and the tag that you chose supports it (has energy harvesting and an output pin) then a resistor and LED will be needed. Press "A" and search for "R_US" ("R" if in the E.U.) as well as "LED" and place one of each.

![All Parts Placed](/images/AllPartsPlaced.jpg)

### Assigning Component Footprints

Before the circuit can be exported to a PCB, the components need to be assigned a physical footprint (i.e. what the connections to the board look like).

In order to assign a footprint to a component click on it and press "E", navigate to the "Footprint" field and click on the books icon:

![Edit Footprint](/images/EditFootprint.jpg)

Then you will enter the footprint selection menu

![Footprint Selection](/images/FootprintSelect.jpg)

If you plan on hand soldering the components these footprints are recommended:

- _Capacitors_: C_0805_2012Metric (smaller) or C_1206_3216Metric
- _Resistors_: R_0805_2012Metric (smaller) or R_1206_3216Metric
- _TestPoints_: TestPoint_Pad_D2.0mm
- _LEDs_: LED_0805_2012Metric (smaller) or LED_1206_3216Metric

If you plan on having JLCPCB or another manufacturer assemble these boards then the following footprints are recommended:

- _Capacitors_: C_0201_0603Metric (smaller) or C_0402_1005Metric
- _Resistors_: R_0201_0603Metric (smaller) or R_0402_1005Metric
- _TestPoints_: TestPoint_Pad_D1.0mm
- _LEDs_: LED_0402_1005Metric  

Assign all of the footprints as needed

The antenna will need it's own custom footprint, which will be created now

#### Creating Custom Antenna Footprint

Antenna construction and geometry is very crucial in the performance of the NFC business card. It is recommended to calculate the antenna characteristics and geometry before implementing it as a footprint.

##### Calculating Antenna Characteristics

When creating an antenna there are three main geometries: Spiral, Rectangular, and Circular. The most common and easiest to create is rectangular. Crab Labs designed a spiral antenna but recommends a rectangular antenna.

ST has an online calculator for rectangular antenna characteristics [here](https://eds.st.com/antenna/#/). ST has an application note explaining NFC antenna design [here](https://www.st.com/resource/en/application_note/an2972-how-to-design-an-antenna-for-dynamic-nfc-tags-stmicroelectronics.pdf).

An additional rectangular antenna calculator is [here](https://www.rfwireless-world.com/calculators/NFC-rectangular-antenna-calculator.html)

It is recommended to have an antenna inductance of 1-4 uH.

Your design will have the following constraints:

- Track/Trace width > .15 mm (6 mils)
- Track/Trace Gap > .15 mm (6 mils)
- Trace Thickness: 35 um
- Substrate Thickness: 1.6mm
- Substrate Relative Permittivity: 4.6

Referring to the [preliminary design of the card](#preliminary-design) manipulate the parameters of the design so that you get the desired inductance value within the area that is dedicated for the antenna.

If you desire to create a custom shape other than rectangular, the formulas in the application note must be used to calculate the inductance.

##### Designing Antenna Footprint

In order to create a custom footprint a custom footprint library must be created. See [this tutorial](/posts/kicadcreatelibs/) for guidance regarding the creation of libraries.



#### Wiring Components

### Creating the Layout

## Ordering the PCB

## Assembling the PCB

