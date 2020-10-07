# The Ontology for open Digital Specimens (ODS)

The Ontology for open Digital Specimens (ODS) situates open Digital Specimens in the relevant [OBO Foundry](http://www.obofoundry.org/) ontologies and extends from those roots to define the new concepts needed to support mass digitization and Digital Specimens on the Internet.

## OBO Foundry Ontologies

The relevant [OBO Foundry](http://www.obofoundry.org/) Ontologies are the following:

- Ontology for Biomedical Investigations ([OBI](http://www.obofoundry.org/ontology/obi.html)): OBI is an ontology for the description of life-science and clinical investigations; 
- Biological Collections Ontology ([BCO](http://www.obofoundry.org/ontology/bco.html)): BCO is an ontology to support the interoperability of biodiversity data, including data on museum collections, environmental/metagenomic samples, and ecological surveys; and,
- Information Artifact Ontology ([IAO](http://www.obofoundry.org/ontology/iao.html)): IAO is an ontology of information entities. 

For an explanation of how the BCO is related to the OBI and IAO ontologies, this recent (2018) book chapter on "*[Integrating and Managing Biodiversity Data with the Biocollections Ontology](http://ebooks.iospress.nl/volumearticle/49542)*" by Ramona Walls et al. is helpful.

## Situating ODS in existing ontologies and extending therefrom

With reference to the following figure, 

![new classes in ODS ontology (dark green)](/images/ods-newconcepts.png)

In the [OBI](http://www.obofoundry.org/ontology/obi.html) there is the concept of a ‘planned_process’ ([OBI_0000011](http://purl.obolibrary.org/obo/OBI_0000011)) that captures the idea of performing some kind of process that has previously been planned. Present examples (subclasses) include: carrying out investigations, assays, creating datasets, developing software and (of immediate relevance) collecting specimens ('specimen_collection_process',[OBI_000659](http://purl.obolibrary.org/obo/OBI_0000659)). 

The result of a specimen_collection_process is a specimen ([OBI_0100051](http://purl.obolibrary.org/obo/OBI_0100051)), which can be further elaborated as a PreservedSpecimen or a LivingSpecimen. And here we arrive at the conjunction between the ontologies of the OBO Foundry and the terms vocabularies/schema of TDWG [Darwin Core (DwC)](https://dwc.tdwg.org/) and [Access to Biological Collections Data (ABCD)](https://abcd.tdwg.org/) and its [Extension for Geosciences (EFG)](http://terms.tdwg.org/wiki/ABCD_EFG).


The concepts 'specimen_collection_process' and 'specimen' are replicated forward into the [BCO](http://www.obofoundry.org/ontology/bco.html) as [BCO:OBI_0000659](http://www.ontobee.org/ontology/BCO?iri=http://purl.obolibrary.org/obo/OBI_0000659) and [BCO:OBI_0100051](http://www.ontobee.org/ontology/BCO?iri=http://purl.obolibrary.org/obo/OBI_0100051) respectively.

ODS situates the act of planned digitization activities as a new kind of OBI:planned_process that we name as 'digitization_event' or 'digitization_process' (ODS_00000nn). This sits alongside the familiar notion of collecting specimens as another major activity performed by institutions holding natural science collections.

The output of a digitization_process is a new class ‘digital specimen’ (ODS_00000nn). This must be considered as a new subclass of ‘information_content_entity’ ([IAO:0000030](http://purl.obolibrary.org/obo/IAO_0000030)) in the IAO), being ‘a result of a digitisation event or process’. We consdier a new subclass because the existing subclasses don't seem appropriate. Subclass 'data_item' ([IAO:0000027](http://purl.obolibrary.org/obo/IAO_0000027)) seems rather too general.

*To do: digitization_event or digitization_process? Go back to earlier notes and have a look at why is event rather than process.*


END.