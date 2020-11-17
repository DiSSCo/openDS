# openDS
The home of the specification for open Digital Specimens (openDS).

openDS is still very much in the early stage of development and this repository is where you can follow its progress.

## Getting started

To help you get started, we've provided answers to [frequently asked questions about Digital Specimens and openDS](faq/faq.md). You can also find there an explanation of [how openDS and the Extended Specimen Network are related](faq/faqcompare.md), as well as several other faq documents.

The openDS data model relates to other important structures, standards and initiatives in the wider world, as well as to information science in different domains of scientific discourse. [Positioning openDS in the landscape](positioning-opends.md) is one of the first and most important steps in development of the specification. Making sure that everyone likely to make use of the model agrees on this is essential to progress.

openDS consists of three principal and interrelated components, as follows:

- The openDS data model. Read the [introduction to the openDS data model](/data-model/data-model-intro.md);
- The Ontology for open Digital Specimens (ODS). Read the [introduction to the ODS ontology](/ods-ontology/ods-ont-intro.md); and,
- The openDS Application Programming Interface (API). Read the [introduction to the openDS API](api-spec/api-intro.md).

## Moving forward

Specification and agreement of openDS is an iterative, spiral process of continuous development (implementation) and improvement (specification) that can begin with the building of one or more 'Hello World' kind of demonstrators. One such example is the demonstrator at [nsidr.org](https://nsidr.org/) / [demo.nsidr.org](https://demo.nsidr.org/). Lessons can be learned from such implementations and fed into the specification process.

## How to become involved and contribute
The openDS initiative welcomes anyone who has a practical interest in Digital Specimens on the Internet and standards for exchanging and working with them. We're especially looking for individuals and organisations willing to become involved in implementation and to transfer the lessons learned in implementation into specification.

You can become involved and contribute by:

- Contacting the Technical Lead (see below) to become an active participant (listed below).
- Watching this github repository, and submitting or commenting on an issue.
- Using and evaluating the specification as it emerges and providing feedback e.g., by submitting an issue or suggesting a new need.

### Technical Lead

| Name | Affiliation | github name or Email |
| --- | --- | --- |
| Alex Hardisty | Cardiff University | @hardistyar |  

### Active participants

| Name | Affiliation | GitHub name or Email |  
| --- | --- | --- |  
| *name* | *affiliation* | *@GitHubname or Email* |  

## Repository structure
The directories in this repository are organised to keep the principal components of openDS (data model, ontology, API specification) separate from one another, and separate from other bits and pieces necessary for the specification work.

The diagram below illustrates the directory structure logically although in reality it appears alphabetically within the repository. At each directory level is a short explanations for orientation.

```
/openDS             <!-- introduction and material relevant to the specification as a whole -->
│   README.md
│   positioning-opends.md
|   serialization.md
|   use-cases.md
|   ... ...    
│
+---/api-spec       <!-- the api specification -->
|       api-intro.md
│       etc. ...
|
+---/data-model     <!-- the data model -->
│       data-model-intro.md
│       etc. ...
|
+---ods-ontology    <!-- the ontology -->
|       ods-ont-intro.md
|       etc. ...
│
+---/faqs           <!-- frequently asked questions and answers -->
│       faq.md
|       etc. ...
│
+---/images         <!-- images used throughout -->
|       etc. ...
|
+---/templates      <!-- markdown templates for definitions and issues -->
|       etc. ...
|
|

```

## Way of working

*To be completed.*

## Convergence and global participation

Linking third-party/extended specimen data together, as openDS proposes requires many stakeholders to adopt the standard. This is especially the case to integrate data at multiple levels: specimen, collection types, species, etc. and cross-discipline to geology, genomics, etc. Thus, an eventual standard needs global collaboration of all players in the landscape converging towards a single specification as far as possible. Fragmentation across countries is not helpful considering that collections-based science is global in nature and the actors practising it are spread worldwide.

The openDS initiative is open to global participation and supports movement towards a collaborative global process leading to a standard on a converged Digital Specimen (DS) / Extended Specimen (ES) concept; for example, under the umbrella of the [Alliance for Biodiversity Knowledge](https://www.biodiversityinformatics.org/). Such a process should have engagement from all stakeholders having interest in specimens/samples (not just biodiversity ones).

## Use cases

DS/ES and openDS must simultaneously simplify and answer the needs of all actors in the landscape – publishers, aggregators, relevant authority repositories and downstream users (consumers) of specimen data.

This page of [use cases](usecases.md) explains some of the scenarios of use envisaged for openDS.

## Resources

*To be added.*


END.

