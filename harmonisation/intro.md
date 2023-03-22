# Introduction to harmonisation

For DiSSCo to provide fully machine actionable units (FDOs), there needs to be a standardized data model.
This data model provides a way to know which information to expect and where to expect it.
The data standard, we will call the open Digital Specimen (openDS), builds upon existing standards.
This openDS will also form the basis of the FDO in the form of the FDO Type.

Data coming into DiSSCo will not conform to the openDS data specification.
They come from a range of different data providers (often CMS's) in a range of different data standards.
In the first instance we have focussed on two, often used, ways of data exposure, Darwin Core Archives (DWCA) and BioCASe.
DWCA use darwin core as data standard while BioCASe uses ABCD(EFG) as data standard.
But even within a single data standard different elements can be filled in differently.
Additionally, we have the elements expected and defined by MIDS, specifically focussed on collection specimens.
The elements in MIDS do not always exact match a term in the existing data standards.

Within the translator we will harmonise the data into the openDS data specification.
The terms of openDS have been determined based on the MIDS elements and checked for existing terms within DWC and ABCD(EFG).
If no matching term was identified in DWC and ABCD(EFG) a new term under the openDS (ods) ontology was proposed.
All terms are subject to change and are open for discussion.

In this folder we will show how we harmonised the information in DWCA and BioCASe endpoints in to a single data specification, openDS.

