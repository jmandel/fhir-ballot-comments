## FHIR's JSON representation is hard to use

FHIR's JSON representation has two key properties that make it difficult for
developers to use:

1.  Object data are all "sitting behind" a property named after the object's type.
2.  Simple values are always expanded into JSON objects with "value" properites

(1) is a problem because it means that an app can't consistently reference a
resource's data (e.g. a text value) with a simple path like `resource.text.div`
-- but instead needs to do something like
`resource[Object.keys(resoruce)[0]).text.div`.  It's easily solved by moving an
object's type into the object (as a property).

(2) can be dramatically improved by representing simple values as  JSON strings.
If extensions or `_id`s are needed, they can be put alongside the values,
rather than inside them. 

There has been some discussion in the Skype FHIR implementers chat room about
how to accomplish both of these changes.  A set of concrete examples of the
"simplified" JSON representation can be seen [in this
repository](https://github.com/jmandel/fhir-js-client/tree/974099986f1b6969f809a8f2a21c9add3297c2c4/test/fixtures)

