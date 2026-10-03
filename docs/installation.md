# Jellyfin Installation

## System

- OS: Ubuntu 24.04.3 LTS
- Architecture: 64-bit

## Updating the system

Before installing Jellyfin, I updated the package lists and upgraded
the existing packages.

Commands used:

```bash
sudo apt update
sudo apt upgrade
...

## Installing Jellyfin

I installed Jellyfin directly on Ubuntu rather than using Docker. This allows Jellyfin to run as a system service managed by systemd.

I downloaded the official Jellyfin Debian/Ubuntu installation script and its checksum:

```bash
curl -s https://repo.jellyfin.org/install-debuntu.sh -O
curl -s https://repo.jellyfin.org/install-debuntu.sh.sha256sum -O
```

Before running the script, I verified that the downloaded file matched the checksum:

```bash
sha256sum -c install-debuntu.sh.sha256sum
```

The result returned:

```text
install-debuntu.sh: OK
```

I also inspected the installation script before executing it:

```bash
less install-debuntu.sh
```

I then ran the installer:

```bash
sudo bash install-debuntu.sh
```

After installation, Jellyfin was configured as a systemd service and started automatically.

## Verifying the Service

I checked whether the Jellyfin service was running using:

```bash
systemctl is-active jellyfin
```

The service returned:

```text
active
```

I also confirmed after rebooting the machine that Jellyfin started automatically.

The web interface can be accessed on port `8096` from a browser on the local network.
