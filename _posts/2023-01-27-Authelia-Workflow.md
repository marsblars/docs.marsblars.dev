--- 
layout: post
title: "Workflow with Authelia and Protected Domain"
date: 2023-01-27 16:17:00 -0500
categories: [Security]
tags: [authelia,docker,code-server]
---



1\. Go to protected Site
----------------------------------------------------------------------------------------------------------------------

Site redirects to Authelia domain

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/f6a44501-1200-40ba-8b38-0edcec9582c1/1.5/50/50?0)

2\. Sign in to authelia
---------------------------------------------------------------------------------------------------------------------

users are stored in users\_database.yml file

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/f4aa4d1e-0c92-40e9-a6d2-41f430280c17/1/0/0?0)

3\. [Proceed to Protected Domain]
-------------------------------------------------------------------------

code-server on docker requires **Yes, I trust the authors** to be clicked

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/a45df2f1-68dd-4453-937f-ab4a5101c2d5/1.5/0/0?0)