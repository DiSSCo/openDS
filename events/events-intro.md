# Introduction to event-based transactions with openDS




**Figure 1**: Graphical summary of the interaction between CMSes, DOA and additional external systems for research and application, e.g. analytical environments or national reporting for biodiversity monitoring.


## Basic CMS - DiSSCo DOA interaction

The interface between a CMS and the DiSSCo Digital Object Architecture (DOA), or DiSSCo Research Infrastructure (RI) involves at a minimum **two agents** and an **abstraction layer** that connects the information flow between the two agents through machine-based transactions including at least one mapping.

In the interaction, the DiSSCo DOA and each CMS endpoint are recognized as **agents**. Thereby, each agent is uniquely identified by a PID (persistent, globally unique and resolvable identifier). In addition to these two types of agents, it is planned that automated machine processes externally originating in, for example, research environments will be able to initiate and run transactions as independent agents. 

In a first development step, agents involved in transactions are only recognized at the organization level, that is, recorded for a transaction on the side of CMS partners are PIDs of institutions (e.g. RORs) or CMS endpoints. It is planned that in the future also agents active within the CMS, for example, individual staff and scientists using and contributing to the data within the CMS can be associated with transactions through their specific PIDs (identified by e.g. ORCIDs), and thus become visible not only within the CMS, but also to the DOA. 

For each CMS its associated companies, developers and users can decide CMS-, client- and user-specific set-ups for the interface with the DOA. A CMS system might have one central endpoint to the DOA, to which its client systems can be connected in the backend, which they use as gateway in transactions with the DOA. Alternatively, CMS clients might be connected directly with the DOA, if they wish so and the CMS architecture enables it. For example, an institution might be connected by its own CMS endpoint. Furthermore, scientific collections, working groups and even single users might have their own endpoints for communication with the DOA. Currently, all CMS clients will be identified by the CMS endpoint that they use to connect to the DOA, more specifically the PID of the organization associated with the endpoint.

The interface between CMS and DOA can be called the **abstraction layer**. It comprises the generation of a notification about an transaction event within the system of origin, its transmission over the internet to the partner system, at least one machine-mediated mapping and the creation of data structures native to the receiving system.

The goal of the event-based interaction model between infrastructures is the communication of individual changes to the data and their structure. Each **transaction event** of creating, reading/receiving, updating or deleting a CMS record or open FAIR digital object (openFDO) will result in a notification process across an interface and the propagation of a corresponding change to the “twin” digital element in the core data pool as well as in partner infrastructures, respectively. The machine-based transactions/interactions between the two agents of the model always arise from a single transactional event. 

No synchronization of whole datasets comprising two to many independent, repeating elements is involved. Synchronization of datasets often is performed at (periodical) intervals as a summary transaction event to create corresponding datasets stored within different infrastructure systems or platforms. It represents the transmission of a partial to whole dataset with an accumulation of events or changes at potentially many places. These might be conflicting, requiring different responses and checks, and might unintentionally overwrite data with and without modifications. Furthermore, considering the existing and expected sizes of the involved data repositories that need to exchange events, the synchronization of whole data pools would overwhelm the system(s). Such an approach would also be exceedingly inefficient regarding the number of changes that need to be communicated within a certain time period and the amount of data that would need to be transferred for synchronization of whole archives.

Events of individual changes on the other hand are immediately transmitted between systems as long as online connectivity, bandwidth and processing power are given. If bulk transfers at certain times (eg. due to a lack of continuous connectivity) or for certain purposes are necessary these involve queues of single events.








END
