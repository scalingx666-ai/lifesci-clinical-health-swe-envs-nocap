# Issue

**Title:** Fix USERNAME setting on IBM_MQ

## Description

On a fresh install from the source (from the main branch.) when you try to create a cluster, you get this error:

```
(code) vagrant@zato:~/zato/code$ zato quickstart create ~/esb/env3 sqlite localhost 6379 --verbose

Key/value database password (will not echo):
Kvdb_password again (will not echo):
[1/9] Certificate authority created
[2/9] ODB schema created
Traceback (most recent call last):
  File "/home/vagrant/zato/code/bin/zato", line 11, in <module>
    load_entry_point('zato-cli', 'console_scripts', 'zato')()
  File "/home/vagrant/zato/code/zato-cli/src/zato/cli/zato_command.py", line 346, in main
    return run_command(get_parser().parse_args())
  File "/home/vagrant/zato/code/zato-cli/src/zato/cli/__init__.py", line 352, in run_command
    command_class[args.command](args).run(args)
  File "/home/vagrant/zato/code/zato-cli/src/zato/cli/__init__.py", line 628, in run
    return_code = self.execute(args)
  File "/home/vagrant/zato/code/zato-cli/src/zato/cli/quickstart.py", line 328, in execute
    create_cluster.Create(create_cluster_args).execute(create_cluster_args, False)
  File "/home/vagrant/zato/code/zato-cli/src/zato/cli/create_cluster.py", line 517, in execute
    self.add_internal_callback_wmq(session, cluster)
  File "/home/vagrant/zato/code/zato-cli/src/zato/cli/create_cluster.py", line 977, in add_internal_callback_wmq
    wmq_username = IPC.CONNECTOR.WEBSPHERE_MQ.USERNAME
AttributeError: class CONNECTOR has no attribute 'WEBSPHERE_MQ'
```

It seems with , you have renamed  WebSphere MQ to IBM MQ.

However, create cluster command tries to access the property of  ```IPC.CONNECTOR.WEBSPHERE_MQ ```.

I have changed it to ```IPC.CONNECTOR.IBM_MQ.USERNAME``` since it looks like the correct property which makes the create-cluster function works.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a3e69ce6f997`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.