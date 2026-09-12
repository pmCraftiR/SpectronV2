> **This is a fork of [TheWindows/SpectronV2](https://github.com/TheWindows/SpectronV2) updated for PocketMine-MP 5.44+ and pmmp-ng (nethergamesmc) fork.**

---

## 🛠️ | Compatibility Fixes (PocketMine-MP 5.44+ / pmmp-ng)

### Bug Fixed
> `Error: Cannot access uninitialized non-nullable property StartGamePacket::$serverTelemetryData by reference`

This crash happened when a fake player connected — `addToSendBuffer()` intercepted every outgoing packet and tried to decode it, including `StartGamePacket`. In the nethergamesmc bedrock-protocol, the decode path passes `$serverTelemetryData` by reference before it's initialized, causing a fatal PHP 8.1+ error.

### Files Changed

| File | What changed |
|---|---|
| `Loader.php` | Handle new `ClientData` namespace (`...login\clientdata\ClientData`) in 5.44+ with `class_alias` fallback |
| `TryChangeMovementInternalspectronBehaviour.php` | Replace removed armour classes (`Helmet`, `Chestplate`, `Leggings`, `Boots`) with `ArmorItem::getArmorSlot()`; replace `Sign` with `BaseSign` |
| `util/PacketUtils.php` *(new)* | Encode/decode helper using `pmmp\encoding\ByteBufferWriter/Reader` with `PacketSerializer` fallback for older builds |
| `network/listener/spectronSpecificPacketListener.php` | Added `hasListener(string $packetClass): bool` for efficient per-packet listener checking |
| `network/spectronNetworkSession.php` | Skip decoding when no listener is interested; wrap all packet decode in `try/catch(\Throwable)` to prevent server crashes from undecodable clientbound packets |

Tested on **PocketMine-MP 5.44.2+dev** with **pmmp-ng (nethergamesmc)** fork.

---

# ❔ | How This Plugin Work?

> Make Sure You Have Permissions Or Op On The Server

> This Is A Recreated Fake Player Plugin By Muqsit

- You Can Add Fake Players To Your Server With No Limit!
- You Can Fully Customize The Fake Player For Example:
- You Can Turn Off Pvp Mode
- You Can Turn Off Random Walking
- And More!
- Also You Can Use All Of The Abilities On A Ui For Easier Access!

# ✨ | Commands 

## Admin Commands

- /spectron menu - Open the Spectron UI
- /spectron tpall - Teleport all fake players to you
- /spectron addmessage <message> - Add a kill chat message
- /spectron removemessage <message> - Remove a kill chat message
- /spectron togglekillchat - Toggle kill chat
- /spectron togglepvp - Toggle PvP for fake players
- /spectron togglerandomwalk - Toggle random walking for fake players
- /spectron setreach <distance> - Set PvP reach distance (1.0-10.0)
- /spectron setcooldown <ticks> - Set PvP damage cooldown (10-60)
- /spectron setdifficulty <easy|normal|hard> - Set PvP difficulty
- /spectron spawn <name> - Spawn a fake player
- /spectron reset - Reset all fake players
- /spectron <name> chat <...chat> - Make a fake player chat
- /spectron <name> form button <#> - Submit a button form response
- /spectron <name> form raw <responseJson> - Submit a raw form response
- /spectron <name> interact - Make a fake player interact
- /spectron info - Show plugin information

# 🧨 | Permissions

- spectron.command.spectron

# 🔑 | Dependencies

[FormApi](https://github.com/jojoe77777/FormAPI)
