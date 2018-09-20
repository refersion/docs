#Call Limits

In order to keep our service running a high level of performance, every account has a limit of requests. If you exceed your allotted limits, a 429 Too Many Requests error code will be returned and future requests may be throttled.

Each request returns a maximum of 200 results, use [Pagination](../../graphql-api/pagination/) to fetch all your results with multiple requests.
