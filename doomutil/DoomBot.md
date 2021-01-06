# DoomBot Concept sheet
&copy; Dominik Reh

### Introduction

The DoomBot uses a heuristic algorithm to predict enemy moves.
This is done by keeping track of the cards played by the enemy in previous rounds,
so we can try to predict which card the enemy will return for a specific value.

### Statistical observation

The DoomBot starts off with a generic middle-field priority strategy.
This means that it doesn't spend its high cards for the highest points, since
many opponents will probably try the same, but instead keeps those high
cards to beat the opponents in the middle field and for negative cards,
leading to an averagely higher number of points.

Additionally, this bot memorizes its opponents behavior in the previous rounds and uses 
this to predict the likelihood that a card will be chosen again. This is
especially effective against deterministic bots without randomness.

:warning: **Note:** Because of the used implementation, the bot's
memorization behaviour is only defined in a 1v1 context since it only keeps
track of one opponent.

### Calculation

The DoomBot looks at the statistics memory each time it should play a new card.
If the stored weight for specific points gets high enough in respect to the total, it is determined as *likely*,
and a card most likely to beat it will be selected. If more than one
return applies, the highest percentage will be used, except if the enemy
can't play this move because he doesn't have the card on hand anymore.

If no return crosses the threshold (as would be likely for bots with high randomness),
the fallback to the aforementioned middle-field-priority is used.

In practice, this means that the DoomBot will get increasingly confident the more
rounds are played, and will be more eficcient for deterministic or limited-scope randomness bots.