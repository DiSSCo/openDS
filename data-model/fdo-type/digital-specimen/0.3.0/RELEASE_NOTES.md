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

## Changed dwc:InstitutionName to ods:OrganisationName
Institution name is not part of the Darwin Core standard, so we changed it to ods:InstitutionName.

## Change InstitutionXXX terms to OrganisationXXX
Institution was determined to narrow for the usage. 
Organisation fits the purpose better. 

## Added ODS status to all Digital Objects
An object can be in draft, active or tombstone state.

## Added optional object TombstoneMetadata to all Digital Objects
This object contains information about the tombstone state of the object.
It will be present when the ODS status of the object is tombstone.

## Reworked the ods:Agent object to be in line with international standards
Make use of schema.org terms for the Agent object.
This makes it more generic and it is now used in all Digital Objects (not just DigitalSpecimen and DigitalMedia0)
It is a bit more generic then it used to be but that also makes it more flexible.
It reduces redundancy between the different Digital Objects
We replaced all instances of agents with a generic Agent object.
This agent object can have the form of a `schema:Person`, `schema:Organization` or `as:Application`.
This should be a generic implementation which should be accepted by most terms as terms such as `dcterms:creator` does not enforce a specific type of value.
The exception to this rule is the CreateUpdateTombstoneEvent which is based on prov-o.
Prov-o enforce their own types for the agent (`prov:Person`, `prov:Organization` and `prov:SoftwareAgent`)


## Other
Small changes in description for some terms.
Fixed the regex for some of the terms.