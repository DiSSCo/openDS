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
So the term `ods:hasIdentification` will contain an array of `ods:Identification` classes.
If the property contains a single class it will just be the capitalised class name.

## Updated ODS boolean field to use the format isXYZ
As the terms which contain an array of object are called hasXYZ we needed a new format for boolean fields.
We followed LTC and use the format isXYZ for boolean fields.

## Classes are singular
All classes are now singular, for example `ods:Identification` instead of `ods:Identification`.
This also changed the file names to singular `citations.json` became `citation.json`

## Added jsonld properties
Each class now contains a required `@type` property to indicate the type of the class.
Optionally (except for the `ods:DigitalSpecimen` class) a `@id` property which can be used for the identifier.
This is an additional property, it does not replace the id terms, such as `dwc:taxonID`.

## EntityRelationship contains Darwin Core terms
Instead of using new ODS terms we will reuse Darwin Core terms for indicating relationships.
Most new terms come from the Darwin Core ResourceRelationship class.    

## Assertion contains Darwin Core terms
Instead of minting new Assertion terms in the ODS namespace we decided to reuse Darwin Core terms.
Most of these terms come from the MeasurementOrFact class.

## Identifier more based on gbif:AlternativeIdentifier DWCA extension
Includes more dcterms instead of ods terms.
We did not copy the class as our Identifier class is broader and includes additional ods terms.

## Changed dwc:InstitutionName to ods:InstitutionName
Institution name is not part of the Darwin Core standard, so we changed it to ods:InstitutionName.

## Other
Small changes in description for some terms.
Fixed the regex for some of the terms.