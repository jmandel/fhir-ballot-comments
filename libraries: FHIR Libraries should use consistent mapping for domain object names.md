## FHIR Libraries should use consistent mapping for domain object names

In the Java client library, domain objects that are sub-classes of
`org.hl7.fhir.instance.model.Element` should have a consistent mapping between
domain class names and FHIR resource/datatype names. This is mostly true but
`String_` and `List_` break the pattern and require special cases when trying
to perform automatic mapping.  For example, my server-side code is 
**more complex** becaues it has to include [this kind of
logic](https://github.com/jmandel/smart-on-fhir/blob/f563c7926c330968f90af9e335e65cd6fc0de688/grails-app/services/fhir/SearchIndexService.groovy#L51)
