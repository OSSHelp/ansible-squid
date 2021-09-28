# Squid

[![Build Status](https://drone.osshelp.ru/api/badges/ansible/squid/status.svg)](https://drone.osshelp.ru/ansible/squid)

The role installs Squid and updates it configuration.

## Deploy example

```yaml
    - role: squid
      visible_hostname: local
      place_cfg_template: true
      squid_users:
        - { name: proxyuser, encrypted_password: '$apr1$vTSRQWtw$5S.9QLgMNbFum6Mvyhfih0' }
      auth_param:
        - 'basic program /usr/lib/squid/basic_ncsa_auth /etc/squid/passwd'
      logs:
        access: '/var/log/squid/access.log'
        cache: '/var/log/squid/cache.log'
        cache_store: '/var/log/squid/store.log'
      localnet_acl:
        - '127.0.0.1'
        - '::1'
        - '10.0.0.0/8'
        - 'fd00::/8'
      cache_dir:
        type: 'aufs'
        path: '/var/spool/squid'
        size: 1024
        level1_dirs: 16
        level2_dirs: 256
      workers: 1
      maximum_object_size: 102400
      refresh_patterns:
        - 'deb$   129600 100% 129600'
        - 'udeb$   129600 100% 129600'
        - 'tar.gz$  129600 100% 129600'
        - 'tar.xz$  129600 100% 129600'
        - 'tar.bz2$  129600 100% 129600'
        - '\/(Packages|Sources)(|\.bz2|\.gz|\.xz)$ 0 0% 0 refresh-ims'
        - '\/Release(|\.gpg)$ 0 0% 0 refresh-ims'
        - '\/InRelease$ 0 0% 0 refresh-ims'
        - '\/(Translation-.*)(|\.bz2|\.gz|\.xz)$ 0 0% 0 refresh-ims'
        - 'changelogs.ubuntu.com\/.*  0  1% 1'
      request_header_access:
        - 'Allow allow all'
      custom_params:
        - { key: follow_x_forwarded_for, value: 'deny all' }
```

Create user crypted password:

```shell
pass=$(apg -n 1 -m 16 -x 16 -M LNC)
echo "$pass"
htpasswd -n username
```

## FAQ

None, so far.

## Useful links

- [Official site](http://www.squid-cache.org/)

## TODO

- Add more information about params.

## License

GPL3

## Author

OSSHelp Team, see <https://oss.help>
