**Maintain a Copy of Customers Data**
----
A consumer may periodically (every 5 minutes) consume the API to enable it (the consumer) to maintain a copy of the provider API's customers (the API represents the system of record).

- In order to enable the API consumer to ontain only those customer records that are changed since the last API call, the API mandates use of request header - `If-Modified-Since`. The consumer needs to maintain and pass the timestamp when the API call was made last time. This way, only the updated record set is returned back, thus minimising both the netwrok traffic and CPU/memory utilization for provider and consumer.
- As an API designer, it may be tempting to provide a **friendly URL** like `HTTP GET` on **`/customers/recentlyUpdated`** where the **API would return only the records updated in last 5 minutes**. Indeed with such a friendly URL, the developer experience will be greately enhanced as they won't have to maintain the timestamp. However this option is ridden with data synchronization issues. For instance, if an API call failed (for whatever reasons), the consumer will never have access to the customer records updated during that timeframe. **Thus option of providing a friendly URL was discarded.**
- The API further provides pagination. in the cases where the customer records updated since the last API call is in great number, the consumer can design their application to make use of pagination.
- The consumer can always get all the records by passing epoch time - `1970-01-01T00:00:00.090Z` as a value of `If-Modified-Since` request header. However the consumer is advised to keep these calls to minimum (only for the first time or in the event of operational issues).
  - *API Design Consideration: to deter such use of API, we may consider billing the consumer based on the amount of data returned.*
- For details on `HTTP GET` on `/customers`, please refer to the [API Documentation](API_DOCUMENTATION.md).

**Important Notes:**
  - ***Granularity of timestamp:*** The API maintains the timestamp at ***3 digit micro seconds***. The client must maintain the same level of granularity. A different granularity may result into missing the existing records or receiving the duplicate records.
  - ***isDeleted field:*** The API returns the deleted customer records with `isDeleted = 1`.
