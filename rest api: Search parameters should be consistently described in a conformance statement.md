## Search parameters should be consistently described in a conformance statement

Currently they're given names and, usually, xpaths that describe the field
being indexed.  But for search parameters that don't correspond directly to a
given xpath, we still need a consistent way to represent them in the structure
of a conformance profile.  For example, some search parameters are defined as
matching a name phonetically: these should have some structured representation
in a conformance profile, such as a combination of "xpath: ./f:name" and
"transform: phonetic-string".  The goal, to be clear, is that server developers
should be able to automate the generation of search indexers, without coding
special-case logic here and there throughout the specification. You can get a
sense of what's missing by seeing the ["spot fixes" I needed to include in my
server](https://github.com/jmandel/smart-on-fhir/blob/52bd9bfed3bddf116fb13f9dad4375da192a63a2/grails-app/conf/Config.groovy#L20)

For `composite` type search params, more is need to be define these in a
machine-readable way.  `composite` terms need **two** xpath expressions: the
first expression to identify composite roots, and a second expression relative
to the root to define which fields should be indexed. See the example "spot
fixes" above for more details.

For terms with variable data types like `value[x]`, consistent and correct xpaths are needed.  The following (which appear in the base conformance profile) cannot be used as xpath expressions to identify values for indexing:

* `f:Condition/f:onset[x]`
* `f:Observation/f:value[x]`
* `f:Group/f:characteristic/f:value[x]`
* `f:Observation/f:applies[x]`

For search parameters that cross element boundaries, specific definitions are
required. For example, several "name" search parameters are described as
matching any part of a name.  This definition needs to be made computable, with
an expanded xpath definition like `./given/@value | ./family/@value |  ...`

In addition, the search parameter definitions for a `Practitioner`'s `given`
and `family` have incorrect xpaths (they point to "name" instead of the more
granular elements.)
