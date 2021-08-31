# WEBOTS SUMO Usage

## Open Street Map Importer
[Link of Source](https://cyberbotics.com/doc/automobile/openstreetmap-importer)

Go to the path of importer folder:
```bash
cd $WEBOTS_HOME/resources/osm_importer
```
Then Run python script to convert osm file to wbt file:
```bash
python3 importer.py --input=/project_world_folder_/myMap.osm --output=/project_world_folder_/myMap.wbt
```

## SUMO Exporter
[Link of Source](https://cyberbotics.com/doc/automobile/sumo-exporter)

Add a path to Webots Sumo libraries:
```bash
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$WEBOTS_HOME/projects/default/resources/sumo/bin:$WEBOTS_HOME/lib
```

Go to exporter folder:

```bash
cd $WEBOTS_HOME/resources/sumo_exporter
```
Run python script to generate sumo.nod.xml , sumo.edg.xml , sumo.sumocfg:

```bash
python3 exporter.py --input=/project_world_folder_/myMap.wbt --output=/project_world_folder_/myMap_net
```
Run netConverter to generate net.xml file

```bash
cd /project_world_folder_/
$WEBOTS_HOME/projects/default/resources/sumo/bin/netconvert --node-files=myMap_net/sumo.nod.xml --edge-files=myMap_net/sumo.edg.xml --output-file=myMap_net/sumo.net.xml
```
## Create a SUMO Route File Randomly
[Link of Source](https://cyberbotics.com/doc/automobile/scenario-creation-tutorial#create-a-sumo-route-file-randomly)

First generate a trip.xml file, possible to define max number of vehicle via `-e 10`, 10 is # of vehicles:
```bash
python3 $WEBOTS_HOME/projects/default/resources/sumo/tools/randomTrips.py -n /project_world_folder_/myMap_net/sumo.net.xml -o /project_world_folder_/myMap_net/sumo.trip.xml -e 10
```
Then generate a rou.xml file from net.xml and trip.xml files:
```bash
$WEBOTS_HOME/projects/default/resources/sumo/bin/duarouter --trip-files /project_world_folder_/myMap_net/sumo.trip.xml --net-file /project_world_folder_/myMap_net/sumo.net.xml --output-file /project_world_folder_/myMap_net/sumo.rou.xml --ignore-errors true
```
