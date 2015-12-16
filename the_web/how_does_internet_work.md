## How does internet work?

### Request–Response
Request-Response is the most basic and common of the client-service interaction patterns. Accessing a web page is an example of request–response communication. Request–response is one of the basic methods computers use to communicate with each other, in which the first computer sends a request for some data and the second computer responds to the request. Usually, there is a series of such interchanges until the complete message is sent. This pattern is typically implemented in a purely synchronous fashion, as in web service calls over HTTP, which holds a connection open and waits until the response is delivered or the timeout period expires. 

This is very important to understand when building applications that will run over internet: the server forgets about who asked for what when a request have been served. 


