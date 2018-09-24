[![No Maintenance Intended](http://unmaintained.tech/badge.svg)](http://unmaintained.tech/)

logstash_forwarder
==================

Installs and configures Logstash Forwarder

Requirements
------------

This role requires Ansible 1.4 or higher.

Role Variables
--------------

| Name                                | Default                                                       | Description                              |
|-------------------------------------|---------------------------------------------------------------|------------------------------------------|
| logstash_forwarder_version          | 0.4.0                                                         | Version of Logstash Forwarder to install |
| logstash_forwarder_nice             | 0                                                             | Nice value of Logstash Forwarder process |
| logstash_forwarder_network_servers  | [ "localhost:5043" ]                                          | List of downstream servers               |
| logstash_forwarder_network_ssl_cert | ''                                                            | Path to SSL certificate file             |
| logstash_forwarder_network_ssl_key  | ''                                                            | Path to SSL key file                     |
| logstash_forwarder_network_ssl_ca   | ''                                                            | Path to trusted SSL CA file              |
| logstash_forwarder_network_timeout  | 15                                                            | Network timeout in seconds               |
| logstash_forwarder_files            | [ paths: [ "/var/log/messages" ], fields: { type: "syslog"} ] | List of files to watch                   |

Dependencies
------------

None

Example Playbook
----------------

Install Logstash Forwarder specifying list of files to watch
```
- hosts: all
  vars:
    logstash_forwarder_files:
      - paths:
          - /var/log/messages
          - /var/log/*.log
        fields:
          type: syslog
      - paths:
          - "-"
        fields:
          type: stdin
      - paths:
          - /var/log/apache/httpd-*.log
        fields:
          type: apache
  roles:
    - { role: kbrebanov.logstash_forwarder }
```

License
-------

BSD

Author Information
------------------

Kevin Brebanov
