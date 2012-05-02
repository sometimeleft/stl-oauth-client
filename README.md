# STLOAuthClient = AFNetwork + OAuth 1.0a
## What is this?
An OAuth 1.0a client using AFNetwork, ARC enabled.
## Does it work?
It was tested against Twitter, Readability and Tumblr APIs.
## I'm in a hurry (TL:DR mode), can you explain in 3 lines?
Add the [AFNetwork](https://github.com/AFNetworking/AFNetworking/) and both files, call `- setConsumerKey:secret:` and `- setAccessToken:secret` to set the signing parameters and all calls after that will be signed. If you want a non-authenticated call, use either `- unsignedRequestWithMethod:path:parameters:` or `- setSignRequests(NO)`.
## How can I install it?
Install [AFNetwork](https://github.com/AFNetworking/AFNetworking/) and add the `STLOAuthClient.m` and `STLOAuthClient.h`.
## Can I use CocoaPods to install it?
Not yet, I don't know how to make a pod.
## Ok, now it is installed and compiles correctly, how to use it?
1. The first thing to do is feeding a new object with the `consumerKey` and `consumerSecret` (the values provided by the service), you can use `- initWithBaseURL:consumerKey:secret:` (it is the designated initializer) or `- setConsumerKey:secret:`;
2. Make a call using `- getPath:parameters:success:failure:`, `- postPath:parameters:success:failure:`, `- putPath:parameters:success:failure:`, `- deletePath:parameters:success:failure:` or `- requestWithMethod:path:parameters:`;
* There is a boolean property called `signRequests`, allowing you to control when a request is signed or not, but you can also use `- unsignedRequestWithMethod:path:parameters:` / `- signedRequestWithMethod:path:parameters:`;
* If you need to set the realm, there's a property called `realm`. If you don't set it, it assumes the value of `baseURL`.

## Example?
Sure :  

```objective-c
STLOAuthClient *client = [[STLOAuthClient alloc] initWithBaseURL:[NSURL URLWithString:@"https://www.readability.com/api/rest/v1/"]];
[client setConsumerKey:CONSUMER_KEY secret:CONSUMER_SECRET];
NSDictionary *params = [NSDictionary dictionaryWithObjectsAndKeys:
                        username, @"x_auth_username", 
                        password, @"x_auth_password",
                        @"client_auth", @"x_auth_mode",
                        nil];

[client getPath:@"oauth/access_token/" parameters:params success:^(AFHTTPRequestOperation *operation, id responseObject) {
  NSLog(@"SUccess %@", operation.responseString);
} failure:^(AFHTTPRequestOperation *operation, NSError *error) {
  NSLog(@"Failure, %@", error);
}];
                          
```

## What the heck with the space after the '-'?
Hey, I like it, don't change it. 

## License?
BSD.

## Thanks (and extra licenses)
There are some functions / methods based on 3rd party code :

* `ASIHTTPRequest+OAuth.m` — Created by Scott James Remnant on 6/1/11.
* `NSString+URLEncode.h` — Created by Scott James Remnant on 6/1/11.
* `AFOAuth2Client.m` — Copyright (c) 2011 Mattt Thompson (http://mattt.me/).
