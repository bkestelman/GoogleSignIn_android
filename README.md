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

### Authenticating your client with Google
This is required to use Google Sign In: https://developers.google.com/android/guides/client-auth

### server_client_id
This is required in your values/strings.xml if you plan on sending a GoogleID token to a backend server. You can obtain one through the Google Console Developers API (look for Web Client ID under OAuth 2.0).

I can't think of why you wouldn't need this, but if that's the case and you really don't want to set it up, you must comment out this line of code from GoogleSignIn.java:
``` .requestIdToken(getString(R.string.server_client_id)) ```
