## FHIR spec represents URLs inconsistently

URIs are frequently represented as "templates" that include parameters.
Sometimes these parameters are optional, and sometimes they're required.  There
are two key problems with how URL templates are used in the current spec:

1.  There is no indication of which path segments are optional vs. required

2.  Parameters are not represented with consistent syntax.  For example,
`http.htm` describes the same operation with `/[type]/validate/@[id]` and
`[service-url]/[resourcetype]/validate/{@id}` (presence vs. absence of
`[service-url]`, square brackets vs. curlies).

3.  In some places (like query.htm), `[base-url]` is used; in others (like
