# ER:LC Management — All-in-One Discord Bot

A new, separate Discord.js v14 bot project using a black/red emergency-services theme. Includes actual Discord rank/department role updates, moderation commands, custom embeds, private support tickets, personnel records, LOA tracking, and audit logs.

## Requirements
- Node.js 20.11+ (or Docker hosting)
- Discord application/bot in the Developer Portal
- A Discord server where you can add a bot

## Local setup / testing
1. Extract this folder.
2. Copy `.env.example` to `.env`.
3. Set `DISCORD_TOKEN`, `CLIENT_ID`, and `GUILD_ID` in `.env`.
4. Edit `config.json` with the IDs of your server's roles and channels.
5. Install dependencies: `npm install`
6. Register commands: `npm run register`
7. Start the bot: `npm start`

## Cloud hosting
This project includes a `Dockerfile` and a `render.yaml` template for a continuously running worker. Choose a cloud host that supports persistent storage: the bot uses SQLite (`data.sqlite`) for personnel, tickets, and action records. If the host's filesystem is ephemeral, attach a persistent disk or migrate the database to managed PostgreSQL. Add the three environment variables in the host's secret/environment settings. Never put the token in source code or upload `.env` to GitHub.

## Discord Developer Portal
- Enable **Server Members Intent** for member update logging.
- Invite with `bot` and `applications.commands` scopes.
- Give only the permissions you need: View Channels, Send Messages, Embed Links, Read Message History, Manage Roles, Manage Channels, Moderate Members, Kick Members, Ban Members, Manage Messages.
- Put the bot's highest role above the rank and department roles it must manage.

## Configuration
In `config.json`, set:
- `brand.colour` to `#C62828` for the red theme.
- `roles.staff`, `roles.moderator`, and `roles.ticketSupport`.
- Department role IDs and every rank role ID under `roles.departments` and `roles.ranks`.
- `channels.logs` and `channels.ticketCategory`.

An empty role ID is intentionally treated as unconfigured. Use Discord's Copy Role ID option with Developer Mode enabled.

## Commands
- `/rank promote member department rank reason`
- `/rank demote member department rank reason`
- `/rank set member department rank reason`
- `/personnel hire member department rank reason`
- `/personnel fire member department reason`
- `/personnel transfer member from to rank reason`
- `/personnel loa member department status reason`
- `/personnel view member`
- `/personnel roster department`
- `/tickets panel` and `/tickets close`
- `/mod warn`, `/mod timeout`, `/mod kick`, `/mod ban`, `/mod purge`
- `/embed send` with title, description, colour, image, thumbnail, footer, author, optional field, and channel.

## Important behaviour
- Rank commands remove the member's other configured rank roles in that department and assign the selected rank role.
- Hire assigns department and rank roles. Fire removes the department role and that department's configured rank roles. Transfer removes old department/rank roles and assigns the new department/rank roles. LOA records status but does not remove department roles.
- The initial staff check permits configured staff/moderator roles, Administrators, and members with Manage Server. Review `src/utils.js` and tighten this for your server before launch.
- Commands are not a replacement for a human approval process. Test role changes in a private test server first.
- Ticket channels are retained after closure for staff review; transcripts, rating controls, and deletion workflows are not included yet.
- The embed builder currently supports one optional field; it can be extended for additional fields, button components, and saved templates.
- This is a working starter project, not a hosted or already-invited bot. It has not been tested against your server's actual role IDs/permissions.
