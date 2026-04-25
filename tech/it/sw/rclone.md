#  Overview

- rclone is a CLI program to manage files on cloud storage.

# Google Drive on Archlinux

- Install rclone and required software:
    + `sudo pacman -S rclone fuse3`
- Configure a new remote
    + `rclone config`
    + New remote, name: `gdrive-<email/etc>`
    + Storage: `drive`
    + Using your private client ID and secret (details below for how to
      obtain one)
    + Authenticate with Google on browser for your account to connect
      with your Google account.
- Get a Google Drive client ID and secret
    + https://rclone.org/drive/#making-your-own-client-id
    + https://www.reddit.com/r/n8n/comments/1p64bfq/your_google_drive_connection_dies_every_7_days/
        * https://youtu.be/_rJHUAHaZa4
    + Enable Google Drive API in one of your Google Cloud project.
    + Create a new credential / client for Google Drive API (Desktop
      App) and take note / download client ID and secret.
    + Got Google Auth Platform to Add Data Access and Audience.
    + Publish the application to production and ignore Google warning
      for verification since we only use this for our personal usage.
- Mount the remote to your local file system
    + Manually
        * `rclone mount <remote-name>: <path-to-mount-point> [options]`
        * `rclone mount gdrive: ~/gdrive --vfs-cahce-mode full`
    + Auto mount with systemd
        * Create `~/.config/systemd/user/rclone-gdrive.service` with the
          below content.
        * Then enable it for the current user:
            - `systemctl --user daemon-reexec`
            - `systemctl --user enable --now rclone-gdrive`
        * Make sure systemd linger (allow user systemd services to keep
          running even log out) is enabled for the user:
            - `loginctl enable-linger $USER`
            - You can check with `loginctl show-user $USER` and look for
              `Linger=yes`

```
[Unit]
Description=Rclone Google Drive Mount
After=network-online.target

[Service]
Type=simple
ExecStart=/usr/bin/rclone mount gdrive: %h/gdrive \
  # Read
  --buffer-size 64M \
  --vfs-read-ahead 128M \
  --vfs-read-chunk-size 64M \
  --vfs-read-chunk-size-limit 2G \
  --vfs-read-chunk-streams 8 \
  # Write
  --vfs-cache-mode full \
  --vfs-write-back 10s \
  --transfers 16 \
  --checkers 16 \
  --tpslimit 10 \
  --tpslimit-burst 20 \
  # Cach
  --cache-dir %h/.cache/rclone \
  --vfs-cache-max-size 20G \
  --vfs-cache-max-age 24h \
  # Directory / Metadata
  --dir-cache-time 10m \
  --poll-interval 1m \
  --vfs-fast-fingerprint \
  # Latency / API Optimization
  --no-modtime \
  --no-checksum
ExecStop=/usr/bin/fusermount3 -u %h/gdrive
Restart=on-failure

[Install]
WantedBy=default.target
```

- Tune the rclone mount options:
    + `buffer-size` (RAM dependent)
    + `chunk-streams` (network speed dependent)
    + `cache size` (disk dependent)
