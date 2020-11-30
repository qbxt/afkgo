What is this?
-----
This is a self-hosted Discord bot capable of managing multiple Minecraft alts simultaneously.
It's designed for AFK farms where multiple accounts need to be loading multiple chunks. Since
none of the accounts are rendering the game, it's incredibly lightweight.

**I offer no guarantee that accounts will not be banned either by Mojang or third-party server
owners. Use at your own risk.**

Setup
-----
In `constants/tokens/`, there are two files prefixed with `EXAMPLE-CHANGEME`. Both need to be
updated.

In `constants/tokens/EXAMPLE-CHANGEME-discord.go`:
  1. Uncomment all the lines
  1. Add your Discord token
  1. Rename the file to `constants/tokens/discord.go`
  
In `constants/tokens/EXAMPLE-CHANGEME-minecraft.go`:
  1. Uncomment all the lines
  1. Add your Minecraft accounts
     - If the account is **migrated**, you'll need to include the email address to sign in with
     - If the account is **unmigrated**, set the email address to a blank string (`""`)
     - Use the `a(ign, email, password string, migrated bool)` function.
    
Then, `go run main.go`

Commands
-----
All commands are prefixed with `/` by default (changed in `constants/constants.go`)

  - `/connect <IGN> <server><:port>`
  - Example: `/connect Xx_Example_xX mc.hypixel.net`
  - Example: `/connect Xx_Example_xX 127.0.0.1:25577`
    - `<IGN>` : an IGN with login information in `constants/tokens/minecraft.go`
    - `<server>` : an IP address or domain name
    - `<:port>` : (optional) port, default to `25565`. 
---
  - `/disconnect <IGN>`
  - Example: `/disconnect Xx_Example_xX`
    - `<IGN>` : an IGN to disconnect
---
  - `/chat <IGN> <message>`
  - Example: `/chat Xx_Example_xX hello, world!`
  - Example: `/chat Xx_Example_xX /summon minecraft:lightning_bolt ~ ~ ~`
    - `<IGN>` : a logged-in account to chat from
    - `<message>` : a message with length \leq 256
    
Known Bugs
-----
  - Certain servers send an MoTD on join that causes an error. This is a bug according to the library
  developer, and may or may not get fixed.
  - Certain servers have a proxy which redirects traffic to the "real server" (e.g. `hypixel.net --> 
  mc.hypixel.net`). This causes an error.
    
TODO
-----
  - [X] Send chat message
  - [ ] Follow player command
  - [ ] Anti-afk jitter
  - [ ] POST to Discord webhook if account disconnects