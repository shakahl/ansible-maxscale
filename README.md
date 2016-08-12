# shakahl.ansible-maxscale

An Ansible role that installs MaxScale on Ubuntu or Debian based systems.

Role Variables
--------------

### Global

- `maxscale_download_token: False` - required
- `maxscale_prepare_logrotate: False`
- `maxscale_version: 'latest'`
- `maxscale_threads: 1`
- `maxscale_log_messages: 1`
- `maxscale_log_trace: 0`
- `maxscale_log_debug: 0`
- `maxscale_logdir: '/var/log/maxscale'`
- `maxscale_cachedir: '/var/cache/maxscale'`
- `maxscale_piddir: '/var/run/maxscale'`
- `maxscale_config: {...}`

### Configuration

Example:

```yaml
maxscale_config:

  'server1':
    type: server
    address: 'server1.local'
    port: '3306'
    protocol: MySQLBackend

  'server2':
    type: server
    address: 'server2.local'
    port: '3306'
    protocol: MySQLBackend

  'MySQL Monitor':
    type: monitor
    module: mysqlmon
    servers: 'server1,server2'
    user: 'example_user'
    passwd: 'example_pass'
    monitor_interval: '10000'

  'Read-Write Service':
    type: service
    router: readwritesplit
    servers: 'server1,server2'
    user: 'example_user'
    passwd: 'example_pass'
    max_slave_connections: 100%

  'MaxAdmin Service':
    type: service
    router: cli

  'Read-Write Listener':
    type: listener
    service: 'Read-Write Service'
    protocol: MySQLClient
    port: '4006'

  'MaxAdmin Listener':
    type: listener
    service: 'MaxAdmin Service'
    protocol: maxscaled
    port: '6603'

```

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: maxscale
      roles:
         - { role: shakahl.ansible-maxscale }

License
-------

GPLv2

Author Information
------------------

- GitHub: [@shakahl](https://github.com/shakahl)
