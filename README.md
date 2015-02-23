# awstoken

Retrieve credentials from STS to allow AWS usage with an MFA (multi-factor authentication) code.

This assumes your IAM account is set up with an MFA device.

There are probably many like this, but this one is what I use.

*You'll need to set your own account id in the script.*

That could be extracted as an environment variable, but mine doesn't change, so I set it in the script.  It's at the top.  The account ID is necessary for the STS call, because it uses an ARN (Amazon Resource Name) to identify the user.

## Usage 
```
awstoken 123456 [profile_name]
```
This is a shell function.  It's written as a function, because the entire purpose is to rewrite shell environment variables, and a subshell won't be able to do that.  You should arrange for "awstoken" to be sourced by your shell (I use a .bashrc.d directory for this sort of snippet). If you'd like, you could also simply paste it into the bottom of your main shell resource file (.bashrc/.zshrc).

## Variables affected

awstoken works by acquiring temporary credentials and resetting your shell environment variables. This is a list of the affected variables. Since the AWS CLI and the EC2 tools use different variables, both are updated.

-      AWS_ACCESS_KEY_ID
-      AWS_SECRET_ACCESS_KEY
-      AWS_SESSION_TOKEN
-      AWS_ACCESS_KEY
-      AWS_SECRET_KEY
-      AWS_DELEGATION_TOKEN

*Be aware that a failed STS token will leave these variables in an unusable state.  If that happens, resubmit a correct code.*

## Configuration
The awstoken function respects the following variables

-      AWS_TOKEN_USER - The username of the IAM account we request tokens for. Defaults to $USER, the local username.
-      AWS_TOKEN_PROFILE - The aws-cli profile used for access/secret keys

The AWS_TOKEN_PROFILE can also be specified as an optional second argument, to enable switching between profiles easily.

*The account ID provided in the script is bogus.  You must edit it to use your own account ID.*
