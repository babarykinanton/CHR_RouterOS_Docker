# Mikrotik RouterOS in Docker

This extrasmall image was created for tests purpose only, for example on
this project based unit testing of [routeros-api-php](https://github.com/EvilFreelancer/routeros-api-php) library.

If you need fully functional "RouterOS in Docker" for production usage
look at [VR Network Lab](https://github.com/plajjan/vrnetlab) project.

## How to use

### Create your own `Dockerfile`

List of all available tags is [here](https://hub.docker.com/r/evilfreelancer/docker-routeros/tags/),
`latest` will be used by default.

```dockerfile
FROM evilfreelancer/docker-routeros
ADD ["your-scripts.sh", "/"]
RUN /your-scripts.sh
```

### Use image from docker hub

```bash
docker pull evilfreelancer/docker-routeros
docker run -d -p 22:22 -p 8728:8728 -p 8729:8729 -ti evilfreelancer/docker-routeros
```

### Use in docker-compose.yml

```yml
version: "2"

services:

  routeros-legacy:
    image: evilfreelancer/docker-routeros:6.42
    restart: unless-stopped
    ports:
      - 12222:22
      - 18728:8728
      - 18729:8729

  routeros-modern:
    image: evilfreelancer/docker-routeros:6.43
    restart: unless-stopped
    ports:
      - 22222:22
      - 28728:8728
      - 28729:8729
```

### Build from sources

For this you need download project and build everything from scratch:

```bash
git clone https://github.com/EvilFreelancer/docker-routeros.git
cd docker-routeros
docker build . --tag ros
docker run -d -p 22222:22 -p 8728:8728 -p 8729:8729 -ti ros
```

Now you can connect to your RouterOS container via VNC protocol
and via SSH on localhost 2222 port.

## List of exposed ports

For access via VNC: 5900

Default ports of RouterOS: 21, 22, 23, 80, 443, 8291, 8728, 8729
