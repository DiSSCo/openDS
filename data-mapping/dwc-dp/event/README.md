# Event Mapping to DwC-DP

For event we can map most fields with a one to one mapping to the DwC-DP.
There are some new fields that are not present in openDS which might require some discussion.

Within DiSSCo event has several one to one relationship for describing location.
In the DwC-DP this has all been flattened to a single event file.

Some properties that openDS has in event, the DwC-DP has put in Occurrence.
In the occurrence file we will therefore see references to the openDS event.

Only one event is currently mapped to the DwC-DP as we can only directly attach one event to a material.
Additional events can be connected to the material through the relationship file.
Support for this needs to be added in the future.