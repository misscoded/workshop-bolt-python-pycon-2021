# Bolt for Python Demo App (PyCon 2021)
This is a basic example app showing off just some of the functionality available in [Bolt for Python](https://slack.dev/bolt-python/tutorial/getting-started), including Socket Mode. 

Make sure you have a development workspace where you have permissions to install apps. If you don’t have a development workspace setup, go ahead and [create one](https://slack.com/create). 

We also recommend that you [create a new app](https://api.slack.com/apps?new_app=1) if you haven’t done so already.

## Install Dependencies
```
pip install -r requirements.txt
```

## Add Scopes & Install App into Workspace
In your [**App Config**](https://api.slack.com/apps), after selecting your app, navigate to **Socket Mode**. Enable Socket Mode to generate and name a dedicated `SLACK_APP_TOKEN` for your app (this token can be located later at **Basic Information** > **App-Level Tokens**).

Next, navigate to **OAuth & Permissions**. In the **Bot Token Scopes** section, add the `channels:history`, `app_mentions:read`, `commands` and `chat:write` permissions.

Click **Install App** to install the app to your workspace and generate a bot token. This token will be used in your app as the `SLACK_BOT_TOKEN` environment variable.

## Setup Environment Variables
This app requires that you setup environment variables. 

You can locate these values by navigating to your [**App Config**](https://api.slack.com/apps) and visiting the **Basic Information** and **OAuth & Permissions** pages.

The `SLACK_APP_TOKEN` can be found under **Basic Information** > **App-Level Tokens** section.

The `SLACK_BOT_TOKEN` can be found under **OAuth & Permissions** > **OAuth Tokens for Your Workspace**.

```
export SLACK_APP_TOKEN=YOUR_SLACK_APP_TOKEN
export SLACK_BOT_TOKEN=YOUR_SLACK_BOT_TOKEN
```

If using OAuth, you'll use the following:

```
export SLACK_SIGNING_SECRET=YOUR_SLACK_SIGNING_SECRET
export SLACK_CLIENT_ID=YOUR_SLACK_CLIENT_ID
export SLACK_CLIENT_SECRET=YOUR_SLACK_CLIENT_SECRET
export SLACK_SCOPES=YOUR_SLACK_SCOPES
```

The above OAuth-related values can be found under **Basic Information** > **App Credentials**.

## Run the App
Start the app with the following command:

```
python app.py
```

## Subscribe to Events
On the **Events Subscriptions** page, after opting in, click **Subscribe to bot events** and add `app_home_opened`, `app_mentioned`, and `message.channels` to the events your app is subscribed to.  

## Create a Shortcut
On the **Interactivity & Shortcuts** page, create a new Global Shortcut with a **Callback ID** of `launch_simple_modal`. 

## Enable Home Tab
In the **App Home** page, navigate to the **Show Tabs** section and enable the **Home Tab**. 

## Define Redirect URL for OAuth (optional)
Bolt's Socket Mode receiver supports OAuth, but it is HTTP-based. This means that on the **OAuth & Permissions** page, you must provide an additional, publicly accessible **Redirect URL**.

For development purposes, we recommend using [`ngrok`](https://ngrok.com/download). Checkout [this guide](https://api.slack.com/tutorials/tunneling-with-ngrok) for setting it up.

The **Redirect URL** should be set to your `ngrok` forwarding address with the `slack/oauth_redirect` path appended and should look something like this:

```
https://3cb89939.ngrok.io/slack/oauth_redirect
```