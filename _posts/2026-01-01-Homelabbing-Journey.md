---
layout: post
title: "Homelabbing Journey"
date: 2026-01-01 12:00:00 -0800
tags: [homelab, proxmox, kubernetes, breaking-stuff]
---

## The Start

A few months back, [a friend of mine](https://www.linkedin.com/in/krenken/) convinced me to start a homelab. Since starting my role at AWS, I've been quite deep into containerization and obviously the cloud, but it abstracted away all of the fun.

OpenClaw/model self-hosting wasn't all the rage yet, so a Mac Mini wasn't really on my mind. I ended up going with a [small mini PC](https://www.amazon.com/BOSGAME-P3-Gigabit-Ethernet-Computer/dp/B0FJ5WG23R/ref=zg_bs_g_13896591011_d_sccl_16/146-9186987-4223917?th=1) with an AMD Ryzen 7 5825U (8 cores, 16 threads), 32GB of DDR4, and 1 TB SSD. The linked mini PC isn't exaclty the same specs since they took down the unit I bought, but close enough.

This was also before the RAM craze, so this wasn't all that expensive, a little over $300 if I remember correctly. 

When it first arrived, I had messed around with it in the ways that seemed easiest (i.e. flash a drive with Ubuntu and host some stuff on there). Conatiners being my day job and all, I first was just running a set of containers via docker compose, reverse proxied by [Nginx Proxy Manager](https://nginxproxymanager.com/) (NPM). Below is essentially the YAML I had running, each domain (i.e. npm.chrdir.com, gatus.chrdir.com, docs.chrdir.com, etc.) would point to the private IP assigned by my routers DHCP and NPM would reverse proxy the traffic to the proper conatiner based on the host header.

```yaml
services:
  nginx-proxy-manager:
    image: 'jc21/nginx-proxy-manager:latest'
    ...
  speedtest-tracker:
    image: lscr.io/linuxserver/speedtest-tracker:latest
    ...
  gatus:
    image: twinproduction/gatus:latest
    ...
  bookstack:
    image: linuxserver/bookstack
    ...
    depends_on:
      - bookstack_db
  bookstack_db:
    image: linuxserver/mariadb
    ...
```

It was great! It worked and I didn't have to think about it at all. But that was the problem.. that wasn't why I wanted to start homelabbing. So I reflashed my drive with Proxmox......

## Virtualization (Proxmox)
Proxmox and adding virtualization is where things got interesting. I can't lie, I did watch a few Youtube videos on proxmox just to find my barrings. They helped for some of the basics (terminology, building first template etc.), but the main learning was actually using it.

Instead of running everything on baremetal (pre-proxmox), I started simple and essentially copied my docker compose setup onto a single VM that I had allocated 4cpu8gb and again, it worked well. I could keep using Bookstack for notes, and keep finding things on [awesome-selfhosted](https://awesome-selfhosted.net/index.html) that I may want to throw into the docker compose YAML.

### Access from the Internet

Since I was using A records pointed to a private IP for my subdomains, I came into an issue when I wanted to actually use the homelab outside of my house. It was easily accessible on my network, but lacked any accessibility 

Tailscale

CloudFlare tunnels

netbird my king

## Make it kubernetes

- eks-anywhere verizon router no like netboot
- To k3s
- CNI change, flannel to cilium (no-KP, talk about how cluster was completely broke)

- lowering the footprint, where am i wasting resources (moving)
- - my cluster manager, dont need it on always, can shutoff the cluster VMs, but that cant run in cluster, so LXC it


