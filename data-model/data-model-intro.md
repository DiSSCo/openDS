# Introduction to the openDS data model

Our design proposal (October 2020) for openDS aligns perfectly with the basic, three-axiom model based on PROV entities (Entity, Activity, Agent) as outlined in the [final recommendations of the RDA/TDWG Attribution Metadata Working Group](http://dx.doi.org/10.15497/RDA00029) to support standardized metadata for attributing work and tracking provenance in the curation and maintenance of research collections.

> **<span style="color: red;">6th October 2020: Note that the content of this page is work-in-progress and therefore incomplete. It does not yet describe all aspects of the model as elaborated in various Powerpoint presentations over the past months.</span>**

We achieve this by defining a three-level class hierarchy that is comprised of:

1. **Primary (abstract) class** definitions matching the PROV and other surrounding object/data models necessary to give context to the openDS model;
2. **Secondary (concrete) class** definitions that are subclasses of the abstract classes and which are actually the main classes making up the practical openDS data model; and,
3. **Traits** definitions that extend and further compose the secondary classes to more specific subclasses associated with different kinds of specimen representation.

## Primary (abstract) class definitions

> | Abstract class | Description | Source<br> (linked IRI where applicable) |
> | --- | --- | --- |
> | Entity | An entity is a thing with some fixed aspects (properties) that is the subject of an activity. | [prov:Entity](http://www.w3.org/ns/prov#Entity) |
> | Activity | An activity is something that occurs over a period of time and acts upon or with entities. It may include consuming, processing, transforming, modifying, relocating, using, or generating entities. | [prov:Activity](http://www.w3.org/ns/prov#Activity) |
> | Agent | An agent is something that bears some form of responsibility for an activity taking place, for the existence of an entity, or for another agent's activity. | [prov:Agent](http://www.w3.org/ns/prov#Agent) |
> | Role | A role is the function of an entity or agent with respect to an activity, in the context of a usage, generation, invalidation, association, start, and end. | [prov:Role](http://www.w3.org/ns/prov#Role) |
> | Transaction | Transactions carried out in relation to a specimen. | ods:Transaction |
> | Derived data | Various third-parties’ data type derived from the physical specimen.  | ods:DerivedData |
> | Dimension | Elements that sub-divide a digital specimen in the openDS data model. <br>Note, compatible with CD | cd:Dimension |
> | Metric | Numeric attributes measuring the secondary objects within the data model. Used for counting, reporting and other purposes. <br> Note, compatible with CD | cd:Metric |

*To do: insert an image that illustrates the model.*


## Secondary (concrete) class definitions

Just a few examples at present:
- Digital Specimen - is an example (subclass) of an Entity.
- Loan and Visit - are examples (subclasses) of a Transaction.
- Annotation and Intepretation - are examples (subclasses) of a Transaction.
- GeographicOrigin - is an example (subclass) of a Dimension.
- GeologicalTimeRange - is an example (subclass) of a Dimension.
- ObjectClassification - is an example (subclass) of a Dimension but it will vary, depending on the Trait that extends it e.g., botanical classification, mineral classification, etc.

To be completed - take from @wouteraddink document on DiSSCo data types

## Trait definitions and their use

To be completed.
== sub-types as suggested by @wouteraddink


END.