## FHIR should use CamelCase resource names consistently (even in URLs)

FHIR has a confusing and error-inducing convention of using CamelCase for
resource names in XML, but lowercase for other contexts (like URL segements).

For example a developer must remember to fetch resources in lowercase:

```
GET /fhir/diagnosticreport
```

But when writing an xpath query over the result, must remember to use CamelCase:
```
xpath(Result, "./DiagnosticReport")
```

This convention increases implementation complexity, because systems need to
handle both conventions in different contexts.  For example, because of these
competing conventions my server needs to generate (and frequently refer to) a [
mapping between lowercase and capitalized resource
names](https://github.com/jmandel/smart-on-fhir/blob/f563c7926c330968f90af9e335e65cd6fc0de688/grails-app/services/fhir/SearchIndexService.groovy#L80).

The resource is, in fact (and more readably) called DiagnosticReport.  FHIR
should eliminate the use of lowercase path segments and adopt a single 
convention of using CamelCase everywhere. That way, clients could simply:

```
GET /fhir/DiagnosticReport
```

I see no downside and two strong upsides: consistency and readability.
