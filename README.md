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

## Importing the osm map
This steps consists of importing our OSM map that will be in xml format :

1. go to [OpenStreetMAP!](https://www.openstreetmap.org/) website.
2. slect the region you want to export and click export button to save your .*osm map file

![Schenario](https://github.com/xobx-cherif/Sumo-OpenStreetMap/blob/master/OSM.png)

3. Use the netconvert tool to convert the osm map to a SUMO network file using the following command

```shell
netconvert --osm-files OSM_file_name.osm -o network_file_name.net.xml
```
4. OSM-data not only contains the road network but also a wide range of additional polygons such as buildings and rivers. These polygons can be imported using POLYCONVERT and then added to a SUMO configuration file(*.sumocfg).

you can use the .poly.xml file from this repository this file contains some basic polygons description like the water, buildings ... etc

now we are ready to generate our poly.xml file by typing the following command:
```shell
polyconvert --net-file network_file_name.net.xml --osm-files OSM_file_name.osm --type-file typemap.xml -o poly_file_name.poly.xml
```
5. At this point we have our scenario street network file, as we know we need and additional description file that describes the vehicles and their routes the file named .rou.xml
For these purpose we can youse the randomtrip tool to generate a random route scenario by typing the following command:

```shell
python {PATH TO SUMO}/tools/randomTrips.py -n network_file_name.net.xml -r route_file_name.rou.xml -e 100 -l 

```
6. At this point we generated our routes file, and we just need one more final file to be ready to execute our simulation.

Now we should put all together in a sumo configuration file that will tell our simulator about the route and network files that we want to use in our simulation the file should look like the following:

```xml
<configuration>
 <input>
  <net-file value="network_file_name.net.xml"/> 
  <route-files value="route_file_name.rou.xml"/> 		
  <additional-files value="poly_file_name.poly.xml"/>
 </input>
 <time>
  <begin value="0"/>
  <end value="1000"/>
  <step-length value="0.1"/> 
 </time>
</configuration>
```
This file should be saved with the extension *.sumocfg

7. Now we are ready to lunch our simulation using the following command :

```shell
sumo-gui config_file_name.sumocfg
```
And here are the cars mooving :D .


![Schenario](https://github.com/xobx-cherif/Sumo-OpenStreetMap/blob/master/cars.png)
