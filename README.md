# Ansible Role: Fluent-Bit

The Ansible Role for install **Fluent Bit** on Debian/Ubuntu.

## Requirements

None.

## Example
```yaml
# Vars
fluentbit_inputs:
  - name: 'tail'
    path:             '/logs/*.log'
    parser:           'my_log'
    refresh_Interval: '5'
    tag:              'my_log'
    alias:            'my_log'

fluentbit_outputs:
  - name: 'opensearch'
    alias: 'my_log'
    match: 'my_log'
    host:  'localhost:443'
    port:  '443'
    retry_limit: 'off'
    replace_dots: 'on'
    tls: 'on'
    suppress_type_name: 'on'
    logstash_format: 'on'
    # index naming - my_log-2023.09.12 ...
    logstash_prefix: 'my_log'

fluentbit_custom_parsers:
  - name: 'my_log'
    format: 'json'
    time_key: 'timestamp'
    time_format: '%Y-%m-%dT%H:%M:%S.%L%z'

# Playbook
tasks:
    - name: fluent-bit
      hosts: all
      roles:
        - role: ansible-role-fluentbit
```

## Role Variables
| Variable                                    | Default                                                                                                    | Description |
|---------------------------------------------|------------------------------------------------------------------------------------------------------------|-------------|
| fluentbit_key_url                           | https://packages.fluentbit.io/fluentbit.key                                                                |             |
| fluentbit_key_local_path                    | /usr/share/keyrings/fluentbit-keyring.gpg                                                                  |             |
| fluentbit_repo_url                          | https://packages.fluentbit.io/ubuntu/{{ ansible_distribution_release }} {{ ansible_distribution_release }} |             |
| fluentbit_apt_source                        | deb [signed-by={{ fluentbit_key_local_path }}] {{ fluentbit_repo_url }} main                               |             |
| fluent_bit_config_dir                       | /etc/fluent-bit                                                                                            |             |
| fluentbit_flush_seconds             | 5                                                                                                          |             |
| fluentbit_daemon                    | false                                                                                                      |             |
| fluentbit_log_level                 | info                                                                                                       |             |
| fluentbit_enable_metrics            | false                                                                                                      |             |
| fluentbit_metrics_listen_ip         | 0.0.0.0                                                                                                    |             |
| fluentbit_metrics_listen_port       | 2020                                                                                                       |             |
| fluentbit_storage_metrics           | true                                                                                                       |             |
| fluentbit_storage_path              | /tmp/storage                                                                                               |             |
| fluentbit_storage_sync_mode         | normal                                                                                                     |             |
| fluentbit_storage_checksum          | false                                                                                                      |             |
| fluentbit_storage_backlog_mem_limit | 5M                                                                                                         |             |
| fluentbit_custom_parsers            | []                                                                                                         |             |
| fluentbit_inputs                            | []                                                                                                         |             |
| fluentbit_filters                           | []                                                                                                         |             |
| fluentbit_outputs                           | []                                                                                                         |             |
