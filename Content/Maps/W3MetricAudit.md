# METRIC AUDIT
## Sizing
- Each block equates to 1 metre
- The player takes up 1m of space

## 3 Spaces: Horizontal Jump-Gaps, Vertical Jump-Gaps, Enemy Take-Out
- Forward path with horizontal jump-gaps
    - The size is a 5m wide path with no walls. The point of this level is to test player movement within a level, so having a set path with no closed-space at the start helps it feel more open, which also encourages the player to explore and engage with the movement and metrics.
- Upward path with vertical jump-gaps
    - Similarly with the horizontal jump-gaps, there are no walls so to not put pressure on the player. Since we are on a platform, there is a ramp along the side of this section in-case the player falls off and can get back to this section, without having to go all the way back to the start of the previous section.
- Enemy area with an optional path to avoid one of them
    - Now that the player has gotten used to the movement, we can introduce walls for an enemy evasion section.
    - 2 enemies, 1 with a patrol path and 1 just standing with their back turned.
    - The 2nd patrolling enemy can be avoided via an optional path which skips their path entirely.

## Adjustments I Would Make
- I would have adjusted the jump height by implementing a low/high jump feature, but I am still unfamiliar with Blueprints and could not figure out how to change this variable in time.
    - By this implementation, I would have changed the vertical jump-gap section with some more variety, as the jump could be further controlled by the player instead of being a simple static jump height from a key press.