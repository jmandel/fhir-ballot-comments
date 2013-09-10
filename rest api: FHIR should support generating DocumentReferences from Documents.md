## FHIR should support generating DocumentReferences from Documents

For documents that conform to certain patterns (CDA, for example, or C-CDA),
FHIR should define a standard operation for POSTing a document that the server
will then hash, index, and represent with a `DocumentReference.` These
functions are currently all the responsibility of the client, but in general a
server will be well-equipped to perform them, and it would be useful to have a
standard operation (with standard URL) to handle it.
