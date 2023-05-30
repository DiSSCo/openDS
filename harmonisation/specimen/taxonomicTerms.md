# Taxonomic terms

This is a set of terms which are combined in this single file.
We combined these terms as we use a similar approach to harmonised them.
Additionally, it would unnecessarily grow the amount of terms files in this repository.

## openDS
These terms will be harmonised for taxonomy.
- `dwc:class`
- `dwc:family`
- `dwc:genus`
- `dwc:infraspecificEpithet`
- `dwc:kingdom`
- `dwc:order`
- `dwc:phylum`
- `dwc:scientificNameAuthorship`
- `dwc:specificEpithet`
- `dwc:taxonRank`
- `dwc:typeStatus`

## Mapping
Before searching for the taxonomy terms we will first check if a default value or explicit mapping has been set.
In the case of taxonomy terms this is improbable however, the functionality is there.

In general for both DWC and ABCD(EFG) we can have multiple taxonomic identifications for one specimen.
This means that before filling in the harmonised field we first have to determine which identification to use.
This determination is stored in a temporary field and used in the calculation of all taxonomic fields.

### DWC
For DWC we first check the core fields to find the accepted identification.
For example for the `dwc:class` we first check this field in the core file of the specimen.
If it is not available there, we check if there is an identification extension.
If this is available, we determine which of the identification is the accepted identification.
We do this based on the `dwc:identificationVerificationStatus`.
Identifications with Verification Status on 1 are seen as accepted, with 0 as unaccepted.
If there is no `dwc:identificationVerificationStatus` we take the first one we encounter.

In some cases there is only one identification, but it has a Verification Status of 0.
This means that we would not give any identification to the specimen.

### ABCDEFG
For ABCD(EFG) we use a similar approach as DWC, only there is no core file.
A specimen in ABCD can have multiple identifications, where `preferredFlag` is used to indicate if the identification is accepted.
To determine which identification to use, we go over all the identifications.
If no preferredFlag has been set, we will use the first identification we encounter.
If a preferredFlag has been set, we use the identification where the flag has been set to `true`.
It is possible that all preferredFlag have been set to `false`, in this case we won't set the taxonomic identification.

After determining which identification to use, we need to gather all taxonomic details from the identification.
In ABCD gathering the higher taxonomy is a structured bit differently, as it structured in generic `higherTaxonRank` and `higherTaxonName`.
We have to check which Taxon Rank we need to use, before we can pick the value.
For example: 
```
                    <abcd:HigherTaxa>
                      <abcd:HigherTaxon>
                        <abcd:HigherTaxonName>Animalia</abcd:HigherTaxonName>
                        <HigherTaxonRank>regnum</HigherTaxonRank>
                      </abcd:HigherTaxon>
                    </abcd:HigherTaxa>
```
Here we see that the `HigherTaxonRank` contains `regnum` which means we can fill the name in under `dwc:kingdom`.
As the `HigherTaxonRank` is a free text field, we check against a list of known values per rank.