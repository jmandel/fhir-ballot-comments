## Validation API has an unused `id` parameter

The validate API defines the following POST URL template:

`[service-url]/[resourcetype]/validate/{@id}`

But `{@id}` does not appear to be used (or at least it's undocumented).  The
URL should be changed to:

`[service-url]/[resourcetype]/validate`
