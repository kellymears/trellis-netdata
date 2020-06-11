# Another Ansible Netdata Role

This Ansible role installs Netdata. It was written to be used with [Trellis](https://github.com/roots/trellis).

Now you can monitor your Trellis deploy(s) from a browser or Discord. That's cool.

I'll pkg on ansible-galaxy when it's finished but for now you'll need to clone this repo into `roles/netdata` manually.

Then add the following child definition to whatever `wordpress_sites` entry you'd like to enable Netdata on:

```yml
nginx_wordpress_site_conf: roles/netdata/templates/netdata.conf.child
```

Optionally you can also configure how you'd like to recieve notifications. Check the defaults to see what's available.

```yml
netdata_curl_options: ""
netdata_use_fqdn: "NO"
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
netdata_email_charset: "UTF-8"
```

Consult the Netdata docs if something is unclear about that. I'm just passing the values along.

If all went smoothly, your dashboard should be available at `yourhostname.com/netdata`.

I'll surface more netdata options soon. Notifications was most important for my use case, right now.
