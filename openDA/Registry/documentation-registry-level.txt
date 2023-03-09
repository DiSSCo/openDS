


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

The overall structure of the registry is comparably simple and consists of one main module (`Registry`) and its three submodules (`hasRegistryRecord`, `ltc:hasRecordLevel` and `ltc:hasReference`). 


### Top-level registry module

The entry point into the structure of the registry schema is a JSON object or module called `Registry`. It is the only module that is accessed from the top-level by `"$ref": "#/definitions/Registry"`. The key `$ref` (as a form of `$id` at a lower level than the root level, see above) is used to identify the overall module or schema for the registry and provide a link to its location. The module itself and its definition is given within the present JSON Schema file as one of the modules listed within the `definitions` section. 

The identifier `"$ref": "#/definitions/Registry"` points to the `definitions` object in the present file and schema (`#`), and more specifically to the object `Registry` within `definitions`. The `Registry` module is of type `object`, which is further specified by its `properties`. Properties specify requirements that need to be fulfilled at the level of the object entity in which they are located, for the entity to successfully validate. At the registry-level, the `"properties": { }` key defines requirements that apply to the registry itself, that is, to the whole list of records as an entity. 

The three `properties` listed under the `properties` keyword are also `required`, that is they are listed as items in the array associated with the `required` keyword. The three properties are the submodules or subschemata `hasRegistryRecord`, `ltc:hasRecordLevel` and `ltc:hasReference`. The submodules themselves are defined in a linked JSON Schema file (cp. `hasRegistryRecord`) or as entities below the `Registry` object within `definitions`.

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
                "hasRegistryRecord",
                "RecordLevelRegistryArray",
                "References"
            ],
            "properties": {
                "hasRegistryRecord": {

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


### hasRegistryRecord array 

A registry represents a list, an array of records. Thus, the `hasRegistryRecord` property forms the core of the registry schema. Its type is an array of items, set with `"type": "array"`. In the case of the DiSSCo Registry, each ``"item"` within the array is the instance of a record describing a collection facility, that is, the record includes information about an organization and its institution-wide collection. 

The type of each `"item"` within the registry array is set to `"type": "object"`, since each record within the registry is itself a compound object (not a simple text string or number). Thus, each item within the array corresponds to a schema-object with several properties.

Since there is only one type (or schema) of `item` defined for the array, all JSON or JSON-LD instances that will be stored within the array will adhere to a single shared subschema. The format and information entered into each collection facility record within the registry will need to adhere to the defined schema. Only then will the record and, thus, the registry instance successfully validate. However, while all records in the registry need to have at least the structure of this subschema in common, each record can have additional elements that do not need to be present in other records. 

For the DiSSCo Registry to fulfill its purpose, all records or items within the hasRegistryRecord-array should be unique, no collection facility should be represented more than once. This ensures that the records cannot drift apart during subsequent updates and annotations. Such drift might lead to a situation, in which the digital representations of a collection facility over time, for example, potentially become associated with two different PIDs. In that case the erroneous impression might arise that two different and independent facilities are represented and exist. Thus, the requirement `"uniqueItems": true` is set.

During the validation of a JSON or JSON-LD encoded registry instance, validation of the `hasRegistryRecord` subschema and an instance of the module is successful if a list of arbitrary length is given, in which all list items are unique and, furthermore, fulfill the same (minimal) subschema. An empty array, that is, a registry without records will always be valid (see https://json-schema.org/understanding-json-schema/reference/array.html?highlight=uniqueitems).  

As already mentioned, the records (array items) within the registry have their own, record-level JSON schema. The key `$ref` again is used to identify this subschema, designed specifically for the registry's records. In this case, the `$ref` keyword provides a (preferably persistent, resolvable and globally unique) link to the storage location of an independent JSON Schema file that defines the subschema for the registry records and allows that information to be retrieved. This subschema for the record level will be defined in the next chapter. For the registry schema to validate as a whole, the `$ref` link needs to be resolvable, that is, at the location to which the link points, a file needs to exist and be accessible. Moreover, the JSON schema within the linked file is required to be valid, too.

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
                "hasRegistryRecord",
                "RecordLevelRegistryArray",
                "References"
            ],
            "properties": {
                "hasRegistryRecord": {
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

The `ltc:hasRecordLevel` property keyword follows the structure of its two fellow subschemata within the main `Registry` module. It has as its value an array. However, this array is constrained to only contain a single item (see `"minItems": 1` and `"maxItems": 1`). Alternatively, it could be defined as an entity of type `object`, too, and in that case directly refer to the definition of the subschema with `"$ref": "#/definitions/RecordLevelRegistry"`.

The subschema uses the `ltc:RecordLevel` class to set requirements that will support the reuse of the registry and provide the basis for recording of a provenance log. 

`ltc:RecordLevel` requires registries, i.e. their JSON or JSON-LD data instances, to provide at least one `ltc:Identifier` that uniquely identifies the registry, as well as a `ltc:license` defining the conditions for the reuse of the registry as a whole dataset. 

In addition to what is defined as mandatory by the Latimer Core (LtC) standard, the subschema `RecordLevelRegistry` derived from the `ltc:RecordLevel` class, requires moreover information about the `ltc:rightsHolder` for the registry in total. Furthermore it requires information about the administrators (`ltc:Person`) for the registry and their allowed `Roles` in maintaining and managing the registry. The information provided by `ltc:PersonRole` can enter DiSSCo's event-based transaction model that logs `prov:Activities` and thus provides a provenance record of changes, see the introduction to openDigitalEvents in this repository.

The `ltc:RecordLevel` class is also used at the record-level, within the linked record-level JSON Schema file (see the link in the subschema `hasRegistryRecord` above). The differences in use at the registry- and record-levels is that at the registry-level the subschema `ltc:hasPersonRole` is constraint to only accept the preset names of the registry's administrators or record dataset's creators. The strings of these `ltc:fullNameAdmins` need to be set manually within the schema's source file before the schema or profile can be used. Therefore, the general schema of the `ltc:RecordLevel` class is modified accordingly and called using the keyword `RecordLevelRegistry`. The names of persons associated with e.g. collections at the record-level might follow other conventions, so that at the record-level the general `ltc:RecordLevel` class will be specified as `RecordLevelRecord` subschema.

The subschemata required by the `ltc:hasRecordLevel` module are added to the bottom of the `definitions` list. These are the subschemata `RecordLevelRegistry`, `PersonRegistry`, `fullNameAdmin`, `ltc:Identifier` and `IdentifierSource`. The details of these schemata will be described at the record-level.


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
                "hasRegistryRecord",
                "RecordLevel",
                "References"
            ],
            "properties": {
                "hasRegistryRecord": {
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
                "hasRegistryRecord",
                "RecordLevel",
                "References"
            ],
            "properties": {
                "hasRegistryRecord": {
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

The three subschemata `hasRegistryRecord`, `ltc:hasRecordLevel` and `ltc:hasReference` together with their required submodules, all situated within the main `Registry` schema conclude the definition of information required to describe a registry, here specifically the DiSSCo Registry, at the registry-level at this point of time. 




