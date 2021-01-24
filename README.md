# squid

[![Build Status](https://drone.osshelp.ru/api/badges/ansible/squid/status.svg)](https://drone.osshelp.ru/ansible/squid)

Simple role for Ansible, which installs Squid

## Requirements

Nope.

## Role Variables

See defaults/main.yml

## Dependencies

Nope.

## Example Playbook

```yaml
    - { role: squid,
        logs: {
          access: '/var/log/squid/access.log',
          cache: '/var/log/squid/cache.log'
        },
        localnet_acl: [
          '127.0.0.1',
          '::1',
          '10.0.0.0/8',
          'fd00::/8'
        ],
        cache_dir: {
          path: '/var/spool/squid',
          size: 1024,
          level1_dirs: 16,
          level2_dirs: 256
        }
    }
```

## TODO

- ...
