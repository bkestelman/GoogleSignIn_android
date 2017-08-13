# GoogleSignIn_android
Easy to implement Google Sign In module for Android 

## Implementation 
GoogleSignIn is an Activity with a Google sign in button which authenticates a user's Google account and returns the result to its parent Activity. 

To use it from your Activity, use startActivityForResult, like so: 
```
private static final String SIGNIN_REQ = 111; // request code to identify result from GoogleSignIn (can be any number)
...
protected void onCreate(Bundle SavedInstanceState) { 
        ...        
        /* Google Sign In */ 
        // use this anywhere in your Activity, doesn't have to be in onCreate()
        Intent signinIntent = new Intent(this, GoogleSignIn.class);
        startActivityForResult(signinIntent, SIGNIN_REQ);        
        ...
}
```
And obtain the result with onActivityResult:
```
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        if(requestCode == SIGNIN_REQ) {
            if(resultCode == RESULT_OK) {
                GoogleSignInResult result = Auth.GoogleSignInApi.getSignInResultFromIntent(data);
                TextView hello = (TextView)findViewById(R.id.hello); // assumes you have a TextView in your layout called hello
                hello.setText("Hello " + result.getSignInAccount()); // test if sign in worked
            }
            else {
                // Error 
            }
        }
}
```
