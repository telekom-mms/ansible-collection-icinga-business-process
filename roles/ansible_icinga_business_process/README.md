# Ansible Icinga Business Process
This role does generate a configuration file for the icinga business process extension
## Installation
TBA

## Role Variables
The role is configured by a single variable `icinga_business_processes` containing an array of configuration hashes

### Structure of the configuration hash:

```yaml
icinga_business_processes:
 - title: process1
   description: Process 1
   owner: user
   menu: yes
   statetype: soft
   nodes:
    - name: testrootnode2
      displayname: Test Root Node Display Name
      operator: and
      visible: true
      info_url: http://localhost/info
      checks:
        - name: testserver1
          type: host
        - name: testserver1
          type: service
          service: webserver_status
        - name: testsubnode
          type: node
        - name: subprocess2
          type: node
          process: process2
```

### Variable Contents
| Variable                         | Required |  Type  |Description
|----------------------------------|----------|--------|-----------
| icinga_business_process_url      | yes      | string | URL to the Incinga instance with installed Business Process extension
| icinga_business_process_user     | yes      | string | User for Icinga Login
| icinga_business_process_password | yes      | string | Password for Icinga Login
| **icinga_business_processes**
| title                            | yes      | string | Title of the Business Process
| description                      | no       | string | Description of the Business Process
| owner                            | yes      | string | Owner
| menu                             | yes      | bool   |
| statetype                        | yes      | string |
| nodes                            | yes      | array  | Array of the Nodes
| **nodes**
| name                             | yes      | string |
| displayname                      | yes      | string |
| operator                         | yes      | string |
| visible                          | yes      | bool   |
| info_url                         | no       | string | Info URL which will be displayed on the "(i)" button on the node
| checks                           | yes      | array  |
| **checks**
| name                             | yes      | string |
| type                             | yes      | string | possible values are: host/service/node
| service                          | no       | string | check service if type is service
| process                          | no       | string | does set the external businessprocess if type is node

## Dependencies
TBA
## Example playbook
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: servers
  vars:
    icinga_business_process_user: username
    icinga_business_process_password: loginpassword
    icinga_business_process_url: https://icinga.example.com
    icinga_business_processes:
      - title: ansible-test
        description: Test Business process for Ansible Role
        owner: user
        menu: yes
        statetype: soft
        nodes:
          - name: service-db-status
            displayname: DB Cluster Status
            operator: 2 of
            visible: false
            checks:
              - name: service-prod-db01
                type: service
                service: db_status
              - name: service-prod-db02
                type: service
                service: db_status
              - name: service-prod-db03
                type: service
                service: db_status
          - name: service-fpm-status
            displayname: PHP FPM Status
            operator: 1 of
            visible: false
            checks:
              - name: service-prod-web01
                type: service
                service: check_php_fpm_status
              - name: service-prod-web02
                type: service
                service: check_php_fpm_status
          - name: service-frontend
            displayname: Frontend
            visible: true
            operator: and
            checks:
              - name: service-db-status
                type: node
              - name: service-fpm-status
                type: node
  roles:
    - ansible_icinga_business_process
```
