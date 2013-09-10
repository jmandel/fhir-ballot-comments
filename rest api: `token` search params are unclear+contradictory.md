## `token` search params are unclear/contradictory

`6.11.2.1.3` defines three scenarios for searching by token:

1.  No modifier
2.  `:code` modifier
3.  `:anyns` modifier

> Without modifier, the search will use the textual parameter
> to do a partial match on code, text or display. 

What does "The textual parameter" refer to? If it's text, why is it not placed
within quotes the way that values are supplied for `string` and `text` search
params? Furthermore, what does "do a partial match" mean?  Is it a substring
match? Is it case sensitive? (In `6.11.2.3`, "partial" means left-side only,
but the examples in `6.11.2.1.3` suggest that perhaps the meaning is that any
substring should match, as in "female" matching "male".)

It is not clear how the "no modifier" case works, especially with respect to
the examples.  In the first example, no modifier is used:

```
 GET [base-url]/patient?identifier=http://acme.org/patient/2345
```

... but the description implies that the identifier is being parsed in two
piences ("an identifier with key='2345' in the system
'http://acme.org/patient'"). This may be a mistake in the example description?
But even if it is, it points to an underlying complexity that should be
addressed.

There is also an implicit assumption that `token` params match two parameters when the `:code` modifier is used:

`namespace` + `/` + `code`.

But it's never explicitly stated how these parameters map to the fields of a
`Coding` vs. `Identifier` vs. `Code`.  That is, for a `Coding`, I presume that
a `namespace` == `system` and `code`==`code`, whereas for an indentifier,
`namespace`==`system` `code`==`key`. If this is correct, it should be stated
explicitly.

Also: can `token` search params be used for `CodeableConcept` elements?
Resources make extensive use of this (e.g. `4.15.3`: `Observation` has a token
param called "name," which searches a `CodeableConcept`). But it's not
documented in `6.11.2.1.3`.

Furthermore, `6.11.2.1.3` states that a `token` search param can be applied to
a `Code` data element. When a `token` search param is used with a `code`
element (such as the "language" search parameter for a `DocumentReference`,
which referes to the `primaryLanguage` element), can modifieres be used? If so,
what do they mean?

Finally, the specification should allow a reader to dermine which of the
following four queries is valid (my buest guess would be "all of them"):

```
GET [service-url]/diagnosticorder/search?status=received
GET [service-url]/diagnosticorder/search?status:code=received
GET [service-url]/diagnosticorder/search?status=http://hl7.org/fhir/diagnostic-order-status/received
GET [service-url]/diagnosticorder/search?status:code=http://hl7.org/fhir/diagnostic-order-status/received
```