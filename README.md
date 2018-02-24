# aws-assume-role
Shell function for assuming roles in to AWS

Based on https://github.com/coinbase/assume-role with a few modifications:

* Reads GPG encrypted base credentials
* Base credentials do not need GetUser permissions
* ZSH auto completion
* Bash auto completion
* List of roles in accounts file for role auto completion
* Validates assumed role against sts:get-caller-identity

## Usage
Assuming account1 is the account alias in ~/.aws/accounts and root is the role to be assumed.
```
aws-assume-role account1 root
```

## Options

`AWS_ASSUME_ROLE_CACHE_TO_FILE`

If set to `true`, the master session credentials will be written to file and will be reused for multiple terminal sessions.

## Set up

### Requirements
1. jq - `brew install jq`
2. [AWS CLI](http://docs.aws.amazon.com/cli/latest/userguide/installing.html)

### Create credentials file
```
cat <<CREDS | gpg -e -r GPG_KEY_ID > ~/.aws/credentials.gpg
export AWS_ACCESS_KEY_ID=.....
export AWS_SECRET_ACCESS_KEY=.....
CREDS
```

### Create mfadevice file

```
echo arn:aws:iam::ACCOUNT_ID:mfa/USERNAME > ~/.aws/mfadevice
```

### Source in .zshrc or .bashrc
Add `. REPO_LOCATION/aws-assume-role`

### Create accounts file

Create an accounts file at `~/.aws/accounts`

#### Example

```
{
    "account1": {
        "id": "1234567890",
        "roles": [
            "admin",
            "ro"
        ],
        "region": "us-west-2"
    },
    "account2": {
        "id": "2234567890",
        "roles": [
            "admin",
            "ro"
        ],
        "region": "us-east-1"
    }
}
```
