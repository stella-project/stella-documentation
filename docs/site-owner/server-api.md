
This section describes how to access and interact with the STELLA Server API once the application is running.

The STELLA Server API is **not intended to be exposed publicly**. In a standard deployment, it is consumed **only by the STELLA App** over the internal Docker network. External clients should not interact with the server API directly.


---

## Application Access

For local testing and validation of a STELLA setup, the STELLA Server API can be accessed via the following endpoints:


- **STELLA App base URL:**  
  `http://localhost:8080`

- **Swagger / OpenAPI documentation:**  
  `http://localhost:8080/docs`


These endpoints are available only in development setups where ports are explicitly exposed.


## Swagger UI

The Swagger UI provides an interactive interface that allows users and developers to:

- inspect request and response schemas
- test API endpoints locally
- validate communication between the STELLA App and the STELLA Server
- debug experiment execution, session handling and feedback ingestion

## Endpoint Semantics

A conceptual and workflow-oriented explanation of the STELLA Server API endpoints is provided in the following documentation:

[**Site Owner → REST API Documentation**](../site-owner/server-rest.md)  

This documentation describes how individual endpoints relate to experiment execution, session lifecycle management and feedback collection.
