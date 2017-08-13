# GoogleSignIn_android
Easy to implement Google Sign In module for Android 

## Implementation 
GoogleSignIn is an Activity with a Google sign in button which authenticates a user's Google account and returns the result to its parent Activity. 

To use it from your Activity, use startActivityForResult, like so: 
```
private static final String SIGNIN_REQ = 1; // request code to identify result from GoogleSignIn (can be any number)
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
                GoogleSignInResult result = Auth.GoogleSignInApi.getSignInResultFromIntent(data);
                TextView hello = (TextView)findViewById(R.id.hello);
                hello.setText("Hello " + result.getSignInAccount());
        }
}
```

### Gradle
The module build.gradle is included in this repository. The only special line is: 
```compile 'com.google.android.gms:play-services-auth:11.0.4'```
Just keep the version up to date. 

In your root/project build.gradle, you need to add: 
```classpath 'com.google.gms:google-services:3.1.0'``` to dependencies, and
```
maven {
            url "https://maven.google.com"
        }
```
to repositories (right after jcenter())

### Authenticating your client with Google and Obtaining Configuration Files
Follow these steps to set up your app to use Google Sign In: https://developers.google.com/identity/sign-in/android/start-integrating

### server_client_id
Set the value of server_client_id in your values/strings.xml if you plan on sending a GoogleID token to a backend server. You can obtain the appropriate value by following the directions in the link above, under the section "Get your backend server's OAuth 2.0 client ID".

