# aws-assume-role

## Set up

### Create credentials file
```
cat <<CREDS | gpg -e -r GPG_KEY_ID > ~/.aws/credentials.gpg
export AWS_ACCESS_KEY_ID=.....
export AWS_SECRET_ACCESS_KEY=.....
CREDS
```

### Create mfadevice file

```
echo arn:aws:iam::ACCOUNT_ID:mfa/USERNAME > ~/.aws/credentials.gpg
```

### Source in .zshrc
Add `. REPO_LOCATION/aws-assume-role`
