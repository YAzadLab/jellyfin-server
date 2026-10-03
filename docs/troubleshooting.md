# Troubleshooting

## Jellyfin Could Not Access the Media Directory

### Problem

While configuring the Movies library, Jellyfin initially had difficulty accessing the media directory correctly.

The media directories had originally been created using `sudo`, meaning they were owned by `root`:

```text
root root
```

Jellyfin runs using its own Linux user account, so filesystem permissions needed to be configured correctly.

### Investigation

I checked the permissions of the media directories using:

```bash
ls -l /media/jellyfin
```

I also checked whether the Jellyfin user could access the Movies directory directly:

```bash
sudo -u jellyfin ls -la /media/jellyfin/movies
```

This allowed me to test access from the perspective of the account actually running the Jellyfin service.

I checked Jellyfin's group membership using:

```bash
groups jellyfin
```

### Solution

I created a shared `media` group and added both my user and the Jellyfin service account:

```bash
sudo groupadd media
sudo usermod -aG media yusuf
sudo usermod -aG media jellyfin
```

I changed the ownership and permissions of the media directory:

```bash
sudo chown -R yusuf:media /media/jellyfin
sudo chmod -R 775 /media/jellyfin
```

I then restarted Jellyfin so that the service used the updated group membership:

```bash
sudo systemctl restart jellyfin
```

Finally, I verified the service:

```bash
systemctl is-active jellyfin
```

and confirmed that the Jellyfin user could access the media directory.

### What I Learned

This demonstrated the importance of Linux file ownership and permissions when running services under separate user accounts.

Rather than giving Jellyfin unrestricted permissions, I used a shared Linux group to give the service access to only the directories it required.
