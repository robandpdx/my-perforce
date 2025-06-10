# my-perforce

Notes on setting up a perforce (p4) server.

## Downloading p4 clients
* [p4 cli client](https://portal.perforce.com/s/downloads?product=Helix%20Command-Line%20Client%20%28P4%29)
* [P4V visual client](https://portal.perforce.com/s/downloads?product=Helix%20Visual%20Client%20%28P4V%29)

## Deploy p4 server to AWS
Follow the instructions in [this video](https://youtu.be/gLSc9Qpe_ww?si=eSGZHU9ZLWGoPvZ4).  
This is the [link to the cloudformation template](https://perforce-cf-templates.s3.amazonaws.com/releases/enhanced-studio-pack-latest.yaml):
```
https://perforce-cf-templates.s3.amazonaws.com/releases/enhanced-studio-pack-latest.yaml
```

## Connect the client
Once the cloudformation stack deploy has completed, get the `P4CommitPublicIP` from the output of the cloudformation stack. You'll need this to connect to the server.

Set the value of `P4PORT` environment variable to the following:
```bash
export P4PORT="ssl:<P4CommitPublicIP>:1666"
```

Use this value also to connect using [P4V](https://portal.perforce.com/s/downloads?product=Helix%20Visual%20Client%20%28P4V%29).  

Default user is `perforce` and the password is the value of `HelixCodeInstanceID` from the stack outputs.

## Notes
[This video show perforce usage in game dev](https://youtu.be/4uuI5C5XNoQ?si=GnISrpYcIrzfSX85).  

## Migrating P4 depot to git

### Initialize git repo
```bash
mkdir volcano
cd volcano
git init
```

### Setup depot branch mappings
```bash
git config git-p4.branchList "main:development"
git config  --add git-p4.branchList "main:release_1.0.0"
```

### Clone the p4 depot to a new git repo
```bash
git p4 clone --destination volcano --detect-branches //volcano@all .
```

### Create a local branch from the branch ref
```bash
git checkout -b main refs/remotes/p4/volcano/main
git checkout -b development refs/remotes/p4/volcano/development
git checkout -b release_1.0.0 refs/remotes/p4/volcano/release_1.0.0
```

### Push the repo to GitHub
```bash
git remote add origin https://github.com/robandpdx/p4-migrate-test6.git
git push -u origin main
git push --all origin
```

