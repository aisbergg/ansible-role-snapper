# Ansible Role: `aisbergg.snapper`

This Ansible role installs and configures [Snapper](http://snapper.io), a snapshot tool for Linux.

## Requirements

To use Snapper, a compatible filesystem like _Btrfs_ needs to be used on the machine.

## Role Variables

| Variable | Default | Comments |
|----------|---------|----------|
| `snapper_templates` | `{}` | Dictionary (key-value pairs) of Snapper templates. The templates can be used, when using `create-config` manually. Available options for the templates can be looked up in the [`templates/snapper-config.j2`](templates/snapper-config.j2) file. |
| `snapper_configs` | `[]` | List of Snapper configurations to be present on the system. | 
| `snapper_configs.path` |  | Path to the volume (e.g. Btrfs subvolume). | 
| `snapper_configs.name` |  | Name of the configuration. | 
| `snapper_configs.vars` | `{}` | Dictionary (key-value pairs) of configuration variables. Available variables can be looked up in the [`templates/snapper-config.j2`](templates/snapper-config.j2) file. | 
| `snapper_configs_absent` | `[]` | List of Snapper configurations to be absent on the system. | 

## Example Playbook

```yaml
- hosts: all
  vars:
    snapper_templates:
      default:
        TIMELINE_LIMIT_HOURLY: 2
        TIMELINE_LIMIT_DAILY: 12

  snapper_configs:
    - path: /
      name: root
      vars:
        TIMELINE_LIMIT_HOURLY: 2
        TIMELINE_LIMIT_DAILY: 12
  roles:
    - aisbergg.snapper
```

## License

MIT

## Author Information

Andre Lehmann (aisberg@posteo.de)
