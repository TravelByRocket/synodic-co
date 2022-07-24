---
title: "Create Directories for States and Forests"
categories:
  - Wild Camp
tags:
  - Python
---

In order to stay organized as I collect maps and extract data from them I wanted to create a set of directories organizing every national forest within the state it is (primarily) contained within.

## Collect Every Forest

I used two sources to create my list:
- [Complete List of American National Forests](https://www.treehugger.com/complete-list-of-american-national-forests-1343075) on Treehugger
- [List of national forests of the United States - Wikipedia](https://en.wikipedia.org/wiki/List_of_national_forests_of_the_United_States)

I then created a text file with all of the raw data, looking like the content below in `List of States and Forests.txt`.
```markdown
**Alabama**
National Forests in Alabama
**Alaska**
Chugach National Forest
Tongass National Forest
**Arizona**
Kaibab National Forest
Coconino National Forest
Prescott National Forest
**Arkansas**
Ozark St. Francis National Forest
Ouachita National Forest
**California**
Angeles National Forest
Cleveland National Forest
Eldorado National Forest
Inyo National Forest
Klamath National Forest
Lake Tahoe Basin Management Unit
Lassen National Forest
Los Padres National Forest
Mendocino National Forest
Modoc National Forest
Plumas National Forest
San Bernardino National Forest
Sequoia National Forest
Shasta-Trinity National Forest
Sierra National Forest
Six Rivers National Forest
Stanislaus National Forest
Tahoe National Forest
**Colorado**
Arapaho and Roosevelt National Forests & Pawnee National Grassland
Grand Mesa, Uncompahgre and Gunnison National Forests
Medicine Bow-Routt National Forests
Pike & San Isabel National Forests, Cimarron & Comanche National Grasslands
Rio Grande National Forest
San Juan National Forest
White River National Forest
**Florida**
National Forests in Florida
**Georgia**
Chattahoochee-Oconee National Forests
**Idaho**
Boise National Forest
Caribou-Targhee National Forest
Idaho Panhandle National Forests
Nez Perce-Clearwater National Forests
Payette National Forest
Salmon-Challis National Forest
Sawtooth National Forest
**Illinois**
Midewin National Tallgrass Prairie
Shawnee National Forest
**Indiana**
Hoosier National Forest
**Kansas**
Cimarron National Grassland
**Kentucky**
Daniel Boone National Forest
Land Between The Lakes National Recreation Area
**Louisiana**
Kisatchie National Forest
**Michigan**
Hiawatha National Forest
Huron-Manistee National Forests
Ottawa National Forest
**Minnesota**
Chippewa National Forest
Superior National Forest
**Mississippi**
National Forests in Mississippi
**Missouri**
Mark Twain National Forest
**Montana**
Beaverhead-Deerlodge National Forest
Bitterroot National Forest
Custer Gallatin National Forest
Flathead National Forest
Helena-Lewis and Clark National Forest
Kootenai National Forest
Lolo National Forest
**Nebraska**
Nebraska & Samuel R. McKelvie National Forests - Buffalo Gap, Fort Pierre, & Oglala National Grasslands
**New Mexico**
Cibola National Forest - Sandia RD
Lincoln National Forest
**North Carolina**
National Forests in North Carolina
**Nevada**
Humbolt-Toiyabe National Forest
**New Hampshire**
White Mountain National Forest
**New York**
Finger Lakes National Forest
**North Dakota**
Dakota Prairie Grasslands
**Ohio**
Wayne National Forest
**Oklahoma**
Black Kettle and McClellan Creek National Grasslands
Ouachita National Forest
**Oregon**
Columbia River Gorge National Scenic Area
Crooked River National Grassland
Fremont-Winema National Forest
Deschutes National Forest
Mt. Hood National Forest
Ochoco National Forest
Siuslaw National Forest
Umatilla National Forest
Willamette National Forest
**Pennsylvania**
Allegheny National Forest
**South Carolina**
Francis Marion National Forest
Sumter National Forest
**South Dakota**
Buffalo Gap National Grassland
Black Hills National Forest
Dakota Prairie Grasslands
Fort Pierre National Grassland
**Tennessee**
Cherokee National Forest
**Texas**
Black Kettle and McClellan Creek National Grasslands
National Forests in Texas
**Utah**
Ashley National Forest
Dixie National Forest
Fishlake National Forest
Manti-La Sal National Forest
Unita-Wasatch-Cache National Forest
**Vermont**
Green Mountain National Forest
**Virginia**
George Washington and Jefferson National Forests
**Washington**
Colville National Forest
Gifford Pinchot National Forest
Mt. Baker-Snoqualmie National Forest
Olympic National Forest
**Wisconsin**
Chequamegon-Nicolet National Forest
**West Virginia**
Monongahela National Forest
**Wyoming**
Bighorn National Forest
Bridger-Teton National Forest
Medicine Bow National Forest
Shoshone National Forest
Thunder Basin National Grassland
```

## Make Directories

```python
# MakeStateAndForestDirectories.py
"""One directory per state, each state containing its forests"""
import os

filename = "List of States and Forests.txt"
with open(filename, 'r') as file:
	lines = file.read().splitlines()
	state = ""
	for line in lines:
		if line.find("**") != -1:
			state = line.replace("**","")
			os.mkdir(state)
		else:
			forest = line
			try:
				os.mkdir(state + os.sep + forest)
			except:
				os.mkdir(state + os.sep + forest + " DUPLICATED")
```