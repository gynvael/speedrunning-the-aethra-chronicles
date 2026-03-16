# Item Use-After-Free

**Discovered by: Gynvael Coldwind**

**Note:** This technically is a pretty versatile bug with several exploitation approaches. A better overall name might be something like "zero-item-list bug family", but since it was discovered as an item use-after-free, the name was kept.

**In short:** Non-inventory item lists (e.g. Use an Item under `I`) have a bug that an empty list fully unlocks the list selection cursor and permits one to pick items which are "not there", including items which are in memory outside of the inventory slots. There are several ways to abuse this. And you can also crash the game with this if not careful (possibility of ACE is still being investigated).

## Item Use-After-Free (Limited Item Duplication)

Simplest way to exploit this glitch:

1. Make sure 1 character has an empty inventory.
2. Give that character an item that can be used multiple times (e.g. a Green Potion which has 3 uses).
3. Remove that item from their inventory (e.g. give it back).
4. Press `I` to Use an Item. You can now pick the item that you gave away and freely move the selection cursor around.

A more efficient way is to give the character e.g. 10 Torches (or whatever) and 1 Green Potion, and then give away first the Torches, and then the Green Potion. This basically fills the inventory slots with "removed" Green Potions.

**Warning**: DO NOT use up an item! This will cause the character to have -1 (255) items in the inventory and it's a really volatile state - see also the Negative Inventory described variant below.

**Important**: Ignore the names of the items shown on the list - they are taken from whatever was shown previously on the list (e.g. if you looked at another character's items in the meantime). Regardless of the item name, the item that will actually be used is the one that occupied said inventory slot previously for the selected character.

## Negative Inventory and Stats Overwrite

If you perform Item Use-After-Free and use up the item, the game will attempt to remove that non-existant item. The result of this is having -1 (255) items in the inventory. This is a very volatile state and some actions will make the game crash.

![Crashed game](res/negative_inventory_crash.png)

On the flip side, if you tread carefully and **give the affected character another item, they will go back to having 0 items**. What happens to the item you gave the character? **It overwrites part of this character's statistics**:

![Overwriten stats](res/stats_overwrite.png)

Please note that it's not yet clear if this is useful and this is still being investigated.

## Other Notes

* "Use an Item" is not the only action that uses the item list. Other actions include casting the (Cleric) "Discover Curse" / "Remove Curse" or (Mage) "Recognize Curse" / "Repeal Curse" spells. These actually seem to be able to flip a 1 to a 0 in memory.
* Shops have a different item list, but it also has a similar though more limited bug. This is yet to be explored though.

## Technical Notes

### Why the bug happens

This table shows actual in-game values of three variables used in "Use an Items" list:

| Case | selector_index | first_item_index | last_item_index |
| :---: | :---: | :---: | :---: |
| **0 Items** | 1 | 1 | 0 |
| **3 Items** | 1 | 1 | 3 |

Pseudocode:

```
# Types:
# selector_index: byte (unsigned)
# first_item_index: byte (unsigned)
# last_item_index: byte (unsigned)

if keystroke_scan_code == ARROW_UP:
  if selection_index == first_item_index:
    selection_index = last_item_index       # Wrap around the list to last item
  else:
    selection_index -= 1                    # Move up the list
elif keystroke_scan_code == ARROW_DOWN:
  if selection_index == last_item_index:
    selection_index = first_item_index      # Wrap around the list to first item
  else:
    selection_index += 1                    # Move down the list
```

Note that because Turbo Pascal is 1-indexed (unlike the majority of other languages), the selector and first item index start at 1 (and not 0). The last item index likely starts at the total number of items.

Given the pseudocode above, when the player has zero items:

* **\[selector\_index \== 1\]** Pressing the up arrow causes a wrap around, but, because `last_item_index` is 0 anyway, it still effectively moves up.  
* **\[selector\_index \== 1\]** Pressing the down arrow causes a normal unrestricted down movement.  
* **\[selector\_index \== 0\]** Pressing the up arrow causes a normal unrestricted up movement (because `first_item_index` is 1).  
* **\[selector\_index \== 0\]** Pressing the down arrow causes a wrap around, but, because `first_item_index` is 1, it still effectively moves down.

Note that this effectively means that `selector_index` is unrestricted in both directions.

