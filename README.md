# Canada Post Box Locator 📮

View those red Canada Post box locations on a map:

![](/docs/header-img.png)

https://xairos.github.io/canada-post-box/

## Updating the geoJSON data file

Collected via [overpass turbo](https://overpass-turbo.eu):
```js
/*
This has been generated by the overpass-turbo wizard.
The original search was:
“amenity=post_box and collection_times!=*”

Share link: https://overpass-turbo.eu/s/1HmA
*/
[out:json][timeout:25];
// gather results
nwr["amenity"="post_box"]["collection_times"!~".*"]({{bbox}});
// print results
out geom;
```

exported, and then processed to remove polygons (postbox "areas") for simplicity of plotting:

```shell
jq '.features |= map(select(.geometry.type != "Polygon"))' export.geojson  > gta_postboxes.geojson
```
