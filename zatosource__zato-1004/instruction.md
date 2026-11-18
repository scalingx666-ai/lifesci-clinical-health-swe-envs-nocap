# Issue

**Title:** Set correlation_id for send to IBM for Python 3.6

## Description

When I want to send a message with parameter passing correlation_id, I get an error 
```
17.12.2019 13:33:542019-12-17 13:33:54,766 - ERROR - 115:DummyThread-12248 - zato.server.connection.http_soap.channel:0 - Caught an exception, cid:`48a57c1ea0f1b0b76e9c06b7`, status_code:`HTTPStatus.INTERNAL_SERVER_ERROR`, `Traceback (most recent call last):
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/connection/http_soap/channel.py", line 355, in dispatch
17.12.2019 13:33:54    payload, worker_store, self.simple_io_config, post_data, path_info, soap_action)
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/connection/http_soap/channel.py", line 625, in handle
17.12.2019 13:33:54    params_priority=channel_item.params_pri)
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/service/__init__.py", line 699, in update_handle
17.12.2019 13:33:54    raise e if isinstance(e, Exception) else Exception(e)
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/service/__init__.py", line 647, in update_handle
17.12.2019 13:33:54    self._invoke(service, channel)
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/service/__init__.py", line 534, in _invoke
17.12.2019 13:33:54    service.handle()
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/service/internal/channel/jms_wmq.py", line 247, in handle
17.12.2019 13:33:54    'mqmd': pickle_loads(msg['mqmd'])
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/service/__init__.py", line 779, in invoke
17.12.2019 13:33:54    return self.invoke_by_impl_name(self.server.service_store.name_to_impl_name[name], *args, **kwargs)
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/service/__init__.py", line 755, in invoke_by_impl_name
17.12.2019 13:33:54    out = self.update_handle(*invoke_args, **kwargs)
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/service/__init__.py", line 699, in update_handle
17.12.2019 13:33:54    raise e if isinstance(e, Exception) else Exception(e)
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/service/__init__.py", line 647, in update_handle
17.12.2019 13:33:54    self._invoke(service, channel)
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/service/__init__.py", line 538, in _invoke
17.12.2019 13:33:54    service.handle()
17.12.2019 13:33:54  File "/opt/zato_dir/env/server/work/hot-deploy/current/mts_response_dispatcher.py", line 343, in handle
17.12.2019 13:33:54    self.outgoing.ibm_mq.send(self.request.payload, 'name_outgoing', QUEUE_NAME, correlation_id=correlation_id)
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/connection/jms_wmq/outgoing.py", line 40, in send
17.12.2019 13:33:54    'delivery_mode': delivery_mode,
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/base/parallel/subprocess_/ibm_mq.py", line 57, in send_wmq_message
17.12.2019 13:33:54    out = self.send_message(*args, **kwargs)
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/connection/connector/subprocess_/ipc.py", line 181, in send_message
17.12.2019 13:33:54    response = self.invoke_connector(msg)
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/connection/connector/subprocess_/ipc.py", line 200, in invoke_connector
17.12.2019 13:33:54    raise Exception(response.text)
17.12.2019 13:33:54Exception: Exception in _on_OUTGOING_WMQ_SEND (2) `Traceback (most recent call last):
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/connection/connector/subprocess_/impl/ibm_mq.py", line 297, in _on_OUTGOING_WMQ_SEND
17.12.2019 13:33:54    conn.send(text_msg, msg.queue_name.encode('utf8'))
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/connection/jms_wmq/jms/connection.py", line 355, in send
17.12.2019 13:33:54    md = self._build_md(message)
17.12.2019 13:33:54  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/connection/jms_wmq/jms/connection.py", line 660, in _build_md
17.12.2019 13:33:54    if message.jms_correlation_id.startswith(_WMQ_ID_PREFIX):
17.12.2019 13:33:54TypeError: startswith first arg must be bytes or a tuple of bytes, not str
```
_WMQ_ID_PREFIX is str type, message.jms_correlation_id is bytes. In Python 2.7 no error, but Python 3.6 i get error TypeError.

Adding .encode('utf-8') fixed this problem (works in Python 2.7 and Python 3.6).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a330abba2f94`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.