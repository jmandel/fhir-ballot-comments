## "Implicit" patient compartments need special consideration

`1.10.1.2` states that "compartments... can also be used implicitly."

The [definition of a patient
compartment](http://www.hl7.org/implement/standards/fhir/compartment-patient.htm)
(no index # available in the spec) states that non-patient resources "are never
in this compartment".

This restriction makes sense for explicit compartments, but not for implicit
compartments (which, presumably, still need to expose Medications, Substances,
Profiles, etc).
