# Material Mapping to DwC-DP

Most fields can be mapped with a one to one mapping to the DwC-DP.
A couple of new fields are not present in openDS which might require some discussion.

We ignore the taxonomical fields in the material file, as we use the DwC-DP Identification file for this.

We put additional identifiers in the material-identifier file.
There we exclude three identifiers as these are either not relevant or are already included in specific fields.
The identifiers we exclude are:
- dwc:catalogNumber
- dwc:recordNumber
- dwca:ID

We put a link to the media in the material-media file.
Here we don't have information about the subject or the physicalSetting so these fields are left blank.

We don't yet support assertions or Digital Specimen Part in the material mapping.
We don't yet map references for material.