# Location Coordinate Terms

This is a set of terms which are combined in this single file.
This is mainly te reduce the amount of files.
In general, we made assumption that the coordinates are provided in World Geodetic System 1984 in decimal numbers.
There is no option yet to change other systems or to change degrees to decimal.

## openDS
Will be harmonised to the DWC terms for coordinates.
- `dwc:decimalLatitude`
- `dwc:decimalLongitude`
- `dwc:geodeticDatum`

## Mapping
Before searching for the Coordinate term in the below terms we will first check if a default value or explicit mapping has been set.
In the case of Coordinate terms this is improbable however, the functionality is there.

### DWC
As we use the DWC fields we will look for an exact match for the coordinate field.
If these term(s) are not available or are null we will leave this field empty (`null`).

### ABCDEFG
Within ABCDEFG we search for the specific coordinate field.
An important assumption is that we will use the first siteCoordinates that we can find.

#### Latitude
For ABCDEFG we will look at matches on the term(s) in this order:
- `abcd:gathering/siteCoordinateSets/siteCoordinates/0/coordinatesLatLong/latitudeDecimal`

If these term(s) are not available or are null we will leave this field empty (`null`).

#### Longitude
For ABCDEFG we will look at matches on the term(s) in this order:
- `abcd:gathering/siteCoordinateSets/siteCoordinates/0/coordinatesLatLong/longitudeDecimal`

If these term(s) are not available or are null we will leave this field empty (`null`).

#### GeodeticDatum
For ABCDEFG we will look at matches on the term(s) in this order:
- `abcd:gathering/siteCoordinateSets/siteCoordinates/0/coordinatesLatLong/spatialDatum`

If these term(s) are not available or are null we will leave this field empty (`null`).