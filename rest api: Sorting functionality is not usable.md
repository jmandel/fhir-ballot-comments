## FHIR's Sorting functionality is not usable

`6.11.3.1` defines a request `_sort` parameter that can be used to request
sorted results.  The interfaces isn't usable as defined for two reasons:

1.  There is no way to request ascending vs. descending order.  ("Fetch the
most recent blood pressure" is a very common query, and needs to be supported.
Similarly, "Fetch a list of patients sorted by name" is a very common query and
needs to be supported. The former is descending by date, and the latter is
ascending by name, so we need a way to specify ascending vs. descending.)

2.  The server does not need to comply with a sort requset, and doesn't even need to tell the client *whether* it complied:

> Where the search parameter returns multiple values, the lowest value will be
> used when ordering the returned records. Note that the actual sort value used
> is not returned explicitly by the server.

This makes search unreliable, because a client can't know whether the results
it has are sorted (as requested) or not.  It's important to note that even if
the client checks the sort order for the results in the first page (an O(n)
operation), it can't be sure that they are, in fact, sorted across all pages.
And when a client requests just one (most recent) result, if the sever doesn't
state whether the results is, in fact, #1 in the client's requested order, then
the client can't use the result.  So the client would never make this kind of
request.

The two proposed fixes are:

1.  Add an additional parameter indicating sorter order (e.g.
`_sort=name$ascending` or `_sort=name&_sortOrder=ascending`)

2.  Add a field to the response Atom/JSON feed indicating what sort order the
server is using (including a value for `none`).

It would also be extremely helpful to support multi-sort (tie-breakers), so
that an app could retrieve a properly-sorted list of patients by name (even if
multiple patients share a last name -- which is pretty much always the case).
The proposed fix for this is to support multiple `_sort` parameters, processed
in order.

Finally: the spec needs to clarify what it means to sort by a field that has
multiple values within a given resource (such as `value` for an `Observation`).
Is it string-based search? Pick the minimum across all values? Unspecified? No
matter what, this should be explicit.