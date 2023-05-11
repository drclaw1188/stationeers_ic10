# Scripts for Stationeers Printers

These are the scripts I use for automating printers in Stationeers. I learned and borrowed bits from CowsAreEvil for this, but have developed my own versions. I have separated the various functions out to different chips. The functions are:
|Function|Description|Script|
| ----------- | ------------- | ------------ |
|AutoStop|Automatically stops the printer once it has printed out the number of items equal to its attached stacker's setting at the time the print job started.|https://github.com/drclaw1188/stationeers_ic10/blob/main/printers/PrinterAutoStop.ic10|
|PrinterMaster|Delivers ingots to printers automatically from a vending machine.|https://github.com/drclaw1188/stationeers_ic10/blob/main/printers/PrinterMaster_v3.ic10|

The two functions work independently of each other, so you can set up only one or the other depending on your needs. I like to setup the autostop earlier in the game since it only requires that each printer have a stacker attached to it, and just one IC10 chip and housing.

## Printer AutoStop

Automatically stops the printer. Printers need to have stackers attached to them and the stackers need to be uniquely labeled. When a new print job is started, the program records the stack size setting on the attched stacker and will stop the printer once the export count increases by that number. The chip only supports three printers, usually the Autolathe, Electronics Printer, and Pipe Bender. This is due to a limitation in the number of pins, and I find I don't use the Tools printer often enough to bother attaching a stacker to it. It might be possible to add support for a Tools printer by making use of the *lbn* and *sbn* IC10 commands. This script also turns the attached stacker on or off to match the current on/off status of its printer.

### Devices

|Device Name|Device Number|Description|Required|
| ----------- | ------------- | ------------ | ---------- |
|AutoLathe|d0|The Autolathe Printer|Yes|
|AutoLatheStacker|d1|The stacker attached to the Autolathe|Yes|
|ElectronicsPrinter|d2|The Electronics Printer|Yes|
|ElectronicsStacker|d3|The stacker attached to the Electronics Printer|Yes|
|PipeBender|d4|The Pipe Bender Printer|Yes|
|PipeBenderStacker|d5|The stacker attached to the Pipe Bender Printer|Yes|

## Printer Master

Automatically delivers ingots to printers from a vending machine. Keeps a minimum of 50 (by default) of each of iron, copper, gold, silicon, and steel in each printer and will request more once the amount of the reagent in the printer goes lower. It delivers all other ingots on demand. It depends on a vending machine that is fed sufficient ingots as required by the printers. Optionally, you can setup a LED light and it will change the color according to its current status:

|Color|Status|
| ----------- | ------------- |
|Green|Normal status, not delivering any ingots|
|Yellow|Checking vending machine to see if it has the required ingot|
|Purple|Delivering ingot to a printer|
|Red|Vending machine does not have any of the requested ingot|

Setup a console with a hash display, and set the hash display to the IC housing of this chip, and it will display the particular ingot it is needing if the LED is red, and what ingot is being delivered the the case of yellow or purple.

### Devices

|Device Name|Device Number|Description|Required|
| ----------- | ------------- | ------------ | ---------- |
|VendingMachine|d0|The vending machine|Yes|
|Autolathe|d1|The Autolathe Printer|Yes|
|PipeBender|d2|The Pipe Bender Printer|Yes|
|Electronics|d3|The Electronics Printer|Yes|
|Tools|d4|The Tools Printer|Yes|

### Setup

Connect the input slot of each printer to the output slot of the vending machine via chutes. Use "Chute Digital Flip Flop Splitter" (either the right or left variety) to split the line so that the straight through connection of the digital chute continues down the line to the rest of the printers and the angled connection to connects to the input slot of the printer. Use the labeler to label each digital chute as follows:

|Printer Connected|Chute Name|
| ----------- | ------------- |
|Autolathe|DC:Autolathe|
|Pipe Bender|DC:PipeBender|
|Electronics Printer|DC:Electronics|
|Tools Printer|DC:Tools|

Optionally, connect an LED light to the same network as the printer to see the chip's status, and a console with a hash display setup to read the IC housing to see what ingot the status refers to.
