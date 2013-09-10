## Validation API does not explain app-specific conformance profiles

Regarding validation, the HTTP API specification states:

> The content is first checked against the general 
> specification and against the conformance profile 
> that applies to the application"

But the spec doesn't define how application-specific conformance profils here
is the idea of app-specific conformance described?  What is an app-specific conformance profile?  How does the server know which one applies to a given app? How does the server know which app is making a given request in the first place? 

It would be simpler and more robust to define a fixed, consistent validation API
where any necessary parameters were passed in explicitly with well-specific
parameter names or headers.
