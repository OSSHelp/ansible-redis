# redis

[![Build Status](https://drone.osshelp.ru/api/badges/ansible/redis/status.svg)](https://drone.osshelp.ru/ansible/redis)

The role for Ansible, which installs redis-server from Ubuntu official repo or from [ppa](https://launchpad.net/~chris-lea/+archive/ubuntu/redis-server)

## Usage (examples)

### Minimal

```yaml
    - role: redis
```

### Configure mode + custom parameters

``` yaml
    - role: redis
      redis_setup: configure
      redis_params:
        maxmemory: 256mb
        maxmemory-policy: allkeys-lru
        "save 900": 5
        "save 300": 30
```

## Available parameters

### Main

| Param | Default | Description |
| -------- | -------- | -------- |
| `redis_setup` | `full` | See [OSSHelp KB article](https://oss.help/kb4895) |
| `redis_from_ppa`| `false` | Installs redis-server from [ppa](https://launchpad.net/~chris-lea/+archive/ubuntu/redis-server) |
| `redis_params` | `{}` | Redis parameters dictionary (key: value). It overrides/combine `redis_default_params` |

### Misc

Internarnal role parameters. Should not be changed.

| Param | Default | Description |
| -------- | -------- | -------- |
| `redis_ppa` | `ppa:chris-lea/redis-server` | PPA url |
| `redis_config_path`| `/etc/redis/redis.conf` | Path to Redis config file |
| `redis_default_params` | `{bind: '0.0.0.0 ::', port: '6379'}` | Default Redis parameters |

## FAQ

### How to set vm.overcommit_memory

Use `sysctl` role for **host** system:

``` yaml
- role: sysctl
  sysctl_params:
    vm.overcommit_memory: 1
```

## Useful links

- [Official documentation](https://redis.io/documentation)
- [OSSHelp KB articles](https://rm.osshelp.ru/projects/support-servers/search?utf8=%E2%9C%93&q=redis&scope=&all_words=&titles_only=&titles_only=1&kb_articles=1&attachments=0&options=0&commit=%D0%9F%D1%80%D0%B8%D0%BD%D1%8F%D1%82%D1%8C)

## TODO

- Add Focal installation from ppa support (`The repository 'http://ppa.launchpad.net/chris-lea/redis-server/ubuntu focal Release' does not have a Release file`)
- Redis cluster support?

## License

GPL3

## Author

OSSHelp Team, see <https://oss.help>
