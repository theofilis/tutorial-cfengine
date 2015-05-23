# Synchronizing clients with the policy server

Synchronizing clients with the policy server happens here, in update.cf. Its main job is to copy all the files on the policy server (usually the hub) under $(sys.masterdir) (usually /var/cfengine/masterfiles) to the local host into $(sys.inputdir) (usually /var/cfengine/inputs).

```
cf-agent --no-lock  -f /var/cfengine/masterfiles/update.cf
```