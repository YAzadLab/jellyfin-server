# Jellyfin Media Server

A self-hosted Jellyfin media server running on Ubuntu Linux, built to gain practical experience with Linux system administration, networking, permissions, troubleshooting and Git.

The server hosts media on the local network and can be accessed by other devices using Jellyfin's web interface.

## Project Overview

This project involved installing and configuring Jellyfin on an Ubuntu machine and configuring the surrounding Linux and network environment required to run it as a server.

The project included:

- Installing and managing Jellyfin as a Linux service
- Creating and configuring media directories
- Managing Linux users, groups and file permissions
- Configuring a static IPv4 address
- Investigating TCP ports and listening services
- Testing Jellyfin access from another device on the LAN
- Investigating firewall configuration
- Troubleshooting service and permission problems
- Documenting the project using Git and GitHub
- Configuring SSH public-key authentication for GitHub

## Architecture

```text
                    Local Network
                         |
            +------------+------------+
            |                         |
       Ubuntu Server               Client
       192.168.1.50            Phone / Browser
            |
            |
     Jellyfin Service
       TCP :8096
            |
            |
    /media/jellyfin/
       |          |
     movies       tv
```

Jellyfin listens for TCP connections on port `8096` and is accessible to devices on the same local network.

The Ubuntu server uses the static local IPv4 address `192.168.1.50`.

## Technologies and Tools

- Ubuntu Linux
- Jellyfin
- systemd / systemctl
- Linux users, groups and permissions
- TCP/IP networking
- NetworkManager / nmcli
- UFW
- Git
- GitHub
- SSH public-key authentication

## Documentation

Detailed documentation for the project is available here:

- [Installation](docs/installation.md)
- [Configuration](docs/configuration.md)
- [Networking](docs/networking.md)
- [Troubleshooting](docs/troubleshooting.md)
- [Lessons Learned](docs/lessons-learned.md)

## Key Lessons

This project helped me understand how Linux services, file permissions and networking work together when hosting a service.

One of the main troubleshooting challenges involved giving the Jellyfin service access to media directories without using unnecessarily permissive file permissions. I solved this using Linux users, groups and ownership.

I also investigated how the server communicates across the local network, including static IP addressing, TCP ports, network interfaces, routing and firewall configuration.

## Future Improvements

Possible future improvements include:

- Enabling secure remote access
- Configuring HTTPS
- Adding automated backups
- Monitoring server resource usage
- Expanding storage
- Adding additional server monitoring and security controls
