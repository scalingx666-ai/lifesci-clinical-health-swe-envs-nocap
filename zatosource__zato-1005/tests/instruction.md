# Issue

**Title:** fix error AttributeError: 'bytes' object has no attribute 'format'

## Description

This exception appears in the server logs.

```
17.12.2019 14:36:002019-12-17 14:36:00,258 - ERROR - 134:DummyThread-57 - zato.server.connection.http_soap.channel:0 - Caught an exception, cid:`53d7808e90da7c21636b540e`, status_code:`HTTPStatus.INTERNAL_SERVER_ERROR`, `Traceback (most recent call last):
17.12.2019 14:36:00  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/connection/http_soap/channel.py", line 355, in dispatch
17.12.2019 14:36:00    payload, worker_store, self.simple_io_config, post_data, path_info, soap_action)
17.12.2019 14:36:00  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/connection/http_soap/channel.py", line 625, in handle
17.12.2019 14:36:00    params_priority=channel_item.params_pri)
17.12.2019 14:36:00  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/service/__init__.py", line 695, in update_handle
17.12.2019 14:36:00    raise resp_e
17.12.2019 14:36:00  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/service/__init__.py", line 677, in update_handle
17.12.2019 14:36:00    response = set_response_func(service, data_format=data_format, transport=transport, **kwargs)
17.12.2019 14:36:00  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/connection/http_soap/channel.py", line 488, in _set_response_data
17.12.2019 14:36:00    self.set_payload(service.response, data_format, transport, service)
17.12.2019 14:36:00  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/connection/http_soap/channel.py", line 681, in set_payload
17.12.2019 14:36:00    response.payload = self._get_xml_admin_payload(service_instance, zato_message_template, None)
17.12.2019 14:36:00  File "/opt/zato_dir/zato/code/zato-server/src/zato/server/connection/http_soap/channel.py", line 647, in _get_xml_admin_payload
17.12.2019 14:36:00    """.format(response_elem=getattr(service_instance.SimpleIO, 'response_elem', 'response'),
17.12.2019 14:36:00AttributeError: 'bytes' object has no attribute 'format'
```

In Python 2.7 this it works, but Python 3.6 - no.
This edit avoids this error in all versions.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5e58c3435000`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.