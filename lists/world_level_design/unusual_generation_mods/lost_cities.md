[Return to Unusual Generation Mods](../unusual_generation_mods.md#Unusual-Generation-Mods)

----
## Lost Cities - Survive the Dead Edition

You can actually build and export Lost Cities templates within 1.12, the commands just weren't showing up in the help output because of a bug. I did some testing earlier this year and figured it out:



``` HTML
/lc_debug
``` 
will print the current building you're standing in and a bunch of other useful info to the log. 

``` HTML
/lc_buildpart <partName>
```
will spawn in the specified building part (The 16x6x16 floor slices. WILL OVERWRITE ALL BLOCKS AT LOCATION). There are currently no commands for spawning in entire buildings. 

``` HTML
/lc_exportpart <filePathAndName> <verticalBlocksInteger>
```
will export a slice as a json file. The file path has to include the entire folder path of the destination of where you want it to save, as well as the file name itself and extension. E.g `C:\Users\Username\curseforge\minecraft\Instances\ModpackName\fileName.json` would put it in the root directory of a Curseforge pack instance. The number is the number of blocks that it will save to the exported slice, counted from one block below where you are standing. So typing "3" will save the layer of blocks below you plus the two layers above that. Obviously this can take a max integer of 6 as that is the maximum height of a building slice (Can actually export more than 6 layers, but you won't be able to put all of it in a floor). 

``` HTML
/lc_exportbuilding <filePathAndName> <floorNumberInteger>
```
uses the same command format as above, except this will export an entire building instead of a slice/ floor. Counts a floor as 6 blocks high using same rules as above, and the integer at the end of the command will instead specify the number of floors the building has. (So for both these commands you need to be standing on top of the bottom most layer of a building or floor to export the entire thing).



Then you can copy over the exported slices from that file into your actual json files in the config. The block character pairs generated in the output file are pulled from existing block palettes and styles, and any that aren't get an "unknown character" placeholder randomly assigned (which may conflict with existing characters in your actual palettes). So you need to set up your block-character pairs for new blocks before exporting parts."

----

[Scroll Back](#Lost-Cities---Survive-the-Dead-Edition)