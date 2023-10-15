---

author:       js
created:      2021-03-01
published: true
title:        "Working with geographic features and spatial data in MySQL 8"
excerpt:      "How to implement geo features in MySQL 8"
lead:         ""
image:        'mysql-spatial-data-poster.png'
imagecredit:  ''

---

With the release of MySQL 8 in the spring of 2018, a mature set of features has entered the mainstream.
Having previously taken a closer look at the [JSON data type](/mysql-json-column-with-laravel), we now turn our attention to spatial data.
Specifically, we will discuss how to **employ MySQL 8 as a spatial database** to  store and process geographic features.

Before we get to the nitty-gritty details, such as how to write spatial queries, let's consider a few basic questions:
**What is spatial data, and what are geographic features?**

## Storing geographic features using spatial data

Spatial data, as explained by the [MySQL reference](https://dev.mysql.com/doc/refman/8.0/en/spatial-types.html) is geometric data defined as **"a point or an aggregate of points" representing anything in the world that has a location**.

The Open Geospatial Consortium (OGC) publishes a set of standards under the label Geospatial Information and Standards (OpenGIS).
The OpenGIS geometry model defines  different types of geometry for representing spatial data.

The different **geometry types serve as an abstract basis to model spatial data**.
Within a spatial database, we furthermore encounter a number of key technical concepts:

* Geometric functions for manipulating spatial data and converting between textual and internal representations.
* Geometric functions for computing spatial relations between different geographic features.
* Spatial indexing for improved access times to spatial columns.

All of these serve to **model, process, and compare the geometry** of geographic features.

### Geographic features, a definition

Geographic features describe **entities that have a physical location in the real world**.
According to the [MySQL reference](https://dev.mysql.com/doc/refman/8.0/en/spatial-types.html), a geographic feature can be:

> * An entity. For example, a mountain, a pond, a city.
> * A space. For example, town district, the tropics.
> * A definable location. For example, a crossroad, as a particular place where two streets intersect.

A geographic feature exists in the real world.
To describe it in terms of spatial data, we make use of geometric objects.
The OpenGIS geometry model defines two basic hierarchies of geometric objects.

### Simple geometric objects

Each simple geometric object defines a **single geographic feature**:

* `Point`
* `LineString`
* `Polygon`

There is also the purely abstract `Geometry` type of geometric object, which can represent any of the other geometry types.

### Compound geometric objects

Each compound  geometric object defines a **collection of features**.
The following compound  geometric objects are available as per the spec:

* `MultiPoint`
* `MultiLineString`
* `MultiPolygon`

Analogous to the  abstract `Geometry` geometry type there is a  corresponding `GeometryCollection` compound geometric object.
This can represent any of the other compound geometric objects.

### Coordinate reference systems

A geometric object consists of points in space.
To anchor a geographic feature within the real world, the corresponding geometric object needs to be linked to a known coordinate reference system.
Such a system is also **commonly called a "spatial reference system"**. Only when the coordinate reference systems for two geometric objects are known can we reason about the spatial relations between the two objects.

| SRID | Description | Unit |
|:--|:--|:--|
| `4326` | GPS satellite navigation system; also used for NATO military geodetic surveying. | degrees |
| `3857` | Web mapping and visualization applications: Google Maps, Open Street Maps, etc. | meters |

## Spatial databases for geographic features: MySQL 8 vs 5.7 compared

Better support for spatial data handling was one of the major improvements included in the MySQL 8 release.
However, it **was already possible to store and process geographic features using earlier MySQL versions** as well as competing database systems. We won't go down the =MySQL vs PostgreSQL=, or MySQL vs MariaDB rabbit hole. Instead, we focus our attention on the direct comparison of using MySQL 8 vs 5.7 as a spatial database.

### How has spatial data handling improved in MySQL 8

The first major improvement brought forth by MySQL 8 was better support for coordinate reference systems a.k.a. spatial reference systems (SRS).
Remember that to **anchor a geographic feature in the real world** requires for the the corresponding geometric object to be assigned a spatial reference system.
With MySQL 8, a number of different spatial reference systems have become available.

To **compute spatial relations between two different geometric objects**, both objects need to be placed within the same spatial reference system.
Below we give an overview of the three kinds of spatial reference system available in MySQL 8:

| Type of spatial reference system (SRS) | Explanation | Coordinates | Units |
|:--|:--|:--|:--|
| Projected SRS | Projection of a globe onto a flat surface — a map | Cartesian | Distance units: meters, feet, etc. |
| Geographic SRS | Non-projected — an ellipsoid | Latitude-longitude | Any angular unit |
| SRS with SRID `0` | Default SRID for spatial data in MySQL | Infinite flat Cartesian plane | Unitless |

While spatial reference systems are not a new concept in MySQL, with version 8.0 they directly affect computation.
Each spatial reference system is **denoted by  a spatial reference system identifier (SRID)**.
There are more than 5,000 spatial reference systems to choose from.
To give a few tangible examples, the [MySQL Server Team](https://mysqlserverteam.com/spatial-reference-systems-in-mysql-8-0/) notes:

> SRID 4326 is GPS coordinates. SRID 3857 is the web map projection that you see on Google Maps, OpenStreetMap, and most other web maps.

The second major improvement to spatial data handling in MySQL 8 pertains to **spatial indexing, that is, the optimization of columns holding spatial data**.
Two requirements have to be met for spatial indexing to work properly:

1. The geometry columns to be included in the index need to be defined as `NOT NULL`.
2. Columns need to be restricted to a spatial reference system identifier (SRID), and all column values must have the same SRID.

### How was spatial data handled in MySQL 5.7?

While it has been possible to store a spatial reference system identifier (SRID) with a geometric object, MySQL versions prior to 8.0 were not able to use this information for computations.
Instead, the provided **geometric functions operated on the infinite flat Cartesian plane** represented by SRID `0`.
To get accurate results, one commonly had to define custom functions to process raw results and convert between units.

Writing custom functions for querying and processing of geographic features **required an intimate understanding of math and geometry**.
Furthermore, many of the provided spatial relations functions were limited to using the minimum bounding rectangle (MBR), instead of the precise shape of geometric objects.

## Spatial queries in MySQL 8

So far, we've  looked at what constitutes a geographic feature, as well as how geographic features are represented as spatial data.
We now turn our attention to the **specific technical implementation** found in MySQL 8:

* How to create, populate and index database tables holding spatial data.
* How to compute spatial relations between geometric objects, and how to retrieve specific pieces of spatial data.

Specifically, since we're using **SQL ("structured query language") as the interface between the database and the user**, we'll be discussing the spatial queries involved.
But first, a bit of background.

The Open Geospatial Consortium (OGC) publishes a set of standards under the name "OpenGIS Simple Feature Access".
These are also normed as `ISO 19125-1`, and `ISO 19125-2`.
The `ISO 19125-1` **standard defines two representations for the exchange of geometric objects** across systems.

In particular, the standard defines the **"Well-known Text" (WKT) representation of geometry**, which provides a human-readable, text-based representation for the definition of geometric objects.
Furthermore, "Well-Known Binary" (WKB) is a corresponding, machine-readable binary representation. Specific technical implementations providing Simple Feature Access exist for different database management systems:

| Database management system | Simple Feature Access extension |
|:--|:--|
| MySQL | MySQL Spatial Extensions |
| PostgreSQL | PostGIS Extension |
| SQLite | SpatiaLite Extension |

### What does a  spatial query look like?

For the most part, spatial queries are **just ordinary SQL queries**.
There are, however, some particularities that make spatial queries stand out:

* Spatial queries employ the different geometry types defined in `ISO 19125-1` as data types for the creation and population of database tables.
* Spatial queries commonly feature Well-known Text (WKT) representations of spatial data; this is particularly the case for queries that add geographic features to the database.
* Spatial queries make use of `ST_`-prefixed functions for computations and transformation of spatial data.

Note: in the examples below we are often using the SQL `SET` statement to define variables.
This is not necessary per se, but makes for cleaner code and more easily understood queries.

#### Creating a table to hold spatial data

Create a new table `spat` with a column `geom` of type `Geometry`:

```sql
CREATE TABLE spat (geom GEOMETRY);
```

Remember that this allows us to store geometric objects of any geometry type.
We can also be more specific;
here we add a new column of type `Point` to the existing `spat` table:

```sql
ALTER TABLE spat ADD pt POINT;
```

#### Inserting spatial data into the database

We've mentioned the Well-known Text (WKT) format a few times, but what does it actually look like?
Here we **use WKT to define a point and process the textual representation** by calling  the `ST_GeomFromText()` function:

```sql
SET @g1 = 'POINT(1 1)';
INSERT INTO spat VALUES (ST_GeomFromText(@g1));
```

Specialized functions exist for the different types of geometry.
As an example, here we employ the `ST_PointFromText()` function to process a WKT-string representing another point:

```sql
SET @g2 = 'POINT(2 3)';
INSERT INTO spat VALUES (ST_PointFromText(@g2));
```

Calling these functions will transform the WKT-representation into an internal storage format.

#### Retrieving spatial data from the database

Once we have spatial data stored inside the database, we'll commonly want to extract the data.
Again, we use **Well-known Text (WKT) as the universal interface**.
Here we're calling the `ST_AsText()` function to retrieve the column `g` from and convert its contents from the internal representation back to WKT:

```sql
SELECT ST_AsText(geom) FROM spat;
```

Correspondingly, we can use the `ST_AsBinary()` function to convert the contents of the `geom` column to a compact binary representation:

```sql
SELECT ST_AsBinary(geom) FROM spat;
```

#### Using geometric functions to compute spatial relations

One of the most practical uses of a spatial database is to query the spatial data according to certain spatial relations.
This allows us to **ask questions about the geometric objects**, such as "find all objects that are located within / outside of a particular object".
Some of the more commonly used spatial relations are:

| Spatial relation | Corresponding `ST_`-function | Set-theory explanation |
|:--|:--|:--|
| Equals | `ST_Equals()` | (a ∩ b = a) ∧ (a ∩ b = b) |
| Disjoint | `ST_Disjoint()` | a ∩ b = ∅ |
| Intersects | `ST_Intersects()` | a ∩ b ≠ ∅ |
| Touches | `ST_Touches()` | (a ∩ b ≠ ∅) ∧ (a<sup>ο</sup> ∩ b<sup>ο</sup> = ∅) |
| Contains | `ST_Contains()` | a ∩ b = b |
| Within | `ST_Within()` | a ∩ b = a |

All of these spatial relations compare the location of two geometric objects and return a boolean (true / false) result. **Besides these boolean relations, there are a number of functions to calculate the distance between geometric objects**.
In these cases, the returned value will be numeric.
The unit of the result depends on the spatial reference system (SRS) in use.
Here we calculate the distance between two points in the SRS defined by SRID `4326`:

```sql
SET @g1 = ST_GeomFromText('POINT(1 1)', 4326);
SET @g2 = ST_GeomFromText('POINT(2 2)', 4326);

SELECT ST_Distance(@g1, @g2);
```

#### Using spatial indexing to improve performance of spatial queries

Indexing of database columns is a best practice to improve query performance.
As was the case in MySQL 5.7, creating a **spatial index in MySQL 8 results in an "R-tree" data structure**, which is optimized for quickly resolving many spatial relations.
Remember that for spatial indexing to work, the column to be indexed must be declared `NOT NULL`and must have an SRID set:

```sql
CREATE TABLE spat (geom GEOMETRY NOT NULL SRID 4326, SPATIAL INDEX(geom));
```

### Popular geospatial libraries for working with geographic features and spatial data

In real-world applications it may not be practical to write out spatial queries using Well-known Text (WKT) by hand.
Fortunately, a number of libraries exist to make this job easier.
They allow for the **programmatic mapping between different representations of geographic features**, such as natural language coordinates, Well-known Text/Binary, and GeoJSON.
Here's a selection of popular geospatial PHP libraries:

| Library / Package | Description |
|:--|:--|
| [GeoPHP](https://geophp.net/) | PHP library for working with geometric objects and geometric functions. Works with a range of formats, including WKT, WKB, and GeoJSON. Used to get centroids, bounding-boxes, area, etc. of a geometric object. |
| [Geocoder](https://geocoder-php.org/) | Get precise geographic coordinates for a geographic feature, such as "Buckingham Palace, London". Supports a wide range of providers. |
| [grimzy/laravel-mysql-spatial](https://packagist.org/packages/grimzy/laravel-mysql-spatial) | Facilitate working with spatial data and spatial relations in Laravel. |
| [sjaakp/yii2-spatial](https://packagist.org/packages/sjaakp/yii2-spatial) | Provide spatial data support for ActiveRecords in the Yii2 framework. |
| [creof/geo-parser](https://packagist.org/packages/creof/geo-parser) | Parse coordinates from their natural-language string representations, such as `'79°56′55″W, 40°26′46″N'`.  |
| [pragmarx/countries](https://packagist.org/packages/pragmarx/countries) | Retrieve country-specific information. Geographic features include states, cities, and borders. Accepts many different formats as input, such as common names, ISO codes, etc. |

<!--

| [creof/wkb-parser](https://packagist.org/packages/creof/wkb-parser) | Description |

| JavaScript | [Terraformer](https://terraformer-js.github.io/ "Home - Terraformer") |
| JavaScript | [Wicket](https://github.com/arthur-e/Wicket "GitHub - arthur-e/Wicket: A modest library for moving between Well-Known Text (WKT) and various framework geometries") |
| C++ | [GEOS - Geometry Engine, Open Source](https://trac.osgeo.org/geos "GEOS") |

-->

# References

## Sources

* [MySQL :: MySQL 8.0 Reference Manual :: 11.4 Spatial Data Types](https://dev.mysql.com/doc/refman/8.0/en/spatial-types.html)
* [MySQL :: MySQL 5.7 Reference Manual :: 11.4 Spatial Data Types](https://dev.mysql.com/doc/refman/5.7/en/spatial-types.html)
* [Simple Feature Access - Part 2: SQL Option | OGC](https://www.ogc.org/standards/sfs)
* [Playing with Geometry/Spatial Data Types in MySQL | by Uday Hiwarale | System Failure | Medium](https://medium.com/sysf/playing-with-geometry-spatial-data-type-in-mysql-645b83880331)
* [Geography in MySQL 8.0 | MySQL Server Blog](https://mysqlserverteam.com/geography-in-mysql-8-0/)
* [Spatial Reference Systems in MySQL 8.0 | MySQL Server Blog](https://mysqlserverteam.com/spatial-reference-systems-in-mysql-8-0/)
* [Simple Features - Wikipedia](https://en.wikipedia.org/wiki/Simple_Features)
* 