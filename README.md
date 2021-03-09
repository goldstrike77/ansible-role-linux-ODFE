![](https://img.shields.io/badge/Ansible-opendistro-green.svg?logo=angular&style=for-the-badge)

>__Please note that the original design goal of this role was more concerned with the initial installation and bootstrapping environment, which currently does not involve performing continuous maintenance, and therefore are only suitable for testing and development purposes,  should not be used in production environments. The author does not guarantee the accuracy, completeness, reliability, and availability of the role content. Under no circumstances will the author be held responsible or liable in any way for any claims, damages, losses, expenses, costs or liabilities whatsoever, including, without limitation, any direct or indirect damages for loss of profits, business interruption or loss of information.__

>__请注意，此角色的最初设计目标更关注初始安装和引导环境，目前不涉及执行连续维护，因此仅适用于测试和开发目的，不应在生产环境中使用。作者不对角色内容之准确性、完整性、可靠性、可用性做保证。在任何情况下，作者均不对任何索赔，损害，损失，费用，成本或负债承担任何责任，包括但不限于因利润损失，业务中断或信息丢失而造成的任何直接或间接损害。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_opendistro.png" align="right" /></p>

__Table of Contents__

- [Overview](#overview)
- [Requirements](#requirements)
  * [Operating systems](#operating-systems)
  * [Opendistro Versions](#opendistro-versions)
- [ Role variables](#Role-variables)
  * [Main Configuration](#Main-parameters)
  * [Other Configuration](#Other-parameters)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Hosts inventory file](#Hosts-inventory-file)
  * [Vars in role configuration](#vars-in-role-configuration)
  * [Combination of group vars and playbook](#combination-of-group-vars-and-playbook)
- [License](#license)
- [Author Information](#author-information)
- [Contributors](#Contributors)
- [Donations](#Donations)

## Overview
Open Distro provides a powerful, easy-to-use event monitoring and alerting system, enabling you to monitor your data and send notifications automatically to your stakeholders. With an intuitive Kibana interface and powerful API, it is easy to set up and manage alerts. Build specific alert conditions using Elasticsearch's query and scripting capabilities. Alerts help teams reduce response times for operational and security events. All of the plugins included in Open Distro are licensed under the Apache License, Version 2.0.
>__There is a file that records the internal users password in /tmp folder at the first node, Burn after reading!__

## Requirements
### Operating systems
This Ansible role installs Opendistro and Logstash OSS on Linux operating system, including establishing a filesystem structure and server configuration with some common operational features, Will works on the following operating systems:

  * CentOS 7

### Opendistro versions

The following list of supported the Opendistro releases:

  * 1.13

## Role variables
### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:

##### General parameters
* `opendistro_version`: Specify the Open Distro for ElasticSearch version.
* `opendistro_logstash_version`: Specify the Logstash version.
* `opendistro_path`: Specify the Open Distro for ElasticSearch storage directory.
* `opendistro_cluster`: Specify name for your ElasticSearch cluster.
* `opendistro_admin_pass`: The password for administrator.
* `opendistro_rotate_day`: Specify the logs retention days.
* `opendistro_es_heap_size`: Specify the maximum memory allocation pool for a Java virtual machine on ElasticSearch.
* `opendistro_logstash_heap_size`: Specify the maximum memory allocation pool for a Java virtual machine on LogStash.
* `opendistro_memory_lock`: A boolean to determine whether or not lock the process address space into memory on startup.
* `opendistro_kibana_proxy`: A boolean to determine whether or not to mount Kibana at if you are running behind a proxy.

##### Role dependencies
* `opendistro_ngx_dept`: A boolean to determine whether or not to proxy web interface and API traffic using NGinx.

##### Listen port
* `opendistro_port.rest`: TCP port for ElasticSearch REST.
* `opendistro_port.transport`: TCP port for ElasticSearch transport port ragne.
* `opendistro_port.elasticsearch_exporter`: TCP port for Prometheus Exporter.
* `opendistro_port.kibana`: TCP port for Kibana server.
* `opendistro_port.analyzer_web`: TCP port for performance analyzer WebService exposed.
* `opendistro_port.analyzer_rpc`: TCP port for performance analyzer RPC Communication.
* `opendistro_port.logstash_exporter`: TCP Port for Logstash exporter.
* `opendistro_port.logstash_api`: TCP Port for the Logstash metrics REST endpoint.

##### Logstash parameters
* `opendistro_logstash_arg.index_refresh_interval`: How often to perform a index refresh operation.
* `opendistro_logstash_arg.pipeline_workers`: The number of workers.
* `opendistro_logstash_arg.pipeline_batch_size`: How many events to retrieve from inputs before sending to workers.
* `opendistro_logstash_arg.pipeline_batch_delay`: How long to wait in milliseconds while polling for the next event.
* `opendistro_logstash_inputs_arg`: Define the global common inputs parameters.

##### NGinx parameters
* `opendistro_ngx_domain`: Defines domain name.
* `opendistro_ngx_port_http`: Defines NGinx HTTP listen port.
* `opendistro_ngx_port_https`: Defines NGinx HTTPs listen port.
* `opendistro_ngx_block_agents`: A boolean to determine whether or not enables or disables block unsafe User Agents.
* `opendistro_ngx_block_string`: A boolean to determine whether or not enables or disables block includes Exploits / File injections / Spam / SQL injections.
* `opendistro_ngx_compress`: A boolean to determine whether or not enables compression.

##### ElasticSearch parameters
* `opendistro_es_arg.action_destructive_requires_name`: Restricts deletions to specific names, instead of allowing the special _all or wildcard options.
* `opendistro_es_arg.cluster_max_shards_per_node`: Controls the number of shards allowed in the cluster per data node.
* `opendistro_es_arg.http_compression`: A boolean to determine whether or not to compression when possible with Accept-Encoding.
* `opendistro_es_arg.http_cors_enabled`: A boolean to determine whether or not to enables cross-origin resource sharing.
* `opendistro_es_arg.http_cors_allow_methods`: Which methods to allow.

##### Service Mesh
* `environments`: Define the service environment.
* `datacenter`: Define the DataCenter.
* `domain`: Define the Domain.
* `customer`: Define the customer name.
* `tags`: Define the service custom label.
* `exporter_is_install`: Whether to install prometheus exporter.
* `consul_public_register`: Whether register a exporter service with public consul client.
* `consul_public_exporter_token`: Public Consul client ACL token.
* `consul_public_http_prot`: The consul Hypertext Transfer Protocol.
* `consul_public_clients`: List of public consul clients.
* `consul_public_http_port`: The consul HTTP API port.

### Other parameters
There are some variables in vars/main.yml:

## Dependencies
- Ansible versions >= 2.9
- Python >= 2.7.5
- [NGinx](https://github.com/goldstrike77/ansible-role-linux-nginx.git)

## Example

### Hosts inventory file
See tests/inventory for an example.

    [siem:vars]
    opendistro_cluster='siem'
    opendistro_version='1.13.1'
    opendistro_logstash_version='7.10.2'

    [siem]
    node01 ansible_host='192.168.1.10'
    node02 ansible_host='192.168.1.11'
    node03 ansible_host='192.168.1.12'

### Vars in role configuration
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: all
  roles:
     - role: ansible-role-linux-opendistro
       opendistro_cluster: 'siem'
       opendistro_version: '1.13.1'
       opendistro_logstash_version: '7.10.2'
```

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`.

```yaml
opendistro_version: '1.13.1'
opendistro_logstash_version: '7.10.2'
opendistro_path: '/data'
opendistro_cluster: 'siem'
opendistro_admin_pass: 'changeme'
opendistro_rotate_day: '180'
opendistro_es_heap_size: '3g'
opendistro_logstash_heap_size: '1g'
opendistro_memory_lock: false
opendistro_kibana_proxy: false
opendistro_ngx_dept: true
opendistro_port:
  rest: '9200'
  transport: '9300'
  elasticsearch_exporter: '9108'
  kibana: '5601'
  analyzer_web: '9601'
  analyzer_rpc: '9650'
  logstash_exporter: '9198'
  logstash_api: '9600'
opendistro_logstash_arg:
  index_refresh_interval: '30s'
  pipeline_workers: '100'
  pipeline_batch_size: '1000'
  pipeline_batch_delay: '100'
opendistro_logstash_inputs_arg:
  - name: 'syslog-gelf'
    protocol: 'udp'
    port: '12201'
opendistro_ngx_domain: 'siem.example.com'
opendistro_ngx_port_http: '80'
opendistro_ngx_port_https: '443'
opendistro_ngx_block_agents: true
opendistro_ngx_block_string: true
opendistro_ngx_compress: true
opendistro_es_arg:
  action_destructive_requires_name: true
  cluster_max_shards_per_node: '10000'
  http_compression: true
  http_cors_enabled: true 
  http_cors_enabled: true
  http_cors_allow_methods: 'HEAD, GET, POST, PUT, DELETE'
environments: 'prd'
datacenter: 'dc01'
domain: 'local'
customer: 'demo'
tags:
  subscription: 'default'
  owner: 'nobody'
  department: 'Infrastructure'
  organization: 'The Company'
  region: 'China'
exporter_is_install: false
consul_public_register: false
consul_public_exporter_token: '00000000-0000-0000-0000-000000000000'
consul_public_http_prot: 'https'
consul_public_http_port: '8500'
consul_public_clients:
  - '127.0.0.1'
```

## License
![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## Author Information
Please send your suggestions to make this role better.

## Contributors
Special thanks to the [Connext Information Technology](http://www.connext.com.cn) for their contributions to this role.

## Donations
Please donate to the following monero address.

    46CHVMbb6wQV2PJYEbahb353SYGqXhcdFQVEWdCnHb6JaR5125h3kNQ6bcqLye5G7UF7qz6xL9qHLDSAY3baagfmLZABz75