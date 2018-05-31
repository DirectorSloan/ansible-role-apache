Ansible Role: Postfix
=====================

An Ansible role that installs [Apache Web Server][apache] and configures it. It is currently used and tested for RHEL / CentOS 6 but may also work for 7. This Role has also a skeleteon for Debian based distributions.

Table of Contents
-----------------

<!-- toc -->

- [Requirements](#requirements)
- [Role Variables](#role-variables)
  * [Basic Variables](#basic-variables)
  * [ssl variables](#ssl-variables)
  * [addon variables](#addon-variables)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Top-Level Playbook](#top-level-playbook)
  * [Role Dependency](#role-dependency)
- [License](#license)
- [Author Information](#author-information)

<!-- tocstop -->

Requirements
------------

- Ansible 2+

Role Variables
--------------

### Basic Variables

Variables with defaults:

```yml
apache_config_dir: '/etc/httpd/conf.d'

apache_use_ssl: 'no'

apache_user: 'apache'


```

You can set this var to simple string values:

```yml
apache_virtual_hostname: 'hostname.domainname.edu'
```
Be careful: It has to be set if you want to use ssl with `apache_use_ssl`

### SSL Variables

Configure ssl certificate variables like paths if `apache_use_ssl` is set, e.g.:

```yml
apache_ssl_cert_file: '/etc/ssl/yourcert.pem'

apache_ssl_cert_key_file: '/etc/ssl/yourkey.key'
```

### Addon Variables

Feel Free to define your own variables for different apache modules. Please use the config dir and avoid hacking the `httpd.conf` main config file.

Dependencies
------------

None.

Example Playbook
----------------

Add to `requirements.yml`:

```yml
---

- src: sloan87.httpd

...
```

Download:

```console
$ ansible-galaxy install -r requirements.yml
```

### Top-Level Playbook

Write a top-level playbook:

```yml
---

- name: head server
  hosts: head

  roles:
    - role: sloan87.httpd
      tags:
        - apache
        - httpd
        - webserver

...
```

### Role Dependency

Define the role dependency in `meta/main.yml`:

```yml
---

dependencies:

  - role: sloan87.httpd
    tags:
      - apache
      - httpd
      - webserver

...
```

License
-------

MIT

Author Information
------------------

This role was created in 2018 by Ben Langenberg aka [sloan87 at GitHub][sloan87]


[apache]: https://www.apache.org
[sloan87]: https://github.com/sloan87

