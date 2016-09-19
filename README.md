# enhanced_tilemap
Kibana ships with a functional tilemap visualization. This plugin provides an additional tilemap visualization containing the enhancments listed below.

## Enhancements

### Add Markers to map
Allows for the placement of markers on the tilemap. Markers are displayed when in the visualization panel or the dashboard panel. Markers can only be added and removed when in the visualization panel.

### Static quantized range bands
The existing tilemap generates quantized range bands dynamically. The enhanced_tilemap provides the ability to set static quantized range bands.

## Planned Enhancements

### backport kibana 5.x tilemap improvements to 4.x.
The kibana tilemap plugin has been updated with several pull-requests but none of these have been merged with the 4.x branch. This plugin supports 4.x so it is a way to use integrate the tilemap improvements in kibana 4.x releases.
* https://github.com/elastic/kibana/pull/6001
* https://github.com/elastic/kibana/pull/8000
* https://github.com/elastic/kibana/pull/6914
* https://github.com/elastic/kibana/pull/6835

### Improved navigation
* Display mouse latitude and longitude location in upper right corner
* Provide inputs to set view location
* Zoom map on mouse scroll (feature can be toggled on/off via visualization option)

### OR geo_bounding_box queries
Kibana's tilemap visualization has a neat feature where you can draw a rectangle on the map and create a geo_bounding_box filter like the one below. The limitation arises when multiple bounding boxes are needed. Each drawn rectangle creates a new geo_bounding_box filter that are ANDed together resulting in "No results found" messages across all visualizations. 
```
{
  "geo_bounding_box": {
    "name_of_field_with_geopoint_type": {
      "top_left": {
        "lat": lat,
        "lon": lon
      },
      "bottom_right": {
        "lat": lat,
        "lon": lon
      }
    }
  }
}
```

The enhanced tilemap visualization will allow for the creation of multiple bounding box filters that will be ORed together. Each drawn rectangle will append a geo_bounding_box filter to an ORed array like the example below.
```
{
  "or": [
    {
      "geo_bounding_box": {
        "name_of_field_with_geopoint_type": {
          "top_left": {
            "lat": lat,
            "lon": lon
          },
          "bottom_right": {
            "lat": lat,
            "lon": lon
          }
        }
      }
    },
    {
      "geo_bounding_box": {
        "name_of_field_with_geopoint_type": {
          "top_left": {
            "lat": lat,
            "lon": lon
          },
          "bottom_right": {
            "lat": lat,
            "lon": lon
          }
        }
      }
    }
  ]
}
```

### add additional layers
Provide the ablity to add additional WFS and WMS layers to the map.

### Sync maps
Sync map movements when dashboard contains multiple map visualizations.

### geo aggregation filtered by geo_bounding_box collar
[Filter geohash_grid aggregation to map view box with collar](https://github.com/elastic/kibana/issues/8087)

# Compatibility
The plugin is compatible with following Versions (other not tested yet):
* kibana (=4.4+)
