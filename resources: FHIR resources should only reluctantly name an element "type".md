## FHIR resources should only reluctantly name an element "type"

Resource elements called "type" can be hard for an implementer to reason about.
In general, models should avoid calling a field "type" without a very good reason.

For example, in the `Group` model, there is a property called `Group.type` and another called
`Group.characteristic.type`. It would be clearer to give these semantically
imbued names -- even `Group.characteristic.name` would be clearer.  (This is
the approach taken by the `DiagnosticReport` models, which has a field called
`DiagnosticReport.results.name`.)
