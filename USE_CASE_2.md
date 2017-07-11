**API Optimization for Mobile Applications (Efficient Network Usage)**
---
In order to improve the performance for mobile applications, the API uses partial resources. Submitting and returning partial resources reduces the network traffic thus optimizing the API for mobile applications.

### Receive Partial Resource for GET on /customers/{customerId}
  - For `HTTP GET` operation, specify the response fields by using `fields` query parameter. This way only the required fields are returned optimizing the network traffic.
### Update Only Select Fields with PATCH
  - Use of `HTTP PATCH` operation where only the fields that need changing are sent over the network.
  - In addition, like GET operation, specify the response fields by using `fields` query parameter. This way only the required fields are returned over the network. No fields are returned if this query parameter is not passed; in that case HTTP code `204 No Content` is returned further optimizing the network traffic.
  - In order to enhance the developer experience however, we also provide `HTTP PUT`.

## Examples

The following is a series of examples that demonstrates how the use of query parameter and PATCH reduces the network traffice; thus optimizing the mobile applications.

### 1) Simple GET Request - Receive Full Resource

This HTTP GET request omits the `fields` query parameter. the API returns the full resource.

**Request**

`GET /api/v1/customers/123456`

**Response**

*HTTP Status*
  
`200 OK`
  
*Response Body*
  
```
{
  "id": 123456,
  "firstName": "David",
  "lastName": "J",
  "shippingAddress": "David's shipping address"
  "billingAddress": "David's billing address"
  "isDeleted": false
}
```

### 2) Optimized GET Request using Query Parameter - Receive Partial Resource

This HTTP GET request adds the `fields` query parameter. The API returns the partial resource.

**Request**

`GET /api/v1/customers/123456?fields=firstName,lastName`

**Response**

*HTTP Status*
  
`200 OK`
  
*Response Body*
  
```
{
  "firstName": "Jon",
  "lastName": "Doe"
}
```

### 3) Update Partial Object with PATCH Request

You can also avoid sending unnecessary data when modifying resources. To send updated data only for the specific fields that you’re changing, use the `HTTP PATCH` verb. The example below shows how using patch minimizes the data you need to send to make the update.

**Request**

`PATCH /api/v1/123456`

*Request Body*

```
{
  "firstName": "Jon",
  "lastName": "Doe"
}
```

**Response**

*HTTP Status*
  
`200 OK`
  
*Response Body*
  
```
{
  "id": 123456,
  "firstName": "Jon",
  "lastName": "Doe",
  "shippingAddress": "Jon's hipping address"
  "billingAddress": "Jon's billing address"
  "isDeleted": false
}
```
### 4) Update Partial Object with PATCH Request and Receive null Response by using fields Query Parameter

The example below shows how in addition to using PATCH, you could use `fields` query parameter to recieve null response thus further reducing the netwrok traffic. In the below example, we are passing fields=null. If you need, you may pass the field names to get those back in the response.

**Request**

`PATCH /api/v1/123456?fields=null`

*Request Body*

```
{
  "firstName": "Jon",
  "lastName": "Doe"
}
```

**Response**

*HTTP Status*
  
`204 No Content`
  
*No Response Body*
