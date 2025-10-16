This folder contains data mappings to other standards for version 0.4.0 of openDS and specifically for the Digital Specimen and Digital Media objects.
It uses the [Simple Standard for Sharing Ontological Mappings (SSSOM)](https://mapping-commons.github.io/sssom/) together with [Simple Knowledge Organisation System (SKOS)](https://www.w3.org/2004/02/skos/) to express the relationships between the terms in openDS and the terms in other standards.
The mappings are stored in tsv format as advised by the SSSOM standard.

At the moment we have three data mappings:
- To Darwin Core Archive, where we indicate which terms in openDS map to which terms in Darwin Core. See [sssom_dwca.tsv](sssom_dwca.tsv). We also indicate from which specific extensions the terms originate.
- To ABCD-EFG, where we indicate which terms in openDS map to which terms in ABCD-EFG. See [sssom_abcdefg.tsv](sssom_abcdefg.tsv). We indicate the path to the term in the ABCD-EFG XML structure, if there is an array we use a * to indicate we iterate over all the objects in the array.
- To Darwin Core Data Package (using Darwin Core Conceptual Model). See [sssom_dwc_dp.tsv](sssom_dwc_dp.tsv). We indicate from which class the term originates. Be aware DwC-DP is still under development and not yet a formal standard.

## Order
What we couldn't capture with SKOS is the order by which we evaluate a match.
If there are multiple possible matches, we evaluate them in the order as they appear in the mapping file, from top to bottom.
For example, in the mapping to ABCD-EFG, the `ods:physicalSpecimenID` can be mapped to two different ABCD-EFG fields.
We will first check `abcd:unitGUIG` if that is empty we will use `abcd:UnitID`.

## Future work
Add term IRI's when they become available.
