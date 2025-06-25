# Relationship to DwC-DP

There are differences in how openDS and DwC-DP handle relationships.
openDS sees every link to an external resource as an entity relationship.
This means that url's present in the metadata are often duplicated in the relationship.
DwC-DP on the other hand is more internally focused and uses this class to indicate relationships between entities in the DwC-DP.
In DiSSCo we will only include relationships that cannot be inferred from the metadata.

