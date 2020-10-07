# Frequently asked questions (FAQ) about Digital Specimens

![Illustration of the data types tied up in physical specimens](/images/whatsinabug.png)

**Q101. What is a Digital Specimen (DS)?**

A Digital Specimen, referenceable by its unique Natural Sciences Identifier (NSId) represents the sum of information on the Internet about a natural specimen object. The Digital Specimen acts as a processable digital twin on the Internet for the physical specimen in a natural sciences collection (for example, in a Natural History Museum).

This [DiSSCo Tech article](https://dissco.tech/2020/03/31/what-is-a-digital-specimen/) introduces the Digital Specimen concept in more depth.

**Q102. What is an _open_ Digital Specimen?**

The word ‘open’ is applied in the sense of an open format for Digital Specimens as defined by a published specification, the openDS specification. With the intention to improve interoperability, open formats can be used by anyone and their use is often encouraged within, by and for specific communities and the associated software applications and systems. 

From the perspective of the commons and the [Open Definition](https://opendefinition.org/), open can be applied further to mean that open Digital Specimens can be “_freely used, modified, and shared by anyone for any purpose_.” However, initial publication of Digital Specimen content is constrained by considerations of applicable legislative constraints, which in the bio- and geo-diversity domain is interpreted to mean that the aim with Digital Specimens is to be “_as open as possible, as closed as legally necessary_.”

‘Open’ is also used in the sense that a Digital Specimen is a mutable digital object, meaning that it can be manipulated and modified by appropriately authorized persons. Open Digital Specimens ultimately act as a common curation space where experts should be able to contribute above and beyond the data held at the local level of a specific natural science collection.

**Q103. How are open Digital Specimens represented?**

Within an information system, the design of the internal data structures used to hold data associated with Digital Specimens is a decision for the system’s designers. However, the importance of being FAIR (‘findable, accessible, interoperable and reusable’) with its emphasis on machine actionability and the increasing use of object store infrastructures with their correspoinding APIs strongly advocates in the direction of using standardized, easily discoverable object type definitions such as the Digital Specimen object type. This is especially true at the external interfaces of systems. Knowing the (object type) definition of a Digital Specimen and what operations can be performed on it provides a shared and congruent understanding of the object context that is essential for correct functional operation and performance of systems, especially at the level of machine-to-machine interactions. Digital object type definitions and interface protocols directly support high levels of interoperability and reusability between systems and between applications. These are two of the four guiding principles of FAIR. To learn how Digital Object Architecture offers adherence to the FAIR principles as an integral characteristic, you may like to read this [paper by Lannom, Koureas and Hardisty](https://doi.org/10.1162/dint_a_00034).

When it is necessary for transfer between different information systems, an open Digital Specimen can be represented (serialized) as a JSON document in which the various attributes of the specimen are represented as related sets of name/value pairs in [Javascript Object Notation (JSON)](https://www.json.org/json-en.html). The details of this transfer representation (serialization) are specified by the openDS specification.

**Q104. How are Digital Specimens made FAIR (Findable, Accessible, Interoperable, Reusable)?**

Digital Specimens are first-class [FAIR Digital Objects](https://fairdo.org/) (FDO), complying with the generic guidelines and requirements of the [FAIR Digital Object Framework](http://bit.ly/fdof102) ([Version 1.02, November 2019, FDOF Technical Implementation Guideline](https://github.com/GEDE-RDA-Europe/GEDE/blob/master/FAIR%20Digital%20Objects/FDOF/FAIR%20Digital%20Object%20Framework-v1-02.docx)). In this respect, they draw on controlled vocabularies and ontologies to introduce meaning (context) into their structure and are represented by object type definitions deposited in (a) public type registry(ies).

**Q105. Can a Digital Specimen contain data for multiple specimens?**

A Digital Specimen has a one-to-one relation with a physical specimen in a physical collection and corresponds to whatever the owning/holding institution deems to be an individual specimen. A specimen in this sense can be any object or entity (physical or conceptual) and is independent from categories such as preparation, sample or biological individual.

If a specimen is a box container or spirit jar containing multiple organisms and that is catalogued as a single specimen, then it will have a single Digital Specimen as a digital surrogate for it. If each of the organisms in the box/jar is catalogued separately then each should have its own Digital Specimen surrogate with appropriate linking relations to the others within the same container.

A Digital Specimen can correspond to a specimen that is no longer physically extant (e.g., lost, destroyed, split into specimens with separate identities, a fish released after taking measurements and samples, etc.). Such _status_ information should be made clear in the DS.


END.