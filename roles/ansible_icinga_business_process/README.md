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
| Variable                   | Required | Type |Description
|----------------------------|----------|------|-----------
| **icinga_business_processes**
| title                      | yes      | string | Title of the Business Process
| description                | no       | string | Description of the Business Process
| owner                      | yes      | string | Owner
| menu                       | yes      | boolean|
| statetype                  | yes      | string |
| nodes                      | yes      | array  | Array of the Nodes
| **nodes**
| name                       | yes      | string |
| displayname                | yes      | string |
| operator                   | yes      | string |
| visible                    | yes      | boolean|
| info_url                   | no       | string | Info URL which will be displayed on the "(i)" button on the node
| checks                     | yes      | array  |
| **checks**
| name                       | yes      | string |
| type                       | yes      | string | possible values are: host/service/node
| service                    | no       | string | check service if type is service
| process                    | no       | string | does set the external businessprocess if type is node
The variable 'operator' is a mandatory variable

## Dependencies
TBA
## Example playbook
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
    - hosts: servers
      roles:
         - ansible_icinga_business_process
```
