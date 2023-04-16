# navidrome

This ansible role installs and configures the [Navidrome](https://www.navidrome.org/about/) self-hosted music server on a Linux server. This role downloads the latest release of Navidrome from the GitHub repository and sets up any custom configuration settings in navidrome.toml set in the navidrome_config variable. It also configures the systemd service as well.

Once installed, the Navidrome server can be accessed via a web browser at the IP address or domain name of the server, using the default port of 4533. You will need to setup an admin user right away for the first installation.

For additional guidance, please visit the [Getting Started](https://www.navidrome.org/docs/getting-started/) page on the Navidrome website.

Please note that this is not an official Navidrome role, but rather a personal project I developed for my own use and am sharing with the community.

# Requirements

Navidrome can be run solo or with a webserver using a reverse proxy.

# Role Variables

The main variable that you will want to set is the *MusicFolder* variable. This will be the location of your music library. Everything else can be left default.

If you would like to know more about the additional variables you can add, refer to [configuration-options](https://www.navidrome.org/docs/usage/configuration-options/) for additional options and explainations.


```yaml
navidrome_user: www-data
navidrome_group: www-data

navidrome_release_url: https://github.com/navidrome/navidrome/releases
navidrome_temp_location: /tmp

navidrome_install_location: /opt

navidrome_config_dir: /var/lib/navidrome
navidrome_config_file: navidrome.toml
navidrome_pid_file: /var/run/navidrome.pid

navidrome_package_requirements:
  - ffmpeg

# The following includes just a few of the configuration settings that Navidrome accepts.
# Additional settings can be added to the dictionary as needed.
navidrome_config:
  MusicFolder:   # Default: "{{ navidrome_config_dir }}/music"
  DataFolder:   # Default: "{{ navidrome_config_dir }}/data"
  LogLevel:   # Default: "info"
  Address:   # Default: 0.0.0.0 and :: (all IPs)
  BaseUrl:   # Default: (empty)
  Port:   # Default: 4533
  AuthRequestLimit:   # Default: 5
  AuthWindowLength:   # Default: "20s"
  AutoImportPlaylists:   # Default: true
  CoverArtPriority:   # Default: cover.*, folder.*, front.*, embedded, external
  CoverJpegQuality:   # Default: 75
  DefaultDownsamplingFormat:   # Default: opus
  DefaultLanguage:   # Default: "en"
  DefaultTheme:   # Default: Dark
...
  UILoginBackgroundUrl:   # Default: random music image from Unsplash.com
  UIWelcomeMessage:   # Default: (empty)
```

# Dependencies

N/A

# Example Playbook

```yaml
    - name: setup navidrom
      hosts: navidrome
      gather_facts: yes
      vars:
        navidrome_config:
          EnableGravatar: true
          EnableDownloads: false
          ImageCacheSize: "1GB"
          MaxSidebarPlaylists: 5
          CoverJpegQuality: 100
          DefaultLanguage: "en"
          MusicFolder: /home/music
          SessionTimeout: "168h"
          TranscodingCacheSize: "5GB"
          AuthRequestLimit: 10
          AuthWindowLength: "30m"
          UIWelcomeMessage: "welcome"
      roles:
        - role: zfuller.navidrome_role
```

# License

GPL-3.0-only

# Author Information

zfuller
