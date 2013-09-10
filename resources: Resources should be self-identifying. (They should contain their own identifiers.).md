## Resources should be self-identifying. (They should contain their own identifiers.)

The FHIR API is highly unusual and perhaps unique in not exposing
self-identifying resources.  That is, if a client issues `GET /patients/@123`,
the response is a resource that **doesn't identify itself as Patient 123**.
The identifer `123` doesn't appear anywhere in the response body.

I haven't seen an example of another REST API, in healthcase or elsewhere, with
this property. Normally when you GET a resource, the response contains
(directly, in-line) an identifier for the resource you just "got".  This is the
case when you (to pick a few):

### In healthcare: 
* GET [any HealthVault "Thing"](http://msdn.microsoft.com/en-us/library/dn312136.aspx#thingIdentifiers)
* GET an [Aetna CarePass Medication](https://developer.carepass.com/docs/carepass/medications/health_medications_medicationId_GET#sampleResponse)
* GET an [Indivo Problem](http://docs.indivohealth.org/en/2.0/api-reference.html#get--records-{0}-{1}-)

### Elsewhere on the web:
* GET a [Facebook user](https://graph.facebook.com/btaylor)
* GET a [Twitter message](https://dev.twitter.com/docs/api/1/get/statuses/show/%3Aid)
* GET a [Google+ message](https://developers.google.com/+/api/latest/people/get#examples)

To re-state: every one of these examples returns a payload that includes a
resource identifier embedded in the resouce.

**The FHIR API does not.**

This leads to serious **complexity and confusion for client apps**. Instead of
just "banking" or storing response content, an app needs to keep track of
where/how it obtained the content (because the content is not
self-identifying).  It complicates app logic and presents an **opportunity for
error** (accidental association, in app-level logic, of a resource with an
incorrect identifier).

The current FHIR convention (non-self-identifying resources) is especially
confusing because resources **do**, by necessity, contain the identifiers of
things they link to.

The proposed fix is to include an identifier in each resource body. (Currently,
this is supported for contained resources, but it should be supported and
required universally.)
