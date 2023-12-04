# MVC

Model-View-Control Architecture

* Modular

## Model

* Business logic
  * Code that solves business problem
  * How the business works, business needs
  * E.g. Authentication, CRUD, comments, reviews

## Controller

* Application logic
  * Application implementation
  * Managing requests and responses

## View

* Presentation logic



## How the process works?

1. Request comes in
2. Hits a router, routes to a controller
3. Depending on request, controller might need to interact with model (data)
4. Sends back response
5. If there is a website to send back, controller interact with view before response
