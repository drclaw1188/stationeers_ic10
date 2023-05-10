# Scripts for Stationeers printers
These are the scripts I use for automating printers in Stationeers. I learned and borrowed bits from CowsAreEvil for this, but made it my own. I have separated the various functions out to different chips. The functions are:
|Function|Description|Script|
--- | --- | ---|
|AutoStop|Automatically stops the printer once it has printed out the number of items equal to its attached stacker's setting at the time the print job started.|https://github.com/drclaw1188/stationeers_ic10/blob/main/printers/PrinterAutoStop.ic10|
|PrinterMaster|Delivers ingots to printers automatically from a vending machine.|https://github.com/drclaw1188/stationeers_ic10/blob/main/printers/PrinterMaster_v3.ic10|

## Printer AutoStop
Automatically stops the printer. Printers need to have stackers attached to them and be uniquely labeled. When a new print job is started, the program records the stack size setting on the attched stacker and will stop the printer once the export count increases by that number. The chip only supports three printers, usually the Autolathe, Electronics Printer, and Pipe Bender. This is due to a limitation in the number of pins, and I find I don't use the Tools printer often enough to bother attaching a stacker to it. It might be possible to add support for a Tools printer by making use of the *lbn* and *sbn* IC10 commands. This script also turns the attached stack on or off to match the current on/off status of its printer.

### Devices
|Device Name|Device Number|Description|Required?|
--- | --- | ---|
|AutoLathe|d0|The Autolathe Printer|Yes|
|AutoLatheStacker|d1|The stacker attached to the Autolathe|Yes|
|ElectronicsPrinter|d2|The Electronics Printer|Yes|
|ElectronicsStacker|d3|The stacker attached to the Electronics Printer|Yes|
|PipeBender|d4|The Pipe Bender Printer|Yes|
|PipeBenderStacker|d5|The stacker attached to the Pipe Bender Printer|Yes|
