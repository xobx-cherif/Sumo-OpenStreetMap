# Sumo-OpenStreetMap
In this tutorial i tried to import a real map to a Sumo scenario.
The map imported here was the region around the LAAS-CNRS lab.
To understand the process of importing real maps to SUMO sumulator we will go through the process step by step.

![Schenario](https://github.com/xobx-cherif/Sumo-OpenStreetMap/blob/master/SUMO-OSM.png)

# Overview

 OpenSTreetMAP is a free editable map of the whole world. The exported files are *.osm but if you take a look inside the exported map files delivred by this website you will quickly notice that it is an xml format.
 And because SUMO streets descriptions are also described in xml, wich make it a pretty easy process to convert the osm maps into SUMO scenarios.
 In my opinion the process consists of making the map lighter with less details, but the conversion is highly flexible and we can choose what to keep and what to get rid of,and we can even edit the resulting maps
 
 In this tuturial i've took the region around the LAAS-CNRS lab (The laboratory where i do my PhD) as a target map to demonstrate the process.

# Steps
