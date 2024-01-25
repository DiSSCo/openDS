# Frequently asked questions (FAQ) about the open Digital Specimens (openDS) specification

**Q201. What is the openDS specification?**

openDS is a speciﬁcation of Digital Specimen and other related object type definitions essential to mass digitization of natural science collections and their digital use in a new generation of infrastructure and applications. For the principal digital object types corresponding to major categories of collections and specimens’ data, openDS deﬁnes the structure and content of each object type, and the operations that can act upon them.

openDS is concerned with: i) the logical structure and content of Digital Specimen and other object types, and the operations permitted on them; ii) the handling rules and behaviors governing object operations in general; and iii) serialization and packaging for transfer between systems. openDS is not concerned with the implementation dependent aspects of storage, indexing and manipulation of different object types, nor with the application and usage dependent presentation of object content e.g., how a human sees data on a screen.

**Q202. What is the purpose of the openDS specification?**

The purpose of openDS and its specification is to enable new freedoms and opportunities for science that arise from digital transformation of natural science collections. openDS and the associated Natural Science Identifiers (NSId) for persistently identifying Digital Specimens are examples of ‘[enabling technology](https://en.wikipedia.org/wiki/Enabling_technology)’ i.e., an innovation that can be applied to drive radical change in the capabilities of a user or culture. Just as with the invention of the internal combustion engine around 170 years ago, no-one can see clearly all the freedoms and opportunities that will become possible. openDS and NSId should be seen as part of the emerging Internet of FAIR Data and Services that will grow alongside the existing Internet and World Wide Web.

**Q203. What can openDS be used for and who would use it?**

openDS can be used to guide design and implementation of infrastructure and its components, as well as software applications and process workflows. For example:

- The serialization and packaging specifications can be used to guide software design for applications where Digital Specimens data must be transferred from one system to another or from one user to another.
- The openDS JSON Schema can be used to validate the structure and content of DS instances e.g., as they are serialized/packaged, or inserted in repositories.
- The Schema(s) can be used as the basis for design of internal data structures within specific components of the DS Architecture.

openDS is principally intended for use by systems engineers and software developers involved in infrastructure, services/applications and workflows development. openDS will also be helpful to those scientists having an informatics component to their work, who may want to develop bespoke software and scripts to make use of or interact with Digital Specimen data directly.

**Q204. How does openDS differ from Darwin Core and ABCD?**

Darwin Core (DwC) and Access to Biological Collection Data (ABCD) are application level data schema specifications that support the exchange and integration of primary collection (and observation) data.

openDS is like Darwin Core and ABCD insofar as it reuses several of the main data model concepts from those well-established specifications, as well as re-using terms where possible. 

openDS goes further than data exchange and integration to provide active (specimen) data management capability more generally. It does this by defining standard operations (beyond create, update, retrieve and delete) that can act on Digital Specimens to access/change their content; even to run algorithms on that content. This is implemented through a standard and secure method for interacting with digital objects, the [Digital Object Interface Protocol (DOIP)](https://www.dona.net/sites/default/files/2018-11/DOIPv2Spec_1.pdf).

**Q205. Is openDS just Linked Open Data?**

No. Linked (Open) Data is a mechanism for creating the Semantic Web, whereby data is interlinked with other data in a structured way such that it receives meaning and can be queried semantically by processing the actual relationships between information and inferring answer(s) to that query.

openDS is an encapsulating approach that works at a more fundamental level. More than just linking data it ensures stable binding between informational entities required for machine actionability. However, openDS does include that the data within Digital Specimen objects is linked, such that the data receives meaning.

In that sense, the data content of a Digital Specimen can be cast as RDF to a triple store if that is what is needed.

**Q206. What about the implementation? What do I have to do?**

*To be answered, from the data provider perspective (and others).*

**Q207. What is the scope of openDS version 1.0?**

openDS version 1.0 will be the first version of openDS. It is intended to support the compatibilities and service components summarized in the table below.

<table>
  <tr>
   <td><strong>Standards</strong>
   </td>
   <td><strong>Compatibility</strong>
   </td>
  </tr>
  <tr>
   <td>Minimum information about a Digital Specimen (MIDS)
   </td>
   <td>Support for all level 0 – 3 information elements, including presence of images and other media types.
   </td>
  </tr>
  <tr>
   <td>CETAF Specimen Preview Profile (CSPP)
   </td>
   <td>Support for 13 CSPP information elements.
   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td><strong>Services</strong>
   </td>
   <td><strong>Service component/functionality</strong>
   </td>
  </tr>
  <tr>
   <td>European Collection Objects Index (ECOI)
   </td>
   <td>Collation of basic specimen information to support indexing, searching and presentation in human-readable and machine-readable (JSON-LD) forms.
   </td>
  </tr>
  <tr>
   <td>European Loans and Visits (ELViS)
   </td>
   <td>Display of basic specimen information to support arrangement of loans and visits.
<p>
Association of loans and visits transaction events to their corresponding Digital Specimens.
   </td>
  </tr>
  <tr>
   <td>European Unified Annotation and Curation (ECAS)
   </td>
   <td>Association of annotation and interpretation record events to their corresponding Digital Specimens.
   </td>
  </tr>
  <tr>
   <td>Provenance and attribution
   </td>
   <td>Association of provenance events i.e., origins of the data and the processing/modifications applied) to their corresponding Digital Specimens.
   </td>
  </tr>
</table>

**Q208. Does openDS capture the change history of a Digital Specimen?**

Capturing the change history of a Digital Specimen, especially the scientific activities that have been performed upon it (such as curation and annotation) is essential for establishing scientific provenance.

Our provisional design proposal (October 2020) for openDS ensures that the primary (abstract) class definitions of openDS (Classes: Entity, Activity, Agent, Role, Transaction, Derived Data) align perfectly with the basic, three-axiom model based on PROV entities (Entity, Activity, Agent) as outlined in the [final recommendations of the RDA/TDWG Attribution Metadata Working Group](http://dx.doi.org/10.15497/RDA00029) to support standardized metadata for attributing work and tracking provenance in the curation and maintenance of research collections.

**Q209. When will the openDS specification be available?**

At the moment there is no explicit timeline for when the specification will be available. We hope to release working drafts during 2021.


END.