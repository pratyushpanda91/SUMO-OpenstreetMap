# SUMO-OpenstreetMap
# Simulation of Traffic Intersections Using SUMO and OpenStreetMap

## 📌 Project Overview
This project analyzes traffic density and queue lengths at **rural, urban, and metro intersections** using **SUMO (Simulation of Urban Mobility)** and **OpenStreetMap (OSM)**. The goal is to identify traffic congestion patterns and optimize signal control for improved flow and reduced delays.

## 🎯 Objectives
- Extract real-world **intersection layouts** from OpenStreetMap for accurate traffic modeling.
- Simulate **traffic density and vehicle flow** using SUMO.
- Analyze **queue lengths** to optimize signal timing and congestion management.

## 🔧 Tools & Technologies
- **SUMO**: Traffic simulation software
- **OpenStreetMap (OSM)**: Real-world road network data
- **Python** (for automation)

---
## 🗺️ Study Areas
1. **Rural Area**: Court Square, Betnoti
2. **Urban Area**: Murgabadi Circle, Baripada
3. **Metro Area**: Wellington Fountain, Kala Ghoda, Mumbai

---
## ⚙️ Implementation Process

# Steps

## Importing the osm map
This steps consists of importing our OSM map that will be in xml format :

### 1. go to [OpenStreetMAP!](https://www.openstreetmap.org/) website.
### 2. slect the region you want to export and click export button to save your .*osm map file

![Schenario](https://github.com/xobx-cherif/Sumo-OpenStreetMap/blob/master/OSM.png)

### 3. Use the netconvert tool to convert the osm map to a SUMO network file using the following command

```shell
netconvert --osm-files OSM_file_name.osm -o network_file_name.net.xml
```
### 4. OSM-data not only contains the road network but also a wide range of additional polygons such as buildings and rivers. These polygons can be imported using POLYCONVERT and then added to a SUMO configuration file(*.sumocfg).

you can use the .poly.xml file from this repository this file contains some basic polygons description like the water, buildings ... etc

now we are ready to generate our poly.xml file by typing the following command:
```shell
polyconvert --net-file network_file_name.net.xml --osm-files OSM_file_name.osm --type-file typemap.xml -o poly_file_name.poly.xml
```
### 5. At this point we have our scenario street network file, as we know we need and additional description file that describes the vehicles and their routes the file named .rou.xml
For these purpose we can youse the randomtrip tool to generate a random route scenario by typing the following command:

```shell
python {PATH TO SUMO}/tools/randomTrips.py -n network_file_name.net.xml -r route_file_name.rou.xml -e 100 -l 

```
### 6. At this point we generated our routes file, and we just need one more final file to be ready to execute our simulation.

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

### 7. Now we are ready to lunch our simulation using the following command :

```shell
sumo-gui config_file_name.sumocfg
```

### 8. Now it will open sumo gui .
Put values like 
a) Delay: 20ms
b) Scale Traffic: 120
c) Choose real world or standard simulation

And here are the cars mooving :D 

---
## 📊 Results & Analysis

Based on the simulations performed using SUMO for traffic analysis at three distinct areas—
Rural (Court Square, Betnoti), Urban (Murgabadi Circle, Baripada), and Metro (Wellington 
Fountain, Kala Ghoda, Mumbai)—the following key observations were made:
### 1. Traffic Density and Queue Length: 
The metro area exhibited the highest traffic density and 
queue length compared to both urban and rural areas. This indicates a significant level of 
congestion in metro regions, with traffic jams more prevalent due to the high volume of vehicles.
 
### 2. Urban Areas: 
Traffic density and queue lengths in the urban area were moderate, reflecting 
typical city traffic conditions, though not as severe as the metro area. These areas experience 
moderate congestion, often during peak hours.
### 3. Rural Areas: 
As expected, the rural area showed the least traffic density and queue length, 
with smoother traffic flow and fewer delays.
### 4. Optimization Potential: 
The higher congestion in the metro area suggests a greater need for 
traffic optimization strategies, such as adaptive signal control or alternative routing to improve 
traffic flow and reduce delays. Urban areas may also benefit from such optimizations, albeit to a 
lesser extent.

---
## 📌 Conclusion
This project demonstrates how **SUMO and OpenStreetMap** can be used to analyze and optimize **traffic flow** at different intersection types. Future work can explore AI-based traffic light optimization to reduce congestion further.

🚀 **Contributions Welcome!** Feel free to fork this repo and improve the simulation!

---
## 📄 References
- [SUMO Documentation](https://sumo.dlr.de/docs/)
- [OpenStreetMap Wiki](https://wiki.openstreetmap.org/wiki/Main_Page)

---
📩 **For queries, contact:** [pratyushpanda530@gmail.com](mailto:pratyushpanda530@gmail.com)
