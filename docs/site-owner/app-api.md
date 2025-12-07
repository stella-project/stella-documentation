
This section describes how to access and interact with the STELLA App API once the application is running.

---

## Application Access

The STELLA App exposes its REST API on the following endpoints:

- **STELLA App base URL:**  
  `http://localhost:8000`

- **Swagger / OpenAPI documentation:**  
  `http://localhost:8000/docs`



## Swagger UI

The Swagger UI provides an interactive interface that allows users and developers to:

- inspect request and response schemas
- test API endpoints directly from the browser
- trigger experimental workflows such as session creation, ranking and recommendation requests

The Swagger interface reflects the current API version exposed by the running STELLA App instance.


## Endpoint Semantics

A conceptual and workflow-oriented explanation of the STELLA App API endpoints is provided in the following documentation:

[**Site Owner → REST API Documentation**](../site-owner/app-rest.md)  

This documentation describes how individual endpoints relate to experiment execution, session lifecycle management and feedback collection.
