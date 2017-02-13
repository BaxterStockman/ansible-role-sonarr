# Ansible Role - Sonarr

A role for managing a [Sonarr](https://sonarr.tv/) installation.

# Requirements

This role is appropriate for systems using
[systemd](https://www.freedesktop.org/wiki/Software/systemd/) as a service
manager.  The role will abort if it detects that `ansible_service_mgr` is
a defined value other than `"systemd"`.

_This role does not install Sonarr itself or any of its dependencies_.

## Role Variables

- `sonarr_settings` - a hash of settings to merge into Sonarr's
  configuration file.  By default the hash is empty.
- `sonarr_data_dir` - directory where Sonarr should store its
  database, cache, and other assets.  Defaults to `/var/data/sonarr`.
- `sonarr_config_file` - Sonarr's configuration file.  Defaults to
  `{{ sonarr_data_dir }}/config.xml`.

## Example Playbook

```yaml
- hosts: sonarr
  roles:
    - role: BaxterStockman.sonarr
      sonarr_data_dir: '/opt/sonarr'
      sonarr_config_file: '/etc/sonarr.xml'
      sonarr_settings:
        port: 8080
        bind_address: 0.0.0.0
        url_base: /sonarr
```

Note that keys in the `sonarr_settings` hash are translated from snake case to
camel case and placed under the XML root `<Config>`.  The settings in the
example playbook translate to:

```xml
<Config>
  <Port>8080</Port>
  <BindAddress>0.0.0.0</BindAddress>
  <UrlBase>/sonnar</UrlBase>
</Config>
```

## License

MIT

## Author Information

Matt Schreiber <mschreiber@gmail.com>
