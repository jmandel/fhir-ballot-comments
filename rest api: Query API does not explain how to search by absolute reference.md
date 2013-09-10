## Query API does not explain how to search by absolute reference

Searching for a reference-type parameter is described in `6.11.2.1.5` as
supporting two modes of query:

> `name=id` the id of a resource (not including the @ that goes in the URL)
> `name=type/id` matches an id of a resource with a specific target type. 

Neither of these provides the means of searching for a reference to an absolute
resource URI.  In FHIR, resource references can be absolute, relative, or
"contained".  Search needs to support absolute and relative references in order
to work in the general caase.

I would propose the following modifications:

1. To perform a search for a resource "on this server", a client can do either:
* `name=type/id`
* `name=[service-url]/type/id`

These two queries are semantically identical and should return the same
results. (That is, it is unimportant whether a given resource reference is
serialized in the FHIR server or in the query as relative or absolute -- the
important thing is the resource that the reference points to.)

2. To perform a search by references to an external resource, a client can do:
* `name=https://full-uri.of/external/resource`
 
