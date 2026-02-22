# Speedrunning Category Rules for The Aethra Chronicles

## Any% (v1.1 DOSBox)

This is the Any% category for the newest known version of the game - v1.1 registered with GAME.EXE/GAME.OVR being dated 1995-11-08 (in the installer's LZH files) - player under DOSBox.

Please note that the rules are preliminary and might change after being tested or as new things are discovered.

Rules:

  1. Time starts once you click `(S)tart or Restart the game` and select the save slot.
  2. Time ends when the King's end-game dialog acknowledging returning of his son pops up. This can be both the good ending (_I am overwhelmed with joy..._) or bad ending (_You have returned with my poor dead child..._).
  3. All available save slots MUST be in the "fresh" (GAME0) state, including current state (just like after installing the game).
  4. DOSBox **MUST run at constant 12000 cycles**** (`dosbox.conf` should have `cycles: #12000` in the `[cpu]` section). Changing CPU cycles is disallowed.
  5. Shutting down DOSBox or the game is **allowed**. Time between DOSBox exiting and DOSBox starting again (DOSBox splashscreen disapears and the terminal window appears) is **not counted**.
  6. Using `F3` ([max sleep divisor](feature-f2-f3.md)) is **allowed**. It can be done before you start the run.
  7. The **only external tool that can be used during the run is a PRNG calculator**. However **it must not read PRNG state from the memory or input from screen capture**, but rather MUST recover the state based on runner inputing values manually (follow the spirit of this rule, not the exact wording). **PRNG calculator must be displayed on screen when used**.
  8. You MUST remain on the same version of the game and MUST run only game (DOSBox) instance.
  9. All in-game glitches and bugs are allowed, with the following exceptions:
     1. Per Rule 3 - using previously existing save states is disallowed. You can use save states which you create from the beginning of the current run.
