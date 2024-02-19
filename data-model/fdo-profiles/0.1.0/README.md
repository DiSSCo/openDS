## FDO Profile schemas

This folder contains a collection of FAIR Digital Object Profiles (FDO Profiles) specific to DiSSCo data model elements. Each folder represents a distinct profile for various digital objects like annotations, digital specimens, media objects, organisations.  We also include profiles for:

- DOI and Handle Kernels: Guaranteeing persistent identifiers and resolution.
- Mappings: Simplifying intricate connections between data entities.
- Machine Annotation Service (MAS): Enabling efficient annotation management.
- Digital Object Tombstone Pages: Preserving crucial information even after object deletion.

These profiles are essential for implementing FAIR principles and ensuring machine-actionability. Moreover, these profiles interlink with each other. For instance, Handle-based objects like MAS, mappings, and annotations rely on the Handle profile, while DOI-based objects like digital specimens and media objects leverage both DOI and Handle profiles. 

These profiles are crucial for implementing FAIR principles and ensuring machine-actionability. The profiles are also rely on each other. For instance, objects with a Handle (e.g. mas, mapping, annotations) depend on the Handle profile, and objects with a doi (digital specimens, media objects) rely on both the Handle and DOI profile.


### Why separate FDO Profiles?

While some common metadata exists across profiles, distinct FDOs offer several advantages:

- Granularity: Tailored profiles cater to specific data object types, ensuring the most relevant metadata is captured.
- Extensibility: Profiles can be extended or inherit from others, promoting reusability and avoiding redundancy.
- Governance: Separate profiles facilitate the governance and maintenance of digital object types.
