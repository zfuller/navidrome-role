# navidrome

Installs and configures Navidrome self hosted music server.
https://www.navidrome.org/about/

# Requirements

Can be run solo or with a webserver with reverse proxy

# Role Variables

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

# Refer to https://www.navidrome.org/docs/usage/configuration-options/ for configuration option definitions.
# Here are a list of config values that navidrome takes, more can be added to the dictionary as they are released
navidrome_config:
  MusicFolder:   # Default: "./music"
  DataFolder:   # Default: "./data"
  LogLevel:   # Default: "info"
  Address:   # Default: 0.0.0.0 and :: (all IPs)
  BaseUrl:   # Default: Empty
  Port:   # Default: 4533
  AuthRequestLimit:   # Default: 5
  AuthWindowLength:   # Default: "20s"
  AutoImportPlaylists:   # Default: true
  CoverArtPriority:   # Default: cover.*, folder.*, front.*, embedded, external
  CoverJpegQuality:   # Default: 75
  DefaultDownsamplingFormat:   # Default: opus
  DefaultLanguage:   # Default: "en"
  DefaultTheme:   # Default: Dark
  EnableArtworkPrecache:   # Default: true
  EnableCoverAnimation:   # Default: true
  EnableDownloads:   # Default: true
  EnableExternalServices:   # Default: true
  EnableFavourites:   # Default: true
  EnableGravatar:   # Default: false
  EnableLogRedacting:   # Default: true
  EnableMediaFileCoverArt:   # Default: true
  EnableReplayGain:   # Default: true
  EnableSharing:   # Default: false
  EnableStarRating:   # Default: true
  EnableTranscodingConfig:   # Default: false
  EnableUserEditing:   # Default: true
  FFmpegPath:   # Default: Empty (search in the PATH)
  GATrackingID:   # Default: Empty (disabled)
  IgnoredArticles:   # Default: "The El La Los Las Le Les Os As O A"
  ImageCacheSize:   # Default: "100MB"
  LastFM.ApiKey:   # Default: Navidrome project's shared ApiKey
  LastFM.Enabled:   # Default: true
  LastFM.Language:   # Default: "en"
  LastFM.Secret:   # Default: Navidrome project's shared Secret
  ListenBrainz.BaseURL:   # Default: https://api.listenbrainz.org/1/
  ListenBrainz.Enabled:   # Default: true
  MaxSidebarPlaylists:   # Default: 100
  PasswordEncryptionKey:   # Default: (empty)
  PlaylistsPath:   # Default: ".:**/**" (meaning MusicFolder and all its subfolders)
  Prometheus.Enabled:   # Default: false
  Prometheus.MetricsPath:   # Default: "/metrics"
  RecentlyAddedByModTime:   # Default: false
  ReverseProxyUserHeader:   # Default: "Remote-User"
  ReverseProxyWhitelist:   # Default: (empty)
  Scanner.Extractor:   # Default: "taglib"
  Scanner.GenreSeparators:   # Default: ";/,"
  ScanSchedule:   # Default: "@every 1m"
  SearchFullString:   # Default: false
  SessionTimeout:   # Default: "24h"
  Spotify.ID:   # Default: (empty)
  Spotify.Secret:   # Default: (empty)
  SubsonicArtistParticipations:   # Default: false
  TranscodingCacheSize:   # Default: "100MB"
  UILoginBackgroundUrl:   # Default: random music image from Unsplash.com
  UIWelcomeMessage:   # Default: (empty)
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
