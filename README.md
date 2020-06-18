Role Name
=========

The ansible role `odp-ansible-cylance` is used to install and configure the Cylance antivirus agent.

Requirements
------------

### OS Supported

* Amazon Linux 2
* Amazon EKS enhanced Linux ( Based on Amazon Linux 2 )

### Cylance Requirements

* Active Cylance account
* Cylance access token

Role Variables
--------------
| Variable | Type | Description |
| ---  | ---  | ---  | 
| cylance_token | string   | Cylance token for authentication | 
| cylance_http_proxy | string   | HTTP proxy to be used in the /usr/lib/systemd/system/cylancesvc.service file.  Only set if required. | 
| cylance_https_proxy | string   | HTTPS proxy to be used in the /usr/lib/systemd/system/cylancesvc.service file.  Only set if required. |

Dependencies
------------

* No external role dependencies

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: odp-ansible-cylance, cylance_token: "XXXXXXXXXXXXXXXXXXX", cylance_http_proxy: "http://myproxy.com:1234", cylance_https_proxy: "https://myproxy.com:1234" }

License
-------

BSD

Author Information
------------------

GSA ODP Team
