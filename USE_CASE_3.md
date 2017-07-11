**Extending the API to Support Future Resources**
---
The effective use of RAML used to design this API makes it easy to extend it to support the future resources such as products and orders.

### Extracting the Patterns in API Definition 
The `/customers` resource is of collection type. Similarly any future resources we may add to API, like `/products` and `/orders`, would be of type collection. When it comes to collections, there are specific methods that a good API would allow, e.g. `GET` and `POST`. Those methods will be applicable to all collections. Similarly, when it comes to method definitions, we could see patterns that could be extracted. For instance, a good API will provide pagination for `GET` on collection resource.

There are various features in RAML 1.0 that help extract such patterns. This in turn, enables API to be easily extended to incorporate future resources. This API definition makes use of some of these features including `types`, `resourceTypes`, and `traits`.

### resourceTypes

There are two resource types `collection` and `collectionItem`. These resource type would be applicable to future resources like products and orders.

### traits

I have created a trait - `pageable`. This trait would be applicable to `GET` on `/products` and `/orders`

### Structure of the RAML project

I have structured the project in such a way that adding future project files will be easy.
