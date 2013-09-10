## `string` and `text` search params are easily confused

The FHIR spec supports search parameters of type `string` and `text`, but it's
unclear when/how  each should be used.  For example

1. `DocumentReference` "description" search parameter is of type `text`
("Human Readable description (title)") 

2. `ValueSet` "description" search parameter is of type `string` ("Human
language description of the value set	ValueSet.description")

Are both really needed? If so, then very clear guidance is required to help
implementers choose correctly (and the existing models need to be reviewed for
conformance to that guidance). If not, then eliminate `text`.

It seems like the primary reason for using `text` is for "a long string". The
semantics of a text search are slightly different (though not fully defined),
e.g. "May match even if the separate words are found out of order."  I would
suggest that this behavior could be achieved with a modifier on "string".
