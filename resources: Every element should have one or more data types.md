## Every element should have one or more data types.

Nearly all FHIR resources are modeled so that each element is defined with
respect to FHIR's base data types.  But a handful of resources use a notation
where an element's type is defined with "Content as for..." and a reference
to some other path.  


For example, this $efinition of `item.event` from the `DiagnosticOrder`
profile XML:

```
      <path value="DiagnosticOrder.item.event"/>
      <definition>
        <short value="Events specific to this item"/>
        <formal value="A summary of the events of interest that have occurred as this item of the request is processed."/>
        <min value="0"/>
        <max value="*"/>
        <type>
          <code value="**@DiagnosticOrder.event**"/>
        </type>
        <isModifier value="false"/>
      </definition>
```

1.  This description ("A summary..") doesn't show up in the DiagnosticOrder
summary HTML representation, and the type is rendered as "Content as for...e

2.  I couldn't figure out where the `@` notation is documented in the spec. (Is
it?) It appears to add substantially to implementation complexity by requiring
that snippets of element definitions be embeddable within other element
definitions. FHIR already provides resources, complex datatypes, and simple
datatypes. 

Furthermore, this notation appears to violate the following principle:

> The elements are assigned one or more types. 
> All of the types are defined in the data types 
> except for "Resource" and "Narrative"

The notation here adds a wrinkle to this simple principle, by saying
(effectively), "a third option is for elements to point ad-hoc to other
elements and borrow their structure as needed."

Since this modeling feature is rarely used, and imposes a substantial
complexity burden, I strongly advocate for removing this representation
and just sticking to FHIR's stated model whereby every element is defined
in terms of a FHIR data type.

When this behavior is needed, intermediate "data type" defintions should be
created.
