# Mapping Json

Before any automated mapping is will be made, the system will first see if the user (data administrator) provided any explicit information on the mapping.
This information can be in two forms:
- Setting of default values
- Setting of an explicit field mapping

The application will first check if a default value has been set, then if an explicit field mapping was set, then it will use the logic described in the specific terms.

## Setting of Default Values
A data administrator can set default values for any attribute in the harmonised data model.
Whenever this mapping is used, all values for a particular field will be set to the default value.
For example, if all information in the dataset has the same license, but this license is not part of the dataset, it can be set as a default value.
The format is `{harmonised key} : {fixed value}`
Before the translator assigns a particular field, it will first check if a default value has been set.

## Setting of Explicit Field Mapping
If no default value has been set, the application will check if there is an explicit field mapping.
This provides the user the opportunity to indicate if a harmonised field needs to be mapped to a particular unharmonised field.
For non-JSON formats, such as DWCA or BioCASe data, we will first convert it to a JSON structure before we will apply the mapping.
For example, the following ABCD field:
```
<abcd:Unit>
 <abcd:Identifications>
   <abcd:Identification>
     <abcd:Result>
       <abcd:Extension>
         <efg:MineralRockIdentified>
           <efg:ClassifiedName>
             <efg:FullScientificNameString>sedimentary rocks</efg:FullScientificNameString>
```
Will be converted to a single field with name:
abcd-efg:identifications/identification/0/result/mineralRockIdentified/classifiedName/fullScientificNameString
This harmonisation to JSON enables us to makes easier searches and create dynamic mappings.
If the field for the explicit mapping is empty, the translator will not check for any other fields, but will fill this harmonised field with `null`.
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
      "ods:physicalSpecimenIDType": "combined"
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

