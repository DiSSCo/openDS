# Use cases for openDS 

This document describes some of the use cases foreseen as driving the specification work on openDS.

They are organised into those of interest from the point of view of being enabling for new modes of work and those more directly relevant to persons that will use specimens for science.

*This is what I've done initially - but the allocation of specific use cases to each of the two main categories is not yet correct. <span style="color:red">Needs changing.</span>*

## Use cases enabling for new modes of work

In this category we are thinking of the cases 1 - 4 shown in the following illustration.* 

![illustration of technical cases](/images/technical-cases.png)

### Use case T1: Transfer Digital Specimen data from one system to another

On request, one system (computer, software) transfers Digital Specimen data to another system (computer, software). Either across a network or within the same machine. 

### Use case T2: Allow operations to act on Digital Specimen remotely 

Machines or machine agents acting on behalf of humans can perform designated operations on a Digital Specimen located on a remote machine across a network.

### Use case T3: Package one or more Digital Specimens for preservation/download

Digital Speciment data (or a subset of it) can be packaged for preservation or download.

### Use case T4: Guide (but not constrain) the internal design of systems

The internal design of a system is guided by but not constrained by the specification of openDS and its requirements e.g., for object model, compliance, etc.

### Use case T5: Allow operations and people to change the Digital Specimen  

Machines and humans can perform operations on a Digital Specimen to enrich it with new data or to improve the quality of the data.


## Use cases for science

### Use case S1: Provide a universal way of discovery of specimens
open Digital Specimens aim to make specimens easily findable by providing specimen data FAIR. It should provide a universal mechanism for all specimens in Europe to make them discoverable: which specimens are there in Europe, where are they and how can they be accessed.

### Use case S2: Finding/accessing more information about specimens

open Digital Specimens provide opportunities for accessing more information about or related to natural science specimens (preserved plants, animals, fossils, rocks, minerals, etc.) with easier access leading to better workflows and better research. As a curated and authoritative digital twin for the physical specimen, a Digital Specimen with its package of links to other data could be a considerably more reliable and efficient information source than crawling potential databases manually for information about and derived from the physical specimen.

### Use case S3: Easier consumption/use of data and improved curation

Higher degrees of standardization, as epitomized by the openDS specification make it easier to consume and use data and improve curation. But such standardization but must accommodate multiple scenarios (e.g., preserved specimens, living specimens, jars of specimens, splitting of specimens, cases where there is no specimen but other objects like photos, illustrations, recordings, etc., and cases where the original specimen has been lost or destroyed). Not everything needs to be standardized but to benefit, you need something more standard for additional (supplementary) content.

### Use case S4: Support transformation of working practices

e.g., in moves towards more community-oriented curatorial practices for data about and derived from specimens.

*To be further elaborated.*

### Use case S5: Linking information from/to other (sub-)disciplines

Linking information makes taxonomic work easier and enables linkage of data and information from and to other disciplines. Community curation saves a lot of effort in making these links compared to the case where every collection must make all the (semantic) links on their own.

### Use case S6: Facilitate tracking of specimen use

Persistently identified open Digital Specimens in conjunction with third-party services can facilitate tracking of specimen use e.g., when mentioned in publications by means of its persistent identifier.

### Use case S7: Crediting work performed
Work performed in relation to a specimen, including gathering in the first place or deriving new data/information through analysis can be unambiguously attributed to the correct person(s) e.g., in conjunction with a researcher's ORCID iD. This can  provide incentives to create open Digital Specimens in the first place.

### Use case S8: Align specimen concepts and provide strong foundation across institutions

Digital Specimens can help to align specimen concepts and specimen metadata structure across institutions, as well as providing a strong foundation for attaching annotations/interpretations and records of loans and visits.

### Use case S9: A single virtual collection and many thematic collections

Handling specimens openly on the Internet offers opportunities for establishing a single virtual collection across multiple participating institutions (such as the European Collection Objects Index to be established by the DiSSCo research infrastructure) as well as the possibility to curate Digital Specimens in multiple thematic collections simultaneously - for example all specimens collected in Charles Darwin's HMS Beagle voyages. The latter is not easily achievable for physical objects. To turn the collections into one virtual collection a standardisation in describing the individual collections is needed. Thematic collections will help communities of scientists to work on them. a single virtual collection can also help in quantifying what is present in the collections, and where gaps and strengths are in Europe.

### Use case S10: Assess data suitability and/or reliability
Provenance data supplied with an open Digital Specimen can help to assess suitability and/or reliability of data for specific purposes. Available metadata can inform about possible usage restrictions and/or obligations associated with use (licenses, Nagoya protocol, etc.).

### Use case S11: Notification of change

Bringing changes in content to notice of researchers, educators and others without the need for them to actively look for that. A subscribe/notify capability (i.e., subscribe to a specimen of interest and be notified that its content has changed or that it’s been used in some way).

### Use case S12: Linking new taxonomic knowledge with type specimen collections data 

New scientific discovery will provide new insight about organisms and might lead to a new taxonomic classification. New names will generate new identifiers and data. As a curator for type specimens, where can I find the link to the previous and current names (pointing to two different types of specimens and identifiers), without going through the taxonomic literature? 

Some of the links and information about the type specimens are stored in local systems and published in aggregators. As a curator, how I can maintain these links to prevent link rot? 

Example scenario: 
*Chromis agilis* is a ray-finned fish species from the reef bass or damselfly family. It has a [fishbase id](https://www.fishbase.de/summary/5669),[WoRMS](http://www.marinespecies.org/aphia.php?p=taxdetails&id=212808) and [gbif occurrence id](https://www.gbif.org/occurrence/1230334143). GBIF has links to the CMS data at the The South African Institute for Aquatic Biodiversity (SAIAB). 

In 2020, a new species name assigned was assigned this fish. *Chromis agilis* now refers to the fish found in the Red and Indian sea. *Chromis pacifica* found in the Pacific Ocean. 

This new knowledge generated new sets of identifiers [http://www.marinespecies.org/aphia.php?p=taxdetails&id=145592](WoRMS) id.

And new data in another collections (Western Australia Museum). 

- How do we make all the links FAIR and machine-actionable? 
- How to prevent link rot? 
- Alert for change (in this case name change; also S10) 


### Use case S12: Documenting anthropogenic materials used for bird nests 

Anthropogenic materials such as foil, plastics, face masks, gloves and pieces of clothing are incorporated into nests of many birds and used by other animals. Researchers are interested in using specimens to understand the impact of such materials. Example studies: [A fish tale: a century of museum specimens reveal increasing microplastic concentrations in freshwater fish](https://doi.org/10.1002/eap.2320); [Plastic ingestion by marine fish in the wild](https://doi.org/10.1080/10643389.2019.1631990); [Use of anthropogenic-related nest material and nest parasite prevalence have increased over the past two centuries in Australian birds](https://doi.org/10.1007/s00442-021-04982-z). 
These studies describe not only the specimens but the properties of the materials found with the specimen such as type and description of the material (Polyethylene terephthalate), frequency of occurrence of plastic ingestion, plastic load, the amount of plastic per fish for example. There are also observational data submitted via various apps (https://www.covidlitter.com/) that has location and other observational details (such as entanglement, ingestion). 

We need structured data elements to capture these. We also need to describe the relationship between the bird nest and the eggs found. Example specimens from Naturalis: [bird nest of Turdus merula merula Linnaeus, 1758](https://bioportal.naturalis.nl/specimen/RMNH.AVES.175460.a), specimen id: RMNH.AVES.175460.a and [a clutch of 5 eggs](https://bioportal.naturalis.nl/specimen/RMNH.AVES.175460.b), specimen id: RMNH.AVES.175460.b. Bird eggs are also used for color analysis to study evolution and impact of pollution. The associated images could be useful for image processing for patter analysis. 

The following is an instance of a Digital Specimen of a bird nest specimen. There are two new data elements created for illustration:   *particleIdentification* or *particleDescription* to describe the water bottle found with the nest. 
	
		
```
{
  "id": "20.5000.1025/abcd",
  "type": "openDS",
  "content": {
    "id": "20.5000.1025/abcd",
    "typeName": "openDS",
    "authoritative": {
      "modified": "2020-06-10T09:18:02.130Z",
      "midsLevel": "1",
      "physicalSpecimenId": "https://data.biodiversitydata.nl/naturalis/specimen/RMNH.AVES.257939",
      "institution": [
        "Naturalis Biodiversity Center",
        "https://ror.org/0566bfb96"
      ],
      "objectType": "bird nest",
      "name": "Fulica atra Linnaeus, 1758"
    },
    "images": {
      "availableImages": [
        {
          "imageName": "hi-res",
          "source": "https://medialib.naturalis.nl/file/id/RMNH.AVES.257939_1/format/large",
          "license": "CC0 1.0"
        }
      ]
    },
    "particleIdentification": "plastic",
    "particleDescription": "plastic water bottle"
  }
}


END.
