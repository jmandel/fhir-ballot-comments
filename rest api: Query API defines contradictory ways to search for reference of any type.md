## Query API defines contradictory ways to search for reference of any type

There is a contradiction in the query specification about how to search for
resource references of "any type" (that is, how to search without imposing a
restriction on the type of the referenced resource). 

In `6.11.2.1`: 

> The resource type may be omitted to search 
> all types if used with the modifier :any. 

vs. in `6.11.2.1.5`, where the following format is described:

> `name=id` the id of a resource (not including 
> the @ that goes in the URL)

Either of these approaches alone would be fine, but both together do not make sense.
