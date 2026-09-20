# rukasu/rockylinux — Dockerfiles

Dockerfiles for the [`rukasu/rockylinux`](https://hub.docker.com/r/rukasu/rockylinux) Docker Hub image family.  
Rocky Linux 9.3 containers pre-configured with SSH access and Fastfetch.

---

## Tags

| Tag | Description |
|-----|-------------|
| [`1.0`](./1.0/Dockerfile) | OpenSSH + Fastfetch |
| [`1.1-docker`](./1.1-docker/Dockerfile) | OpenSSH + Fastfetch + Docker CLI (host engine sharing) |

---

## Usage

### Tag `1.0`

```bash
docker run -d \
  --name rocky-ssh \
  -p 2222:22 \
  rukasu/rockylinux:1.0
```

### Tag `1.1-docker`

```bash
docker run -d \
  --name rocky-docker \
  -p 2222:22 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  rukasu/rockylinux:1.1-docker
```

> The `-v /var/run/docker.sock:/var/run/docker.sock` flag is required for Docker CLI to work. It shares the host Docker engine with the container.

---

## Connecting

```bash
ssh root@<HOST_IP> -p 2222
# password: rockylinux
```

If you get a fingerprint mismatch after recreating the container:

```bash
ssh-keygen -R [<HOST_IP>]:2222
```

---

## Repository Structure

```
.
├── 1.0/
│   └── Dockerfile
├── 1.1-docker/
│   └── Dockerfile
└── README.md
```

---

## Base Image

[`rockylinux:9.3.20231119`](https://hub.docker.com/_/rockylinux)

You can run 

```bash
docker run -d --name rockylinux -p 2222:22 rukasu/rockylinux:1.0 sleep infinity

docker exec -it rockylinux /bin/bash
```

OR

```bash
docker run -d --name rocky-docker -p 2222:22 -v /var/run/docker.sock:/var/run/docker.sock rukasu/rockylinux:1.1-docker sleep infinity

docker exec -it rocky-docker /bin/bash
```
