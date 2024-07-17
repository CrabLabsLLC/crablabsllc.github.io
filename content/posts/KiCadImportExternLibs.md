---
author: Orion Serup
title: Importing External Part Libraries into KiCad
date: "2024-07-12T16:49:48-07:00"
cover:
  image: /images/kicad_logo_paths.svg
  alt: KiCad Logo
  relative: false
tags: ["pcb", "kicad", "schematics"]
categories: ["tutorial"]
---

If a component is not available in the KiCad standard library it can either be created from scratch using the symbol and footprint editor or imported from an external source.

Many times manufacturers or distributors will provide libraries for their components and make them available online, this guide will show how to find and utilize these libraries in your projects.

## Finding External Part Libraries

The largest and most centralized repository for finding components and their libraries is [Octopart](https://octopart.com)

Let's say we are developing an NFC product and are looking for the N24RF NFC Tag, we can search for it on Octopart

![N24RF04 on Octopart](/images/N24RFOctopart.jpg)

Octopart will indicate if there is a footprint/symbol available for the part by displaying "CAD Models". Let's select one of the variants at random and click in to it.

![N24RF04 Page](/images/N24RF04Page.jpg)

At the bottom of the page there will be a selection which details which footprints, 3D models, as well as symbols they have available for download

![CAD Models](/images/CADModelSelection.jpg)

If Octopart does not have the component or does not have library it is often worthwhile to look at the manufacturer's website. Sometimes there are similar component libraries that can be used with slight modification.

If all else fails then the part library has to be created from scratch. See [this tutorial](/posts/kicadcreatelibs)

## Downloading External Part Libraries

It is best to find a source to download the footprint, symbol, as well as 3-D model at once, in this case we should download from "Component Search Engine". You can preview the component to check against the datasheet. Proceed to download if the preview looks correct.

Various providers have different procedures for accessing files, most of them require a login (some providers will have you select the PCB software). Download the data package from the provider.

Extract the package and enter in to the folder, there will be several files we want to look for:

- *.stp or *.step, this is the 3-D model of the component
- *.kicad_mod, this is the KiCad footprint definition file
- *.kicad_sym, this is the KiCad schematic symbol definition file

Those 3 files are the only files that are needed, if the footprint is standardized then the footprint and 3-D model are often not necessary but are recommended to download if available to ensure compatibility.

## Creating Local Libraries

In the folder containing the project you should create a folder that will be used as a place to store external library files. Crab Labs officially calls this folder "lib" but any name will do.

Enter this folder and create 3 separate sub-folders (one for 3-D models, one for symbols, and the last for footprints). The folder for the footprints must be named *.pretty to be recognized by KiCad. Crab Labs calls these folders "models", "footprints.pretty", and "symbols"

Copy the 3-D model of the component in to the 3-D model folder in the project library. Copy the kicad_sym file in to the symbol folder in the project library. Copy the kicad_mod file into the footprint folder in the project library.

Once all of the files are copied to the project local directory we want to make them available to use in the project.

## Importing Libraries into Project

Go in to the schematic editor. In the "Preferences" drop down menu there will be an option to "Manage Symbol Libraries", click in to it.

![Symbol Library Manager](/images/SymLibraryManager.jpg)

Navigate to "Project Specific Libraries"

![Project Specific Libraries](/images/ProjectSpecificLibraries.jpg)

Click on the folder icon which is "Add From Existing File" and navigate to the kicad_sym that you just added in the library folder, click OK

![Library Added](/images/LibraryAdded.jpg)

The symbol library is now added and available for use in your design. This process much be done for all kicad_sym files individually.

The procedure for adding the footprint library is the same.

Go to the PCB editor, go to Preferences -> Manage Footprint Libraries

Go to "Project Specific Libraries", add from an existing file the "*.pretty" folder in the library folder.

Any footprint files added in to that folder will be available after that point.