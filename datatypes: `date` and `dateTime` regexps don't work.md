## `date` and `dateTime` regexps don't work

The definitions of `date` and `dateTime` data types use regular expression that
are problematic.

* I'm not sure what syntax is being used to represent these.  For example, what
  does `:-?` mean?  A link to a reference explaining the syntax would help
  here.

* The expression `([1-9][0-9]{3,}|0[0-9]{3})` has a misplaced comma and will
  mistakenly match dates with *at least three* digits after a `1-9` (e.g.
  `2012359-04-12` would match).

* If a time zone is forbidden for `date` values ("there is no time zone"), then
  why does the regular expression have a matcher for time zones? 

* The time zone regular expression component is
  `((0[0-9]|1[0-3]):[0-5][0-9]|14:00))`.  This expression allows invalid
  timezone offsets like `+05:14:00`.

Furthermore, some of the constraints imposed by FHIR's `dateTime` datatype
simply cannot be captured in a regular expression.  For example, the idea that
a timezone is required when hours are supplied, an optional otherwise cannot be
captured in a regular expression (assuming that it's **also** illegal for a
dateTime to have *two* timezones).
