# Collector

## openDS
Will be harmonised to `ods:collector`
There is no exact match for collector in either DWC nor ABCD(EFG)

## Mapping
Before searching for collector in the below terms we will first check if a default value or explicit mapping has been set.
In the case of collector this is improbable however, the functionality is there.

### DWC
For DWCA we will look at matches on the term(s) in this order:
- `dwc:recordedBy`
- `dwc:recordedByID`

If these term(s) are not available or are null we will leave this field empty (`null`).

### ABCDEFG
For ABCDEFG there could be multiple collectors in the data.
We will collect them all and concatenate them using the vertical slash `|` as a separator.
We will run over all indexes and look for any values in one of these fields (in this order):
- `abcd:gathering/agents/gatheringAgent/{index}/person/fullName`
- `abcd:gathering/agents/gatheringAgent/{index}/person/agentText`

This means that the value with a single index is `collector1`
If there are two indexes with a collector the value is `collector1 | collector 2`
If these term(s) are not available or are null we will leave this field empty (`null`).
