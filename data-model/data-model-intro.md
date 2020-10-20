# Introduction to the openDS data model

Our design proposal (October 2020) for openDS aligns perfectly with the basic, three-axiom provenance model based on PROV entities (Entity, Activity, Agent) as outlined in the [final recommendations of the RDA/TDWG Attribution Metadata Working Group](http://dx.doi.org/10.15497/RDA00029) to support standardized metadata for attributing work and tracking provenance in the curation and maintenance of research collections.

> **<span style="color: red;">6th October 2020: Note that the content of this page is work-in-progress and therefore incomplete. It does not yet describe all aspects of the model as elaborated in various Powerpoint presentations over the past months.</span>**

We achieve this by defining a three-level class hierarchy comprised of:

1. **Primary (abstract) class** definitions matching the PROV/Attribution metadata and other surrounding object/data models necessary to give context to the openDS model;
2. **Secondary (concrete) class** definitions that are subclasses of the abstract classes and which are actually the main classes making up the practical openDS data model; and,
3. **Traits (extenders)** definitions that extend and further compose (or precise) the secondary classes to more specific subclasses associated with different kinds of specimen representation e.g., for botany, for zoology, for geology, etc.

For now, the class definitions for each of these levels are given below. As these become accepted and grow in size and complexity they will eventually be split out into separate pages. To help keep track of the class definitions and their development, an [openDS class index spreadsheet](https://docs.google.com/spreadsheets/d/1Tb3zZZWY-TY50nttg3Jj8T0S2ZhJaNQKftv-a4ywV1I/) is maintained for quick reference. This also helps with synchronisation and alignment with the [MIDS](https://github.com/tdwg/cd/tree/master/mids) and [CD](https://github.com/tdwg/cd) standards developments.

## Primary (abstract) class definitions

> | Primary (abstract) class | Description | Source<br> (linked IRI where applicable) |
> | --- | --- | --- |
> | Entity | An entity is a thing with some fixed aspects (properties) that is the subject of an activity. | [prov:Entity](http://www.w3.org/ns/prov#Entity) |
> | Activity | An activity is something that occurs over a period of time and acts upon or with entities. It may include consuming, processing, transforming, modifying, relocating, using, or generating entities. | [prov:Activity](http://www.w3.org/ns/prov#Activity) |
> | Agent | An agent is something that bears some form of responsibility for an activity taking place, for the existence of an entity, or for another agent's activity. | [prov:Agent](http://www.w3.org/ns/prov#Agent) |
> | Role | A role is the function of an entity or agent with respect to an activity, in the context of a usage, generation, invalidation, association, start, and end. | [prov:Role](http://www.w3.org/ns/prov#Role) |
> | Transaction | Transactions carried out in relation to a specimen. | ods:Transaction |
> | Derived data | Various third-parties’ data type derived from the physical specimen.  | ods:DerivedData |
> | Dimension | Elements that sub-divide a digital specimen in the openDS data model. <br>Note, compatible with CD | cd:Dimension |
> | Metric | Numeric attributes measuring the secondary objects within the data model. Used for counting, reporting and other purposes. <br> Note, compatible with CD | cd:Metric |

Figure 1, reproduced from the [final recommendations of the RDA/TDWG Attribution Metadata Working Group](http://dx.doi.org/10.15497/RDA00029) illustrates the PROV/Attribution model with its three principal PROV classes (entity, activity, agent) that form the foundation of openDS. The figure also illustrates additional classes added for proper tracking and attribution of work carried. 

![figure: attribution model concept](/images/attributionmodel.png)

**Figure 1: RDA PROV/Attribution metadata model**

Figure 2 illustrates how the principal object classes relate to one another in a high-level object model concept.

![figure: high-level object model concept](/images/modelconcept.png)

**Figure 2: High-level object model concept**

Using two examples (yellow and green), Figure 3 illustrates how the secondary (concrete) classes are instances of a specific primary (abstract) classes. Figure 1 also illustrates how a specific concrete class, such as `DigitalSpecimen` and `ObjectClassification` can be extended with traits that make the object instance more precise for specific circumstances. 

![figure: secondary classes are instances of primary classes and traits extend secondary classes](/images/classhierarchy.png)

**Figure 3: Seconday (concrete) classes as instances of primary (abstract) classes, with trait extenders**

## Secondary (concrete) class definitions

Just a few examples at present:
- DigitalSpecimen - is an example (subclass) of an Entity.
- Loan and Visit - are examples (subclasses) of a Transaction.
- Annotation and Intepretation - are examples (subclasses) of a Transaction.
- GeographicOrigin - is an example (subclass) of a Dimension.
- GeologicalTimeRange - is an example (subclass) of a Dimension.
- ObjectClassification - is an example (subclass) of a Dimension but it will vary, depending on the Trait that extends it e.g., botanical classification, mineral classification, etc.

To be completed - take from @wouteraddink document on DiSSCo data types

### Classes with parent class Entity

> | Secondary (concrete) class | Description | Source<br> (linked IRI where applicable) |
> | --- | --- | --- |
> | DigitalSpecimen |  |  |
> | Loan |  |  |
> | Visit |  |  |
> | Annotation |  |  |
> | Interpretation |  |  |

### Classes with parent class Dimension

> | Secondary (concrete) class | Description | Source<br> (linked IRI where applicable) |
> | --- | --- | --- |
> | GeographicOrigin |  |  |
> | GeologicalTimeRange |  |  |
> | ObjectClassification |  |  |

## Traits (extenders) definitions and their use

To be completed.
== sub-types as suggested by @wouteraddink

> | Traits (extenders) | Description | Source<br> (linked IRI where applicable) |
> | --- | --- | --- |
> |  |  |  |



END.