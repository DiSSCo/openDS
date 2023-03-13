# HasMedia

## openDS
Will be harmonised to `ods:hasMedia`
There is no exact match for hasMedia in either DWC nor ABCD(EFG).
It is a boolean value to indicate whether the specimen has a media object attached to it.

## Mapping
Before searching for objectType in the below terms we will first check if a default value or explicit mapping has been set.
In the case of objectType this is improbable however, the functionality is there.

### DWC
For DWCA we will look at matches on the term(s) in this order:
- `dwc:associatedMedia`

To implement, is to check the associated media extensions.
Jira ticket:
https://naturalis.atlassian.net/browse/DD-301

If these term(s) are not available or are null we will leave this field empty (`null`).

### ABCDEFG
For ABCDEFG we will look at matches on the term(s) in this order:
- `abcd:multiMediaObjects/multiMediaObject/0/fileURI`

Here we make the assumption that the first images is always at index 0 and the fileURI is always filled if a media object is present.
This means that if we find a value here we can assume that there is one or more media objects attached. 