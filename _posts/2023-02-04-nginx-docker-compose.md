---
layout: post
title: "Hosting a Web Server using Nginx with Docker Compose"
date: 2023-02-04 22:24:00 -0100
categories: [Self-Host]
tags: [ngnix,website,docker,docker-compose]
--- 


In this post, we will discuss the benefits and capabilities of hosting a web server using Nginx with Docker Compose and provide step by step instructions to set it up.

## Benefits of using Nginx with Docker Compose:
- **Scalability:** With Docker Compose, it is easy to scale the number of Nginx containers to handle increasing traffic on your website.
- **Portability:** Your web server can be easily moved between different hosts as it is containerized with Docker.
- **Isolation:** Each container runs in its own isolated environment, reducing the risk of security vulnerabilities or system-wide changes affecting your web server.
- **Ease of deployment:** With Docker Compose, you can define and run multiple containers in a single file, making deployment and management much easier.

## Capabilities of Nginx:
- **Load balancing:** Nginx can distribute incoming traffic to multiple web servers, improving the reliability and performance of your website.
- **Reverse proxy:** Nginx can act as a reverse proxy, forwarding requests from clients to other servers and returning their responses.
- **Serving static content:** Nginx is known for its ability to serve static content such as images, stylesheets, and JavaScript files quickly and efficiently.
- **Security features:** Nginx can be configured to provide additional security features such as SSL termination, rate limiting, and basic authentication.

## Step by Step Instructions:
1. [Install Docker and Docker Compose](https://docs.marsblars.dev/posts/docker-compose-pi4/) on your host machine.
2. Create a new directory for your project and navigate to it in your terminal.
3. Create a new file called `dockerfile` and add the following content to it:
```dockerfile
FROM nginx:stable-alpine
COPY ./index.html /usr/share/nginx/html
```
1. Next create another file named `docker-compose.yml` and add the following:
```yml
version: '3'
services:
  nginx:
    build:
      context: .
      dockerfile: dockerfile
    ports:
      - "2000:80"
    volumes:
      - .:/usr/share/nginx/html/

```
4. Create a new file in the same directory called `index.html` and add some HTML content to it.
5. In your terminal, run 

```bash
docker compose up -d
```
to start your Nginx container.
1. In your web browser, visit `http://hostip:2000` to view your website.

That's it! You now have a fully functional Nginx web server running in a Docker container