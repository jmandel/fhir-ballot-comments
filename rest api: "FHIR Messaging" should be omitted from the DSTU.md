## "FHIR Messaging" should be omitted from the DSTU

`6.9` defines a large set of rules that create a "messaging" interface for
FHIR.  These rules propose "message" and "mailbox" abstractions that can be used in a
RESTful context or non-RESTful context, and when they are used, they present a
wholesale alternative for how resources can created an updated. There is a huge
amount of complexity around the relationship (if any) between this kind of
messaging and RESTful access. For example, `6.9.7` states:

> The server is under no obligation to do anything particular with the
> resources except as required by the semantics of the event code in the
> message resource. A server may choose to retain the resources and make them
> available on a RESTful interface, but is not required to do so.

As I understand it, these rules have not yet been implemented by any FHIR
server or client.

Given  that

1. These are complex rules, and 

2. This functionality largely duplicates FHIR's widely implemented REST API, and 

3. FHIR Messaging has not yet been implemented by any server or client, and

4. None of the use cases in `2.5` rely on FHIR Messaging

... **the prudent approach is to remove this aspect of FHIR from the DSTU** until
the community has had a chance to implement and experiment with these
interfaces, and iterate on their definition. It still seems possible that many
of these functions may be unnecessary in practice, and there is no question
that including them in the specification increases the work of editing and
maintaining (let alone implementing) FHIR.
