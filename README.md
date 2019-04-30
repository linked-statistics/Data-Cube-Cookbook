# Data-Cube-Cookbook

This document should help producers of RDF Data Cube in deciding about how to model multi-dimensional data in RDF. It is written and maintained by people producing RDF Data Cubes.

## Related Documents

* [ Linked Data Cubes Best Practices ](https://islab-uom.github.io/qbBestPractices/): Outcome of an EU H2020 project called [OpenGovIntelligence](http://www.opengovintelligence.eu/). The document did not get any updates for a while, one should check if this could be integrated here or vice versa.

## Recipes

### Measurements with no or invalid number

A common pattern in the real world is that there is an observation with a measurement that cannot be properly represented as a number. We have seen that multiple times, for example:
* There is more than one measurement for a particular observation and it cannot be told which one is/was correct.
* There was a measurement but the result is lost.
* There was a measurement but for whatever reason it cannot be represented as a number.

In all those cases the data owner cannot give a proper number for the measurement. The question is how to handle that in RDF. Not providing a measure or providing more than one measure would violate the RDF Data Cube model, providing a string instead of a number would make validation and handling of the data very complex.

Fortunately there is a proper way to handle this using `NaN` as measure, which is a valid value for [xsd:double](http://www.datypic.com/sc/xsd/t-xsd_double.html), [xsd:float](http://www.datypic.com/sc/xsd/t-xsd_float.html) but *not* for [xsd:decimal](http://www.datypic.com/sc/xsd/t-xsd_decimal.html):

```turtle
BASE <http://example.org/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

<observation> <measure> "NaN"^^xsd:double .
```

This should pass as proper RDF in validators like `riot`.
