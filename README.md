# System Of Records (SOR) API
> Best Practices for RESTful API Design using RAML. Sample implementation using Mulesoft Anypoint Studio.

This is an example API design using RAML. The implementation of this API using Mulesoft Studio is coming soon. In its current state, the project demonstrates the following:

- Best practices for RESTful API design.
- Use of built in aspects of the HTTP protocol (status codes, headers, etc.).
- Use of various RAML features.
- Performance considerations when designing the API for mobile applicationsl; that is feficient use of the network.
- Sample implementation of the API using Mulesoft Anypoint Studio.

This API, in its present state, contains a single resource `/customers`. The operations allowed on the `/customers` resource are listed below.  For more details see [API Documentation](API_DOCUMENTATION.md).

- List Customers
  - `HTTP GET`
  - The request must contain `If-Modified-Since` header to specify the datetime. The records updated since this datetime will be returned.
  - In addition to the request header `If-Modified-Since` to obtain only a subset of customers, this operation supports pagination. For more details see [Use Case 1: Maintain a Copy of Customers Data](USE_CASE_1.md).
- Create a New Customer
  - `HTTP POST`
- Update a Customer
  - Supports both `HTTP PATCH` and `HTTP PUT`.
  - `HTTP PATCH` is supported to support the performance optimization needed for mobile applications. For more details see [Use Case 2: API Usage Optimization for Mobile Applications](USE_CASE_2.md)
- Remove a Customer
  - `HTTP DELETE`

## Getting Started

You can use this project in various ways:

- Import this project into Mulesoft Anypoint Studio. This project used Apache Derby standalone database. In order to run this project, you will need to [Setup Apache Derby](DERBY_SETUP.md).
- Use the api.raml (and the subdirectories/files) in your API design. This project makes use of RAML features making it easy to extend it to support future resources such as products and orders. For more details see [Use Case 3: Extention of this API to Support Future Resources](USE_CASE_3.md).
- Create your own Mulefost project by importing api.raml using APIkit.
- Create an API in API Designer (a part of Mulesoft Anypoint Platform) and import it into your Mulesoft project using APIkit.

### API Definition

A detailed API definition is provided at:

- [API Documentation](API_DOCUMENTATION.md)

### Commentary on API Usage

Detailed commentaries on various use cases of this API are provided at:

- [Use Case 1: Maintain a Copy of Customers Data](USE_CASE_1.md)
- [Use Case 2: API Usage Optimization for Mobile Applications](USE_CASE_2.md)
- [Use Case 3: Extending the API to Support Future Resources](USE_CASE_3.md)
