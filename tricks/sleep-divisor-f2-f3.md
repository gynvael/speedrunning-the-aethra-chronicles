# Sleep Divisor (F2/F3)

**Discovered by: Gynvael Coldwind** in Feb'26

(If you find prior art let me know, but I haven't found it documented/mentioned anywhere.)

**TL;DR: hold F3 in main menu or when in world/city/dungeon map for ~5 seconds and your game will speed up a lot.**

The `F2` and `F3` keyboard buttons control a "sleep divisor" variable, which is used to, well, divide values passed to the sleep/delay function in game. The higher the divisor value is, the faster the game works.

The "sleep divisor" default value is 100, and it can take values between 25 and 1000 (yup, this makes your game about 10x faster). Pressing `F2` decreases the value, while `F3` increases it. You can hold either of these for a few seconds to min/max the value.

Note that `F2` and `F3` aren't controllable in every GUI state. It works in the main section of the main menu, as well as when in any map view (world/city/dungeon). It does not work e.g. when in combat, nor when e.g. in a shop.

Random remarks:

  * I'm not sure about the default value. I saw some indications that the game actually adjusts the value based on CPU speed when starting, but never checked it.
  * Sleep divisor state isn't preserved anywhere - you need to re-max it after every game restart.
