# Security Discord Bot

Clean and minimal Discord.js security and moderation bot with:

- Global slash command sync on startup
- Prefix and slash commands from the same command files
- Subcommand-based command design
- Local JSON database storage
- Minimal Components V2 response UI

## Features

- Security tools for lockdown and whitelist management
- Moderation tools for warnings, timeouts, kicks, bans, and unbans
- Case history tracking with local storage
- Channel tools for slowmode, clear, hide, and unhide
- Global application commands without a separate deploy script

## Tech

- Node.js `20.11.0+`
- `discord.js` v14
- `dotenv`

## Project Structure

```text
src/
  commands/
  events/
  lib/
  index.js
data/
  guilds/
```

## Setup

1. Install dependencies:

```bash
npm install
```

2. Create a `.env` file:

```env
DISCORD_TOKEN=your_discord_token_here
CLIENT_ID=your_client_id_here
PREFIX=!
```

3. Start the bot:

```bash
npm start
```

When the bot becomes ready, it automatically syncs global slash commands using your `CLIENT_ID`.

## Bot Permissions

Make sure your bot has the permissions needed for the commands you want to use, such as:

- `Manage Guild`
- `Manage Channels`
- `Manage Messages`
- `Moderate Members`
- `Kick Members`
- `Ban Members`
- `View Channels`
- `Send Messages`
- `Read Message History`

Also enable these gateway intents in the Discord Developer Portal if needed:

- `MESSAGE CONTENT INTENT`
- `SERVER MEMBERS INTENT`

## Commands

### General

- `ping`
- `help`

### Security

- `security status`
- `security lockdown <channel|server> [reason]`
- `security unlock <channel|server>`
- `security whitelist add <user|role|channel> <target>`
- `security whitelist remove <user|role|channel> <target>`
- `security whitelist list`

### Member

- `member warn <user> [reason]`
- `member warnings <user>`
- `member clearwarns <user>`
- `member timeout <user> <minutes> [reason]`
- `member untimeout <user>`
- `member kick <user> [reason]`
- `member ban <user> [reason]`
- `member unban <user_id> [reason]`

### Case

- `case view <id>`
- `case recent [limit]`
- `case user <user> [limit]`

### Channel

- `channel slowmode <seconds>`
- `channel clear <amount>`
- `channel hide`
- `channel unhide`

## Prefix and Slash Commands

This bot supports both:

- Prefix commands like `!member warn @user spam`
- Slash commands like `/member warn`

Each command is defined in a single file, so prefix and slash logic stay together.

## Local Database

This project uses a local JSON database instead of an external service.

Data is stored in:

```text
data/guilds/<guild-id>.json
```

Stored data includes:

- Security whitelist state
- Lockdown snapshots
- Moderation cases
- User warnings

## Notes

- Global slash commands can take a little time to update across Discord.
- `channel clear` can only bulk delete messages supported by Discord's API rules.
- Some actions depend on the bot's role being high enough in the server role list.

## Open Source

This project is licensed under the MIT License.

See [LICENSE](./LICENSE) for details.
