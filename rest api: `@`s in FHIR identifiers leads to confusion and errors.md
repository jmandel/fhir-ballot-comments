## `@`s in FHIR identifiers leads to confusion and errors

The FHIR HTTP API uses logical identifiers and URLs that have `@` signs
embedded in various places. It's an unusual pattern in Web APIs (though not
unique) and it leads to confusion and predictable errors.

For example, I found a bug in Grahame's reference server where `@` signs were
incorrectly positioned in server-assigned identifiers.  This bug would never
have occurred if FHIR simply didn't use `@`s in its URLs.

Part of what makes this convention so hard to work with is that it's not
universal.  For example, while a patient resource's "logical identifier" might
be `patient/@123`, a search parameter referencing that patient would be passed
as `subject=patient/123` (no `@`).  Also when searching by identifier, no `@`
is used, as in `subject._id=123`.

### This is a burden for documentation
The spec has to make note about when `@` is
neeed vs. other cases when it must be omitted ("not including the @ that goes
in the URL").

### This is also a burden for client developer

If I'm building a client that wants to resolve references, I might find the
following in a Patient instance:

```
<link>
  <type value="Patient"/>
  <reference value="patient/@pat2"/>
</link>
```

Now if I want to find other patients that are *also* linked to `@pat2`, I need
to do (pseudocode):

```
var ref = xpath(patient, "./link/reference/@value").replace("@", "");
GET /patient/search?link={ref}
```

That's complicated and -- most important -- very easy to get wrong (most likely
by skipping the "replace" step).  We wouldn't have these problems if FHIR URLs
didn't include `@` signs.
