# Chronostratigraphic terms

This is a set of terms which are combined in this single file.
We combined these terms as we use a similar approach to harmonised them.
Additionally, it would unnecessarily grow the amount of terms files in this repository.

## openDS
Will be harmonised to the DWC terms for chronostratigraphy.
- `dwc:earliestAgeOrLowestStage`
- `dwc:earliestEonOrLowestEonothem`
- `dwc:earliestEpochOrLowestSeries`
- `dwc:earliestEraOrLowestErathem`
- `dwc:earliestPeriodOrLowestSystem`
- `dwc:latestAgeOrHighestStage`
- `dwc:latestEonOrHighestEonothem`
- `dwc:latestEpochOrHighestSeries`
- `dwc:latestEraOrHighestErathem`
- `dwc:latestPeriodOrHighestSystem`

## Mapping
Before searching for the chronostratigraphy term in the below terms we will first check if a default value or explicit mapping has been set.
In the case of chronostratigraphy terms this is improbable however, the functionality is there.

### DWC
As we use the DWC fields we will look for an exact match for the chronostratigraphic field.
If these term(s) are not available or are null we will leave this field empty (`null`).

### ABCDEFG
For the ABCDEFG we will look need to look at two different fields.
The first specifies the chronostratigraphic division.
- `abcd-efg:earthScienceSpecimen/unitStratigraphicDetermination/chronostratigraphicAttributions/chronostratigraphicAttribution/{index}/chronoStratigraphicDivision`
After we identified the chronostratigraphic division we can put the correct value in the dwc field.
- `abcd-efg:earthScienceSpecimen/unitStratigraphicDetermination/chronostratigraphicAttributions/chronostratigraphicAttribution/{index}/chronostratigraphicName`
In general we will put the same value in the earliest and latest DWC division field, unless we are able to determine a sub or super division.
Then we will put the subdivision in the earliest and the division in the latest (or with super the other way around).
We do make the assumption that we can use the first division match we can find.
#### Stage
We will look for a division that matches one of these fields (ignores case):
- `Stage`
For `dwc:earliestAgeOrLowestStage` we will first look at:
- `SubStage`

If these term(s) are not available or are null we will leave this field empty (`null`).
#### Eonothem
We will look for a division that matches one of these fields (ignores case):
- `Eonothem`

If these term(s) are not available or are null we will leave this field empty (`null`).
#### Series
We will look for a division that matches one of these fields (ignores case):
- `Series`
- `Serie`
For `dwc:earliestEpochOrLowestSeries` we will first look at:
- `SubSeries`
- `SubSerie`

If these term(s) are not available or are null we will leave this field empty (`null`).
#### Erathem
We will look for a division that matches one of these fields (ignores case):
- `Erathem`

If these term(s) are not available or are null we will leave this field empty (`null`).
#### System
We will look for a division that matches one of these fields (ignores case):
- `System`

If these term(s) are not available or are null we will leave this field empty (`null`).