---
# Basic json - example 3
---

## Introduction
Continuing from [example 2](basic-json-example2.md), let's take a [real example from NHMUK](https://data.nhm.ac.uk/object/893e0b8c-9dab-40b5-872b-51f08a69e765/1620691200000) and see what we can do to change that into a Digital Specimen object with semantics. 

## Example 3: NHMUK010517563, *Elophila nymphaeata* (Linnaeus, 1758)

We begin from [its JSON-LD](https://data.nhm.ac.uk/object/893e0b8c-9dab-40b5-872b-51f08a69e765.jsonld) representation, which I've pasted here.

<details>
 <summary>Click to see the pasted JSON-LD.</summary>

``` json
{
  "@context": {
    "aiiso": "http://purl.org/vocab/aiiso/schema#",
    "cc": "http://creativecommons.org/ns#",
    "dc": "http://purl.org/dc/terms/",
    "dwc": "http://rs.tdwg.org/dwc/terms/",
    "foaf": "http://xmlns.com/foaf/0.1/",
    "owl": "http://www.w3.org/2002/07/owl#",
    "rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "void": "http://rdfs.org/ns/void#",
    "xsd": "http://www.w3.org/2001/XMLSchema#"
  },
  "@graph": [
    {
          "@id": "https://data.nhm.ac.uk/object/893e0b8c-9dab-40b5-872b-51f08a69e765.jsonld",
          "dc:created": {
            "@type": "xsd:dateTime",
            "@value": "2021-05-11T11:47:31.672203"
          },
          "dc:creator": "Natural History Museum, London",
          "dc:subject": {
            "@id": "https://data.nhm.ac.uk/object/893e0b8c-9dab-40b5-872b-51f08a69e765"
          }
    },
    {
          "@id": "https://www.nhm.ac.uk/services/media-store/asset/5bb2274d436ebab560cb85b83ba21d89fa8bc065/contents/preview",
          "@type": "foaf:Image",
          "cc:license": {
            "@id": "http://creativecommons.org/licenses/by/4.0/"
          },
          "dc:Format": "image/jpeg",
          "dc:RightsStatement": "The Trustees of the Natural History Museum, London",
          "dc:title": "010517563_136914_1083460",
          "foaf:depicts": {
            "@id": "https://data.nhm.ac.uk/object/893e0b8c-9dab-40b5-872b-51f08a69e765"
          },
          "foaf:thumbnail": {
            "@id": "https://www.nhm.ac.uk/services/media-store/asset/5bb2274d436ebab560cb85b83ba21d89fa8bc065/contents/thumbnail"
          }
    },
    {
          "@id": "https://data.nhm.ac.uk/object/893e0b8c-9dab-40b5-872b-51f08a69e765",
          "aiiso:Department": "Entomology",
          "aiiso:Division": "Lepidoptera",
          "dc:created": {
            "@type": "xsd:dateTime",
            "@value": "2019-07-24T09:24:28"
          },
          "dc:identifier": "893e0b8c-9dab-40b5-872b-51f08a69e765",
          "dc:publisher": {
            "@id": "https://nhm.ac.uk"
          },
          "dc:title": "Elophila nymphaeata (Linnaeus, 1758)",
          "dc:type": "Specimen",
          "dwc:associatedMedia": "https://www.nhm.ac.uk/services/media-store/asset/5bb2274d436ebab560cb85b83ba21d89fa8bc065/contents/preview",
          "dwc:basisOfRecord": "PreservedSpecimen",
          "dwc:catalogNumber": "NHMUK010517563",
          "dwc:class": "Insecta",
          "dwc:collectionCode": "BMNH(E)",
          "dwc:dynamicProperties": "{\"barcode\": \"010517563\", \"preservative\": \"Dry - pinned\", \"subDepartment\": \"Lepidoptera\", \"determinationNames\": \"Elophila nymphaeata (Linnaeus, 1758)\", \"project\": \"iCollections - British and Irish Pyraloidea\", \"associatedMediaCount\": 1}",
          "dwc:family": "Crambidae",
          "dwc:genus": "Elophila",
          "dwc:higherClassification": "Insecta; Lepidoptera; Pyraloidea; Crambidae; Acentropinae",
          "dwc:individualCount": "1",
          "dwc:institutionCode": "NHMUK",
          "dwc:modified": {
            "@type": "xsd:dateTime",
            "@value": "2021-01-30T23:50:56"
          },
          "dwc:occurrenceID": "893e0b8c-9dab-40b5-872b-51f08a69e765",
          "dwc:occurrenceStatus": "present",
          "dwc:order": "Lepidoptera",
          "dwc:otherCatalogNumbers": "NHMUK:ecatalogue:8966212",
          "dwc:scientificName": "Elophila nymphaeata (Linnaeus, 1758)",
          "dwc:scientificNameAuthorship": "(Linnaeus, 1758)",
          "dwc:specificEpithet": "nymphaeata",
          "foaf:depiction": {
            "@id": "https://www.nhm.ac.uk/services/media-store/asset/5bb2274d436ebab560cb85b83ba21d89fa8bc065/contents/preview"
          },
          "owl:sameAs": {
            "@id": "https://data.nhm.ac.uk/object/893e0b8c-9dab-40b5-872b-51f08a69e765/1620691200000"
          },
          "owl:versionInfo": 1620691200000,
          "void:inDataset": {
            "@id": "https://data.nhm.ac.uk/dataset/56e711e6-c847-4f99-915a-6894bb5c5dea#dataset"
          }
    }
  ]
}

```

</details>

### Step 1: Basic ODS, as per example 1.
First, let's make an object that's equivalent to the simple example 1 object.

This will store in nsidr.org with the type schema specified by the `typeName`. You can find it by searching nsidr.org directly, or by resolving the `id` value using, for example the https://doi.org resolver.

<details>
  <summary>Click to see JSON for example 3</summary>

```json
{
  "id": "20.5000.1025/ae88bb3a666ec72dbc51",
  "typeName": "ODStype1802",
  "authoritative": {
    "modified": "2021-06-17T09:18:02.130Z",
    "midsLevel": 1,
    "physicalSpecimenId": "NHMUK010517563",
    "institution": [
      "NHMUK",
      "https://ror.org/039zvsn29"
    ],
    "materialType": "Dry - pinned",
    "name": "Elophila nymphaeata (Linnaeus, 1758)"
  }
}
```
</details>

### Step 2: Basic semantic ODS
Let's turn this object into a semantically meaningful ODS by adding JSON-LD `@context`, `@graph` and `@id` elements.

<details>
  <summary>Click to see JSON for the basic semantic ODS.</summary>
 
```json
{
  "id": "20.5000.1025/ae88bb3a666ec72dbc52",
  "typeName": "ODStype1802",
  "@context": {
    "ods": "http://github.com/hardistyar/openDS/terms/"
  },
  "@graph" : [
    {
      "@id" : "https://doi.org/20.5000.1025/ae88bb3a666ec72dbc52",
      "ods:authoritative": {
        "ods:modified": "2021-06-17T09:18:02.130Z",
        "ods:midsLevel": 1,
        "ods:physicalSpecimenId": "NHMUK010517563",
        "ods:institution": [
          "NHMUK",
          "https://ror.org/039zvsn29"
        ],
        "ods:materialType": "Dry - pinned",
        "ods:name": "Elophila nymphaeata (Linnaeus, 1758)"
      }
    }
  ]
}
```

</details>

This is valid JSON-LD and it saves in nsidr.org as a valid object of type ODStype1802. I've given it a slightly different Handle suffix to distinguish it from the previous object. Notice several things:

- The JSON-LD `@id` node identifier is derived from and matches the object `id`, making this object machine-readable by Semantic Web tools. Note that by using a URI that points to a proxy for a Handle resolver, we've introduced a level of indirection that removes the location dependence typically associated with URIs. We know that we can always find this object via its `id` and a resolver of our choice. We could have pointed to the actual resource at the place where it is located (stored) by setting the `@id` node identifier to the URL https://nsidr.org/#objects/20.5000.1025/ae88bb3a666ec72dbc52.
- This object isn't semantically useful yet because the ods: terms referenced by the `@context` node are not defined anywhere. The IRI is just a placeholder. However, what we have achieved is to embed semantic assertions into a digital object. (Note: Whether or not this DO is a FAIR DO is still an open question. We need to check the extent to which it meets the requirements of the draft FDO Core Specification / FDO Framework).
- In nsidr.org, apart from the `modified` field which is autogenerated by Cordra anyway, none of the fields the type schema expects are filled . It doesn't recognise what I've given as corresponding to the schema but at the moment we're not prohibiting nsidr from storing any valid JSON. This means we need a new schema (type) for this object if we want to control its content with `required` properties.

### Step 3: Autogenerate a JSON schema
Let's now autogenerate a JSON schema to validate the object we have.

First question is which version of the JSON Schema standard do we want to work with? We don't think Cordra is fully up to date with recent specification drafts, being dependent on the V4 library.

This schema is autogenerated at https://www.jsonschema.net/home. It includes our complete example object at the beginning, as well as providing parts of that example all the way through. It provides `description` elements allowing us to be clear and specific about what each property is, and `default` elements allowing us to set default values to be used when no value is provided during object creation.

<details>
  <summary>Click to see the auto-generated JSON schema.</summary>

```json
{
    "$schema": "http://json-schema.org/draft-07/schema",
    "$id": "http://example.com/example.json",
    "type": "object",
    "title": "The root schema",
    "description": "The root schema comprises the entire JSON document.",
    "default": {},
    "examples": [
        {
            "id": "20.5000.1025/ae88bb3a666ec72dbc52",
            "typeName": "ODStype1802",
            "@context": {
                "ods": "http://github.com/hardistyar/openDS/terms/"
            },
            "@graph": [
                {
                    "@id": "https://doi.org/20.5000.1025/ae88bb3a666ec72dbc52",
                    "ods:authoritative": {
                        "ods:modified": "2021-06-17T09:18:02.130Z",
                        "ods:midsLevel": 1,
                        "ods:physicalSpecimenId": "NHMUK010517563",
                        "ods:institution": [
                            "NHMUK",
                            "https://ror.org/039zvsn29"
                        ],
                        "ods:materialType": "Dry - pinned",
                        "ods:name": "Elophila nymphaeata (Linnaeus, 1758)"
                    }
                }
            ]
        }
    ],
    "required": [
        "id",
        "typeName",
        "@context",
        "@graph"
    ],
    "properties": {
        "id": {
            "$id": "#/properties/id",
            "type": "string",
            "title": "The id schema",
            "description": "An explanation about the purpose of this instance.",
            "default": "",
            "examples": [
                "20.5000.1025/ae88bb3a666ec72dbc52"
            ]
        },
        "typeName": {
            "$id": "#/properties/typeName",
            "type": "string",
            "title": "The typeName schema",
            "description": "An explanation about the purpose of this instance.",
            "default": "",
            "examples": [
                "ODStype1802"
            ]
        },
        "@context": {
            "$id": "#/properties/%40context",
            "type": "object",
            "title": "The @context schema",
            "description": "An explanation about the purpose of this instance.",
            "default": {},
            "examples": [
                {
                    "ods": "http://github.com/hardistyar/openDS/terms/"
                }
            ],
            "required": [
                "ods"
            ],
            "properties": {
                "ods": {
                    "$id": "#/properties/%40context/properties/ods",
                    "type": "string",
                    "title": "The ods schema",
                    "description": "An explanation about the purpose of this instance.",
                    "default": "",
                    "examples": [
                        "http://github.com/hardistyar/openDS/terms/"
                    ]
                }
            },
            "additionalProperties": true
        },
        "@graph": {
            "$id": "#/properties/%40graph",
            "type": "array",
            "title": "The @graph schema",
            "description": "An explanation about the purpose of this instance.",
            "default": [],
            "examples": [
                [
                    {
                        "@id": "https://doi.org/20.5000.1025/ae88bb3a666ec72dbc52",
                        "ods:authoritative": {
                            "ods:modified": "2021-06-17T09:18:02.130Z",
                            "ods:midsLevel": 1,
                            "ods:physicalSpecimenId": "NHMUK010517563",
                            "ods:institution": [
                                "NHMUK",
                                "https://ror.org/039zvsn29"
                            ],
                            "ods:materialType": "Dry - pinned",
                            "ods:name": "Elophila nymphaeata (Linnaeus, 1758)"
                        }
                    }
                ]
            ],
            "additionalItems": true,
            "items": {
                "$id": "#/properties/%40graph/items",
                "anyOf": [
                    {
                        "$id": "#/properties/%40graph/items/anyOf/0",
                        "type": "object",
                        "title": "The first anyOf schema",
                        "description": "An explanation about the purpose of this instance.",
                        "default": {},
                        "examples": [
                            {
                                "@id": "https://doi.org/20.5000.1025/ae88bb3a666ec72dbc52",
                                "ods:authoritative": {
                                    "ods:modified": "2021-06-17T09:18:02.130Z",
                                    "ods:midsLevel": 1,
                                    "ods:physicalSpecimenId": "NHMUK010517563",
                                    "ods:institution": [
                                        "NHMUK",
                                        "https://ror.org/039zvsn29"
                                    ],
                                    "ods:materialType": "Dry - pinned",
                                    "ods:name": "Elophila nymphaeata (Linnaeus, 1758)"
                                }
                            }
                        ],
                        "required": [
                            "@id",
                            "ods:authoritative"
                        ],
                        "properties": {
                            "@id": {
                                "$id": "#/properties/%40graph/items/anyOf/0/properties/%40id",
                                "type": "string",
                                "title": "The @id schema",
                                "description": "An explanation about the purpose of this instance.",
                                "default": "",
                                "examples": [
                                    "https://doi.org/20.5000.1025/ae88bb3a666ec72dbc52"
                                ]
                            },
                            "ods:authoritative": {
                                "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative",
                                "type": "object",
                                "title": "The ods:authoritative schema",
                                "description": "An explanation about the purpose of this instance.",
                                "default": {},
                                "examples": [
                                    {
                                        "ods:modified": "2021-06-17T09:18:02.130Z",
                                        "ods:midsLevel": 1,
                                        "ods:physicalSpecimenId": "NHMUK010517563",
                                        "ods:institution": [
                                            "NHMUK",
                                            "https://ror.org/039zvsn29"
                                        ],
                                        "ods:materialType": "Dry - pinned",
                                        "ods:name": "Elophila nymphaeata (Linnaeus, 1758)"
                                    }
                                ],
                                "required": [
                                    "ods:modified",
                                    "ods:midsLevel",
                                    "ods:physicalSpecimenId",
                                    "ods:institution",
                                    "ods:materialType",
                                    "ods:name"
                                ],
                                "properties": {
                                    "ods:modified": {
                                        "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative/properties/ods%3Amodified",
                                        "type": "string",
                                        "title": "The ods:modified schema",
                                        "description": "An explanation about the purpose of this instance.",
                                        "default": "",
                                        "examples": [
                                            "2021-06-17T09:18:02.130Z"
                                        ]
                                    },
                                    "ods:midsLevel": {
                                        "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative/properties/ods%3AmidsLevel",
                                        "type": "integer",
                                        "title": "The ods:midsLevel schema",
                                        "description": "An explanation about the purpose of this instance.",
                                        "default": 0,
                                        "examples": [
                                            1
                                        ]
                                    },
                                    "ods:physicalSpecimenId": {
                                        "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative/properties/ods%3AphysicalSpecimenId",
                                        "type": "string",
                                        "title": "The ods:physicalSpecimenId schema",
                                        "description": "An explanation about the purpose of this instance.",
                                        "default": "",
                                        "examples": [
                                            "NHMUK010517563"
                                        ]
                                    },
                                    "ods:institution": {
                                        "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative/properties/ods%3Ainstitution",
                                        "type": "array",
                                        "title": "The ods:institution schema",
                                        "description": "An explanation about the purpose of this instance.",
                                        "default": [],
                                        "examples": [
                                            [
                                                "NHMUK",
                                                "https://ror.org/039zvsn29"
                                            ]
                                        ],
                                        "additionalItems": true,
                                        "items": {
                                            "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative/properties/ods%3Ainstitution/items",
                                            "anyOf": [
                                                {
                                                    "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative/properties/ods%3Ainstitution/items/anyOf/0",
                                                    "type": "string",
                                                    "title": "The first anyOf schema",
                                                    "description": "An explanation about the purpose of this instance.",
                                                    "default": "",
                                                    "examples": [
                                                        "NHMUK",
                                                        "https://ror.org/039zvsn29"
                                                    ]
                                                }
                                            ]
                                        }
                                    },
                                    "ods:materialType": {
                                        "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative/properties/ods%3AmaterialType",
                                        "type": "string",
                                        "title": "The ods:materialType schema",
                                        "description": "An explanation about the purpose of this instance.",
                                        "default": "",
                                        "examples": [
                                            "Dry - pinned"
                                        ]
                                    },
                                    "ods:name": {
                                        "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative/properties/ods%3Aname",
                                        "type": "string",
                                        "title": "The ods:name schema",
                                        "description": "An explanation about the purpose of this instance.",
                                        "default": "",
                                        "examples": [
                                            "Elophila nymphaeata (Linnaeus, 1758)"
                                        ]
                                    }
                                },
                                "additionalProperties": true
                            }
                        },
                        "additionalProperties": true
                    }
                ]
            }
        }
    },
    "additionalProperties": true
}
```

</details>

### Step 4: Optimise the schema to an ODStype schema
The next step is to take the autogenerated schema above and optimise it to the needs of openDS. At the very least, this involves renaming the schema and putting it into version control, which is what we do in this example. But there is probably more to it than that; to be further investigated.

The changes we need to make are the following:

1. The identifier of the schema, `$id` must be given a suitable URI so that it can be found. We change this to point to a location in the GitHub repository for openDS where this schema can be found.
   - `"$id": "https://github.com/DiSSCo/openDS/json-examples-and-schemas/digital-specimen-object/example3-opends-schema.json",`
2. The `title` of the schema must be changed to reflect the object `typeName` that this schema applies to. At this point, it's appropriate to allocate a new `typeName` as well, so we'll set that to "ODStype1804".
   - change: `"title": "The root schema",` to `"title": "root openDS schema for ODStype1804",`.
   - In the `"examples"` array, change: `"typeName": "ODStype1802",` to `"typeName": "ODStype1804",`.
3. In the `"properties"` node, make the following changes:
   - change example for `"typeName"` to ODSType1804, to match the earlier changes.
   - replace the `"description"` of the purpose of each instance with something appropriate. (*17 June 2021: note that at this experimental stage I haven't provided any new description of the purposes of each instance. These can be added later when we've stabilised the design better. And here is where the needed changes should be listed.*).
   - for `"ods:midsLevel"`, set maximum and minimum permitted values by including `"minimum": 0, "maximum": 3,` before the `"default": 0,` key.
4. For `"typeName"`, replace `"default": "",` with `"enum": [ "ODStype1804" ]` as the only permitted value for this object type definition.

Change `title` for `ods:physicalSpecimenId` from `"title": "The ods:physicalSpecimenId schema",` to `"title": "Physical specimen identifier",`.

Change `title` for `ods:institution` from `"title": "The ods:institution schema",` to `"title": "Code (GRSciColl)",`.

*17 June 2021: Got to here>>: At line 710: need to do some more work there to get the referent in - is missing and needs `"title": "Referent",`. See schema at end, taken from Cordra.*

<details>
  <summary>Click to see JSON for the ODStype schema in JSON.</summary>

```json

{
    "$schema": "http://json-schema.org/draft-07/schema",
    "$id": "https://github.com/DiSSCo/openDS/json-examples-and-schemas/digital-specimen-object/example3-opends-schema.json",
    "type": "object",
    "title": "root openDS schema for ODStype1804",
    "description": "The root schema comprises the entire JSON document.",
    "default": {},
    "examples": [
        {
            "id": "20.5000.1025/ae88bb3a666ec72dbc52",
            "typeName": "ODStype1804",
            "@context": {
                "ods": "http://github.com/hardistyar/openDS/terms/"
            },
            "@graph": [
                {
                    "@id": "https://doi.org/20.5000.1025/ae88bb3a666ec72dbc52",
                    "ods:authoritative": {
                        "ods:modified": "2021-06-17T09:18:02.130Z",
                        "ods:midsLevel": 1,
                        "ods:physicalSpecimenId": "NHMUK010517563",
                        "ods:institution": [
                            "NHMUK",
                            "https://ror.org/039zvsn29"
                        ],
                        "ods:materialType": "Dry - pinned",
                        "ods:name": "Elophila nymphaeata (Linnaeus, 1758)"
                    }
                }
            ]
        }
    ],
    "required": [
        "id",
        "typeName",
        "@context",
        "@graph"
    ],
    "properties": {
        "id": {
            "$id": "#/properties/id",
            "type": "string",
            "title": "The id schema",
            "description": "An explanation about the purpose of this instance.",
            "default": "",
            "examples": [
                "20.5000.1025/ae88bb3a666ec72dbc52"
            ]
        },
        "typeName": {
            "$id": "#/properties/typeName",
            "type": "string",
            "title": "The typeName schema",
            "description": "An explanation about the purpose of this instance.",
            "enum": [
              "ODStype1804"
            ],
            "examples": [
                "ODStype1804"
            ]
        },
        "@context": {
            "$id": "#/properties/%40context",
            "type": "object",
            "title": "The @context schema",
            "description": "An explanation about the purpose of this instance.",
            "default": {},
            "examples": [
                {
                    "ods": "http://github.com/hardistyar/openDS/terms/"
                }
            ],
            "required": [
                "ods"
            ],
            "properties": {
                "ods": {
                    "$id": "#/properties/%40context/properties/ods",
                    "type": "string",
                    "title": "The ods schema",
                    "description": "An explanation about the purpose of this instance.",
                    "default": "",
                    "examples": [
                        "http://github.com/hardistyar/openDS/terms/"
                    ]
                }
            },
            "additionalProperties": true
        },
        "@graph": {
            "$id": "#/properties/%40graph",
            "type": "array",
            "title": "The @graph schema",
            "description": "An explanation about the purpose of this instance.",
            "default": [],
            "examples": [
                [
                    {
                        "@id": "https://doi.org/20.5000.1025/ae88bb3a666ec72dbc52",
                        "ods:authoritative": {
                            "ods:modified": "2021-06-17T09:18:02.130Z",
                            "ods:midsLevel": 1,
                            "ods:physicalSpecimenId": "NHMUK010517563",
                            "ods:institution": [
                                "NHMUK",
                                "https://ror.org/039zvsn29"
                            ],
                            "ods:materialType": "Dry - pinned",
                            "ods:name": "Elophila nymphaeata (Linnaeus, 1758)"
                        }
                    }
                ]
            ],
            "additionalItems": true,
            "items": {
                "$id": "#/properties/%40graph/items",
                "anyOf": [
                    {
                        "$id": "#/properties/%40graph/items/anyOf/0",
                        "type": "object",
                        "title": "The first anyOf schema",
                        "description": "An explanation about the purpose of this instance.",
                        "default": {},
                        "examples": [
                            {
                                "@id": "https://doi.org/20.5000.1025/ae88bb3a666ec72dbc52",
                                "ods:authoritative": {
                                    "ods:modified": "2021-06-17T09:18:02.130Z",
                                    "ods:midsLevel": 1,
                                    "ods:physicalSpecimenId": "NHMUK010517563",
                                    "ods:institution": [
                                        "NHMUK",
                                        "https://ror.org/039zvsn29"
                                    ],
                                    "ods:materialType": "Dry - pinned",
                                    "ods:name": "Elophila nymphaeata (Linnaeus, 1758)"
                                }
                            }
                        ],
                        "required": [
                            "@id",
                            "ods:authoritative"
                        ],
                        "properties": {
                            "@id": {
                                "$id": "#/properties/%40graph/items/anyOf/0/properties/%40id",
                                "type": "string",
                                "title": "The @id schema",
                                "description": "An explanation about the purpose of this instance.",
                                "default": "",
                                "examples": [
                                    "https://doi.org/20.5000.1025/ae88bb3a666ec72dbc52"
                                ]
                            },
                            "ods:authoritative": {
                                "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative",
                                "type": "object",
                                "title": "The ods:authoritative schema",
                                "description": "An explanation about the purpose of this instance.",
                                "default": {},
                                "examples": [
                                    {
                                        "ods:modified": "2021-06-17T09:18:02.130Z",
                                        "ods:midsLevel": 1,
                                        "ods:physicalSpecimenId": "NHMUK010517563",
                                        "ods:institution": [
                                            "NHMUK",
                                            "https://ror.org/039zvsn29"
                                        ],
                                        "ods:materialType": "Dry - pinned",
                                        "ods:name": "Elophila nymphaeata (Linnaeus, 1758)"
                                    }
                                ],
                                "required": [
                                    "ods:modified",
                                    "ods:midsLevel",
                                    "ods:physicalSpecimenId",
                                    "ods:institution",
                                    "ods:materialType",
                                    "ods:name"
                                ],
                                "properties": {
                                    "ods:modified": {
                                        "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative/properties/ods%3Amodified",
                                        "type": "string",
                                        "title": "The ods:modified schema",
                                        "description": "An explanation about the purpose of this instance.",
                                        "default": "",
                                        "examples": [
                                            "2021-06-17T09:18:02.130Z"
                                        ]
                                    },
                                    "ods:midsLevel": {
                                        "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative/properties/ods%3AmidsLevel",
                                        "type": "integer",
                                        "title": "The ods:midsLevel schema",
                                        "description": "An explanation about the purpose of this instance.",
                                        "minimum": 0,
                                        "maximum": 3,
                                        "default": 0,
                                        "examples": [
                                            1
                                        ]
                                    },
                                    "ods:physicalSpecimenId": {
                                        "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative/properties/ods%3AphysicalSpecimenId",
                                        "type": "string",
                                        "title": "Physical specimen identifier",
                                        "description": "An explanation about the purpose of this instance.",
                                        "default": "",
                                        "examples": [
                                            "NHMUK010517563"
                                        ]
                                    },
                                    "ods:institution": {
                                        "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative/properties/ods%3Ainstitution",
                                        "type": "array",
                                        "title": "Code (GRSciColl)",
                                        "description": "An explanation about the purpose of this instance.",
                                        "default": [],
                                        "examples": [
                                            [
                                                "NHMUK",
                                                "https://ror.org/039zvsn29"
                                            ]
                                        ],
                                        "additionalItems": true,
                                        "items": {
                                            "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative/properties/ods%3Ainstitution/items",
                                            "anyOf": [
                                                {
                                                    "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative/properties/ods%3Ainstitution/items/anyOf/0",
                                                    "type": "string",
                                                    "title": "The first anyOf schema",
                                                    "description": "An explanation about the purpose of this instance.",
                                                    "default": "",
                                                    "examples": [
                                                        "NHMUK",
                                                        "https://ror.org/039zvsn29"
                                                    ]
                                                }
                                            ]
                                        }
                                    },
                                    "ods:materialType": {
                                        "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative/properties/ods%3AmaterialType",
                                        "type": "string",
                                        "title": "The ods:materialType schema",
                                        "description": "An explanation about the purpose of this instance.",
                                        "default": "",
                                        "examples": [
                                            "Dry - pinned"
                                        ]
                                    },
                                    "ods:name": {
                                        "$id": "#/properties/%40graph/items/anyOf/0/properties/ods%3Aauthoritative/properties/ods%3Aname",
                                        "type": "string",
                                        "title": "The ods:name schema",
                                        "description": "An explanation about the purpose of this instance.",
                                        "default": "",
                                        "examples": [
                                            "Elophila nymphaeata (Linnaeus, 1758)"
                                        ]
                                    }
                                },
                                "additionalProperties": true
                            }
                        },
                        "additionalProperties": true
                    }
                ]
            }
        }
    },
    "additionalProperties": true
}

```


</details>

### Step 5: Further optimise to a CORDRA schema
Next, we further optimise the openDS schema to become a CORDRA (or other object server) internal schema that we can use to store our example object against in nsidr.org. A record of these optimisations must also be kept.

The changes we need to make are the following:

1. The ...





<details>
  <summary>Click to see JSON for the CORDRA schema in JSON.</summary>

```json


```

</details>

### Step 6: Derive and register type definitions into type registry
Finally, we would need to derive and register type definitions into a type registry such as the [ePIC experimental type registry](http://dtr-test.pidconsortium.eu/#) but we don't go that far with this example.

---

## Relevant files for this example

- example3-plainjson-object.json
- example3-jsonld-object.json
- example3-auto-schema.json
- example3-opends-schema.json
- example3-cordra-schema.json

END.



{
  "definitions": {
    "previewInResultsTrue": {
      "cordra": {
        "preview": {
          "showInPreview": true
        }
      }
    },
    "previewInResultsFalse": {
      "cordra": {
        "preview": {
          "showInPreview": false
        }
      }
    }
  },
  "$schema": "http://json-schema.org/draft/2019-09/schema#",
  "$id": "https://nsidr.org/schemas/opendsschema.json",
  "type": "object",
  "title": "ODStype1802",
  "properties": {
    "id": {
      "type": "string",
      "cordra": {
        "type": {
          "autoGeneratedField": "handle",
          "prependHandleMintingConfigPrefix": true
        },
        "preview": {
          "showInPreview": true
        }
      }
    },
    "typeName": {
      "type": "string",
      "enum": [
        "ODStype1802"
      ]
    },
    "authoritative": {
      "$id": "#/properties/a_section",
      "type": "object",
      "properties": {
        "modified": {
          "type": "string",
          "cordra": {
            "type": {
              "autoGeneratedField": "modificationDate"
            }
          }
        },
        "midsLevel": {
          "type": "integer",
          "minimum": 0,
          "maximum": 3
        },
        "physicalSpecimenId": {
          "type": "string",
          "title": "Physical specimen identifier",
          "$ref": "#/definitions/previewInResultsFalse"
        },
        "institution": {
          "type": "array",
          "items": [
            {
              "type": "string",
              "title": "Code (GRSciColl)",
              "$ref": "#/definitions/previewInResultsTrue"
            },
            {
              "type": "string",
              "format": "uri",
              "title": "Referent",
              "$ref": "#/definitions/previewInResultsFalse"
            }
          ]
        },
        "materialType": {
          "type": "string",
          "title": "Material type",
          "$ref": "#/definitions/previewInResultsFalse"
        },
        "name": {
          "type": "string",
          "maxLength": 128,
          "title": "Name",
          "cordra": {
            "preview": {
              "showInPreview": true,
              "isPrimary": true
            }
          }
        }
      },
      "required": [
        "modified",
        "midsLevel",
        "physicalSpecimenId",
        "institution"
      ]
    }
  },
  "required": [
    "id",
    "typeName",
    "authoritative"
  ]
}

