
# Sign in With Apple (JS, Vue)

Documentation about Apple login with Javascript and Vue JS both.


## Acknowledgements

 - [Apple Login Official Document](https://developer.apple.com/documentation/sign_in_with_apple/sign_in_with_apple_js/configuring_your_webpage_for_sign_in_with_apple)


## Usage/Examples

Add CDN JS of apple login

```javascrip
<script type="text/javascript" src="https://appleid.cdn-apple.com/appleauth/static/jsapi/appleid/1/en_US/appleid.auth.js"></script>
```

in your main html file or header.

---
**For javascript**

add meta tags for config variable like below

```javascrip
<head>
    <meta name="appleid-signin-client-id" content="[CLIENT_ID]">
    <meta name="appleid-signin-scope" content="[SCOPES]">
    <meta name="appleid-signin-redirect-uri" content="[REDIRECT_URI]">
    <meta name="appleid-signin-state" content="[STATE]">
    <meta name="appleid-signin-nonce" content="[NONCE]">
    <meta name="appleid-signin-use-popup" content="true"> <!-- or false defaults to false -->
</head>
```
then add below code when you want to add apple sign in button

```javascrip
<div id="appleid-signin" data-color="black" data-border="true" data-type="sign in"></div>
```
---
**Important**

*The host specified in appleid-signin-redirect-uri must include a domain name. It can’t be an IP address or localhost.*

You can also configure the authorization object using the 
JavaScript APIs and display a Sign in with Apple button, as in the following example:

---

```javascrip
<html>
    <head>
    </head>
    <body>
        <script type="text/javascript" src="https://appleid.cdn-apple.com/appleauth/static/jsapi/appleid/1/en_US/appleid.auth.js"></script>
        <div id="appleid-signin" data-color="black" data-border="true" data-type="sign in"></div>
        <script type="text/javascript">
            AppleID.auth.init({
                clientId : '[CLIENT_ID]',
                scope : '[SCOPES]',
                redirectURI : '[REDIRECT_URI]',
                state : '[STATE]',
                nonce : '[NONCE]',
                usePopup : true //or false defaults to false
            });
        </script>
    </body>
</html>
```
---
**Note**

*Use space separation when requesting multiple scopes; for example, "scope=name email".*

**Handle the Authorization Response**

If you use the pop-up option, your app sends the authorization information to Apple when the user clicks the Sign in with Apple button. After Apple’s server processes the authorization request, it dispatches a DOM Event containing the results of the authorization: AppleIDSignInOnSuccess on success, orAppleIDSignInOnFailure on failure.

To handle the response, add an event listener:

```javascrip
//Listen for authorization success
document.addEventListener('AppleIDSignInOnSuccess', (data) => {
     //handle successful response
});
//Listen for authorization failures
document.addEventListener('AppleIDSignInOnFailure', (error) => {
     //handle error.
});
```

---

If the signIn function started the authorization process, the function returns a promise object that resolves if the authorization succeeds, or rejected if fails.

Here is an example of how to handle the response when using the signIn function.

```javascrip
try {
     const data = await AppleID.auth.signIn()
} catch ( error ) {
     //handle error.
}
```
---

*Upon authorization success, the server returns the following data object:*
```json
{
     "authorization": {
       "state": "[STATE]",
       "code": "[CODE]",
       "id_token": "[ID_TOKEN]"
     },
     "user": {
       "email": "[EMAIL]",
       "name": {
         "firstName": "[FIRST_NAME]",
         "lastName": "[LAST_NAME]"
       }
     }
}
```

---

**Note**

*The user object will only be presented the first time the user authorizes the application.*

---
----------
----------
## For Vue JS
Add CDN JS of apple login in your index or main html file

```javascrip
<script type="text/javascript" src="https://appleid.cdn-apple.com/appleauth/static/jsapi/appleid/1/en_US/appleid.auth.js"></script>
```

Now add a button or any tag that you want to perform apple login on click.

```html
<a href="#" class="btn btn-block theme-btn-blank" v-on:click="doAppleLogin">
    Sign in with Apple
</a>
```

Now we have to add **doAppleLogin** method in methods section.

```javascrip
methods:{
    async doAppleLogin(){
            AppleID.auth.init({
                clientId : [APPLE_CLIENT_ID],
                scope : [APPLE_SCOPE], // like email name. jsut add space between two scope
                redirectURI : [APPLE_REDIRECT_URI],
                state : [APPLE_STATE], // uuid or unique key
                usePopup : true //or false defaults to false for popup login
            });

            try {
                const data = await AppleID.auth.signIn();
                // do something with response
            } catch ( error ) {
                // Handle error
            }
        },
}
```
## Authors

- [@amit_m13](https://twitter.com/amit_m13)

