# Overwrite with GAME0 (aka Ow0)

**Discovered by: Blimix** (not sure if there was prior art, but that's how I've learnt about it)

**Technical Analysis by: Gynvael Coldwind**

[Blimix on his website](https://www.blimix.com/aethra/tips.html) wrote:

> If you start a new game in a particular save slot, but quit during character creation, the party that was in that save slot beforehand will be introduced into the new game, the next time you load that slot.

This actually it a bit more complicated and has additional consequences.

The Aethra Chronicles has an initial game state in the `GAME0` directory which is copied over the selected game slot when selecting `(S)tart or Restart the game`. This state *does not* include `PARTY.DAT`, which contains all the information about the player's party and their inventory - that's why the old party is preserved.

This said, **the quest flags in `GAME0/SAVEGAME.DAT` have weird mid-game values** - they are only initialized to proper new game values after successfully creating the whole initial party. This can softlock the game if your party doesn't have certain quest items in their inventory already (as there would be no way to get them due to quest flags being weird), but it may also be useful if you do have the proper quest items (e.g. to farm the Marsh Monster).

## GAME0 Quest Flag State

Remarks:

  * Quest flag names are a bit random, there are some unknown ones.
  * In case we think the quest flag is unused, it was skipped.

| Quest                       | GAME0 Quest Flag Value | Description and notes                         |
| --------------------------- | ---------------------- | --------------------------------------------- |
| quest_vizier                | 2                      | Book of Prophecy was presented to Vizier      |
| quest_painting_guy          | 2                      | I think it means the quest is finished        |
| quest_bandit_galoran        | 2                      | Quest finished                                |
| quest_father_gyman_missing  | 0                      | Not started, father Gyman still missing       |
| quest_NO_IDEA_2             | 1                      | No idea (dragon related?)                     |
| quest_NO_IDEA_3             | 0                      | No idea (dragon related?)                     |
| quest_dragon                | 2                      | Book of Prophecy was received from the dragon |
| quest_pissed_off_dragon     | 0                      | Dragon is not angry with you                  |
| quest_salamander            | 5                      | Salamander fully completed                    |
| quest_oracle                | 0                      | Didn't meet the Oracle yet                    |
| quest_dwarven_sword         | 2                      | Agreed to find sword for dwarven king         |
| quest_dwarf_khaled_joining  | 1                      | Dwarf Khaled joined the party                 |
| quest_dwarven_prisoner_released | 0                  | Dwarven prisoner still in Giant's cave        |
| quest_dwarven_prisoner_reward_collected | 0          | Reward not collected from Dwarven prisoner    |
| quest_elven_beast           | 4                      | Elven beast quest complete and GEM received   |
| quest_elf_timmar_joining    | 2                      | Mama's boy Timmar left the party              |
| quest_thief_henchmen_joining | 5                     | NPC Chrissta was told to try joining the party later |
| quest_NO_IDEA_10_likely_NPC_joining | 1              | No idea (related to paladin NPC wanting to join) |
| quest_NO_IDEA_11_likely_NPC_joining | 0              | No idea (related to last NPC wanting to join) |
| quest_dragon_deliver_letter | 0                      | Dragon letter fetch quest not started         |
| quest_dragon_cave_state     | 0x14 (20)              | Likely: still 20 fights to have in dragon's cave |
| quest_prophercy_oracle      | 0                      | No proophecies bought from Oracle             |
| quest_marsh_monster         | 0                      | Did not fight Marsh Monster yet               |
| quest_book_reader           | 0                      | Did not show Book of Prophecies to book reader |
| quest_letter_recipient      | 0                      | Dragon's letter not yet delivered             |
| quest_elemental_half_key_1  | 0                      | Did not fight with the ?first? elemental      |
| quest_elemental_half_key_2  | 0                      | Did not fight with the ?second? elemental     |
| quest_another_bandid_lair   | 0                      | Did not start second bandid lair quest        |
| quest_cemetary_i_think      | 0                      | Likely: Cemetary quest not started            |
| quest_king                  | 0                      | King won't speak with you                     |
| quest_prison_guard          | 0                      | Not chatted with prison guard                 |
