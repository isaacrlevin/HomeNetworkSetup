# My Home Network/Docker Setup

## Intro

I have 2 Raspberry Pi 4bs in my house that is running a handful of docker containers to do MISC things on my home network and I wanted to be able to easily
reach these services and have a more managed approach. I decided that I wanted to configure a Reverse Proxy to forward all my services under a single domain.
This repo is what I have currently configured on my home network, and includes docker-compose yml files, and scripts to set up a similar environment.

#### **NOTE: The docker images below all have ARM tags, so make sure that if you aren't using ARM that the image has the arch you need**

## Prerequisites

- [**READ THIS**](https://www.smarthomebeginner.com/traefik-2-docker-tutorial) as I followed it very closely (and stole code/files) to do my setup.
- Bookmark these Repos
  -  https://github.com/htpcBeginner/docker-traefik
  - https://github.com/CVJoint/traefik2
- Have [docker installed](https://docs.docker.com/engine/install/debian/) on your devices
  - Post Install Docker Things

```bash
# Create docker group and add user to it (allows non-root to run docker)
sudo groupadd docker
sudo usermod -aG docker <youruser>`
newgrp docker

# Run docker at startup
sudo systemctl enable docker
```

- Have [docker-compose](https://docs.docker.com/compose/install) installed on your devices
  - I personally used the [pip install ](https://docs.docker.com/compose/install/#install-using-pip)
- Buy a domain (I did it on [Google Domains](https://domains.google/))
- [Configure your domain](https://support.cloudflare.com/hc/en-us/articles/360027989951-Getting-Started-with-Cloudflare) on Cloudflare
- [Port forward](https://www.smarthomebeginner.com/setup-port-forwarding-on-router/) your router
- Clone this repo wherever you want your docker stuff to be
  - `git clone https://github.com/isaacrlevin/HomeNetworkSetup.git docker`
  - Configure appropriate permissions on folders/file

```bash
sudo setfacl -Rdm g:docker:rwx ~/docker
sudo chmod -R 775 ~/docker
chmod 600 ~/docker/traefik/acme/acme.json
```
- Create Traefik Proxy Network

`docker network create --gateway 192.168.50.1 --subnet 192.168.50.0/24 traefik_proxy`

- **OPTIONAL**
  - If you want to be able to monitor both Rasperry Pis in the same Portainer instance, you will need to enable a TLS Remote Endpoint
    - https://lemariva.com/blog/2019/12/portainer-managing-docker-engine-remotely

## Ok Now What?

At this point you should have an environment ready to start building containers. At this point, you can follow the [**BLOG**](https://www.smarthomebeginner.com/traefik-2-docker-tutorial)(starting [**HERE**](https://www.smarthomebeginner.com/traefik-2-docker-tutorial/#Traefik_2_Docker_Compose)) and start configuring to your heart's content.

### Few things to point out

- You really need to take a look at the Traefik configuration section of the blog. More than likely OOB my setup will work for you, but you should take a look at the `.bash_aliases` as they are super helpful, as well as the .env file in the `ymlfiles` directory.
- I added a `resolv.conf` to this repo as I had a problem with DNS on SOME containers. Mounting this file inside the container (done in the yml files) resolved it (PUN INTENDED).
- Since some of my services run on a host that Traefik is not configured on, I need to configure a rule to forward those requests. For instance [here](https://raw.githubusercontent.com/isaacrlevin/HomeNetworkSetup/main/traefik/rules/app-pihole.toml) is how I do it for Pi Hole

### Reach out if you want to chat!

I am not even close to an expert on these things, but I was able to hack away to get what I was looking for, and I am pretty happy with it. All my services are accessible outside my network and are secured with Google Auth. Is this the best/safest implementation? NO! If you want to know how I did some of this stuff, or want to chat, hit me up on [Discussions](https://github.com/isaacrlevin/HomeNetworkSetup/discussions)
