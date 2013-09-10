## Need support for non-integer numerical searches

There is a serach parameter type defined for "integer," but not for other
numerical data.  The spec should clarify how to search for float-type numerical
data.  (It's not clear that we need different search parameter types for different
types of numbes; probably a single "number" parameter type would suffice.

In addition, the following language from `6.11.2.1.2` is unclear:

> The prefixes >, >=, <=, and < may be used on the parameter value

*How* are these prefixes used? An example would help.