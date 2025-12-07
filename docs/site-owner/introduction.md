# Introduction

This page provides an overview of the STELLA infrastructure from the site owner’s perspective and explains the roles of the STELLA App and the STELLA Server.

## What is the STELLA App?

The **STELLA App** is a multi-container application deployed at partner sites. Its primary responsibilities are to:

- serve experimental ranking and recommendation results
- collect user interaction and feedback data
- forward collected feedback to the central STELLA Server

The app is composed of multiple microservices built using the STELLA micro-template and is typically deployed using **Docker Compose**. It functions as the execution and experimentation layer within the STELLA ecosystem.

## What is the STELLA Server?

The **STELLA Server** is the central component of the STELLA infrastructure. It is responsible for:

- user and role administration
- providing access to administrative and analytical dashboards
- coordinating and managing STELLA App updates
- hosting the central database that stores user interaction logs and experimental data

While the STELLA App operates locally at partner sites, the STELLA Server serves as the aggregation, coordination and persistence layer for the entire system.


## What is a STELLA Microservice?

A **STELLA microservice** is a Dockerized experimental ranking or recommendation system that integrates directly with the STELLA App.

STELLA supports **only Dockerized microservices** for experimental systems. Each system runs as an independent container and exposes a well-defined REST API that the STELLA App uses at runtime to request rankings or recommendations.

Using microservices enables:

- dynamic, real-time generation of rankings and recommendations
- experimentation without being limited to pre-defined queries or datasets
- isolation between experimental systems
- reproducible deployment and evaluation via Docker

To simplify integration, STELLA provides a **microservice template** that defines the required API contract, request and response formats, and deployment structure. Experimenters adapt this template to wrap their experimental logic and deploy it alongside the STELLA App using Docker Compose.

This microservice-based approach is the **only supported mechanism** for integrating experimental systems into the STELLA infrastructure.









