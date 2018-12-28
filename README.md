# Wireguard tools

This is a simple script and systemd unit file to setup wireguard tunnels automatically.

It's old, but I was asked at #35c3 to upload it somewhere, so here it is.

## Installation

Copy the contents of `bin` to `/usr/local/bin` and the contents of `systemd` to
`/etc/systemd/system`. Reload your systemd daemon (`systemctl daemon-reload`).

You may want to adjust the `wireguard` script inside `bin` to not use link up/down
scripts.

## Configuration of tunnels

Create two files per tunnel, using the examples below. You may have to create link up/down
scripts named `$name-up.sh` and `$name-down.sh`, those will be executed after the link is up
and before it is destroyed.

### /etc/wireguard/`$name`.sh

```sh
# ipv4 address of your peer
IPv4_REMOTE=
# your ipv4 address
IPv4_LOCAL=

# the same for v6
IPv6_REMOTE=
IPv6_LOCAL=
```

### /etc/wireguard/`$name`.conf

This is the normal wireguard configuration file, an example is below:

```
[Interface]
PrivateKey = 
[Peer]
PublicKey = 
AllowedIPs = 0.0.0.0/0, ::/0
Endpoint = 
```

Insert the required information as documented by wireguard, you may need other fields
in your config.

## Usage

```sh
systemctl enable --now wireguard@$name.service
systemctl disable --now wireguard@$name.service
systemctl restart --now wireguard@$name.service
systemctl start --now wireguard@$name.service
systemctl stop --now wireguard@$name.service
```
