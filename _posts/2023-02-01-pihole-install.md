---
layout: post
title: "Pi-hole: Pi Rasbian and Ubuntu Installation"
date: 2023-02-01 18:24:00 -0100
categories: [Self-Hosted]
tags: [pi4,docker,docker-compose,guide]
---



Pi-hole is an open-source project that provides a network-wide ad-blocker that can be installed on a variety of devices, including the Raspberry Pi 4 and Ubuntu Linux. With its ability to block ads and tracking on all devices on a network, Pi-hole is a powerful tool that can greatly enhance the privacy and security of your online experience. 

In this blog post, we'll explore the benefits and capabilities of Pi-hole, and provide step-by-step guides for installation on both the Raspberry Pi 4 and Ubuntu Linux.

## Benefits of Pi-hole

**Network-Wide Ad Blocking:** Pi-hole blocks ads and tracking on all devices on a network, providing a clean and privacy-focused online experience for all users.

**Increased Privacy:** By blocking ads and tracking, Pi-hole helps to protect the privacy of users by preventing companies from collecting and using personal data.

**Reduced Bandwidth Usage:** By blocking ads, Pi-hole reduces the amount of data that needs to be downloaded, saving bandwidth and improving the overall speed of the network.

**Customization:** Pi-hole can be customized to block specific domains, making it easy to tailor the ad-blocking experience to individual needs.

## Capabilities of Pi-hole

**Ad Blocking:** Pi-hole blocks ads, tracking, and malicious domains, providing a clean and secure online experience.

**Reporting:** Pi-hole provides detailed reporting on the domains that have been blocked, making it easy to see which domains are being blocked and why.

**DHCP Server** Pi-hole has the ability to host its own DHCP server which can be benificial if your current router doesn't support static IP.

**Local DNS** Pi-hole allows for the the use of local dns. This can be useful when self-hosting many lan servers.

**DNS Over HTTPS (DoH):** Pi-hole supports the use of DoH, providing an encrypted connection between the device and the DNS resolver, improving privacy and security.

---

## Step-by-Step Installation of Pi-hole on Raspberry Pi 4

**Install Raspberry Pi OS:** Before installing Pi-hole, you'll need to install Raspberry Pi OS on your Raspberry Pi 4. You can download the latest version of Raspberry Pi OS from the official [Raspberry Pi website](https://www.raspberrypi.com/software/).

**Install Pi-hole:** To install Pi-hole on Raspberry Pi 4, you'll need to use the command line. To do this, open a terminal and run the following command:
```bash
curl -sSL https://install.pi-hole.net | bash
```
>This will download and run the Pi-hole installer, which will guide you through the installation process.

**Configure Pi-hole:** After the installation is complete, you'll need to configure Pi-hole. This includes setting the IP address of the Raspberry Pi 4, selecting the DNS resolver to use, and setting the web interface password.

---

## Step-by-Step Installation of Pi-hole on Ubuntu Linux

**Install Ubuntu:** Before installing Pi-hole, you'll need to install Ubuntu on your device. You can download the latest version of Ubuntu from the official [Ubuntu website](https://ubuntu.com/download/desktop).

**Install Pi-hole:** To install Pi-hole on Ubuntu, you'll need to use the command line. To do this, open a terminal and run the following command:
```bash
curl -sSL https://install.pi-hole.net | bash
```
>This will download and run the Pi-hole installer, which will guide you through the installation process.

Configure Pi-hole: After the installation is complete, you'll need to configure Pi-hole. This includes setting the IP address of the device, selecting the DNS resolver to use, and setting the web interface password

## Pi-hole Install Using Docker Compose
```yml
---
version: "3"

services:
 pihole:
   container_name: pihole
   image: pihole/pihole:latest
    #For DHCP it is recommended to remove these ports and instead add: network_mode: "host"
   ports:
     - "53:53/tcp"
     - "53:53/udp"
     - "88:88/tcp"
   environment:
     TZ: 'America/Los_Angeles'
     WEBPASSWORD: ''
    #Volumes store your data between container upgrades
   volumes:
     - './etc-pihole:/etc/pihole'
     - './etc-dnsmasq.d:/etc/dnsmasq.d'
     # https://github.com/pi-hole/docker-pi-hole#note-on-capabilities
    #Required if you are using Pi-hole as your DHCP server, else not needed
   restart: unless-stopped
```
>Visit my previous post for a Docker Compose installation guide on a [Rasberry Pi 4](https://docs.marsblars.dev/posts/docker-compose-pi4)

## Configuration of Pi-hole

**Login to the web interface:** Once Pi-hole is installed, you can access the web interface by navigating to `http://<IP address of Pi-hole>/admin` in your web browser. Log in using the username `admin` and the password you set during the installation process.
![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/f492ec3c-79cf-4f8c-9d5e-36b3839f47ad/1.5/50.752688172043/38.151086866683?0)

**Set up the network:** In the web interface, go to the `Settings` tab, and then click on the `DNS` sub-tab. Here, you can set the IP address of the device running Pi-hole as the primary DNS server for your network. You can also set a secondary DNS server, if desired.
![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/8d06a92f-d894-43ae-a642-f2c7e8b01fcb/2.5/70.045516475554/0?0)

**Configure the DNS resolver:** In the `DNS` sub-tab, you can select the DNS resolver that Pi-hole will use. The default resolver is Google, but there are several other options available, including OpenDNS and Cloudflare.
![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/e31cc476-6482-4774-9a7d-50a994049b20/2.5/35.350932459677/31.727014619779?0)

**Set up adlists:** Click on the `Adlists` tab. Here, you can add or remove adlists to determine which domains Pi-hole should block. There are several pre-configured adlists available, but you can also add custom adlists by entering the URL.
![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/3d214a72-1922-44a3-b36f-10eac805df4d/2.0910931174089/50.32705618813/25.620209709049?0)

**Whitelist domains:** If there are any domains that you don't want Pi-hole to block, you can add them to the whitelist. This can be useful when services aren't working properly like youtube not remembering your watch history. To do this, go to the `Domains` tab and enter the domains you want to allow. 
>To add multiple domains at once use:
>```bash
>pihole -w
>```
> To find domains to whitelist, visit [Commonly Whitelisted Domains](https://discourse.pi-hole.net/t/commonly-whitelisted-domains/212)
{: .prompt-tip }


**Save changes:** Once you have finished configuring Pi-hole, make sure to save your changes by clicking the `Save` button in the web interface.

By following these steps, you can fully configure Pi-hole to meet your specific needs and ensure a clean and secure online experience for all devices on your network.
