---
title: "Encodings, Formats and Libraries"
teaching: 10
exercises: 0
questions:
- "What are common ways to encode vector geospatial data in Python, and how do they relate to broader encoding standards?"
objectives:
- Learn about common community standards (broader than Python) for vector data encoding, and how they're implemented in core Python libraries.
- Learn to transform from one encoding type to another. Learn the `GeoJSON` format and exchange encoding interface, including the `__geo_interface__` method implemented across libraries.
keypoints:
- Python vector packages implement community standards for vector encoding. While these can seem complex, tools exist for conversion into various forms, and many of the tools include common interfaces for seamles exchange of data across tools.
- Packages exist for easily reading data from file-based and other serialized data formats.
- Most of these packages involve a series of steps to handle data, such as stepping through features via a loop, etc. Most tools do one or a couple of things only. `GeoPandas` addresses these challenges by enabling operations on feature collections in one step and bundling multiple tools via a coherent interface that builds on `Pandas`.
---


## Standard Geometry/Data Encodings

Standards exist for text (and binary) encoding of the geometry and feature types we saw. These include OGC/ISO [Well-Known Text (WKT)](https://en.wikipedia.org/wiki/Well-known_text) and Well-Known Binary (WKB), OGC [Geography Markup Language (GML)](https://en.wikipedia.org/wiki/Geography_Markup_Language), and [GeoJSON](http://geojson.org/) (based on JSON, and now an ISO standard). GML is a complex XML-based encoding that we won't discuss much here. We also won't touch on WKB in much detail. In this tutorial we'll focus on **WKT** and specially **GeoJSON.**

### WKT
WKT text representations of geometric entities are fairly intuitive. Here are some examples of the basic geometric entities we saw earlier (where coordinates are ordered as X Y):
* `POINT(0 0)`
* `LINESTRING(0 0, 1 1, 1 2)`
* `POLYGON((0 0, 4 0, 4 4, 0 4, 0 0), (1 1, 2 1, 2 2, 1 2, 1 1))`
* `MULTIPOINT((0 0), (1 2))`


## GeoJSON and `__geo_interface__` interface
* GeoJSON arose as a community convention leveraging the ubiquity of JSON encoding, specially on the web. Being JSON, it maps easily into Python dictionaries.
* See [http://geojson.org](http://geojson.org), including examples at [http://geojson.org/geojson-spec.html#examples](http://geojson.org/geojson-spec.html#examples)
* Additional resources/tools online
  * GitHub lets you view GeoJSON files natively (see the [minimum requirements here](https://help.github.com/articles/mapping-geojson-files-on-github/))
  * GitHub's [http://geojson.io](http://geojson.io) provides interactive creation and viewing of small GeoJSON serializations (as strings or files)
  * [http://dropchop.io](http://dropchop.io). Spatial operations on GeoJSON data, online and interactive. Brought to you by the great people of [CUGOS](https://cugos.org/), an open geospatial community in the broader Puget Sound area.
* Python `__geo_interface__` method: Passing feature data around between code packages, as GeoJSON-like objects
  * [GeoJSON and the geo interface for Python](https://sgillies.net/2013/06/27/geojson-and-the-geo-interface-for-python.html). See also [https://gist.github.com/sgillies/2217756](https://gist.github.com/sgillies/2217756)
  * [Processing vector features in Python](http://www.perrygeo.com/processing-vector-features-in-python.html)
* [`geojson`](https://github.com/frewsxcv/python-geojson) is a light-weight package for converting to and from convenient, Pythonic, GeoJSON-like objects.


GeoJSON Example:

{% highlight json %}
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [102.0, 0.5]
      },
      "properties": {
        "prop0": "value0",
        "prop1": 0
      }
    },
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [-90.0, 10.5]
      },
      "properties": {
        "prop0": "value3",
        "prop1": 3
      }
    }
  ]
}
{% endhighlight %}


## GIS file formats, including Relational Databases (RDBMS)
* Most of the time you will likely interact (read/write) with geospatial data in common (open or otherwise) GIS file formats and geospatial relational database servers.
  * File formats: Shape files (the most ubiquitous), GeoPackage (based on SQLite), KML, GeoJSON, ESRI File Geodatabase (proprietary but fairly accessible), etc
  * Relational Database servers with geospatial extensions: PostgreSQL, PostGIS, MS SQL Server, Oracle, and to a lesser extent MySQL
* Common Python packages: [OGR](http://gdal.org/python/) (see also [http://gdal.org/](http://gdal.org/) and [https://pcjericks.github.io/py-gdalogr-cookbook/](https://pcjericks.github.io/py-gdalogr-cookbook/)), [fiona](https://github.com/Toblerity/Fiona), [PyShp](https://github.com/GeospatialPython/pyshp)


## Standard encodings and libraries for projections, codes
* [Projections]((https://en.wikipedia.org/wiki/Map_projection)) and [Coordinate Reference Systems (**CRS**)](https://en.wikipedia.org/wiki/Spatial_reference_system) are fundamental!
* We'll get into this in more detail in the GeoPandas notebooks, and in another tutorial
* Some common libraries: pyepsg, pyproj, `fiona.from_epsg`, `GeoPandas.to_srs`

