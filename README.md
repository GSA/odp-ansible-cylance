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
* Cylance package available in your OS software repository
* Cylance access token

Role Variables
--------------
| Variable | Type | Description |
| ---  | ---  | ---  | 
| cylance_token | string   | Cylance token for authentication | 
| cylance_zone | string   | Cylance zone systems will be added to when connecting | 
| cylance_http_proxy | string   | HTTP proxy to be used in the /usr/lib/systemd/system/cylancesvc.service file.  Only set if required. | 
| cylance_https_proxy | string   | HTTPS proxy to be used in the /usr/lib/systemd/system/cylancesvc.service file.  Only set if required. |
| cylance_version | string | Cylance package version to install |

Dependencies
------------

* No external role dependencies

Example Playbook When Using OS Native Package Manager
----------------
```
- hosts: servers
  roles:
    - { role: odp-ansible-cylance, cylance_zone: "My Cool Zone", cylance_token: "123itsamystery", cylance_version: "CylancePROTECT-2.1.1560-1525", cylance_http_proxy: "http://myproxy.com:1234", cylance_https_proxy: "https://myproxy.com:1234" }
```

Example when downloading install from S3 bucket

```
- hosts: servers
  roles:
    - { role: odp-ansible-cylance, cylance_zone: "My Cool Zone", cylance_token: "123itsamystery", cylance_version: "CylancePROTECT-2.1.1560-1525", cylance_http_proxy: "http://myproxy.com:1234", cylance_https_proxy: "https://myproxy.com:1234", cylance_s3_bucket: "my_package_s3_bucket", cylance_s3_prefix: "packages" }
```



License
-------

BSD

Author Information
------------------

GSA ODP Team
