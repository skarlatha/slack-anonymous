# Anonymous Bot for Slack

Express your personal thoughts and desires in the depersonalized way concealing your true identity from the rest of your Slack team.

## What it does

![](https://raw.githubusercontent.com/TargetProcess/slack-anonymous/master/docs/images/anon1.png)

![](https://raw.githubusercontent.com/TargetProcess/slack-anonymous/master/docs/images/anon2.png)

When someone posts `/anon @user Some anonymous text`, that message is sent to this simple service, which sends the text back to the specified user with a modified text, omitting the information about the author of the message.

To avoid revealing your identity by accidentally typing the wrong command, it's recommended to post all messages in your private conversation with SlackBot.

## Usage

*Assuming that the configured slash-command is called "/anon" *

- `/anon help` -- Displays the help information
- `/anon @user Text` -- Sends `Text' to the specified user
- `/anon #channel Text` -- Sends `Text' to the specified public channel
- `/anon group Text` -- Sends `Text' to the specified private group
- `/anon :here Text` -- Sends `Text' to the current channel/group/DM, where the message is typed

## Deployment

We use Heroku for deployment, but the process should be similar for any other environment.

- Create a new Heroku app
- Point its deployment target to the repository

From the Slack's side:

- Create a new slash-command integration in your team's Slack.
- Set its URL to your Heroku app, i.e. https://myanonymousslackbot.herokuapp.com
- Optionally, copy the autogenerated Token field value of the Slash Command integration, and add it as a configuration parameter `SLACK_COMMAND_TOKEN` of your Heroku app. *This helps to verify that the origin of the command is your team's account and not someone else.*
- Create a new Incoming WebHook integration, copy its WebHook URL (something like https://hooks.slack.com/services/****/***) to the configuration parameter `POSTBACK_URL` of your Heroku app. *This lets the anonymous bot to post the message back to your team's Slack account.*
- Customize the integration in Slack settings: give it a custom name, icon, etc.