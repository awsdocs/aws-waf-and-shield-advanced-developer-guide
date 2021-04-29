# Supported status codes for custom response<a name="customizing-the-response-status-codes"></a>

For detailed information about HTTP status codes, see [Hypertext Transfer Protocol Status Code Definitions](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) and [List of HTTP status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)\.

The following are the HTTP status codes that AWS WAF supports for custom responses\. 
+ `2xx Successful`
  + `200` – `OK`
  + `201` – `Created`
  + `202` – `Accepted` 
  + `204` – `No Content` 
  + `206` – `Partial Content`
+ `3xx Redirection `
  + `300` – `Multiple Choices`
  + `301` – `Moved Permanently`
  + `302` – `Found`
  + `303` –` See Other`
  + `304` – `Not Modified`
  + `307` – `Temporary Redirect`
  + `308` – `Permanent Redirect`
+ `4xx Client Error `
  + `400` – `Bad Request`
  + `401` – `Unauthorized`
  + `403` – `Forbidden`
  + `404` – `Not Found`
  + `405` – `Method Not Allowed`
  + `408` – `Request Timeout`
  + `409` – `Conflict`
  + `411` – `Length Required`
  + `412` – `Precondition Failed`
  + `413` – `Request Entity Too Large`
  + `414` – `Request-URI Too Long`
  + `415` – `Unsupported Media Type`
  + `416` – `Requested Range Not Satisfiable`
  + `421` – `Misdirected Request`
  + `429` – `Too Many Requests`
+ `5xx Server Error`
  + `500` – `Internal Server Error`
  + `501` – `Not Implemented`
  + `502` – `Bad Gateway`
  + `503` – `Service Unavailable`
  + `504` – `Gateway Timeout`
  + `505` – `HTTP Version Not Supported`