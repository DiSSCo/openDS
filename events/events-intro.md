# Introduction to event-based transactions with openDS


![Interaction paths between DiSSCo technical infrastructure, CMSes and additional research or application systems](https://github.com/DiSSCo/openDS/blob/jbstatgen_events/events/FullPath_Detail_20221102b.drawio.png "FullPath_Detail_png")

**Figure 1**: Graphical summary of the interaction between CMSes, DOA and additional external systems for research and application, e.g. analytical environments or national reporting for biodiversity monitoring.

This introduction describes the use case of a local Content Management System (CMS) in use by a natural science institution or scientific collection interacting with an online infrastructure, in this case the technical Research Infrastructure of the European [Distributed System of Scientific Collections](https://www.dissco.eu/) (DiSSCo RI). The DiSSCo RI will be implemented following the concept of a [Digital Object Architecture](https://www.dona.net/digitalobjectarchitecture) (DOA) and will be part of a globally integrated DOA.

## Basic CMS - DiSSCo DOA interaction

The interface between a CMS and the DiSSCo Digital Object Architecture (DOA), or DiSSCo Research Infrastructure (RI), involves at a minimum **two agents** and an **abstraction layer** that connects the information flow between the two agents through automated event-based transactions including at least one mapping.

### Agents

In the interaction, the DiSSCo DOA and each CMS endpoint are recognized as **agents**. Thereby, each agent is uniquely identified by a PID (persistent, globally unique and resolvable identifier). In addition to these two types of agents, it is planned that automated machine processes externally originating in, for example, research environments will be able to initiate and run transactions as independent agents. 

In a first development step, agents involved in transactions are only recognized at the organization level, that is, recorded for a transaction on the side of CMS partners are PIDs of institutions (e.g. RORs) or CMS endpoints. It is planned that in the future also agents active within the CMS, for example, individual staff and scientists using and contributing to the data within the CMS can be associated with transactions through their specific PIDs (identified by e.g. ORCIDs), and thus become visible not only within the CMS, but also to the DOA. 

For each CMS its associated companies, developers and users can decide CMS-, client- and user-specific set-ups for the interface with the DOA. A CMS system might have one central endpoint to the DOA, to which its client systems can be connected in the backend. The CMS clients will then use this shared gateway in transactions with the DOA. Alternatively, CMS clients might be connected directly with the DOA, if they wish so and the CMS architecture enables it. For example, an institution might be connected by its own CMS endpoint. Furthermore, scientific collections, working groups and even single users might have their own endpoints for communication with the DOA. Currently, all CMS clients will be identified by the CMS endpoint that they use to connect to the DOA, more specifically the PID of the organization associated with the endpoint.

### Abstraction Layer

The interface between CMS and DOA can be called the **abstraction layer**. Its functionality includes the generation of a notification about a change within the system of origin, the initiation of an event-based transaction, its transmission over the internet to the partner system, at least one machine-mediated mapping and the creation of data structures native to the receiving system.

### Transaction Event

The goal of the event-based interaction model between infrastructures is the communication of individual changes to the data and their structure. Each **transaction event** of creating, reading/receiving, updating, deleting or more specific predefined operations to a CMS record or open FAIR digital object (openFDO) will result in a notification process across an interface and the propagation of a corresponding change to the “twin” digital element in the core data pool as well as subsequently in additional linked partner infrastructures. The machine-based transactions/interactions between the two agents of the model always arise from a single event. If several changes are involved, these are queued and processed as individual events.

No synchronization of whole datasets comprising two to many independent elements is involved. Synchronization of datasets often is performed at (periodical) intervals as a summary transaction event to create corresponding datasets stored within different infrastructure systems or platforms. It represents the transmission of a partial to whole dataset with an accumulation of events or changes at potentially many places. These might be conflicting, requiring different responses and checks, and might unintentionally overwrite data with and without modifications. Furthermore, considering the existing and expected sizes of the involved data repositories that need to exchange events, the synchronization of whole data pools would overwhelm the system(s). Such an approach would also be exceedingly inefficient regarding the number of changes that need to be communicated within a certain time period and the amount of data that would need to be transferred for synchronization of whole archives.

Events of individual changes on the other hand can be immediately transmitted between systems as long as online connectivity, bandwidth and processing power are given. If bulk transfers at certain times (eg. due to a lack of continuous connectivity) or for certain purposes are necessary these involve queues of single events.


## Creation of an openDigitalEvent
![Interaction paths between DiSSCo technical infrastructure, CMSes and additional research or application systems](https://github.com/DiSSCo/openDS/blob/jbstatgen_events/events/FullPath_Step3_4_20221006_half.drawio.png "AbstractionLayer_png")

**Figure 2**: The abstraction layer mediating the mapping between the data model of the CMS and the DOA with its openDOs.

### Provenance Ontology as Standard for Events

Event-based transactions between CMS and DiSSCo DOA will follow the model provided by the W3C-recommended Provenance Ontology (PROV). The model has three main elements: an entity (the openDS), an activity (a predefined operation to be conducted on the entity) and an agent, which might act in a specific role. In the interaction between CMS and DiSSCo DOA there are a transmitting and a receiving partner as agents.

The details of event-based transactions are still under development. Questions that need to be decided are, for example:

* *Will events always involve fully wrapped digital objects, that is openDS entities, or will only the information be transmitted that is impacted by a change? This involves considerations of suitable granularity.*
* *Associated with the previous question are also questions about which types of operations are needed or performed? Will* diffs *, that is checks for differences, be sufficient or are more specialized and thus explicit operation types necessary? Such specific types can refer specifically to, e.g., updates of taxon identifications, changes in locations during loans, etc.*
* *Will the transmitting partner first only send a notification informing about a change and the receiving partner then decides if they are interested in the change and its associated transaction? If the receiving partner is interested, they request the full information about the change, that is, the "payload" of the change. Alternatively, the transmitting partner might send the payload of the change already with the notification and the receiving partner, if interested can immediately incorporate the change in its pool of digital objects or records.*

### openDigitalEvents

The event-based transactions become open FAIR digital objects (openFDOs) themselves in the form of **openDigitalEvents** (openDEs). For this purpose, events are associated with a predefined set of metadata that is sufficiently informative for the event as openDE to "stand on its own". Thus, openDEs are wrapped in several layers of (meta)data, which contain and store all context necessary to understand (and/or recreate) the event and hence enable the digital object to be self-explanatory, self-sufficient and fully functional. At the same time, openDEs and their metadata layers are expected to be minimal, only providing functions and information that are indispensable for the transmission and the generation of the required action in the receiving system. Hence they should not carry excessive functions and information.

openDEs are on one hand stored as part of the **provenance record** generated by the DiSSCo infrastructure that logs all interactions and changes. This record can be used to recreate certain states and/or retrieve user-selected past states of an openDS as the basis for subsequent changes by this user. On the other hand, schemata of repreatedly performed types of events can be stored as openDEs for later retrieval and reuse.

### CloudEvents

In their outermost layer, openDEs become payload information and are wrapped for transmission between networked digital systems and infrastructures in a specific layer of metadata defined by the **CloudEvent standard**. The CloudEvents standard provides a standardized format for transferring information packets between different infrastructure systems. 

### Mapping

If a CloudEvent package delivers information from a CMS to the DiSSCo RI, it is first processed by the **mapping** module of the DOA’s abstraction layer. The information carried by the openDE is mapped to the corresponding DOA data model(s). Following the mapping the DOA then generates for each of the PROV elements in the transaction the corresponding openDO(s) or links to them if they already exist. For example, generated will be an openDS, openDigitalAgent for the CMS and an openDigitalActivity. These openFAIRDigitalObjects (openFDOs) are then brought together and integrated as an openDE, which is the format used to create or update a new or already existing full digital object, respectively. This now up-to-date or newly created openDO finally is deposited in the DOA's storage module. Thus, once the CMS’s information has arrived within the DOA, it is the DOA that checks for changes and either creates a new openDO or updates an existing openDO within the DOA in correspondence to the annotated/changed record in the CMS. 

Therefore, operations on digital objects are performed only by the DOA. New or updated digital objects might then be transferred back to the CMS upon manual request and/or predefined (search) filters. Upon manual authorization by collection staff and/or scientists this updated information can be subsequently incorporated into the CMS’ database as records or updates to existing records.


END
