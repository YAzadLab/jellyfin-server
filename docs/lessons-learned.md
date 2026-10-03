# Lessons Learned

Building this Jellyfin server gave me practical experience with Linux system administration, networking, permissions and troubleshooting.

## Linux Services

I learned how applications such as Jellyfin can run as background services rather than needing to be manually started every time the computer boots.

I used `systemctl` to restart Jellyfin and check whether the service was running. This helped me understand how `systemd` manages services on Linux.

## Linux Users, Groups and Permissions

One of the main problems I encountered was Jellyfin being unable to access the media directories correctly.

Jellyfin runs under its own Linux user rather than under my personal account. This meant that creating a directory did not automatically guarantee that the Jellyfin service could access it.

I learned how Linux ownership and permissions control access to files and directories. Instead of giving unrestricted permissions, I created a shared `media` group and gave both my user and the Jellyfin user access to it.

This gave me a better understanding of the principle of least privilege: a service should only receive the permissions it actually requires.

## Networking

I learned how an application running on one computer can be accessed by other devices across a local network.

My server uses the local IPv4 address `192.168.1.50`, while Jellyfin listens for TCP connections on port `8096`.

This helped me understand the distinction between an IP address and a port. The IP address identifies the device on the network, while the port identifies a particular service running on that device.

I also verified that Jellyfin was listening on the server's network interfaces and successfully connected to it from another device on the same network.

## Static IP Addressing

I learned why servers benefit from having a static local IP address.

My server is manually configured to use `192.168.1.50`. This provides a predictable address for devices connecting to Jellyfin instead of relying on an address that could change dynamically.

I also investigated the server's routing table and identified `192.168.1.1` as the default gateway used to reach networks outside the local subnet.

## Troubleshooting

A major lesson from this project was the importance of investigating a problem rather than immediately changing configuration.

I used commands such as `systemctl`, `ss`, `nmcli`, `ip route`, `ls` and `groups` to inspect the current state of the system before making changes.

For example, when Jellyfin had difficulty accessing the media directory, I checked the directory ownership and tested access as the Jellyfin user. This allowed me to identify the permissions problem rather than simply giving the directory unrestricted permissions.

## Git and SSH

I also used Git and GitHub to document the project as I worked on it.

I learned the difference between staging changes with `git add`, creating a local commit with `git commit`, and uploading commits to a remote repository with `git push`.

Initially I authenticated Git operations over HTTPS using a Personal Access Token. I later configured SSH public-key authentication by generating an Ed25519 key pair, adding the public key to GitHub and changing the repository remote from HTTPS to SSH.

This helped me understand how public-key authentication allows a remote service to verify possession of a private key without the private key itself being shared.

## Overall

This project improved my understanding of how several areas of computing work together in a real system. Rather than treating Linux, networking, permissions, services and Git as separate topics, I was able to use them together to configure and troubleshoot a working media server.
