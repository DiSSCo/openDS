# Release Notes

New version 0.3.0 for all files concerning the digital specimen.

## ODS Prefix
ODS prefix for all terms which still weren't assigned to a ontology.

## ID capitalised
All terms that contain ID are now capitalised, for example `ods:ID` instead of `ods:id`.
This makes it more in line with Darin Core from which we borrow most of our terms.

## Added Organism terms
Added terms for dwc:Organism class and put them on the top level.
They can be used to indicate that this specimen is from a particular organism.
We could use this to group all specimen from a single organism together.

## Updated classes to be in line with best practices
All class are now capitalised.
When there will a property contains an array of classes it will start with `has`.
So the term `ods:hasIdentifications` will contain an array of `ods:Identification` classes.
If the property contains a single class it will just be the capitalised class name.

## Classes are singular
All classes are now singular, for example `ods:Identification` instead of `ods:Identifications`.
This also changed the file names to singular `citations.json` became `citation.json`

## Added jsonld properties
Each class now contains a required `@type` property to indicate the type of the class.
Optionally (except for the `ods:DigitalSpecimen` class) a `@id` property which can be used for the identifier.
This is an additional property, it does not replace the id terms, such as `dwc:taxonID`.

## Other
Small changes in description for some terms.
dwc:institutionName is not a Darwin Core term, converted to ods:institutionName. 
Fixed the regex for some of the terms.