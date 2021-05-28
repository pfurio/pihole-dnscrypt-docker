<div align="center">
<p align="center">
  <a href="https://github.com/pfurio/pihole-dnscrypt-docker">
    <img src="img/logo.png" alt="logo" width="150" height="150">
  </a>

  <p align="center">
    <h3 align="center">Pi-hole DNSCrypt Docker</h3>
    <p align="center">
      A docker-compose for Pi-hole and DNSCrypt ready to work on a Synology NAS server.
    </p>
  </p>
</p>
</div>

## Dependencies

```
docker
docker-compose
```

### Uses the following Docker containers:

- https://github.com/pi-hole/docker-pi-hole
- https://github.com/klutchell/dnscrypt-proxy

## Table of Contents

- [Configuration](#configuration)
- [Installation](#installation)
- [Updating images](#updating-images)

## Configuration

Edit `docker-compose.yml` in the following ways.

Uncomment `WEBPASSWORD` and put in a password, by default it will be randomized.

```yaml
WEBPASSWORD: 'password'
```

Uncomment `TZ` and put in your timezone, default is UTC.

- On Linux you can use `timedatectl list-timezones` to find the correct timezone.

```yaml
TZ: 'America/Chicago'
```

Edit `etc-dnscrypt-proxy/dnscrypt-proxy.toml` to your preference.

## Installation

1. Clone this repository in /volume1/docker/pihole-dnscrypt/ inside your NAS.

    ```
    git clone https://github.com/pfurio/pihole-dnscrypt-docker
    ```

2. Create missing directories:
  ```
    mkdir /volume1/docker/pihole-dnscrypt/etc-pihole/
    mkdir /volume1/docker/pihole-dnscrypt/etc-dnsmasq.d/
  ```

3. Copy docker-compose.yml file as a new Portainer stack and deploy.

4. Change router DNS server to point to your NAS server.

## Updating images

1. To update all images used by this docker-compose.

    ```
    sudo docker-compose pull
    ```

2. Restart the systemd service.

    ```
    sudo systemctl restart pihole-dnscrypt-docker
    ```

List old/unused images.

```
sudo docker images -f dangling=true
```

Remove old/unused images.

```
sudo docker image prune
```
