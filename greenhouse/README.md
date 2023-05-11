# Scripts for Stationeers Greenhouses

The scripts in this directory are used for automating the management of a greenhouse environment, automating the production of food, or automating the harvesting of plants.

|Function|Description|Script|
| ----------- | ------------- | ------------ |
|Automatic Food Canning|Automates the oven and packager to make cans of soup automatically as plants are fed into the oven|https://github.com/drclaw1188/stationeers_ic10/blob/main/greenhouse/Automatic_Food_Canning_v5.ic10|
|Greenhouse Master|Maintains the temperature, pressure, and percentage of CO2 and O2 in a room. Activates a flashing light if values go too far out of range.|https://github.com/drclaw1188/stationeers_ic10/blob/main/greenhouse/Greenhouse_Master.ic10|
|Harvie Automator|Makes a Harvie automatically harvest and plant plants|https://github.com/drclaw1188/stationeers_ic10/blob/main/greenhouse/Harvie_Automator_2.ic10|
|Hydroponics Light|Turns the light on or off on a Hydroponics Device to keep plants happy.|https://github.com/drclaw1188/stationeers_ic10/blob/main/greenhouse/HydroponicsLight_v2.ic10|

## Greenhouse Master

Maintains an environment in a room. Requires two digital switches (or other devices) that can heat up or cool down the room, and 3 volume pumps (or other devices) that can pump CO2, O2, or nitrogen into the room. Optionally add a flashing light and connect it to the same network, and the chip will activate the light if it detects the environment has changed outside of safe ranges.

### Devices

|Device Name|Device Number|Description|Required|
| ----------- | ------------- | ------------ | ------------ |
|InsideSensor|d0|A gas sensor inside the room|Yes|
|OxygenPump|d1|A volume pump or similar to pump oxygen into the room|Yes|
|NitrogenPump|d2|A volume pump or similar to pump nitrogen into the room|Yes|
|CO2Pump|d3|A volume pump or similar to pump CO2 into the room|Yes|
|HeatingSwitch|d4|A digital valve or similar to heat up the room|Yes|
|CoolingSwitch|d5|A digital valve or similar to cool down the room|Yes|

## Hydroponics Light

Finds the average of the "Efficiency" values for the plants in all occupied slots of a Hydroponics Station. If the average is increasing or staying the same, it does nothing. If the average is decreasing over time, it alternates the status of the light. So if the light is on, it turns it off, and if it's off, it turns it on.

### Devices

|Device Name|Device Number|Description|Required|
| ----------- | ------------- | ------------ | ------------ |
|Hydroponics|d0|The hydroponics device|Yes|
