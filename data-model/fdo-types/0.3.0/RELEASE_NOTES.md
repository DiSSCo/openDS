# Release Notes

New version 0.3.0 for all files concerning the digital specimen.

## ODS Prefix
ODS prefix for all terms which still weren't assigned to a ontology.

## Updated arrays to be plural
We decided to update the arrays to be plural, in line with recommendated practices.
This means that where Darwin Core Classes where available we wrapped this by an ods term with the plural.
For example, `dwc:Identification` becomes wrapped in `ods:Identifications` which now contains zero or more instances of `dwc:Identification`.
The tradeoff is that we added an additional layer of nesting, but we believe this is worth it to keep the terms in line with the Darwin Core standard.

## Other
Small changes in description for some terms.
dwc:institutionName is not a Darwin Core term, converted to ods:institutionName. 
