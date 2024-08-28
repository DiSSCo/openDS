Open Digital Specimen (openDS) is the cornerstone of DiSSCo's vision for a seamless and standardised digital representation of physical specimens in Natural Science Collections. openDS serves as a comprehensive data specification, unifying diverse scientific information derived from both biological and geological specimens. Born out of the need for a structured description that integrates effortlessly into various workflows, openDS is designed to enhance the Findable, Accessible, Interoperable, and Reusable (FAIR) aspects of biodiversity data.

As a digital surrogate on the internet, openDS encapsulates the essence of a "Digital Specimen," offering a solution for collections ranging from marine specimens to botanical and mineralogical holdings. Leveraging established biodiversity information standards such as Darwin Core, Minimal Information Digital Specimen, Latimer Core, Access to Biological Collection Data Schema, Extension FOR Geosciences, and the emerging Global Biodiversity Information Facility Unified Model, openDS harmonises and elevates the quality and machine actionability of scientific data.

The openDS data model consists of a documented set of [JSON schemas](https://schemas.dissco.tech/) that describe the Digital Specimen and related digital objects. The documentation can be found here: https://dev.terms.dissco.tech/

## How to become involved and contribute
Linking third-party/extended specimen data together, as openDS proposes, requires many stakeholders to test and adopt the specification. This is especially the case for integrating data at multiple levels, like: specimen, collection types, species, genomics, and cross-discipline to geology, genomics, etc. This necessitates global collaboration among all players in the landscape converging towards a single specification as far as possible. 

You can become involved and contribute by making comments through Github issues. For this, we created two simple [Github templates](https://github.com/DiSSCo/openDS/issues/new/choose): one for feedback on a term and another for general comments. When commenting on a term please include the term name, for example, dwc:highestBiostratigraphicZone. Note that most terms are coming from existing standards but a few are openDS specific. We aim to apply controlled vocabularies for terms where appropriate to increase data quality and interoperability. These are not yet part of the documentation.

DiSSCo is supported by different EU grants. A dedicated development team and other collaborators working towards a robust specification. The implementations can be seen in our current [Sandbox](https://sandbox.dissco.tech/). Note that the openDS data model v0.3 has not yet been implemented in our sandbox annotations portal (sandbox.dissco.tech), which still uses version v0.2. However, some JSON examples of v0.3 can be found through our development API, for example, https://dev.dissco.tech/api/v1/digital-specimen.



