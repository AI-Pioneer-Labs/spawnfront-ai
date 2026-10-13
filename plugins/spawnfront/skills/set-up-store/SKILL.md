---
name: set-up-store
description: Help a team connect its Fourthwall shop to its Spawnfront site through the Spawnfront connector. Use when someone asks to set up, connect or check their team's store or merch shop on Spawnfront.
---

# Set up a team store

This skill needs the **Spawnfront** connector (`https://spawnfront.com/api/mcp`) connected with the **Site and news** area, on a team whose owner or an admin turned on **Allow AI assistants**. The store is part of a team's hosted site.

## Steps

1. Call `get_store_status` to see whether a Fourthwall shop is connected.
2. If not, explain that the shop itself lives on Fourthwall, and is connected to Spawnfront with its storefront token, which the player pastes on Spawnfront.
3. Call `connect_store` and give the player the link. **Never ask for the token**, and never accept one pasted into the chat — tell the player to paste it on Spawnfront instead.
4. Afterwards, call `get_store_status` again to confirm the shop is connected.
