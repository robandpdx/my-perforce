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

Once the cloudformation stack deploy has completed, get the `P4CommitPublicIP` from the output of the cloudformation stack. You'll need this to connect to the server.

Set the value of `P4PORT` environment variable to the following:
```bash
export P4PORT="ssl:<P4CommitPublicIP>:1666"
```

Use this value also to connect using [P4V](https://portal.perforce.com/s/downloads?product=Helix%20Visual%20Client%20%28P4V%29).  


## Notes
[This video show perforce usage in game dev](https://youtu.be/4uuI5C5XNoQ?si=GnISrpYcIrzfSX85).  