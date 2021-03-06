# micropython-examine-mem-maps
##Aims:
The Micropython compile process generates a gcc style .map file.
This file  explains how memory is mapped to Blocks, Regions and Symbols.
Use D3 to visualise this information and add user interaction.
* Show useful aspects of the data to see where memory is allocated and how much is used. (some)
* Allow comparisons between versions of map files. (not yet)

Note that the *Microsoft* .map format is completely different and not supported here yet.

##Currently V1
Allows several files to be processed at the same time and shown as thumbnail pie charts at top of page.
* These can be clicked on and refocus the main pie chart when selected.
* When selected the main pie chart will morph between them and show byte sizes and percents.
Bit of effort in here to make it smoothly interpolate each region even if some regions are missing in some maps.
* This v1 is a starter to get the map files read, regions extracted and exported for displaying in D3 style.
* all in the html file. Associated d3.min.js file is standard.
* The program read_maps_v1.py reads .map files and exports a csv.
 * List of map files is hardcoded.
 * Exports only the main regions listed in a variable called CATS.
   * E.g. .bss, heap, .rodata, .text,...

Its weak in several areas:
* does not yet parse all the symbols but structure is there.
* exports in csv only - needs to be a more complex json structure.
* does not organise the parsed data into the Blocks.
 * E.g. in RAM block - which regions. and in each region - which symbols.

![v1](https://cloud.githubusercontent.com/assets/899355/12369288/9822cba4-bc59-11e5-9957-b87b55ad8e3a.png)

## v2
Now starter project is there so next step is to:

In python file:
* parse symbols better.
* group by Block.
* allow several pointers to all point to same memory addresses.
* export in json.

In D3 file:
* read the json style instead of csv.
* add nested bar graph vertically down LHS, next to main pie chart.
 * allow expansion/contraction of groupings in this chart.
   * (e.g. open .text to see symbols inside and close again to hide them).
 * refocus pie chart on parent structure of selection.

## v3
Allow for comparison between any two selected thumbnail pie chart.

Show the differences in memory size and where that is. more complex style of diff may not be required.
Play with it to see what's the best solution for this problem.
