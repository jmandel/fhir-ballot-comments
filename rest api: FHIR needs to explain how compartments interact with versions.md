## FHIR needs to explain how compartments interact with versions

In general, the interaction between compartment membership and versioning is
not spelled out, and could be highly complex. Consider, for instance, resources
that have non-version-specific references to each other, and different versions
drop/add compartments over time (e.g. for resources that have chained
compartment membership...)

The key question that needs to be answered is: Are resources, or resource
versions, placed into compartments?
