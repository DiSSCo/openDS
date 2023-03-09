# DiSSCo Registry & Record Schemata


## Table of Contents

See also build-in drop-down menu on left-hand end of display header for file on GitHub.

* [Introduction](#introduction)
  * [Technical implementation as JSON Schema-based profiles](#technical-implementation-as-json-schema-based-profiles)
  * [Some JSON Schema defaults](#some-json-schema-defaults)
* [Defining the registry-level schema](#defining-the-registry-level-schema)
  * [Top-level registry module](#top-level-registry-module)
  * [hasRegistryRecord array](#hasregistryrecord-array)
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




