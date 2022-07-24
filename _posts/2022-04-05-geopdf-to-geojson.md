---
title: "GeoPDF to GeoJSON"
categories:
  - Wild Camp
tags:
  - mapping
  - GeoJSON
  - GeoPDF
  - Python
  - Bash
  - GDAL
---

The United States Forest Service (USFS) provides [Motor Vehicle Use Maps](https://www.fs.usda.gov/visit/maps/mvum-faq) (MVUMs) in [GeoPDF](https://www.usgs.gov/faqs/what-geopdfr) ([more](https://en.wikipedia.org/wiki/GeoPDF)) format. I would like to put the map rectangles on a `MapKit` map as an overlay but the map extents in the PDF were difficult to get to.

I met a helpful resource in the Denver Devs community that pointed me toward the [`GDAL` Python libray](https://pypi.org/project/GDAL/). Between this library and the [MyGeoData](https://mygeodata.cloud/converter/geopdf-to-geojson) website I was able to get the coordinates into a [GeoJSON](https://en.wikipedia.org/wiki/GeoJSON) file in two ways. 

## Manually: Using MyGeoData Website

This website was great for finding out what I was dealing with but I was limited to one file at a time, all by hand. Toget the GeoJSON, just upload the PDF and then select “Dataset Info”. The map extents were output as a rectangle (well, quadrilateral at least)in the following format.

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {},
      "geometry": {
        "type": "Polygon",
        "coordinates": [
          [
            [-105.72891082981914, 39.7741391086867 ],
            [-105.2340227421917 , 39.7741391086867 ],
            [-105.2340227421917 , 40.07188076474783],
            [-105.72891082981914, 40.07188076474783],
            [-105.72891082981914, 39.7741391086867 ]
          ]
        ]
      }
    }
  ]
}
```

## Scripted: Bash, Python, and GDAL

I had to automate the process and found that I could pull that same metadata from the PDF and save it to JSON in the terminal with

```bash
# for a GeoPDF named map.pdf and JSON output map.json
gdalinfo map.pdf -json | tr -d '[:space:]' | grep -o' "wgs84Extent".*\]\]\]\}' > map.json
```

which outputs (prettified afterward) the following content.

```json
{
  "wgs84Extent": {
    "type": "Polygon",
    "coordinates": [
      [
        [-105.7320528, 40.0698042],
        [-105.7289108, 39.7741391],
        [-105.2330182, 39.7761942],
        [-105.2340227, 40.0718808],
        [-105.7320528, 40.0698042]
      ]
    ]
  }
}
```

This works perfectly for a majority of the maps but 

### References

- [Convert GeoPDF with GDAL](https://gis.stackexchange.com/questions/121226/convert-geopdf-with-gdal)
- [Enable PDF Support in `gdal`](https://gis.stackexchange.com/questions/259547/how-can-i-enable-pdf-support-in-gdal)

## Other References

- [GDAL Library Website](https://gdal.org)
- [osgeo4mac](https://github.com/OSGeo/homebrew-osgeo4mac) I don't recall if I ever used this
- [QGIS](https://www.osgeo.org/projects/qgis/) is a wildly powerful app that I enjoyed but did not need 