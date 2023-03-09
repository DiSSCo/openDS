# DiSSCo Registry & Record Schemata

* [Introduction](https://github.com/DiSSCo/openDS/blob/jbstatgen_registry/openDA/Registry/documentation-intro.md)
* [Defining the registry-level schema](https://github.com/DiSSCo/openDS/blob/jbstatgen_registry/openDA/Registry/documentation-registry-level.md)
* [Defining the record-level schema](https://github.com/DiSSCo/openDS/blob/jbstatgen_registry/openDA/Registry/documentation-record-level.md)
  * [The top-level structure of a record](#the-top-level-structure-of-a-record)
  * [ObjectGroup module](#objectgroup-module)
    * [collectionName and baseTypeOfCollection (required)](#collectionname-and-basetypeofcollection-required)
    * [description](#description) 
    * [collectionManagementSystem](#collectionmanagementsystem-required)
    * [RecordLevel](#recordlevel-required)


---
> Information persistently and globally uniquely identifying each organization and its overall collection entity will be stored as one record within the DiSSCo registry. 
---


## Defining the record-level schema

For the registry to validate as a whole, records need to validate against a clearly defined, preset record-level schema. The record-level JSON schema can be defined in a file independent of the JSON schema file for the registry-level. This is the approach taken here.

The begin of the JSON Schema object at the record-level has the same structure as the JSON Schema object for the registry-level schema. The keywords `$schema`, `$id`, `title` and `description` are given. 

Subsequently the record-level schema is defined using a modular approach that employes the JSON Schema `definitions` keyword together with `$ref`, an identifier that points to the definitions of the different modules (i.e. objects and arrays), in this case, within the file.

The `type` of a record as a whole is `object` since the subsequently in the form of `properties` described schema of the record entity is of compound structure.

EXAMPLE CODE:  Begin of the validation JSON schema for the registry records

```json
{
    "$schema": "https://json-schema.org/draft/2020-12/schema",
    "$id": "https://raw.githubusercontent.com/tdwg/cd/registry-schema/examples/implementation%20examples/dissco-record-schema.json",
    "title": "DiSSCo Collection Facility Profile",
    "description": "JSON-Schema for records of collection facilities focusing on uniquely identifying the institution (ROR-identifier) and providing information summarizing a single top-level institution-wide collection for the purpose of dashboard visualizations",
	"$ref": "#/definitions/RegistryRecord",
	"definitions": {
    
        [...]
            
    }
}
```

### The top-level structure of a record

The `RegistryRecord` module at the highest level of the record defines a top-level structure that starts out with two `properties`, which reside side-by-side. One main submodul describes the scientific collections hosted at the facility, the `ObjectGroups`. The other main submodule provides information about the organization or institution that is (legally) responsible for and managing the collection facility, the `Agents`. 

According to the Latimer Core standard for describing collections as object groups, the `ObjectGroup` is the single starting point for structuring and storing information about scientific collections. Information about the organization that is responsible for the collection(s) is given within a top-level `ObjectGroup` or more precisely it is linked from within the `ObjectGroup`. From the perspective of the standard, organizational information is only considered as a "property" of the `ObjectGroup` and not seen as independent information object.

However, registry records go beyond the description of collections as object groups. They exist at the boundary between the representation of collections and the contexts that they are embedded in. In these contexts, scientific collections, as well as their digital representations as `ObjectGroups` fulfill different roles. 

On one hand, they exist in a role that represents the sum of the material or information artifact objects within the collection and summarizes their traits. They act as "entities". On the other hand, collections and digital object groups can act as "agents" in analog and digital transactions. They do so by authorizing and delegating action to persons (and machines) associated with the collection, e.g. collection staff, authorized scientists, facility administrators or insitution directors. At the same time, formal legal recognition generally lies with the organizational unit that is responsible and accountable for the collection. For example, in loan transactions involving physical collection objects, the official partners in the loan transaction often are the organizations and institutions associated with the loan, that is, the institution in which the physical object is accessioned and the institution that employs the staff who borrows the specimen.

These multiple roles correspond, for example, to the primary elements in the W3C-recommended Provenance ontology (PROV), which will be used to describe and record event-based transactions within DiSSCo. In applications of the ontology, `ObjectGroups` can be both `prov:Entities` and `prov:Agents`. Therefore, the structure of the registry records supports both main roles and sets `ObjectGroups` and `Agents` (i.e. `OrganisationalUnits`) equally at the top level of the records. To adhere to the structure of the Latimer Core standard, an `ObjectGroup` links to its associated `OrganisationalUnit` from within its JSON object using the LtC term `hasOrganisationalUnit`.

Currently, information is considered only at the level of the highest-up parent organization and an institution-wide collection. Therefore, the number of allowed entries in the lists (arrays) for `ObjectGroups` and `Agents` is set to one (see the combination of `minItems` and `maxItems`). To avoid the potential development of ambiguities, no duplicated entries are allowed. Future extensions of the schema can allow the representation of hierarchical structures that are differentiating more specialized collection units and lower level organizational units.

---
> **RecordLevel added - needs to be described. Check if RL is ok or needs to be RecordLevelfullRegistryRecord**

EXAMPLE CODE: Declaring, identifying and describing the top-level structure of a DiSSCo Registry record 

```json
{
    "$schema": "https://json-schema.org/draft/2020-12/schema",
    "$id": "https://raw.githubusercontent.com/jbstatgen/dissco_registry/main/LtCProfile_RecordLevel_20230203.json?token=GHSAT0AAAAAAB6K52PCM3SKFHT5G567TRVIY66G55Q",
    "title": "DiSSCo Collection Facility Profile",
    "description": "LtC-based JSON schema for the record of a collection facilities focusing on uniquely identifying the institution (ROR-identifier) and providing information summarizing a single top-level institution-wide collection for the purpose of dashboard visualizations",
    "$ref": "#/definitions/RegistryRecord",
    "definitions": {
        "RegistryRecord": {
            "type": "object",
            "title": "Schema for a registry record",
            "additionalProperties": true,
            "required": [
                "ObjectGroups",
                "Agents"
            ],
            "properties": {
                "ObjectGroups": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/ObjectGroup"
                    },
                    "minItems": 1,
                    "maxItems": 1,
                    "uniqueItems": true
                },
                "Agents": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/OrganisationalUnits"
                    },
                    "minItems": 1,
                    "maxItems": 1,
                    "uniqueItems": true
                },
                 "RecordLevelFullRegistryRecord": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/RecordLevelFullRegistryRecord"
                    },
                    "minItems": 1,
                    "maxItems": 1,
                    "uniqueItems": true
                }
           }
        },

    [...]
    
    }
}

```

In the following part of the code for the JSON schema, still within `definitions`, all required submodules referenced in `ObjectGroups` and `Agents` are defined as JSON Schema objects. 

For clarity and brevity, the first four lines with the keywords `$schema`, `$id`, `title` and `description` are omitted. the following code examples will start with the reference identifier (`$ref`) linking to the top-level `RegistryRecord` within `definitions`.


### ObjectGroup module

Each object group that might be defined within a record, will follow the same JSON schema. Thus, in future extensions of the schema to represent hierarchical structures, all sub-collections will adhere to the same record schema.

The submodule `ObjectGroup` starts in its first line with an identifier (`$ref`) that links to the file providing the JSON Schema code for the class `ltc:ObjectGroup` in the official TDWG Latimer Core repository. In this way, all functionality of the class is made available to the record schema in its most up-to-date form. Since the line `"additionalProperties": true` explicitly enables additional keywords, which are not given in the schema defining the DiSSCo Registry record. Thus, instances of records from other sources containing additional data can still be validated by the registry, as long as they adhere to the linked version of the JSON Schema code for the LtC classes. 

Subsequently, the properties `required` within `ObjectGroup` are listed. These properties currently are properties that are all defined within the `ltc:ObjectGroup` class, including relationships to other ltc classes. Links to these ltc classes are provided in the form of properties that start with `has`, e.g. `hasOrganisationalUnit`, `hasIdentifier`, etc. The outcome of these links are always arrays according to the standard, which needs to be taken into account in the design of the JSON schema.

`Required` properties for the description of `ObjectGroups` in DiSSCo Registry records are first `collectionName` and `baseTypeOfCollection`. These two properties are required as a minimum of information that needs to be provided, as set by the standard. For the registry context considered here, in addition `hasRecordLevel`, `hasReference` and `hasOrganisationalUnit` are required. Currently set as required are the properties `ObjectClassification` and `MeasurementOrFacts`, though these will be only needed if the data stored within the DiSSCo Registry should be visualized, e.g. in the form of dashboards, or further analyzed by integrating the registry's data into analytical workflows.

Now the `properties` of the `ObjectGroup` are listed within the code. These submodules will be discussed individually in the following.

EXAMPLE CODE: Defining the ObjectGroup module and listing its properties

```json
    "$ref": "#/definitions/RegistryRecord",
    "definitions": {
        "RegistryRecord": {
            "type": "object",
            "title": "Schema for a registry record",
            "additionalProperties": true,
            "required": [
                "ObjectGroups",
                "Agents"
            ],
            "properties": {
                "ObjectGroups": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/ObjectGroup"
                    },
                    "minItems": 1,
                    "maxItems": 1,
                    "uniqueItems": true
                },
                "Agents": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/OrganisationalUnits"
                    },
                    "minItems": 1,
                    "maxItems": 1,
                    "uniqueItems": true
                }
            }
        },
        "ObjectGroup": {
            "$ref": "https://raw.githubusercontent.com/tdwg/cd/registry-schema-update/standard/json-schema/object-group.json",
            "title": "Object representing institution-wide collection",
            "type": "object",
            "additionalProperties": true,
            "required": [
                "collectionName",
                "baseTypeOfCollection",
                "collectionManagementSystem",
                "RecordLevel",
                "Reference",
                "OrganisationalUnits",
                "ObjectClassification",
                "MeasurementOrFacts"
            ],
            "properties": {
                "collectionName": {
                    "type": "string"
                },
                "baseTypeOfCollection": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/BaseTypeOfCollection"
                    },
                    "minItems": 1
                },
                "description": {
                    "type": "string"
                },
                "collectionManagementSystem": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/CollectionManagementSystem"
                    },
                    "minItems": 1
                },
                "RecordLevel": {
                    "$ref": "#/definitions/RecordLevel"
                },
                "Reference": {
                    "$ref": "#/definitions/Reference"
                },
                "OrganisationalUnits": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/OrganisationalUnit"
                    }
                },
                "PersonRoles": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/OrganisationalUnitPersonRole"
                    }
                },
                "disciplines": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/Discipline"
                    }
                },
                "typeOfCollections": {
                    "type": "array",
                    "items": {
                        "type": "string"
                    }
                },
                "MeasurementOrFacts": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/ObjectGroupMeasurementOrFact"
                    }
                },
                "ResourceRelationships": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/ResourceRelationshipElement"
                    }
                },
                "discipline": {
                    "type": "string"
                },
                "ResourceRelationship": {
                    "$ref": "#/definitions/PurpleResourceRelationship"
                }
            }
        },

    [...]
    
    }

```


#### collectionName and baseTypeOfCollection (required)

First, a name has to be given to the `ObjectGroup`, here the organization- or institution-wide collection by the record provider.

In addition, information needs to be provided about the most general type(s) of objects that are preserved, maintained and managed by the organization or institution. A controlled vocabulary is used to allow record providers to describe the basis of the objects in a standardized way. Objects within the collection, that is, object group can be of type `MaterialEntity`, that is, physical objects (the focus of the DiSSCo Registry currently), of type `InformationArtifact`, including e.g. digital media, datasets of DNA sequences, etc., or they can be for comprehensiveness of type `other` and a set of related controlled value strings.

In the LtC standard, the property's `type` is a `string`. However, to describe a collection, specifically an organization-wide group of objects, several types of entities might be present within the collection. Thus, in this case multiple controlled value strings will need to be selected from a list of standardized terms. Therefore, for use within a registry record, the expected data for this property here is set to `array`.

*Controlled vocabulary:*

The controlled vocabulary used for `baseTypeOfCollection` is under development and discussion by TDWG. 

Controlled value strings: `MaterialEntity`, `InformationArtifact`, `AbstractionConcept`, `other`, `knownAndWithheld`, `unspecified`, `unknown`, `notApplicable`

#### description 

A free-text, verbal description of the overall collection at the organization can be provided with the record. This data is not required.


#### collectionManagementSystem (required)

Data is required about the collection management system(s) (CMS) that is/are in use for the management of the collection(s) at the organization. LtC defines the expected type for this property to be an array.

This property is not set as required term by the standard. However, for the purposes of the DiSSCo registry, the data provided by `CollectionManagementSystem` is of interest. It can be used to determine the specific settings needed in interactions between a local CMS and the DiSSCo technical infrastructure. The type of CMS in use might require a specific mapping to the data model employed by the DiSSCo technical infrastructure.

*Controlled vocabulary:*

A controlled vocabulary will need to be developed and/or found. It might be based on existing lists of CMS' in use. 

Controlled value strings (currently): `Arctos`, `Axiell EMu`, `DINA`, `Diversity Workbench/Collection`, `Earthcape`, `JACQ`, `Specify`, `other`, `knownAndWithheld`, `unspecified`, `unknown`, `notApplicable`


```json
        "CollectionManagementSystem": {
            "type": "string",
            "enum": [
                "Arctos",
                "Axiell EMu", 
                "DINA",
                "Diversity Workbench/Collection",
                "Earthcape",
                "JACQ",
                "Specify",
                "other",
                "knownAndWithheld",
                "unspecified",
                "unknown",
                "notApplicable"
            ]
        },

```

#### RecordLevel (required)

This property is the equivalent of the `ltc:hasRecordLevel` class property in Latimer Core. The `ltc:RecordLevel` class provides information necessary for the reuse of the record and its information contents. Only one `RecordLevel` instance is allowed per `ObjectGroup` since e.g. several `license` properties are not meaningful. Multiple identifiers can be created within the `RecordLevel` object.

In the standard the `hasIdentifier` and `license` properties are set to be required. **In addition, functionality for `personRole`** is defined.

---
> both objects are needed: the one at the top-level and the one within the OG
> TopLevel: upload or creation of record within registry
> OG level: creation and editing of record itself, that is the information within it. This might have happened before the record was uploaded or after the record was uploaded. 

> Thus both objects are indepenent of each other. 
> However both might follow the same schema, for simplicity. 
> However, TopLevel should have controlled vocab for allowed administrator names.

> MinMaxItems: ID min 1, no max; License MinMax=1 - no, since license is not array but only string, PersonRole Min=0 since not required

> required: only ID and license

> TopLevel and RecordLevel: Identifiers minItems=1, since PID required, or at least some ID or Code
> 

    





```json

```

