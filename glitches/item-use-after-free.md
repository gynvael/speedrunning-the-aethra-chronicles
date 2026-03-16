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

**Warning**: DO NOT use up an item! This will cause the character to have -1 (255) items in the inventory and it's a really volatile state - see also the Negative Inventory described variant below.

## Negative Inventory

If you perform Item Use-After-Free and use up the item, the game will attempt to remove that non-existant item. The result of this is having -1 (255) items in the inventory. This is a very volatile state and some actions will make the game crash.



