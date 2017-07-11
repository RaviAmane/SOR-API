Design Decisions
---
Followin are design decisions I am made along with my rational.

#### 1) Use of `If-Modified-Since` Request Header instead of a Friendly URL `/customers/recentlyUpdated`
In order to enable the API consumer to ontain only those customer records that are changed since the last API call, the API mandates use of request header - `If-Modified-Since`. The consumer needs to maintain and pass the timestamp when the API call was made last time. This way, only the updated record set is returned back, thus minimising both the netwrok traffic and CPU/memory utilization for provider and consumer.

As an API designer, it may be tempting to provide a **friendly URL** like `HTTP GET` on `/customers/recentlyUpdated` where the **API would return only the records updated in last 5 minutes.** Indeed with such a friendly URL, the developer experience will be greately enhanced as they won't have to maintain the timestamp. However this option is ridden with data synchronization issues. For instance, if an API call failed (for whatever reasons), the consumer will never have access to the customer records updated during that timeframe. **Thus option of providing a friendly URL was discarded.**

For a detailed discussion calling `HTTP GET` on `/customers`, please see [Use Case 1: Maintain a Copy of Customers Data](USE_CASE_1.md).

#### 2) A Case for using `billingAddress` and `shippingAddress` instead of `addresses` in customer object
For customer object, instead of array of "addresses", I would have prefered to use specific address fields, e.g. `billingAddress` and `shippingAddress`.

*Pros:*

This would give more granualarity especially needed for the network optimization for mobile applications. With this approach the API client could get and update the individual address instead of array of objects as is presently the case.

*Cons:*

This would make the object regid; i.e. customer can not hold any other address than the two.
