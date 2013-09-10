## `composite` search parameters don't handle basic, essential use cases

The FHIR spec does not explain how composite-type search parameters interact
with modifiers.  For example, if I'm searching for an observation by name and
value, it's extremely common and useful to be able to find CBC results with an
absolute neutrophil count < 10*3uL, or a Hemoglobin A1C > 7%.

I can (apparently) only find exact matches for Absolute Neutrophil Count like:

```
GET /observation/search?name-value=http://loinc.org/751-8$1302
```

... which is not clinically useful because I never know the exact count.

Similarly, there is no way to find `DiagnosticOrder` resources whose status
changed *after* a certain date, or *before* a certain date -- only on an exact
date.  And since datetime precision can be even smaller (hour, or second),
searching on datetime equality is hardly ever useful.

The FHIR spec could use a way to "and" together queries with modifiers. An
appropriate syntax would be something like:

```
GET /observation/search?component=(name:anyns=751-8,valueQuantity<1000)
```
