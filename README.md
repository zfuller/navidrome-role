# navidrome

Installs and configures Navidrome self hosted music server.
https://www.navidrome.org/about/

# Requirements

Can be run solo or with a webserver with reverse proxy

# Role Variables

```yaml
# User that will run navidrome
navidrome_user: www-data
navidrome_group: www-data

# download information
navidrome_version: 0.23.1
navidrome_arch: "{{ ansible_architecture }}"
navidrome_system: "{{ ansible_system }}"

# default location of the tar
navidrome_release_tar: https://github.com/deluan/navidrome/releases/download/v{{ navidrome_version }}/navidrome_{{ navidrome_version }}_{{ navidrome_system }}_{{ navidrome_arch }}.tar.gz

# If you have a local tar.gz that you would like to use you can set
# navidrome_release_tar: to the location of it and then set
# navidrome_remote_src to no
navidrome_remote_src: yes


navidrome_install_location: /opt/navidrome
navidrome_config_dir: /var/lib/navidrome

navidrome_configuration_file: navidrome.toml

# additional package requirements
navidrome_package_requirements:
  - ffmpeg

# systemd service options
navidrome_service_privatedevices:
navidrome_service_protectsystem:
navidrome_service_protecthome:

navidrome_pid_file: /var/run/navidrome.pid

# configuration file settings, blank here which will use navidromes default settings
# Read https//www.navidrome.org/docs/usage/configuration-options/ for more info
navidrome_musicfolder: ""
navidrome_datafolder: ""
navidrome_scaninterval: ""
navidrome_loglevel: ""
navidrome_port: 4533
navidrome_enabletranscodingconfig: ""
navidrome_transcodingcachesize: ""
navidrome_imagecachesize: ""
navidrome_sessiontimeout: ""
navidrome_baseurl: ""
navidrome_uiloginbackgroundurl: ""
navidrome_ignoredarticles: ""
```

# Dependencies

N/A

# Example Playbook

## Standalone
```yaml
    - name: setup navidrom
      hosts: navidrome
      gather_facts: yes
      roles:
         - role: zfuller.navidrome
```

## w/Caddy reverse proxy
[example_playbook.yml](example_playbook.yml)

# License

GPL-3.0-only

# Author Information

zfuller
