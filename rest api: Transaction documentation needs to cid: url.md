## Transaction documentation needs to define "cid: url"

In `2.1.14`, the trandaction operation states:

>  For clarity, when the client intends a resource to have a transient identity
>  that the server must replace, it should use a cid: url on the resource. 

... but the concept of a "cid: url" is never defined. Is it a URN whose value
begins with `cid:`? This needs to be made explicit.

