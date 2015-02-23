# awstoken

Retrieve credentials from STS to allow AWS usage with an MFA (multi-factor authentication) code.

This assumes your account is set up with an MFA device.

There are probably many like this, but this one is what I use.

*You'll need to set your own account id in the script.*
That could be extracted as an environment variable, but mine doesn't change, so I set it in the script.  It's at the top.

## Usage 
```
awstoken 123456 [profile_name]
```

## Variables affected

awstoken works by acquiring temporary credentials and resetting your shell environment variables. This is a list of the affected variables. Since the AWS CLI and the EC2 tools use different variables, both are updated.

-      AWS_ACCESS_KEY_ID
-      AWS_SECRET_ACCESS_KEY
-      AWS_SESSION_TOKEN
-      AWS_ACCESS_KEY
-      AWS_SECRET_KEY
-      AWS_DELEGATION_TOKEN

## Configuration
The awstoken function respects the following variables

-      AWS_TOKEN_USER - The username of the IAM account we request tokens for. Defaults to $USER, the local username.
-      AWS_TOKEN_PROFILE - The aws-cli profile used for access/secret keys

The AWS_TOKEN_PROFILE can also be specified as an optional second argument, to enable switching between profiles easily.
   
