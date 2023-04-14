# AWS WAF JavaScript SDK<a name="waf-javascript-sdk"></a>

You can use the AWS WAF JavaScript SDK to implement AWS WAF application integrations in your browsers and other devices that execute JavaScript\. The JavaScript SDK lets you manage token authorization, and to include the tokens in the requests that you send to your protected resources\. By using the SDK, you ensure that the remote procedure calls by your client contain a valid token\. Additionally, when this integration is in place on your application's pages, you can implement mitigating rules in your web ACL, such as blocking requests that don't contain a valid token\.

The following listing shows basic components of a typical implementation of the JavaScript SDK in a web application page\. 

```
<head>
<script type="text/javascript" src="Web ACL integration URL/challenge.js" defer></script>
</head>
<script>
const login_response = await AwsWafIntegration.fetch(login_url, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: login_body
  });
</script>
```