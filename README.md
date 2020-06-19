Role Name
=========

The ansible role `odp-ansible-cylance` is used to install and configure the Cylance antivirus agent.

Requirements
------------

### OS Supported

* RHEL 7 & 8
* CentOS 7 & 8
* Amazon Linux 2
* Amazon EKS enhanced Linux ( Based on Amazon Linux 2 )
* Ubuntu releases running systemd ( 16.04, 18.04, etc )

### Cylance Requirements

* Active Cylance account
* Cylance package available in your OS software repository or stored in an ***AWS*** S3 bucket
* Cylance access token

Role Variables
--------------
| Variable | Type | Description | Required |
| ---  | ---  | ---  | --- |
| cylance_token | string   | Cylance token for authentication | true  |
| cylance_zone | string   | Cylance zone systems will be added to when connecting | true  | 
| cylance_http_proxy | string   | HTTP proxy to be used in the /usr/lib/systemd/system/cylancesvc.service file. |  false |
| cylance_https_proxy | string   | HTTPS proxy to be used in the /usr/lib/systemd/system/cylancesvc.service file. | false |
| cylance_version | string | Cylance package version to install. For S3 download use the full package name stored in S3. | true | 
| cylance_s3_bucket | string   | Set ONLY if you are using an S3 bucket to store Cylance install package. | false  |
| cylance_s3_prefix | string   | Set ONLY if you are using an S3 bucket to store Cylance install package. | true  |

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

Todo
-------

* Currently the S3 copy to local happens ***EVERY*** time the role is deployed.  There needs to be a check, maybe with package_facts, to determine if the specific version of the package is installed and if so skip.  
  * This is potentially costly and time consuming if run outside of an image build pipeline.


License
-------

BSD

Author Information
------------------

GSA ODP Team
