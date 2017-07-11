**Get a List of Customers**
----
  - Returns a collection of customer objects in JSON format.
  - Only the customer objects updated since the given datetime are returned.
  - If you need entire list of customer objects, pass the epoch as datetime (see request header section).
  - This API supports pagination.

**URL**
  
  /customers

**METHOD**
  
  `GET`

**REQUEST HEADERS**
   
  **Required**
   
  `If-Modified-Since=<<datetime>>`
   
  Get the customers that are updated since this datetime in the format 2017-07-18T14:30:37.090Z. To get the list of all customers (caution advised!), enter the epoch time - 1970-01-01T00:00:00.090Z.

**QUERY PARAMETERS**
   
  **Optional**
   
  `page=<<integer>>`
   
  **Default**
   
  `0`

  Skip over a number of elements by specifying a page value for the query.

**Optional**
   
  `limit=<<integer>>`
   
  **Default**
   
  `100`
   
  Limit the number of elements in the response.
   
**SUCCESS Responses**

  * **STATUS 200 OK**
    
    **Response Body**
	
    `application/json`
    
    **Sample Response**

        [
          {
            "id": 1,
            "firstName": "David",
            "lastName": "J",
            "addresses": [
              {
                 "type": "home",
                 "value": "David's home address"
              },
              {
                "type": "shipping",
                "value": "David's shipping address"
              },
              {
                "type": "billing",
                "value": "David's billing address"
              }
            ],
            "isDeleted": false
          },
          {
            "id": 2,
            "firstName": "Fibha",
            "lastName": "M",
            "addresses": [
            {
              "type": "shipping",
              "value": "Fibha's shipping address"
            },
            {
              "type": "billing",
             "value": "David's billing address"
            }
            ],
            "isDeleted": false
          }
        ]
	
  * **STATUS 304 Not Modified**
	
    NO customer records were modified since the provided `If-Modified-Since` header value. Response Body is blank in this case.

**ERROR Responses**

  * **STATUS 500 Server Error**
    
    **Response Body**
	  
    `application/json`
    
    **Sample Response**
    
        { "message": "The server was unable to complete your request at this time; please try after some time." }
