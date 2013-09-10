## FHIR `service-url` should be define without a trailing slash

`2.1.1` states that a Service Root URL has an

> optional path may end with a trailing slash or not

However in practice, all FHIR URLs assume that the service URL does **not**
contain a trailing slash.   That is, all relative URLs are written with a leading "/",
which implies that the Service Root URL should never have a trailing slash
(otherwise, concatenating to create FHIR paths would result in URLs with `//`
between segments).

FHIR should instead state: "a Service Root URL never has a trailing slash."
