# Issue

**Title:** Fix path to send_wmq_message

## Description

Add correct path to function send_wmq_message.
I want to send a message to IBM MQ. 
My code looks like this
`self.outgoing.ibm_mq.send("test message", "outconn_name", self.queue_name)  `

I get an error - 
```2019-12-16 10:26:48,638 - WARNING - 179:DummyThread-27 - zato.server.service:0 - Traceback (most recent call last):
  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/service/__init__.py", line 647, in update_handle
    self._invoke(service, channel)
  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/service/__init__.py", line 534, in _invoke
    service.handle()
  File "/opt/zato_dir/env/server/work/hot-deploy/current/sender.py", line 10, in handle
    d=self.outgoing.ibm_mq.send("test message", "outconn_name", self.queue_name) 
  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/connection/jms_wmq/outgoing.py", line 31, in send
    return self.service.server.send_wmq_message({
AttributeError: "ParallelServer" object has no attribute "send_wmq_message"
```

If i replace "self.service.server.send_wmq_message(" to "self.service.server.connector_ibm_mq.send_wmq_message" then everything works, because 
no function `send_wmq_message` in ParallelServer, she in IBMMQIPC. In ParallelServer on init
is available self.connector_ibm_mq = IBMMQIPC(self).
I'm sorry for my bad english.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2385120229ab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.