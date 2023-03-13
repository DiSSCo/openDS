# Mapping Json

Before any automated mapping is being made the system will first see if the user (data administrator) provided any explicit information on the mapping.
This information can be in two forms:
- Setting of default values 
- Setting of an explicit field mapping

The application will first check if a default value has been set, then if an explicit field mapping was set, then it will use the logic described in the specific terms. 

## Setting of default values
A data administrator can set default values for any attribute in the harmonised data model.
Whenever this mapping it used, all attributes for a particular field will be set.
This means that for example all information in the dataset has the same license but this license is not part of the dataset, it can be set as a default value.
The format is `{harmonised key} : {fixed value}`
Before the translator does anything for a particular field it will first check if a default value has been set.

## Setting of explicit field mapping
If no default value has been set the application will check if there is an explicit field mapping.
This means if there is any explicit mapping saying that a harmonised field needs to be mapped to a particular unharmonised field.
For this we will use the JSON variant for none JSON based data standards (such as DWCA, ABCDEFG).
This also means that if the field for the explicit mapping is empty we will not check for any other fields but will fill this harmonised field with `null`.
The format is `{harmonised key} : {unharmonised key}`

## Example
```
{
  "mapping": [
    {
      "ods:physicalSpecimenId": "dwc:occurrenceID"
    },
    {
      "ods:specimenName": "dwc:acceptedNameUsage"
    }
  ],
  "defaults": [
    {
      "ods:physicalSpecimenIdType": "combined"
    },
    {
      "ods:type": "ZoologyInvertebrateSpecimen"
    },
    {
      "ods:organizationId": "https://ror.org/040ck2b86"
    }
  ]
}
```
