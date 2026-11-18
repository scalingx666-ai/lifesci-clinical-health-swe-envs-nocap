# Issue

**Title:** Save move destinations in confs/server.xml as XML attributes

## Description

The current implementation of the server settings will save each move destination like this:

```xml
<move-destination>
    <aetitle>ANOTHER-STORAGE</aetitle>
    <address>192.168.42.42</address>
    <port>6666</port>
    <public>false</public>
    <description>Our test storage</description>
</move-destination>
```

A more compact form would be this, which is already supported transparently for reading and is more similar to the legacy format:

```xml
<move-destination
    aetitle="ANOTHER-STORAGE"
    address="192.168.42.42"
    port="6666"
    public="false"
    description="Our test storage"/>
```

This PR changes the file saving logic to persist the parameters of each move destination via XML attributes. Users can still manually edit the file in both ways, but on the first save, it will be normalized to the second format. No incompatibilities are introduced, as the application is still capable of reading existing files either way.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5507ee7d8b8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.