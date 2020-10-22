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
navidrome_version: 0.36.0
navidrome_arch: "{{ ansible_architecture }}"
navidrome_system: "{{ ansible_system }}"

# default location of the tar
navidrome_dl_url: github.com/deluan/navidrome/releases/download
navidrome_release_tar: |
  https://{{ navidrome_dl_url }}/v{{ navidrome_version }}/navidrome_{{ navidrome_version }}_{{ navidrome_system }}_{{ navidrome_arch }}.tar.gz

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
  - libtag1v5

# systemd service options
navidrome_service_privatedevices:
navidrome_service_protectsystem:
navidrome_service_protecthome:

navidrome_pid_file: /var/run/navidrome.pid

# configuration file settings, blank here which will use navidromes default settings
# Read https//www.navidrome.org/docs/usage/configuration-options/ for more info
navidrome_altconfigfile: ""

navidrome_ipaddress: ""  # 0.0.0.0
navidrome_port: 4533  # 4533

navidrome_baseurl: ""
navidrome_loglevel: ""  # "info", error info debug trace

navidrome_datafolder: ""  # "./data"
navidrome_musicfolder: ""  # "./music"
navidrome_scaninterval: ""  # "1m"

navidrome_authlimit: ""  # 5
navidrome_authratelimit: ""  # "20s"

# Google analytics account ID
navidrome_gaid: ""  # UA-XXXXXXXX

navidrome_ignoredarticles: ""  # "The El La Los Las Le Les Os As O A"
navidrome_sessiontimeout: ""  # "24h"
navidrome_transcodingcachesize: ""  # "100MB"
navidrome_uiloginbackgroundurl: ""
navidrome_uiwelcomemessage: ""
navidrome_coverartpriority: ""  # "embedded, cover.*, folder.*, front.*"
navidrome_imagecachesize: ""  # "100MB"
navidrome_jpegquality: ""  # 75
navidrome_enabletranscodingconfig: ""  # false

# WIP features and such
navidrome_dev_logsourceline: ""
navidrome_dev_autocreateadminpassword: ""
navidrome_dev_oldscanner: ""  # false
```

# Dependencies

N/A

# Example Playbook

## Standalone
```yaml
    - name: setup navidrom
      hosts: navidrome
      gather_facts: yes
      vars:
        navidrome_musicfolder: /home/music
        navidrome_sessiontimeout: 168h
        navidrome_transcodingcachesize: 5GB
        navidrome_imagecachesize: 5GB
        navidrome_authlimit: 10
        navidrome_authratelimit: 30m
        navidrome_uiwelcomemessage: "yo"
        navidrome_jpegquality: 100
      roles:
         - role: zfuller.navidrome_role
```

## w/Caddy reverse proxy
[example_playbook.yml](example_playbook.yml)

# License

GPL-3.0-only

# Author Information

zfuller
