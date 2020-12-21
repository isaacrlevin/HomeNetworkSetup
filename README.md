# My Home Network/Docker Setup

## Intro

I have 2 Raspberry Pi 4bs in my house that is running a handful of docker containers to do MISC things on my home network and I wanted to be able to easily
reach these services and have a more managed approach. I decided that I wanted to configure a Reverse Proxy to forward all my services under a single domain.
This repo is what I have currently configured on my home network, and includes docker-compose yml files, and scripts to set up a similar environment.

## Prerequisites

- [READ THIS](https://www.smarthomebeginner.com/traefik-2-docker-tutorial) as I followed it very closely (and stole code/files) to do my setup.
- Bookmark these Repos
  -  https://github.com/htpcBeginner/docker-traefik
  - https://github.com/CVJoint/traefik2
- Have [docker installed](https://docs.docker.com/engine/install/debian/) on your devices
- Have [docker-compose](https://docs.docker.com/compose/install) installed on your devices
  - I personall used the [pip install ](https://docs.docker.com/compose/install/#install-using-pip)
- Buy a domain (I did it on [Google Domains](https://domains.google/))
- [Configure your domain](https://support.cloudflare.com/hc/en-us/articles/360027989951-Getting-Started-with-Cloudflare) on Cloudflare