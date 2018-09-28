# fs-spec
a common specifications for fs (feature stream)

## background
I wanted to have a common interface for various data source to connect with tippecanoe. 

## 1. command line interface
```console
$ {command} {schema.js} {z} {x} {y} {maxzoom}
```
{z}-{x}-{y} is the what3numbers for the module you need to have the data. {maxzoom} will help to skip unnecessary data. {maxzoom} shall be optional. 

## 2. schema.js specification
```javascript
module.exports = {
  // some data source specific configuration e.g. data source encoding can also be here.
  
  data: [
    [
      'un_base::custom_planet_land_a_l08', // data source identifier to pass to *-fs
      ['fclass'], // list of property names to be included in the fs
      {layer: 'landmass', maxzoom: 9}, // GeoJSON tippecanoe extension.
      (f) => { return f }, // modify function as in modify-js-spec
      'geom' // name of the geometry property (data source dependent and optional) 
    ] //,
    // ...
  ]
}
```

## 3. output interface
The output shall be NDJSON of GeoJSON features to the standard output. 

## see also
1. [postgis-fs](https://github.com/hfu/postgis-fs)
2. [shapefile-fs](https://github.com/hfu/shapefile-fs)
3. qatiles-fs
