---
title: "From GeoPDFs to Usable Data"
categories:
  - Wild Camp
tags:
  - Python
  - gdal
---

In a preceding post [GeoJSON form GeoPDF]({% post_url 2022-04-05-geopdf-to-geojson %}) we did some fast work to prove that we could get the data we need, but now we need to dig a little deeper to put it into a format that we think we can use. 

## All GeoPDF Content to JSON
Create JSON files containing all the data retrieved with the GDAL library with the script below.

```python
# PDF2JSON.py
"""Create a JSON of the same base filename of every PDF in the directory, recursively, in-place"""

import subprocess
from glob import glob

filenames = glob("**/*.pdf",recursive=True)
for pdf in filenames:
	json = pdf.replace("pdf","json")
	with open(json, 'w') as outfile:
		result = subprocess.run(["gdalinfo",pdf,"-json"], stdout=subprocess.PIPE)
		out = result.stdout.decode("utf-8")
		outfile.write(out)
```

## Parse & Reform Useful Parts
Convert the raw JSON files into parsed JSON files with the content that I want with the file below.

```python
# Process Maps with Extents.py
from glob import glob
import json

filenames = glob("**/*.json", recursive=True)
failures = []
for json_filename in filenames:
    if json_filename.find("parsed") != -1:
        continue
    with open(json_filename, 'r') as file:
        data = json.load(file)
        try:
            corners = data["wgs84Extent"]["coordinates"][0]
            lats = [lat for (_, lat) in corners[:-1]] # 5th point repeats first so slice
            lngs = [lng for (lng, _) in corners[:-1]] # 5th point repeats first so slice

            lat_avg = sum(lats) / float(len(lats))
            lng_avg = sum(lngs) / float(len(lngs))

            dict = {}
            dict["center"] = {
                "latitude": lat_avg,
                "longitude": lng_avg
            }
            for (lng, lat) in corners:
                if lng < lng_avg and lat > lat_avg:
                    dict["northwest"] = {
                        "latitude": lat,
                        "longitude": lng
                    }
                elif lng < lng_avg and lat < lat_avg:
                    dict["southwest"] = {
                        "latitude": lat,
                        "longitude": lng
                    }
                elif lng > lng_avg and lat > lat_avg:
                    dict["northeast"] = {
                        "latitude": lat,
                        "longitude": lng
                    }
                elif lng > lng_avg and lat < lat_avg:
                    dict["southeast"] = {
                        "latitude": lat,
                        "longitude": lng
                    }
            # dict["rotationsCW"] = 0
            new_fn = json_filename.replace(".json","-parsed.json")
            content = json.dumps(dict, indent=4)
            with open(new_fn, 'w') as new_file:
                new_file.write(content)
        except:
            failures.append(json_filename)

with open("parsing failed.txt", 'w') as output:
    output.writelines("%s\n" % l for l in failures)
```

## List Missing Rectangles
Some files don't give up their contents like the others, and they will need to be process manually later. We can get a list of the files with problems by running the script below.

```python
# ListMissingLatLonExtent.py

import subprocess
from glob import glob

missing = []
filenames = glob("**/*.json", recursive=True)
for json in filenames:
    with open(json, 'r') as file:
        str = file.read()
        if str.find("wgs84Extent") == -1 & str.find("testing") == -1:
            missing.append(json)
            print(json)

with open("missing rectangle.txt", 'w') as output:
    output.writelines("%s\n" % l for l in missing)
```

## Final Usable Output
The final result of the JSON that I will use in the app looks like the example below, `stelprdb5339604-parsed.json`, which aligns with the raw filename of the GeoPDF. I have added a rotation property because some raw PDFs are not oriented with the North at the top, and I would rather not modify the source file every time it is updated, so I will track it in the JSON file.

```json
{
    "center": {
        "latitude": 40.248042999999996,
        "longitude": -106.0403644
    },
    "northwest": {
        "latitude": 40.430488,
        "longitude": -106.3666026
    },
    "southwest": {
        "latitude": 40.0597988,
        "longitude": -106.359167
    },
    "southeast": {
        "latitude": 40.0655602,
        "longitude": -105.7158853
    },
    "northeast": {
        "latitude": 40.436325,
        "longitude": -105.7198027
    },
    "rotationsCW": 0
}
```