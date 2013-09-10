## Organization `partOf` search param is documented incorrectly

In `5.4.3` of the Organization model, the `partOf` property represents
organizations that the current organization **is a part of**.  But the search
paramter is described backwards:

> partof : reference
> Search all organizations that are part of the given organization

This should say "Search all organizations that the given organization is part of."
