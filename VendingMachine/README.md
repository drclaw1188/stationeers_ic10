# IC10 Scripts for Stationeers vending machines

## Vending_Machine_Controller.ic10

Displays amount of each item in a vending machine and number of slots used, and can optionally automatically request more of a particular item if the count is too low, or automatically eject a particular item if the count is too high. Requesting more of an item is accomplished by setting a hash value to an external memory, and an external system must then read the memory and send the item into the vending machine via chutes, or any other means you would like. The script will wait until the item is added, then re-count all the items. If an item count is above the desired maximum, it can automatically eject items until the count is at or lower than the desired amouunt, optionally setting a sorter so the ejected item can go somewhere else.

### Devices

The devices are:

* VendingMachine d0 - The vending machine to control. Required.
* QuantityDisplay d1 - An LED display to display the quantity of the selected item. Required.
* UsedSlotsDisplay d2 - An LED display to display the number of slots used in the vending machine. Required.
* ItemRequest d3 - An external memory (or other device) to tell an external system to produce an item. Optional.
* OutputSorter d4 - A sorter to sort ejected items if there is too much of a certain item in the vending machine. Optional.
* VendButton d5 - A button to press to vend the selected item. Optional.

A dial is batch read to select the item. It is theoretically optional, but without it you won't be able to change the selected item. You should also create a console with a hash display and configure it to read the IC10 housing, so you can see what item is currently selected.

Whenever the import or export count of the vending machine changes, this script automatically re-counts the items in the vending machine. Since counting can take a while to complete, the LEDs change to yellow while the counting is taking place and the dial and button will be unresponsive.

If the count of any of the items is less than the minimum for that item, the script will set the device connected to "ItemRequest" to the hash of that item, set the color of the LEDs to red, and wait for the import count to increase. If the count of any of the items is greater than the maximum for that item, the script will eject the item, set the "OutputSorter" to Output 1, set the color of the LEDs to orange, and wait for the export count to increase.

If the minimum and maximum for all the items is satisfied, the script goes into a mode where it will display the count of the number of items for the item selected by the dial, display the number of used slots, and eject one of the items (with the output sorter set to Output 0) if the button is pressed. While it is in this mode, the LEDs will be green.

### Stack pre-programming

To program the stack, you need to load a program that has many 'push' commands in it on to the chip, then just power up the chip for a second or so, and the stack is then programmed. After you program the stack, you can then load a different program on to the chip and run it, and the stack will be preserved. The stack format is:

Item #1 Quantity
Item #1 Minimum
Item #1 Maximum
Item #1 ItemHash
Item #2 Quantity
Item #2 Minimum
Item #2 Maximum
Item #2 ItemHash
...

The quantity values should always be zero, but they could theoretically be any number you want, as whatever is in that location in the stack will be overritten. It just needs to have that push command to preserve the spot in the stack.
The define "STACKSIZE" in Vending_Machine_Controller.ic10 needs to be changed to the number of push lines in the stack writer script.
Take a look at my [Ingot Storage Stack Writer](https://github.com/drclaw1188/stationeers_ic10/blob/main/VendingMachine/Ingot_Storage_Stack_Writer.ic10) or [Ore Storage Stack Writer](https://github.com/drclaw1188/stationeers_ic10/blob/main/VendingMachine/Ore_Storage_Stack_Writer.ic10) for examples of stack writing programs. The order is backwards compared to some other stack writers for efficiency purposes, so that the item hash comes at the end.
