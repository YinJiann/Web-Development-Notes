# REST API

## API

* Application Programming Interface
* Softwrae that can be used by another software, to allow application to talk to each other



## REST

* Representational Structure
* Separate API into logical resources
* Expose structured, resource-based URLs
  * E.g. https://www.natours.com/Tours/7
    * /Tours is an endpoint
    * /7 is ID
* Use HTTP methods
* Send data as JSON
  * Difference from Object is that keys have to be string
* Stateless
  * All states are handled on the client
  * Each request must contain all information to process request
    * Authenticated
    * Current page
