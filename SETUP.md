# Discord setup

Site and exact OAuth2 redirect URL: https://sergioitis.github.io/nezuko-install/

1. Add that exact URL (including trailing slash) under OAuth2 > Redirects in application 623481583411658753.
2. Enable Guild Install and User Install under Installation.
3. Configure User Install with applications.commands; Guild Install with bot and applications.commands.
4. This static version requires Require OAuth2 Code Grant to be OFF. If your bot requires a full code exchange, use a backend callback instead; do not disable an existing required-code policy without reviewing why it is enabled.
5. Register global commands with integration_types [0,1] and contexts [0,1,2] where appropriate.

## Behavior and limits

The initial page starts server authorization with the original permissions=8 (Administrator) and guilds, email, bot, guilds.join, applications.commands scopes. A matching callback starts user installation. A second matching callback opens https://discord.gg/nezuko. Each step requires Discord consent. Cancellation stops the chain. Session state expires after 30 minutes, is consumed once, and is bound to the current browser tab. Codes are cleared from the address bar and never logged, stored, or forwarded.

GitHub Pages cannot securely exchange authorization codes using a client secret. This version discards codes, does not access email or guild data, does not automatically join users, and cannot verify that installations completed. The extra scopes are retained from the requested URL but their API access is not consumed. A backend is required if these grants need to be used, if Require OAuth2 Code Grant is enabled, or if server-side installation verification is needed. Never put a Discord client secret or bot token in this repository.

OAuth end-to-end verification requires the above portal configuration and a real consenting test user; publication alone does not verify Discord installation.
