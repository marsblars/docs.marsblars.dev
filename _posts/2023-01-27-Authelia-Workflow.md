--- 
layout: post
title: "Authelia: The Next Generation Authentication and Authorization Solution for Docker"
date: 2023-01-27 16:17:00 -0500
categories: [Security]
tags: [authelia,docker,docker-compose]
---


Authelia is a modern and secure authentication and authorization solution designed to work seamlessly with Docker and Docker Compose. With its advanced features and intuitive user interface, Authelia provides a secure and user-friendly way to manage access to your Docker applications.

In this blog post, we will explore the benefits and capabilities of using Authelia with Docker, and provide a step-by-step guide to install and configure it using Docker Compose. We will also show you how to integrate Traefik with Authelia for a complete and secure Docker environment.

## Benefits of Authelia on Docker

1. Easy installation and setup: Authelia is designed to work seamlessly with Docker, making it easy to install and configure. You can get started with Authelia in just a few steps, without having to worry about complex dependencies or configurations.

2. Secure authentication and authorization: Authelia provides a secure and user-friendly way to manage access to your Docker applications. With its advanced features and intuitive user interface, you can easily manage user accounts and permissions, and ensure that only authorized users have access to your sensitive data.

3. Scalability: Authelia is designed to be scalable and performant, allowing you to easily manage large numbers of users and applications. Whether you have a small team or a large organization, Authelia can handle your authentication and authorization needs.

4. Integration with popular tools: Authelia integrates seamlessly with popular tools like Traefik, providing a complete and secure solution for your Docker environment.

## Install and Configure Authelia on Docker

Here is a step-by-step guide to install and configure Authelia using Docker Compose:

1. Install [Docker and Docker Compose](https://docs.marsblars.dev/posts/docker-compose-pi4/) on your machine.

2. Create a new directory for your project and navigate to it in the terminal.
```bash
mkdir authelia
cd authelia
```

3. Create a new file named "docker-compose.yml" in the project directory.
```bash
nano docker-compose.yml
```

4. In the "docker-compose.yml" file, define the services for Authelia:

```yml
version: '3'
services:
authelia:
image: authelia/authelia:latest
environment:
AUT_DEBUG: true
AUT_HOSTNAME: authelia.localhost
ports:
- "9091:9091"
```
5. Include a `configuration.yml` and `users_database.yml` file in the same directory:

>`configuration.yml`

```yml
---
theme: dark
jwt_secret: "VkYp2s5v8y/B?E(H+MbQeThWmZq4t6w9"
default_redirection_url: https://example.com/
server:
  host: 0.0.0.0
  port: 9091
  path: ""
  read_buffer_size: 4096
  write_buffer_size: 4096
  enable_pprof: false
  enable_expvars: false
  disable_healthcheck: false
  tls:
    key: ""
    certificate: ""
log:
  level: debug
totp:
  issuer: example.com
  period: 30
  skew: 1
authentication_backend:
  password_reset:
    disable: false
  refresh_interval: 5m
  file:
    path: /config/users_database.yml
    password:
      algorithm: argon2id
      iterations: 1
      key_length: 32
      salt_length: 16
      memory: 1024
      parallelism: 8
access_control:
  default_policy: deny
  rules:
    - domain:
        - "auth.example.com"
      policy: bypass
    - domain:
        - "overseerr.example.com"
      policy: bypass
    - domain: "*.example.com"
      resources:
        - "^/api([/?].*)?$"
      policy: bypass
    - domain:
        - "*.example.com"
      subject:
        - group:admins
      policy: one_factor
session:
  name: authelia_session
  domain: example.com
  same_site: lax
  secret: ""
  expiration: 1h
  inactivity: 5m
  remember_me_duration: 2M
  redis:
    host: redis
    port: 6379
    password: "Marselo1"
    database_index: 0
    maximum_active_connections: 10
    minimum_idle_connections: 0
regulation:
  max_retries: 3
  find_time: 10m
  ban_time: 12h
storage:
  encryption_key: ""
  mysql:
    host: mariadb
    port: 3306
    database: authelia
    username: authelia
    password: ""
notifier:
 # disable_startup_check: false
 # smtp:
 #   username: xbox720730@gmail.com
  #  password: "M5UjctvZB8iutbYL!y"
   # host: smtp.gmail.com
  #  port: 587
  #  sender: xbox720730@gmail.com
   # identifier: localhost
  #  subject: "[Authelia] {title}"
 #  startup_check_address: test@authelia.com
 #   disable_require_tls: false
 #   disable_html_emails: false
 #   tls:
  #    skip_verify: false
  #    minimum_version: TLS1.2
  filesystem:
    filename: /config/notification.txt
...
```

>`users_database.yml`

```yml
---
###############################################################
#                         Users Database                      #
###############################################################

# This file can be used if you do not have an LDAP set up.

# List of users
users:
  marbles:
    displayname: "Marbles"
    # Password is Authelia
    password: "$argon2id$v=19$m=65536,t=3,p=4$vOz5QfqZLs1jwOrkFO/EXA$EeWKEKJmrHUxtysv4FoSN4IqJU4HYnDf9Gh7ReLvGMs" 
    email: xbox720730@gmail.com
    groups:
      - admins
      - dev
...
```

---

## Authelia and Code-Server Workflow Example

1\. Go to protected Site
---

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/f6a44501-1200-40ba-8b38-0edcec9582c1/1.5/50/50?0)
>Site redirects to Authelia domain

2\. Sign in to authelia
---------------------------------------------------------------------------------------------------------------------

>users are stored in `users_database.yml` file

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/f4aa4d1e-0c92-40e9-a6d2-41f430280c17/1/0/0?0)

3\. Proceed to Protected Domain
-------------------------------------------------------------------------

>code-server on docker requires **Yes, I trust the authors** to be clicked

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/a45df2f1-68dd-4453-937f-ab4a5101c2d5/1.5/0/0?0)

---
## Conclusion
In conclusion, Authelia is a powerful and user-friendly solution for authentication and authorization in Docker environments. With its advanced features and seamless integration with popular tools like Traefik, Authelia provides a secure and scalable way to manage access to your Docker applications. By using Docker Compose, the installation and configuration of Authelia can be done quickly and easily, allowing you to focus on what really matters - your applications and users. In this blog post, we have explored the benefits and capabilities of using Authelia with Docker and provided a step-by-step guide to install and configure it. If you are looking for a modern and secure solution for authentication and authorization in your Docker environment, Authelia is definitely worth considering.

