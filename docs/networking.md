# Networking

## Jellyfin Port

Jellyfin uses TCP port `8096` by default for its HTTP web interface.

I verified that Jellyfin was listening on this port using:

```bash
sudo ss -tulpn | grep 8096
```

The output showed:

```text
tcp LISTEN 0 512 0.0.0.0:8096 0.0.0.0:* users:(("jellyfin",...))
```

This confirmed that the Jellyfin process was listening for TCP connections on port `8096`.

The address `0.0.0.0:8096` means Jellyfin is listening on port 8096 across the server's IPv4 network interfaces rather than only accepting connections from the local machine.

## Local IP Address

I found the server's local IP address using:

```bash
hostname -I
```

The server's IPv4 address on my local network was:

```text
192.168.1.50
```

Devices on the same local network can therefore access the Jellyfin web interface using:

```text
http://192.168.1.50:8096
```

The IP address identifies the Ubuntu server on the local network, while port `8096` identifies the Jellyfin service running on that server.

## Firewall

I checked the status of Ubuntu's UFW firewall using:

```bash
sudo ufw status
```

The result was:

```text
Status: inactive
```

This showed that UFW was not currently filtering incoming connections to the server.

## Testing LAN Access

To verify that Jellyfin was accessible from another device, I connected my phone to the same local network and opened:

```text
http://192.168.1.50:8096
```

The Jellyfin interface loaded successfully and I was able to log in.

This confirmed that the Jellyfin server was accessible from another device across the local network.

## Static IP Configuration

I verified the server's IPv4 configuration using:

```bash
nmcli connection show "CommunityFibre10Gb_AC36D" | grep ipv4
```

The configuration showed:

```text
ipv4.method:       manual
ipv4.addresses:    192.168.1.50/24
ipv4.gateway:      192.168.1.1
```

The `manual` IPv4 method confirms that the server is configured with a static local IP address of `192.168.1.50`.

Using a static IP is useful for a server because other devices can consistently connect to the same address rather than relying on an address that may change through DHCP.

The `/24` prefix represents the local subnet, while `192.168.1.1` is the default gateway used to reach networks outside the local subnet.
