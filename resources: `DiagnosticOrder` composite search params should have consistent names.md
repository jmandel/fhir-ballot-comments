## `DiagnosticOrder` composite search params should have consistent names

In `4.17.3`: There's currently one search parameter called `#item-status-date`,
and another called `status-date`.  The latter should be re-named to
`#event-status-date` for consistency and to avoid confusion about its purpose.
