## The FHIR REST API should recommend CORS and Conformance should allow declaration

To support browser-based client applications, the FHIR REST API should
recommend that servers [enable cross-origin resource
sharing](http://enable-cors.org/)  for query and retrieval operations.  

Furthermore, a conformance profile should provide a place for servers to
declare whether or not they support CORS (overall, or for each operation).
