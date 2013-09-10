## Asynchronous Queries on REST should be omitted from the DSTU

`6.11.8.3` defines a framework for asynchronous RESTful queries.  The proposal
is highly complex seven-step process (as the specification notes directly):

> This pattern is more complex than the other uses, so will be used less. There
> are several variations on this theme. 

Given that there are much simpler approaches to asynchrous web API design (such
as [Webhooks](http://en.wikipedia.org/wiki/Webhook), and given that (as I
understand it) no one has yet implemented FHIR's asynchronous query API, I
believe it's highly advisible to remove this functionality until the community
has time to explore alternatives and gain some experience.

In particular, two of the most troubling aspects of the proposal as written are:


1.  The original requester needs to synchronously poll for responses (with no
indication of whether the response time is likely to be seconds, hours, or
days).

2.  Queries are generated in response to queries (step 4 of the proposal).
