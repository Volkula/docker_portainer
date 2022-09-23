volkula.docker_portainer
=========

Install [portainer](https://www.portainer.io/) 

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

```yaml
    vars:
    - auth_method: 1 - host auth
    - auth_method: 2 - LDAP auth
    - host_port: 9000
    - http_port: 9000
    - https_port: 9443
    - admin_user: admin
    - admin_password: password
    - portainer_edition: ce - Community edition
    - portainer_edition: be - Business edition
    - registry_url: 1.2.3.4
    - registry_port: 5001
    - registry_auth: false
# 1 (Quay.io), 2 (Azure container registry) or 3 (custom registry)
    - registry_type: 3
    - registry_username: username
    - registry_password: password
    - remove_persistent_data: false
    - remove_existing_container: false
```

Dependencies
------------

-

Example Playbook
----------------

```yml
- name: Docker
  hosts: portainer
  become: true
  gather_facts: true
  vars:
    company_logo_url: ""
    admin_user: admi
    admin_password: "password"

    remove_existing_container: false
    remove_persistent_data: false

    version: latest
    portainer_edition: ee
    portainer_http_port: 8440
    portainer_https_port: 8443
    container_ports:
      - "{{portainer_http_port}}:9000"
      - "{{portainer_https_port}}:9443"
  roles:
    - volkula.docker_portainer
  tasks:
    - name: WebURL HTTP
      debug:
        msg: "http://{{hostvars[inventory_hostname]['fqdn']}}:{{portainer_http_port}}"
    - name: WebURL HTTPS
      debug:
        msg: "https://{{hostvars[inventory_hostname]['fqdn']}}:{{portainer_https_port}}"
```

License
-------

BSD

Author Information
------------------

Made by Volkula (https://github.com/Volkula) 2022
