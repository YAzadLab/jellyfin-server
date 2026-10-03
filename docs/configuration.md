# Jellyfin Configuration

## Media Directories

I created separate directories for movies and TV shows under `/media/jellyfin`:

```bash
sudo mkdir -p /media/jellyfin/movies
sudo mkdir -p /media/jellyfin/tv
```

This keeps different types of media organised and allows them to be configured as separate Jellyfin libraries.

## User and Group Permissions

Jellyfin runs under its own Linux user rather than my normal user account. Therefore, I needed to configure permissions so that both my user and the Jellyfin service could access the media directories.

I created a shared `media` group:

```bash
sudo groupadd media
```

I added my user and the Jellyfin service user to the group:

```bash
sudo usermod -aG media yusuf
sudo usermod -aG media jellyfin
```

I then changed the ownership of the media directory:

```bash
sudo chown -R yusuf:media /media/jellyfin
```

Finally, I configured the directory permissions:

```bash
sudo chmod -R 775 /media/jellyfin
```

The `775` permissions give the owner and members of the `media` group read, write and execute permissions, while other users receive read and execute permissions.

After changing the Jellyfin user's group membership, I restarted the service:

```bash
sudo systemctl restart jellyfin
```

I verified that Jellyfin was running successfully:

```bash
systemctl is-active jellyfin
```

which returned:

```text
active
```

## Jellyfin Libraries

Inside the Jellyfin web interface I configured two libraries:

- **Movies** → `/media/jellyfin/movies`
- **TV Shows** → `/media/jellyfin/tv`

Jellyfin can then scan these directories and automatically retrieve metadata and artwork for recognised media.
