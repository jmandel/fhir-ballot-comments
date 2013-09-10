## Elements should never be defined with type `string|CodeableConcept`

In `4.9.1`, a MedicationPrescription's `reasonForPrescribing[x]` presents an
unnecessary choice between `string|CodeableConcept`.  Since a `CodeableConcept`
is allowed to have its own `text` element, it can serve the role whether or not
a code is available.
