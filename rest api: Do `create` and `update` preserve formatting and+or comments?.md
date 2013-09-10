## Do `create` and `update` preserve formatting and+or comments?

FHIR's definition for `create` and `update` operations should specify how
payloads are parsed.  Specifically, it should address the question of whether
formatting and XML comments need to be preserved and visible across future
`read` and `search` operations.  I would suggest that a FHIR server should NOT
need to preserve formatting and comments (but the spec should make it explicit
either way).
