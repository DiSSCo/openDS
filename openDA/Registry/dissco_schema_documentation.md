# DiSSCo Registry & Record Schemata


## Table of Contents

See also build-in drop-down menu on left-hand end of display header for file on GitHub.

* [Introduction](#introduction)
  * [Technical implementation as JSON Schema-based profiles](#technical-implementation-as-json-schema-based-profiles)
  * [Some JSON Schema defaults](#some-json-schema-defaults)
* [Defining the registry-level schema](#defining-the-registry-level-schema)
  * [Top-level registry module](#top-level-registry-module)
  * [RegistryRecords array](#registryrecords-array)
  * [ltc:hasRecordLevel module at the registry-level](#ltchasrecordlevel-module-at-the-registry-level)
  * [ltc:hasReference module at the registry-level](#ltchasreference-module-at-the-registry-level)
* [Defining the record-level schema](#defining-the-record-level-schema)
  * [The top-level structure of a record](#the-top-level-structure-of-a-record)
  * [ObjectGroup module](#objectgroup-module)
    * [collectionName and baseTypeOfCollection (required)](#collectionname-and-basetypeofcollection-required)
    * [description](#description) 
    * [collectionManagementSystem](#collectionmanagementsystem-required)
    * [RecordLevel](#recordlevel-required)



## Introduction

The DiSSCo Registry will be storing and making available records of collection facilities. For each facility, its record in a first version comprises top-level information about the cumulative institution-wide collection holdings and the legal entity that is responsible for these collection holdings. 

The purpose of the DiSSCo registry initially is two-fold: First, the registry will provide authoritative information about organizations and institutions that will be interacting with the DiSSCo Research Infrastructure (RI) as agents in transactions. Second, information describing the organizations' collections and their holdings will provide data on the collections themselves as well as their contents for analyses (e.g. a national, continent-level or global sum of collection entities or objects) and dashboard visualizations.

Transactions between collection-holding organizations and the DiSSCo RI, for example, can be mediated by the ELViS module of the DiSSCo RI and be in the form of digital representations of loan requests and subsequent loan procedures. These include assessments of the request and, upon approval, the shipping of physical specimens between institutions. 

Furthermore, all digital transactions between the DiSSCo RI and partner infrastructures, for example Collection Management Systems (CMS) locally maintained by collection facilities, require the association of at least one acting agent to all events within a transaction. Such a digital transaction can be, for example, that the DiSSCo RI in a first step or event informs a local CMS about new or updated data, often in the form of FAIR open Digital Specimen (openDS) entities, that arrived in its infrastructure. This data might be of interest to collection staff and scientists, who can decide to initiate the transfer of the data from the networked DiSSCo RI to the local CMS. Once the offer of new data is accepted, forming a second event, the data will be transferred to the partner CMS in a following third event. In all of these events the agents associated with the activities need to be reliably identified. The DiSSCo Registry will be the authoritative source for information on the organizations that interact with it. The DiSSCo Registry will fulfill this role in coordination and collaboration with the Global Registry of Scientific Collections ([GRSciColl](https://www.gbif.org/grscicoll)) maintained by the Global Biodiversity Information Faciliity ([GBIF](https://www.gbif.org/)).

In an initial operational phase of the DiSSCo RI, identification of partners interacting with the RI as agents will be at the level of the top-level formal organization that is legally responsible for all the collection(s) that it preserves and manages. The collection(s) hosted by an organization initially also will be represented by a top-level organization-wide, cumulative collection entity. Thus, no organizational or collection hierarchies are represented in a first step.


### Technical implementation as JSON Schema-based profiles

Technically, a DiSSCo Registry record or set of records will be transcribed into JSON or JSON-LD for the transfer of its information over digital networks and, thus, its participation in interactions between the DiSSCo RI and its partners. Thereby, it needs to be ensured that all records or instances that are transmitted for interaction with the DiSSCo RI adhere to the requirements set by the RI. JSON / JSON-LD encoded records can be validated using a profile or schema encoded by the human-readable "[JSON Schema](https://json-schema.org/)" language, here called in short a "JSON schema". JSON schemata define, set and document the structure, rules and settings that a JSON or JSON-LD instance needs to fulfill. Thus, JSON schemata are the molds or cookie-cutters into which an e.g. metal form or cookie aka the JSON instance or record needs to fit.

In the following, the development and structure of the two JSON schemata for the DiSSCo registry and its records are described stepwise. The starting point of the present schemata formed a machine-generated translation of the [JSON instance providing a record of the Natural History Museum, London](https://github.com/tdwg/cd/blob/master/examples/implementation%20examples/json/nhm_uk_json_example.json) by Matt Woodburn, one of the conveners of the TDWG Latimer Core standard task group. This record-level JSON object was translated into a JSON Schema applying the [translation tool](https://app.quicktype.io/#l=schema) provided by [quicktype](https://quicktype.io/). The output of the translation subsequently was modified and adapted further.

As a very first step it can be pointed out that a JSON Schema object is delimited by a pair of brackets `{}`. Generally a schema is structured by key - value pairs, which store the information and are separated by a comma.

EXAMPLE CODE:	JSON Schema basics
    
```json
{
    "key1": "value1", 
    "key2": "value2"
}
```


### Some JSON Schema defaults

As preamble for the following descriptions, some defaults for objects defined in schemata are summarized here for the validation of JSON or JSON-LD instances based on a JSON schema. The information is taken from  https://json-schema.org/understanding-json-schema/index.html. By default: 
* Leaving out properties and providing additional properties is valid. 
* Therefore an empty object is valid. This corresponds to the situation for arrays, since an empty array is valid, too.
* Defined properties are not required. Should they be mandatory, they need to be listed as items in the array associated with the `required` keyword.
* Any property name that doesn't match the property names stated in a schema for a key - value pair is ignored.



## Defining the registry-level schema

The DiSSCo Registry can be represented by two interlinked JSON schemata. One schema describes the structure of the registry itself and defines information that needs to be provided for the registry and each set of records transferred from a different registry or source. Within this top-level or registry-level schema a link connects to the record-level schema, which describes the minimal requirements for all records stored within the registry.

All JSON schemata start out by being declared, identified and described. The keyword `$schema` provides information on the version of the JSON Schema language that is employed. `$id` sets the link to the location at which the schema is stored and from which it can be retrieved. The title and description keywords provide slots to store descriptive information about the schema.

The registry-level schema corresponds to the DiSSCo Registry as a whole in the form of an entity. Accordingly the title and description name the registry and describe the purpose of the registry as a tool, respectively.

EXAMPLE CODE:   Information declaring and identifying the registry-level JSON schema, and describing the DiSSCo registry as well as its purpose

```json
{
    "$schema": "https://json-schema.org/draft/2020-12/schema",
    "$id": "*<link to registry-level file location>*",
    "title": "DiSSCo Registry Profile",
    "description": "JSON Schema- and Latimer Core-based profile describing a registry of collection facilities for the DiSSCo RI in a standardized way.",

    [...]
    
}
```

The overall structure and requirements for a valid registry are here defined in the form of modules and submodules. These modules are defined at the bottom of the file in an independent object or section opened by the keyword `"definitions"`. In this section of the schema, an unsorted list of all modules (i.e. (sub-)schemata) provides access to their definitions, independent of their positions in the overall structure of the top-level schema.

The overall structure of the registry is comparably simple and consists of one main module (`Registry`) and its three submodules (`RegistryRecords`, `RecordLevel` and `References`). 


### Top-level registry module

The entry point into the structure of the registry schema is a JSON object or module called `Registry`. It is the only module that is accessed from the top-level by `"$ref": "#/definitions/Registry"`. The key `$ref` (as a form of `$id` at a lower level than the root level, see above) is used to identify the overall module or schema for the registry and provide a link to its location. The module itself and its definition is given within the present JSON Schema file as one of the modules listed within the `definitions` section. 

The identifier `"$ref": "#/definitions/Registry"` points to the `definitions` object in the present file and schema (`#`), and more specifically to the object `Registry` within `definitions`. The `Registry` module is of type `object`, which is further specified by its `properties`. Properties specify requirements that need to be fulfilled at the level of the object entity in which they are located, for the entity to successfully validate. At the registry-level, the `"properties": { }` key defines requirements that apply to the registry itself, that is, to the whole list of records as an entity. 

The three `properties` listed under the `properties` keyword are also `required`, that is they are listed as items in the array associated with the `required` keyword. The three properties are the submodules or subschemata `RegistryRecords`, `RecordLevelRegistryArray` and `References`. The submodules themselves are defined in a linked JSON Schema file (cp. `RegistryRecords`) or as entities below the `Registry` object within `definitions`.

The key `additionalProperties` is set to `true`, since the registry does not prohibit a registry to store additional information. The present registry-level schema only requires a shared minimal set of information given and defined by its modules.

This last general requirement states a default, i.e. `"additionalProperties": true`. This default is highlighted here, since it is of importance for future interactions of the DiSSCo Registry with other catalogs of collection facilities, as for example the CETAF Registry and GBIF's GRSciColl. The latter two registries have their independent, potentially wider and/or divergent scopes regarding e.g. their use cases, application purposes and involved stakeholders. While it is advantageous for these registries to share certain properties, that is key - value pairs, so that all registries are easily integrated and interoperable, they might also define additional properties to store more and/or different information. Such additional information is not necessary for a sucessfully fulfilling of the functions for which the DiSSCo Registry is designed. It is thus not included in the schemata for the DiSSCo Registry. Thus, as long as the minimum set of properties required by the DiSSCo Registry and its records is present and the information stored in them is validated, the key `additionalProperties` in the schema for the DiSSCo Registry explicitly allows additional properties to be present. In other words, the DiSSCo Registry schema doesn't care if JSON or JSON-LD-encoded records of collection facilities contain additional information.


EXAMPLE CODE:	Defining the top-level module of the JSON schema for the registry

```json
{
    "$schema": "https://json-schema.org/draft/2020-12/schema",
    "$id": "*<link to registry-level file location>*",
    "title": "DiSSCo Registry Profile",
    "description": "JSON Schema- and Latimer Core-based profile describing a registry of collection facilities for the DiSSCo RI in a standardized way.",
    "$ref": "#/definitions/Registry",
    "definitions": {
        "Registry": {
            "type": "object",
            "additionalProperties": true,
            "required": [
                "RegistryRecords",
                "RecordLevelRegistryArray",
                "References"
            ],
            "properties": {
                "RegistryRecords": {

                    [...]

                },
                "ltc:hasRecordLevel": {

                    [...]

                },
                "ltc:hasReference": {

                    [...]

                }
            },
	    "title": "Overall structure at the registry-level"
        }
    }
}
```


### RegistryRecords array 

A registry represents a list or array of records. Thus, the `RegistryRecord` property forms the core of the registry schema. Its type is an array of items, set with `"type": "array"`. In the case of the DiSSCo Registry, each item within the array is the instance of a record describing a collection facility, that is, the record includes information about an organization and its institution-wide collection. 

The type of each item within the registry array is set to `"type": "object"`, since each record within the registry is itself a compound object (not a simple text string or number). At the metalevel of the validation schema, the `"item"` keyword corresponds to a schema-object with several properties.

In other words, the keyword `item` is used to define a single shared subschema for all JSON or JSON-LD instances that will be stored within the array. The items stored within the array are of `"type": "object"`, since the defined subschema, and thus eventually the instances of registry records, are compound objects. The format and information entries of each collection facility record within the registry need to adhere to the defined schema, for the record and, thus, the registry instance to validate. However, while all records in the registry need to have at least the structure of this subschema in common, each record can have additional elements that do not need to be present in other records. 

For the DiSSCo Registry to fulfill its purpose, all records or items within the RegistryRecords-array should be unique, no collection facility should be represented more than once. This ensures that the records cannot drift apart during subsequent updates and annotations. Such drift might lead to a situation, in which the digital representations of a collection facility over time, for example, potentially become associated with two different PIDs. In that case the erroneous impression might arise that two different and independent facilities are represented and exist. Thus, the requirement `"uniqueItems": true` is set.

During the validation of a JSON or JSON-LD encoded registry instance, validation of the `RegistryRecord` subschema and an instance of the module is successful if a list of arbitrary length is given, in which all list items are unique and, furthermore, fulfill the same (minimal) subschema. An empty array, that is, a registry without records will always be valid (see https://json-schema.org/understanding-json-schema/reference/array.html?highlight=uniqueitems).  

As already mentioned, the records (array items) within the registry have their own, record-level JSON schema. The key `$ref` again is used to identify the subschema, here for the registry's records. In this case, the `$ref` keyword provides a (preferably persistent, resolvable and globally unique) link to the storage location of an independent JSON Schema file, which defines the subschema for the registry records and allows that information to be retrieved. This subschema for the record level will be defined in the next chapter. For the registry schema to validate as a whole, the `$ref` link needs to be resolvable, that is, at the location to which the link points, a file needs to exist and be accessible. Moreover, the JSON schema within the linked file is required to be valid, too.

The properties of the list items (of `"type": "object"`) are defined in the linked record-level JSON Schema file using the keyword `"properties": { [...] }`. Nevertheless, additional properties might be defined also here at the registry level. This can be of interest, if individual records of collection facilities that are shared with the DiSSCo Registry are treated differently from whole registries or registry-formated datasets of several records that are uploaded to the DiSSCo Registry. For registry-formatted exchanges, additional properties might be added at this place.



EXAMPLE CODE:	Defining the array of records within the DiSSCo registry

```json
{
    "$schema": "https://json-schema.org/draft/2020-12/schema",
    "$id": "*<link to registry-level file location>*",
    "title": "DiSSCo Registry Schema",
    "description": "JSON Schema- and Latimer Core-based profile describing a registry of collection facilities for the DiSSCo RI in a standardized way",
    "$ref": "#/definitions/Registry",
    "definitions": {
        "Registry": {
            "type": "object",
            "additionalProperties": true,
            "required": [
                "RegistryRecords",
                "RecordLevelRegistryArray",
                "References"
            ],
            "properties": {
                "RegistryRecords": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "description": "Each item in the array is the record of a DiSSCo collection facility. These records share in common the  DiSSCo record-level schema defined in the linked file.",
                        "$ref": "*<link to record-level file location>*",
			"properties": {
			},
                        "title": "A single schema shared by all registry records"
                   },
                    "minItems": 0,
                    "uniqueItems": true,
                    "title": "The list of DiSSCo collection facility records stored within the registry"
                },
                "ltc:hasRecordLevel": {

                    [...]

                },
                "ltc:hasReference": {

                    [...]

                }
            },
            "title": "Overall structure at the registry-level"
        }
    }
}
```



### ltc:hasRecordLevel module at the registry-level 

The `ltc:hasRecordLevel` properties keyword follows the structure of its two fellow subschemata within the main `Registry` module. It has as its value an array. However, this array is constrained to only contain a single item (see `"minItems": 1` and `"maxItems": 1`). It could be defined as an entity of type `object`, too, and in that case directly refer to the definition of the subschema with `"$ref": "#/definitions/RecordLevelRegistry"`.

The subschema uses the `ltc:RecordLevel` class to set requirements that will support the reuse of the registry. `ltc:RecordLevel` requires registries, i.e. their JSON or JSON-LD data instances, to provide at least one identifier that uniquely identifies the registry, as well as a license defining the conditions for the reuse of the registry as a whole dataset. In addition to the standard, also information about the rights holder needs to be provided.

The `ltc:RecordLevel` class is also used at the record-level, within the subschema `RegistryRecord` of the linked record-level JSON Schema file. The differences in use at the registry- and record-levels are, first, that in contrast to the registry-level, at the record-level `ltc:rightsHolder` is not required. Second, at the registry-level the subschema `ltc:hasPersonRole` is constraint to only accept the preset names of the registry's administrators or record dataset's creators. The strings of these `ltc:adminFullNames` need to be set manually within the schema's source file before the schema or profile can be used. Therefore, the schema of the `ltc:RecordLevel` class is called using the keyword `RecordLevelRegistry`, since the names of persons associated with e.g. collections at the record-level might follow other conventions.

The subschemata required by the `ltc:hasRegistryRecord` module are added to the bottom of the `definitions` list. These are the subschemata `RecordLevelRegistry`, `RecordLevelRegistryPerson`, `adminFullName`, `ltc:Identifier` and `IdentifierSource`. The details of the schemata will be described at the record-level.


EXAMPLE CODE:  Defining the properties of the ltc:hasRecordLevel subschema

```json
{
    "$schema": "https://json-schema.org/draft/2020-12/schema",
    "$id": "https://raw.githubusercontent.com/jbstatgen/dissco_registry/main/LtCProfile_RegistryLevel_20230207.json?token=GHSAT0AAAAAAB6WZYLAAT7QUDYLKKKY74RAY7KJGDA",
    "title": "DiSSCo Registry Profile",
    "description": "JSON Schema- and Latimer Core-based profile describing a registry of collection facilities for the DiSSCo RI in a standardized way.",
    "$ref": "#/definitions/Registry",
    "definitions": {
        "Registry": {
            "type": "object",
            "additionalProperties": true,
            "required": [
                "RegistryRecords",
                "RecordLevel",
                "References"
            ],
            "properties": {
                "RegistryRecords": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "description": "Each item in the array is the record of a DiSSCo collection facility. These records share in common the  DiSSCo record-level schema defined in the linked file.",
                        "$ref": "https://raw.githubusercontent.com/jbstatgen/dissco_registry/main/LtCProfile_RecordLevel_20230207.json?token=GHSAT0AAAAAAB6WZYLAJZOUSQPX6K4MEDT4Y7KO26Q",
                        "properties": {
                        }
                        "title": "A single schema shared by all registry records"
                    },
                    "minItems": 0,
                    "uniqueItems": true,
                    "title": "The list of DiSSCo collection facility records stored within the registry"
                },
                "ltc:hasRecordLevel": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/RecordLevelRegistry"
                    },
                    "minItems": 1,
                    "maxItems": 1,
                    "uniqueItems": true,
                    "title": "(P)ID, license, rights holder & registry administrators"
                },
                "ltc:hasReference": {

                    [...]

                }
            },
            "title": "Overall structure at the registry-level"
        },
        "RecordLevelRegistry": {
            "$ref": "https://raw.githubusercontent.com/tdwg/cd/registry-schema-update/standard/json-schema/record-level.json",
            "type": "object",
            "additionalProperties": true,
            "required": [
                "ltc:hasIdentifier",
                "license",
                "rightsHolder"
            ],
            "properties": {
	        [...]
	    },
	    "title": "ltc:RecordLevel_Registry"
	    }
	},
	
        [...]
	
    }
}
```



### ltc:hasReference module at the registry-level

The third and final subschema directly at the top-level within the `Registry` schema is the `ltc:hasReference` subschema. The schema should provide a full citation for the DiSSCo Registry and potentially a link (IRI) to its dataset. Furthermore, it can be used to store information about a registry's homepage, logo and publications citing the registry. 

`ltc:hasReference` is of type `array` and the schema of its items is provided by the `LtcHasReference` subschema. `LtcHasReference` can be found at the end of list of modules within `definitions`.


---
> 
>  potentially different references might be defined as independent object for types of references, ie. homepage, logo, IRI, citation
> 
---


```json
{
    "$schema": "https://json-schema.org/draft/2020-12/schema",
    "$id": "https://raw.githubusercontent.com/jbstatgen/dissco_registry/main/LtCProfile_RegistryLevel_20230207.json?token=GHSAT0AAAAAAB6WZYLAAT7QUDYLKKKY74RAY7KJGDA",
    "title": "DiSSCo Registry Profile",
    "description": "JSON Schema- and Latimer Core-based profile describing a registry of collection facilities for the DiSSCo RI in a standardized way.",
    "$ref": "#/definitions/Registry",
    "definitions": {
        "Registry": {
            "type": "object",
            "additionalProperties": true,
            "required": [
                "RegistryRecords",
                "RecordLevel",
                "References"
            ],
            "properties": {
                "RegistryRecords": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "description": "Each item in the array is the record of a DiSSCo collection facility. These records share in common the  DiSSCo record-level schema defined in the linked file.",
                        "$ref": "https://raw.githubusercontent.com/jbstatgen/dissco_registry/main/LtCProfile_RecordLevel_20230207.json?token=GHSAT0AAAAAAB6WZYLAJZOUSQPX6K4MEDT4Y7KO26Q",
                        "properties": {
                        }
                        "title": "A single schema shared by all registry records"
                    },
                    "minItems": 0,
                    "uniqueItems": true,
                    "title": "The list of DiSSCo collection facility records stored within the registry"
                },
                "ltc:hasRecordLevel": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/RecordLevelRegistry"
                    },
                    "minItems": 1,
                    "maxItems": 1,
                    "uniqueItems": true,
                    "title": "(P)ID, license, & registry admin"
                },
                "ltc:hasReference": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/LtcHasReference"
                    },
                    "minItems": 1,
                    "uniqueItems": true,
                    "title": "eg registry citation, homepage, logo, IRI"
                }
            },
            "title": "Overall structure at the registry-level"
        },

        [...]

    }
}
```

The three subschemata `RegistryRecords`, `ltc:hasRecordLevel` and `ltc:hasReference` together with their required submodules, all situated within the main `Registry` schema conclude the definition of information required to describe a registry, here specifically the DiSSCo Registry, at the registry-level at this point of time. 




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


