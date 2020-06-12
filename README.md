# Another Ansible Netdata Role

This Ansible role installs Netdata. It was written to be used with [Trellis](https://github.com/roots/trellis).

Now you can monitor your Trellis deploy(s) from a browser or Discord. That's cool.

I'll pkg on ansible-galaxy when it's finished.

## Install

First, you'll need to clone this repo into `roles/netdata`.

Next, add the following to your `wordpress_sites` definition on whatever site you would like to enable netdata access on. You can add it to multiple sites but there is no point if they share a server.

This addition supplies a child nginx template that serves the dashboard on requests to `/netdata`.

```yml
# wordpress_sites.yml

wordpress_sites:
  example_site:
    nginx_wordpress_site_conf: roles/netdata/templates/netdata-nginx.conf.child
```

Add the netdata role to `server.yml`. I think it makes sense right after nginx.

```yml
# server.yml

    # ...
    - { role: netdata, tags: [netdata, nginx] }
    # ...
```

## Basic auth (optional)

The netdata dashboard is read-only and exposes nothing that is explicitly secret. Stil, you may wish to limit its availability.

Add the following variables into the target `main.yml` to password protect `/netdata`.

```yml
# main.yml

netdata_user: admin
netdata_password: generate_me
```

## API auth (optional)

Netdata exposes a pretty nice API. You can lock it down if you're worried about security.

```yml
# main.yml

netdata_api_key: generate_me
```

## Notification services (optional)

Netdata supports a ton of alerting/pager services and team workplace apps, etc.

```yml
# main.yml

netdata_slack_webhook_url:
netdata_msteam_webhook_url:
netdata_rocketchat_webhook_url:
netdata_alerta_webhook_url:
netdata_alerta_api_key:
netdata_flock_webhook_url:
netdata_discord_webhook_url:
netdata_pushover_app_token:
netdata_pushbullet_access_token:
netdata_pushbullet_source_device:
netdata_account_sid:
netdata_twilio_account_token:
netdata_twilio_number:
netdata_hipchat_server:
netdata_hipchat_auth_token:
netdata_messagebird_access_key:
netdata_messagebird_number:
netdata_kavengear_api_key:
netdata_kavengear_api_sender:
netdata_telegram_bot_token:
netdata_kafka_url:
netdata_kafka_sender_ip:
netdata_pd_service_key:
netdata_awssns_message_format:
netdata_syslog_facility:
netdata_email_sender:
netdata_email_threading:
netdata_email_plaintext_only:
netdata_irc_nickname:
netdata_irc_realname:
netdata_irc_network:
```
