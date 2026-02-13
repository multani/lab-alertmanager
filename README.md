# 🧪 Lab: Alertmanager

This runs Prometheus + Alertmanager with a set of:

* Prometheus:
  1. Aggressive configuration to scrape and trigger alerts quickly
  2. Some basic alerting rules to start/stop alerts easily
* Alertmanager:
  1. A basic alert routing tree + inhibition + receivers
  1. A few basic templates to send alerts to Slack and console


## Run with Docker Compose

In the `compose` folder, run:

```bash
cd compose
docker compose up -d
```

To read the changes on the configuration, rules, templates, etc., run:

```bash
docker compose kill --signal=HUP alertmanager prometheus
```

To see the alert payload received by Alertmanager, look at the logs of the webhook logger:

```bash
docker compose logs -f webhook-logger
```


## Slack receiver

To receive notifications on Slack, you will need to have a Slack app and get its OAuth token.

1. Login to your Slack workspace
2. Build a new Slack app "from scratch" from: https://api.slack.com/apps/
3. In the application configuration:
   1. Open the *OAuth & Permissions* page
   2. Scroll down to *Scopes* and add the `chat:write.public` scope
   3. Scroll to the top and click on *Install to Workspace* and follow the instructions
   4. Copy the *Bot User OAuth Token* into a file in `compose/alertmanager/secrets/slack-app-token.secret`

