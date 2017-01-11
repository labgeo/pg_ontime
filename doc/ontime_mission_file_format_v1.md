# ONTIME Mission File Format (v1)

*Note: All values unless otherwise specified are in meters.*

## Extending the GeoJSON specification

This file format is based on the [GeoJSON RFC 7946](https://tools.ietf.org/html/rfc7946) specification, proposed by the Internet Engineering Task Force (IETF), in conjunction with the original specification authors. This specification was published in August 2016 and is the new standard specification of the GeoJSON format and replaces [the 2008 GeoJSON specification](http://geojson.org/geojson-spec.html).

The GeoJSON RFC 7946 is extended via Foreign Members. The base file format is a FeatureCollection wich contains items of type Feature and general metadata from the mission. 

```json
{ "type": "FeatureCollection",
 "features": [
   { "type": "Feature",
    "geometry": {
      "type": "LineString",
      "coordinates": [
        [102.0, 0.0], 
        [103.0, 1.0], 
        [104.0, 0.0], 
        [105.0, 1.0]
      ]
    },
    "properties": {
      "prop0": "value0",
      "prop1": 0.0
    }
   },
   { "type": "Feature",
    "geometry": {
      "type": "Point", 
      "coordinates": [
        102.0, 0.5
      ]
    },
    "properties": {
      "prop0": "value0"
    }
   }
 ]


}
```

## FeatureCollection

The full mission 



## Features

### Track
Track feature The flight track is the first Feature in the list. It is defined as a LineString geometry, but its coordinates may be extended as follows:

```json
"geometry": {
  "name": "Track",
  "type": "LineString",
  "coordinates": [
    [lat, lon, alt, ...],
    [lat, lon, alt, ...],
    [lat, lon, alt, ...],
    [lat, lon, alt, ...]
  ]
}
```

where the `...` represents an ordered list of comma separated values of sensor data. In this format version there is a proposed list of values that can be attached to the typical `xyz` json array.

Apart from data sensor, the `properties` section of the `Track` can represent any of these values:




### Observation

Observations are listed inmediately after the `Track`. Observations are Features that can be represented by any type of geometry. GeoJSON supports the following geometry types:

* Point
* LineString
* Polygon
* MultiPoint
* MultiLineString
* MultiPolygon
* GeometryCollection. 

However, the most common observations will be represented by points associated to an operator comments or a single RGB picture. As for example, an InSAR observation could be represented as a LineSring that overlaps the `Track`. This is because the InSAR is a sequentially or continuous captured observation.

```json
"geometry": {
  "name": "InSAR",
  "type": "LineString",
  "coordinates": [
    [lat, lon, alt, ...],
    [lat, lon, alt, ...],
    [lat, lon, alt, ...],
    [lat, lon, alt, ...]
  ]
}
```

