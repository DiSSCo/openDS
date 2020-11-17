# Introduction to the openDS data model <!-- omit in toc -->

> **<p style="color: red;">17th November 2020: Note that the content of this page is work-in-progress and therefore incomplete. It does not yet describe all aspects of the model as elaborated in various Powerpoint presentations over the past months.</p>**
> **<p style="color: red;">The important point at this moment is to obtain consensus on the foundation model described here.</p>**

- [Three-level class hierarchy](#three-level-class-hierarchy)
- [Abstract (primary) level class definitions](#abstract-primary-level-class-definitions)
- [Concrete (secondary) level class definitions](#concrete-secondary-level-class-definitions)
  - [Classes with parent class Entity](#classes-with-parent-class-entity)
  - [Classes with parent class Dimension](#classes-with-parent-class-dimension)
- [Extender (tertiary) level class definitions](#extender-tertiary-level-class-definitions)

## Three-level class hierarchy
As explained in [positioning openDS in the landscape](/positioning-opends.md), our design proposal (November 2020) aligns perfectly with the basic, three-axiom attribution model based on PROV entities (Entity, Activity, Agent) as outlined in the RDA Recommendation on '[Attribution Metadata](http://dx.doi.org/10.15497/RDA00029)'. We achieve this by defining a three-level class hierarchy in which we set the PROV model as the abstract or primary level from which some of the concrete classes of the openDS specification are inherited. To account for the wide variation in specimen categories (plants, insects, rocks, etc.) we use a lower level of extender classes or traits to make the concrete classes precise to specific situations. Thus, openDS defines a three-level class hierarchy comprised of:

1. **Abstract (primary) level:** The class definitions match the PROV/Attribution metadata and other surrounding object/data models necessary to give context to the openDS model;
2. **Concrete (secondary) level:** The class definitions are subclasses of the abstract level classes and are actually the main classes making up the practical openDS data model; and,
3. **Extender (tertiary) level:** The definitions that extend and further compose (or precise) the secondary level classes to more specific subclasses associated with different kinds of specimen representation e.g., for botany, for zoology, for geology, etc. In object modelling terms this level of definitions is sometimes referred to as traits that can be applied by mixing them into classes. A concrete class at the secondary level can mix in any number of traits from the extender level to make it more precise to the context in which it is instantiated.

For now, the class definitions for each of these levels are given below. As these become accepted and grow in size and complexity they will eventually be split out into separate pages. To help keep track of the class definitions and their development, an [openDS class index spreadsheet](https://docs.google.com/spreadsheets/d/1Tb3zZZWY-TY50nttg3Jj8T0S2ZhJaNQKftv-a4ywV1I/) is maintained for quick reference. This also helps with synchronisation and alignment with the [MIDS](https://github.com/tdwg/cd/tree/master/mids) and [CD](https://github.com/tdwg/cd) standards developments.

## Abstract (primary) level class definitions

> | Abstract (primary) class | Description | Source<br> (linked IRI where applicable) |
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

Figure 1 illustrates the PROV/Attribution model with its three starting point PROV classes (Entity, Activity, Agent) and two qualified classes (Role, Association) that form the foundation of openDS. 

![figure: attribution model concept](/images/attributionmodel.png)

**Figure 1: RDA PROV/Attribution metadata model**<br>Reproduced from the RDA Recommendation on '[Attribution Metadata](http://dx.doi.org/10.15497/RDA00029)'.

Figure 2 illustrates how the principal object classes relate to one another in a high-level object model concept.

![figure: high-level object model concept](/images/modelconcept.png)

**Figure 2: High-level object model concept**

Using two examples (yellow and green), Figure 3 illustrates how the secondary (concrete) classes are instances of a specific primary (abstract) classes. Figure 1 also illustrates how a specific concrete class, such as `DigitalSpecimen` and `ObjectClassification` can be extended with traits that make the object instance more precise for specific circumstances. 

![figure: secondary classes are instances of primary classes and traits extend secondary classes](/images/classhierarchy.png)

**Figure 3: Seconday (concrete) classes as instances of primary (abstract) classes, with trait extenders**

## Concrete (secondary) level class definitions

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

## Extender (tertiary) level class definitions

Traits (extenders) definitions and their use

To be completed.
== sub-types as suggested by @wouteraddink

> | Traits (extenders) | Description | Source<br> (linked IRI where applicable) |
> | --- | --- | --- |
> |  |  |  |



END.