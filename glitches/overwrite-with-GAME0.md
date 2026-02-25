# Overwrite with GAME0 (aka Ow0)

**Discovered by: Blimix** (not sure if there was prior art, but that's how I've learnt about it)

**Technical Analysis by: Gynvael Coldwind**

[Blimix on his website](https://www.blimix.com/aethra/tips.html) wrote:

> If you start a new game in a particular save slot, but quit during character creation, the party that was in that save slot beforehand will be introduced into the new game, the next time you load that slot.

This actually it a bit more complicated and has additional consequences.

The Aethra Chronicles has an initial game state in the `GAME0` directory which is copied over the selected game slot when selecting `(S)tart or Restart the game`. This state *does not* include `PARTY.DAT`, which contains all the information about the player's party and their inventory - that's why the old party is preserved.

This said, **the quest flags in `GAME0/SAVEGAME.DAT` have weird mid-game values** - they are only initialized to proper new game values after successfully creating the whole initial party. This can softlock the game if your party doesn't have certain quest items in their inventory already (as there would be no way to get them due to quest flags being weird), but it may also be useful if you do have the proper quest items (e.g. to farm the Marsh Monster).

## GAME0 Quest Flag State

| Quest                       | GAME0 Quest Flag Value | Description and notes                         |
| --------------------------- | ---------------------- | --------------------------------------------- |
| TODO                        | TODO                   | TODO                                          |
