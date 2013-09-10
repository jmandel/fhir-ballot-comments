## "Feed" should say "Entry" in transaction definition?

In `1.10.2.2.1`, I believe the following text:

> If the feed.id for the resource that contains the link above is
> http://example.org/, then the absolute URL is
> http://example.org/organization/@23. 

... is suppose to say "`entry.id`" instead of "`feed.id`".  (If `feed.id` is
correct, then further explanation is needed -- I haven't seen any FHIR
reference servers that use such a `feed.id`. Grahame's server, for instance,
has a GUID for its `feed.id`.)

