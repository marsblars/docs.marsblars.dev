---
layout: post
title: "Creating a Discord Webhook using Tautulli for Plex"
date: 2023-03-04 22:24:00 -0100
categories: [Media-Server]
tags: [Discord,Webhook,Tautulli,Plex]
--- 

Discord is a popular messaging platform used by millions of people around the world. It allows users to communicate with others via text, voice, and video, making it a great tool for online communities. Discord also has a feature called webhooks that allows users to send automated messages to channels or groups.

Tautulli is a popular third-party tool for Plex that provides various statistics and monitoring features for Plex Media Server. One of the many features of Tautulli is the ability to send notifications to various messaging platforms, including Discord.

## Benefits of Using Discord Webhook with Tautulli

Using a Discord webhook with Tautulli has several benefits, including:

1. Instant Notifications - With a webhook, you can receive instant notifications about events happening in your Plex Media Server. This means you can be alerted when a new movie is added or when a user starts watching a show.
2. Customization - Webhooks allow you to customize your notifications by adding your own messages or formatting the notification message.
3. Organization - Using webhooks, you can easily organize your notifications by creating separate channels or groups for specific types of notifications.

## Capabilities of Discord Webhook with Tautulli

Using a Discord webhook with Tautulli provides several capabilities, including:

1. Sending notifications for new media added to Plex Media Server.
2. Sending notifications for new users added to Plex Media Server.
3. Sending notifications for when a user starts watching a movie or TV show.
4. Sending notifications for when a user stops watching a movie or TV show.
5. Sending notifications for when a user pauses, resumes, or stops playback.
6. Sending notifications for when a user requests a movie or TV show.

## Step-by-Step Instructions to Create a Discord Webhook Using Tautulli

To create a Discord webhook using Tautulli, follow these steps:

1. Create a Webhook in Discord
   - Open Discord and navigate to the server/channel where you want to receive notifications.
   - Click on the server/channel settings and select "Integrations" and then click "Webhooks."
   - Click "Create Webhook" and follow the instructions to set up your webhook.

2. Configure Tautulli to Use the Webhook
   - Open Tautulli and navigate to "Settings" and then "Notification Agents."
   - Click on "Add a new notification agent" and select "Webhook"
   - Fill in the Discord webhook URL using POST as the method.
   - Select the events you want to receive notifications for, and paste your custom json in the data tab for each event.
## Example Webhook:

```json

    {
    "embeds": [
        {
            "color": 16556313,
            "fields": [
                {
                    "inline": true,
                    "name": "Source Quality",
                    "value": "<movie>[{video_full_resolution}]</movie><episode>[{video_full_resolution}]</episode><track>[{audio_codec}]</track>"
                },
                	<episode>{
                    "inline": true,
                    "name": "Season/Episode",
                    "value": "S**{season_num00}**E**{episode_num00}**"
                }, </episode>
                <movie>{
                    "inline": true,
                    "name": "IMDb Rating",
                    "value": "🍿{rating}"
                },</movie>
                <track>{
                    "inline": true,
                    "name": "Artist/Album",
                    "value": "Artist - {artist_name}/Album - {album_name}"
                },</track>
                {
                    "inline": true,
                    "name": "Details",
                    "value": "<episode>[Series Info]({imdb_url})</episode><movie>[Movie Info]({imdb_url})</movie><track>[Track Info]({musicbrainz_url})</track>"
                },
                {
                    "inline": true,
                    "name": "<episode>Watch Now</episode><movie>Watch Now</movie><track>Listen Now</track>",
                    "value": "[Plex Web]({plex_url})"
                }
            ],
            "thumbnail": {
                "url": "{poster_url}"
            },
            "title": "{title} <movie> ({year})</movie>",
            "description": "{summary}",
            "timestamp": "{utctime}",
            "url": "{plex_url}",
            "footer": {
                "text": "{server_name} | {username} | {video_decision!c} | {device} | {media_type!c}"
            }
        }
        
    ],
    "username": "Plex - {library_name}"
    }

```

3. Test the Webhook
   - Click "Save" to save the new notification agent.
   - Click "Test" to send a test message to the Discord channel.
   - Check the Discord channel to make sure the notification was sent correctly.

## Conclusion

Using a Discord webhook with Tautulli provides many benefits, including instant notifications, customization, and organization. With the step-by-step instructions above, you can set up a webhook in Discord and configure Tautulli to send notifications to the channel or group of your choice. By doing so, you can stay up-to-date with what is happening on your Plex Media Server and respond to events quickly and efficiently.
