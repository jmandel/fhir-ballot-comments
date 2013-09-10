## FHIR should forbid "dangling" contained resources.

See [this discussion thread](http://lists.hl7.org/read/messages?id=237825)
about the dangers of "dangling" contained resources.

To summarize: FHIR should prohibit "dangling" or un-referenced "contains"
elements such as the one found in Grahame's [Prescription @1](http://hl7connect.healthintersections.com.au/svc/fhir/medicationprescription/@1)
