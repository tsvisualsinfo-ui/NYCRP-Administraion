# Setup checklist

- [ ] Create a new application named ER:LC Management in Discord Developer Portal
- [ ] Create bot user and securely copy token into hosting environment variables
- [ ] Enable Server Members Intent
- [ ] Invite with bot + applications.commands scopes
- [ ] Set token, client ID, and guild ID as environment variables
- [ ] Configure all department and rank role IDs in config.json
- [ ] Configure staff, moderator, ticket support roles
- [ ] Configure log channel and ticket category IDs
- [ ] Ensure bot role is above all roles it must assign/remove
- [ ] Run `npm run register`
- [ ] Start bot and test in a private test server
- [ ] Confirm promotion, demotion, hire, fire, transfer, and LOA logs work
- [ ] Attach persistent storage for data.sqlite if hosting in the cloud
