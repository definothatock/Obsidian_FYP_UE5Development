# Core Gameplay: Resource Management

Why resource management (why game/fun)?
- Loot / values
	- Human loves hoarding. Even the final result is just the Loot / Score, if the process was meaningful / rewarding enough we will be happy with it.
- Story
	- Human loves great tales / understanding interesting mysteries. However, this is entirely outside of our current scope as of now.
- Experience
	- Stimulations. Human loves visuals / events that are unique from day to day life (non-realistic / rare to have). Or, experiences that we have never experienced before (this one is almost impossible for us to do)
	- Some people seek a certain "vibe". This is not about spike of emotions, but rather a prolonged satisfaction. 
- Control
	- Human loves being in charged of certain thing. Sense of control give the feeling of being strong, in different ways.

What we aim?
- Mainly Loot / values. Most straightforward and simple.

### what are the main resources to manage in this game?
- Stamina^1
- Health^1
- Loot^2
- Time
- Inventory (Weight & Space)^3
*Stamina & Health can be the same resource (Max Stamina cap by Max Health, like Peak)* ^1
*Inventory Space does not count. Direct consequence should be handled by Value/Weight.*^2
*Weight punish stamina regeneration? ^3

Why should player care these resource?
- Stamina
	- Ability to get out of sticky situations
	- Able to traverse difficult terrains (depends on map generation) 
- Health
	- Ability to continue on playing on the round as the intended way (death player becomes a drone?)
	- Limit Stamina (depends on one bar design or not)
- Loot
	- Game Goal. The more, the better, but it adds contains on all the other resources.
	- Provide limited useful abilities that cannot be called easily by other means.
- Time
	- There should be a limit of how long a player can linger around the same location / round.
	- Directly affect the amount of loot players can get.
- Inventory
	- Weight
		- Affect Speed/Max Stamina/Stamina Regeneration (up to debate)
	- Space
		- Affect how much of item the player can carry

External obstacles constrains
- Environment
	- Main Purpose: Provides conditions for risk and reward dynamics.
	- Passive: 
		- Bad route to Loot (Drain Stamina) / Dangerous location (Drain Health)
	- Aggressive:
		- Dynamic environmental hazards (maybe sth like STALKER anomalies?). Force player to relocate / retreat / leave the round.
- Hostile Creatures
	- Main Purpose: drain player's any type of resources, in any way.
		- Stop player from playing the intended way / reaching their Goals (By Draining Health or Stamina / Existing around a goal)
		- remove loot values from player (By forcing player using them / damaging loots from player)
	- Can also be a mean to risk and reward when paired with Environment (creature guarding loots)
- Loot
	- Not all loot are immediately beneficial to player (good utility). Some provide great values but also are burdens for finishing the round.
- Death
	- Permanent (per round) resources Punishment for being careless / too aggressive.
		- Getting Revived by Peers should not comes with 0 consequence, and should not be able revive many times.
		- Up to debate: Reduce Max Health / Stamina?

### Special Resources that do not directly live in the game
These resources faces towards the player, instead of the game framework.
They highly depends on the player, and we as developers/designers, we do not have full control. Still, they are very important in terms of 'game experience'.
- Cognitive Load
	- How much the player need to think/plan
- Skill Requirement
	- How harsh is the mechanical difficulty the player is facing

---
# The Core Resource: Loot
All decision lead to more Loots / save Loots.
==For balancing and Simplicity: Most loot should have **1 use**, and **no more than 2 use** for all loot.==

### Encouraging smart play: 
Using loot might reduce it's value, so player could never have a 'god tool' forever. On paper, this should encourage player to be more aware of the situation and player smarter.
However, humans have strong min-max behaviours (hoarding). If using loot = consistence lost in value (damage/break), it will lead to player just not using any tool, minimize loss, maximize score (even if in short term they are going to die). This kills the intension for smart play.

So instead, some 'decent' tool should not loose value directly proportional to use-time. Alternatives can be:
- Depletion base
	- explicit damaging threshold. Punish bad counting.
	- can be recharged, but hitting '0' will risk reduce value
- Overcharging state
	- Push beyond standard use. Punish abusing.
	- hard to recharge, but allow 'over use', each time will risk reduce value by chance
	- This could suggest a stronger use variant (overcharging on demand)
- chassis
	- using it does not loose value at all. Instead it required external value reduction (battery? Ammo?)
	- This is the most common one among games, basically Bow and Arrows. Unless we gate external value too, player might still be able to have 'god tool' 24/7. (this is not bad if there is a proper level scaling system, but rn we do not have it)
- Fixable
	- There is chances to fix it. It could be limiting fixing chance, requires certain condition, or any way that makes the damage 'reversible' (with a cost).
- ...
- ...

Most 'broken' loot should also provide minimal value, so 'cashing in' or being careless would not feel too punishing. 

The way how a loot is damage/broken gives heavy hits to player how the tool was intended-to-use / limited. In such, We should find a way to let player knows how the tool loose their values. The most straightforward way is writing them in description (or a better one could be unlocking base: next time it shows basic info if they have been turned-in before).
Also, the Weight and Inventory Size are also a good sign to let player knows 'you can't take all, use some, smartly'.

## Loots in General:
- Safe loot
	- almost a pick up and go, maybe a little hassle
	- always low in value, should give a vibe or "yeah sure why not"
	- rarely has any real, good use.
- Mediocre loot
	- Post noticeable inconvenience retrieving / carrying
- Legendary loot
	- Threatening retrieving / carrying condition
	- Heavy resources cost (in any way)

## Type of Loot Utilities
Usefulness and Effectiveness almost entirely based on world building.
Better tools should comes with greater constraints / scarcity / drawbacks. 
Tools can have/blend from these categories:
- Mobility 
	- Provides movement/route that would otherwise hard to perform.
	- Rope Cannon? teleportation? swapping?
- Control
	- Limit Target's mobility.
	- Decoy? Stunner?
- Survivability
	- Increase the odds for a player to keep on playing.
	- health pack? extra revive? cure curse (from tool, reviving etc)? smoke to break LOS?
- Lethality
	- Reduce Target's Survivability. This category should be heavily governed, player can kill some but not overall powerful.
	- Entirely up to creativity. Usually will draw some resource from player is used.
	- as simple as fireball (1 time use, loss value), as complicated as charge up beam (requires time to do on spot charge up).
- Information
	- Provides knowledge for planning.
	- Motion Tracker? Geiger Counter? Bio-Scanner? Flares? locate other loot? weather forecast?
- General
	- Power Cell / Battery

## Type of Loot inconvenience
Same categories with 'Utilities', but instead the effects are not so kind to players.
Extra category that are specific to inconvenience:
- Fragility
	- Damages / breaks on certain environment / owner condition
- handling
	- needs to treat in specific way / cannot be put in backpack /  must put in hotbar
- Availability
	- Some Loot are awesome (good utility + low drawback), in this case they should be 'expired' after using it (reduce/lost value)
- Inventory shape
	- Some loot might be good in Utility / Value, but they are awful to be placed in backpack (Grid).

## 'Useless' loot
- Not poritized. Doesn't affect core gameplay, mainly for shit and giggles. Can be cosmetic too. 

## How players can know the item?
- Knowledge-transfer
	- the purpose is understood via environmental reading and prior experience

A very good reference about what loot to make:
https://www.youtube.com/watch?v=Jqh7SVpMR1o

---
# Player Dynamics
Players 

### Play tactics / style
Player should be some what vulnerable by themselves in the game. Without specific condition / Loots, player should always play it 'smart' (stealth, disengage).

### Reviving
Cost players Time.
There is a phase where player is in 'coma'. Reviving player from 'coma' requires a long 'CPR' act within a time limit. Other player can 'drag' or 'carry' unconscious player, but while performing the revive, the helping player cannot move. Any cancelation reset Reviving progress. Each player has only 1 reviving token each round, non replenishable (bring back from actual dead will not replenish token). 

There might be tools to reduce the Time needed to revive player. But nothing should revive actual 'dead' (to emphasis urgency).
Amount of Revives is hard limited, up to debate.

Revival punishment: Reduce Max Health/Stamina?

Up to debate: Free health upon finishing the round?
## Death
Happens when Health depleted and reviving Time ran out.
Actual death is round permanent, all loot is dropped, on spot. Dead player becomes spectator. 

- Extra: Actually Dead player may play as a drone.
	- They cannot talk directly, but perhaps make some beep sounds? 
	- Drone can only perform small actions (or just watching and pinging).
	- During Major events (last player hunted by oppressor?), Drones are all deactivated (intensify stress for the lonewolf?)
- Might increase development cycle significantly.  

Dead player are revived for free at the end of each round.

If we make permanent upgrade: 
Actually Dead player's core must be brought to exit to regain some permanent upgrade.

Up to debate: should replenish Amount of Revives?
## Extra: Saving
Players can save extra loot, or trade them for currency.
not pioritized in development.

---
# Creatures 
Essentially, Creatures are the dynamic puzzles from the environment.
As for now, Creatures are separated into 3 category: harmless, hostile, oppressive.

#### harmless
Harmless creature usually are very passive, and essentially are 'loots on the move' on framework level. 
To player they are:
- Lesser Tools, like some loot but less effective (Noisy bug make distraction? light bug gives some radiating light for a while?)
- Some unique Value (normal loot does not move)
#### Hostile
Almost always cost player any type of resources of ignored, even if the consequence is not immediate.  How they achieve that is up to creativity, but generally treat Hostile Creatures as ops players, they will use their **Utilities** to go against your **Resources**. This metal model allows Player to Creature back-and-forth.
#### Oppressive
This is the least prioritized, as it require serious environment building, good amount of trial-and-error to make it convincing.   
Player literally cannot 'defeat' this type of Creature. This is to pressure player during the run, or punish player who disrespected the environment. Could draw some inspiration from actual horror games. 
Highly tied with Time.

### Working Memory system
Most Creature will use this custom built temporary memory system. This system aims help Creatures to 'aware'.
Workflow: AI perception -> Evaluator -> StateTree

Available perceptions for AI to choose (engine provided)
- Sight
- Hearing
- Touch
- Damage
- Prediction

Function of Evaluator:
- Convert Perception into WorkMem Entry 
- Push Entries into WorkMem Array
- Evaluate Array and condition
- Throw result into StateTree

Function of StateTree:
- Perform action based on result in Evaluator

*Extra: Evaluator gives utilities instead and StateTree works with some randomization. This heavily increase development cycle.*

---
# Environmental Hazard  
Another form of environmental dynamic puzzles.
Highly tied with Time.

Environmental Hazard is more about world building, aesthetic choice or Environmental story telling. And since there is no aggressive act that player can perform to grand scale Hazards, Hazards should not be too lethal (one shot dead = no back and forth). Still, it should be fearful.

Depends on what the Hazard is, in general the Counterplay Categories (all information dependent):
- Detect
	- Knows where the intense area? where it is coming from?
- Suppress
	- Some method to reduce the effect temporarily? 
- Exploit
	- Risk and use the nature of the Hazard (time the knockback?)

---
# Game Director