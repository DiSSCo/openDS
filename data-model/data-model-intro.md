# Introduction to the openDS data model <!-- omit in toc -->

> **<p style="color: red;">19th November 2020: This page is work-in-progress and therefore not yet complete and consistent. As yet, it doesn't describe all aspects as elaborated in Powerpoint presentations over the past months.</p>**
> **<p style="color: red;">The important point at this moment is to obtain consensus on the foundation model described here.</p>**

- [Class grouping](#class-grouping)
- [Abstract group class definitions](#abstract-group-class-definitions)
- [Digital Specimen (DS) group class definitions](#digital-specimen-ds-group-class-definitions)
  - [Classes with abstract parent class Entity](#classes-with-abstract-parent-class-entity)
  - [Classes with abstract parent class Dimension](#classes-with-abstract-parent-class-dimension)
- [Extender group class definitions](#extender-group-class-definitions)

## Class grouping
As explained in [positioning openDS in the landscape](/positioning-opends.md), our design proposal (November 2020) aligns perfectly with the basic, three-axiom attribution model based on PROV entities (Entity, Activity, Agent) as outlined in the RDA Recommendation on '[Attribution Metadata](http://dx.doi.org/10.15497/RDA00029)'. We extend from this by organising classes of the openDS object model into three groups in which we set the PROV model as the abstract group from which the concrete classes of the DS group inherit their principal characteristics. To account for the wide variation in specimen categories (plants, insects, rocks, etc.) and approaches to classification we use a group of extender classes or traits to make the concrete classes precise to specific situations. Thus, openDS defines three class groupings comprised of:

1. **Abstract group:** The primary class definitions match the PROV/Attribution metadata and other surrounding object/data models necessary to give context to the openDS model;
2. **Digital Specimen (DS) group:** The class definitions are subclasses of the abstract classes and are the main classes making up the practical openDS data model; and,
3. **Extender group:** The definitions that extend and further compose (or precise) the Digital Specimen (DS) group classes to more specific subclasses associated with different kinds of specimen representation e.g., for botany, for zoology, for geology, etc. In object modelling terms this level of definitions is sometimes referred to as traits that can be applied by mixing them into classes. A class in the DS group can mix in any number of traits from the extender group to make it more precise to the context in which it is instantiated.

For now, the class definitions for each of these groups are given below. As these become accepted and grow in size and complexity they will eventually be split out into separate pages. To help keep track of the class definitions and their development, an [openDS class index spreadsheet](https://docs.google.com/spreadsheets/d/1Tb3zZZWY-TY50nttg3Jj8T0S2ZhJaNQKftv-a4ywV1I/) is maintained for quick reference. This also helps with synchronisation and alignment with the [MIDS](https://github.com/tdwg/cd/tree/master/mids) and [CD](https://github.com/tdwg/cd) standards developments.

## Abstract group class definitions

> | Abstract group class | Description | Source<br> (linked IRI where applicable) |
> | --- | --- | --- |
> | Entity | An entity is a thing with some fixed aspects (properties) that is the subject of an activity. | [prov:Entity](http://www.w3.org/ns/prov#Entity) |
> | Activity | An activity is something that occurs over a period of time and acts upon or with entities. It may include consuming, processing, transforming, modifying, relocating, using, or generating entities. | [prov:Activity](http://www.w3.org/ns/prov#Activity) |
> | Agent | An agent is something that bears some form of responsibility for an activity taking place, for the existence of an entity, or for another agent's activity. | [prov:Agent](http://www.w3.org/ns/prov#Agent) |
> | Association | An activity association is an assignment of responsibility to an agent for an activity, indicating that the agent had a role in the activity. | [prov:Association](http://www.w3.org/ns/prov#Association) |
> | Role | A role is the function of an entity or agent with respect to an activity, in the context of a usage, generation, invalidation, association, start, and end. | [prov:Role](http://www.w3.org/ns/prov#Role) |
> | Transaction | Transactions carried out in relation to a specimen. | ods:Transaction |
> | Derived data | Various third-parties’ data type derived from the physical specimen.  | ods:DerivedData |
> | Dimension | Elements that sub-divide a digital specimen in the openDS data model. <br>Note, compatible with CD | cd:Dimension |
> | Metric | Numeric attributes measuring the secondary objects within the data model. Used for counting, reporting and other purposes. <br> Note, compatible with CD | cd:Metric |

Figure 1 illustrates the PROV/Attribution model with its three starting point PROV classes (Entity, Activity, Agent) and two qualified classes (Role, Association) that form the foundation of openDS. These five classes exist at the abstract (primary) level of the class hierarchy. 

![figure: attribution model concept](/images/attributionmodel680.png)

**Figure 1: RDA PROV/Attribution metadata model**<br>Reproduced from the RDA Recommendation on '[Attribution Metadata](http://dx.doi.org/10.15497/RDA00029)'.

In the DS group, the principal object classes are sub-classes (specializations) of classes at the abstract level. Figure 3 illustrates how these principal openDS classes relate to one another in the overall object model concept. The principal Digital Specimen object, the main subject of this openDS specification is coloured pink. Figure 3 also illustrates how specific openDS classes, such as `DigitalSpecimen` can be extended with traits such as `Extenders` and `ObjectClassification` that make the object instance more precise for specific circumstances.

![figure: DS classes as specializations of abstract classes, with extending traits](/images/defaultview1000.png)

**Figure 3: DS classes as specializations of abstract classes, with extending traits**

## Digital Specimen (DS) group class definitions

Just a few examples at present:
- DigitalSpecimen - is an example (subclass) of an Entity.
- Loan and Visit - are examples (subclasses) of a Transaction.
- Annotation and Intepretation - are examples (subclasses) of a Transaction.
- GeographicOrigin - is an example (subclass) of a Dimension.
- GeologicalTimeRange - is an example (subclass) of a Dimension.
- ObjectClassification - is an example (subclass) of a Dimension but it will vary, depending on the Trait that extends it e.g., botanical classification, mineral classification, etc.

To be completed - take from @wouteraddink document on DiSSCo data types

### Classes with abstract parent class Entity

> | Secondary (concrete) class | Description | Source<br> (linked IRI where applicable) |
> | --- | --- | --- |
> | DigitalSpecimen |  |  |
> | Loan |  |  |
> | Visit |  |  |
> | Annotation |  |  |
> | Interpretation |  |  |

### Classes with abstract parent class Dimension

> | Secondary (concrete) class | Description | Source<br> (linked IRI where applicable) |
> | --- | --- | --- |
> | GeographicOrigin |  |  |
> | GeologicalTimeRange |  |  |
> | ObjectClassification |  |  |

## Extender group class definitions

Traits (extenders) definitions and their use

To be completed.
== sub-types as suggested by @wouteraddink

> | Traits (extenders) | Description | Source<br> (linked IRI where applicable) |
> | --- | --- | --- |
> |  |  |  |



END.