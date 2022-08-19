# How to use `getToken`<a name="waf-javascript-sdk-get-token"></a>

AWS WAF requires your login requests to include the cookie named `aws-waf-token` with the value of your current token\. 

The `getToken` operation is an asynchronous SDK call that retrieves the AWS token and stores it in a cookie on the current page with name `aws-waf-token`, and the value set to the token value\. You can use this token cookie as needed in your page\. 

When you call `getToken`, it does the following: 
+ If an unexpired token is already available, the call returns it immediately\.
+ Otherwise, the call retrieves a new token from the AWS token provider, waiting for up to 2 seconds for the token acquisition workflow to complete before timing out\. If the operation times out, it throws an error, which your calling code must handle\. 

The `getToken` operation has an accompanying `hasToken` operation, which indicates whether the `aws-waf-token` cookie currently holds an unexpired token\. 

**Basic `getToken` implementation**  
The following example listing shows standard code for implementing the `getToken` operation\.

```
const login_response = await AwsWafIntegration.getToken()
    .catch(e => {
        // Implement error handling logic for your use case
    })
    // The getToken call returns the token, and doesn't typically require special handling
    .then(token => {
        return loginToMyPage()
    })

async function loginToMyPage() {
    // Your existing login code
}
```

**Submit form only after token is available from `getToken`**  
The following listing shows how to register an event listener to intercept form submissions until a valid token is available for use\. 

```
<body>
  <h1>Login</h1>
  <p></p>
  <form id="login-form" action="/web/login" method="POST" enctype="application/x-www-form-urlencoded">
    <label for="input_username">USERNAME</label>
    <input type="text" name="input_username" id="input_username"><br>
    <label for="input_password">PASSWORD</label>
    <input type="password" name="input_password" id="input_password"><br>
    <button type="submit">Submit<button>
  </form>

<script>
  const form = document.querySelector("#login-form");

  // Register an event listener to intercept form submissions
  form.addEventListener("submit", (e) => {
      // Submit the form only after a token is available 
      if (!AwsWafIntegration.hasToken()) {
          e.preventDefault();
          AwsWafIntegration.getToken().then(() => {
              e.target.submit();
          }, (reason) => { console.log("Error:"+reason) });
        }
    });
</script>
</body>
```