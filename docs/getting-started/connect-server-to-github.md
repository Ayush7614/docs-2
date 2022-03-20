---
id: connect-server-to-github
title: Connect Amplication server to GitHub
sidebar_label: Connect Amplication server to GitHub
slug: /connect-server-to-github
---

# Connect Amplication server to GitHub

Amplication provides built-in integration with GitHub to push the generated application to a GitHub repository.

When running a local Amplication server you first need to configure the server to integrate with a new GitHub app, following the steps below.

:::info
When using the hosted service on https://app.amplication.com, the integration is pre-configured and you just need to follow [this guide](/docs/sync-with-github) to sync your application with GitHub.
:::

### Create a new GitHub App

1. Go to https://github.com/settings/developers.
2. Click **OAuth Apps**.
3. Click **Register a new application**.
4. Give the application any name.
5. Set the **Authorization callback URL** URL to `http://localhost:3001`

:::info
If you are hosting the Amplication server on any other address, use the specific address instead of `http://localhost:3001`
:::

6. Copy and save the client secret and client ID of the GitHub application.

### Configure Amplication server to work with the GitHub app

1. Go the `../packages/amplication-server/`

2. Add a `.env.local` file in the root of the server directory

```
../packages/amplication-server/.env.local
```

3. Add the following content to the file

```
GITHUB_SECRET_SECRET_NAME=use_local_settings
GITHUB_CLIENT_SECRET=[client_secret_here]
GITHUB_CLIENT_ID=[client_id_here]
GITHUB_APP_AUTH_SCOPE=user:email,repo,read:org
GITHUB_APP_AUTH_REDIRECT_URI=http://localhost:3001/github-auth-app/callback/{appId}
```

4. Replace `[client_secret_here]` with the client secret of the GitHub application.
5. Replace `[client_id_here]` with the client ID of the GitHub application.

6. Restart Amplication server.
