# Development Commentary - 2309516

**Unit Name:** Tools and Production FGCT5017

**Student Name:** Bradley Curtis

**Student ID:** 2309516


**Build Link:** [URL or Embed]

**Video Demonstration Link:** [URL or Embed]

---

## Overview

![TitleScreen](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/GreddyPiggiesTitle.png)
*Figure 1 - Greedy Piggies Steam Banner* (Greedy Piggies on Steam, s.d.)

For this project I worked on Greedy Piggies, a multiplayer card game built in Unreal Engine 5. I had three main responsibilities across the project. The first was acting as one of two development project coordinators, where I worked alongside another coordinator to manage the team, assign tasks, and keep development moving. The second was implementing and fixing the multiplayer gameplay systems, which included getting the auditing mechanic working across all players, fixing card submission so it worked correctly on both the server and client, and resolving input issues that were stopping players from being able to interact properly. The third was building a Python asset scanner tool that ran inside the UE5 editor to help the team check their assets met the project's quality standards before they were brought into the game. I also managed the team's Git repository throughout the project, handling merges between branches to make sure nobody lost their work.

---

## Research

### What sources or references have you identified as relevant to this task?

When researching how to approach the design and implementation of Greedy Piggies, I looked at existing games that share similarities with our mechanics. These ranged from digital card games to a classic card game that has been around for centuries. Looking at how other games solved similar problems — shops, card hand logic, multiplayer bluffing — helped inform how we thought about our own systems.

---

#### Slay the Spire

![SlayTheSpireShopScreen](https://interfaceingame.com/wp-content/uploads/slay-the-spire/slay-the-spire-store-1920x1080.jpg)
*Figure 2 - Slay the Spire Shop Screen* (Store - Slay the Spire, s.d.)

Slay the Spire is a roguelike deckbuilder developed by MegaCrit. (Games - Mega Crit Games, s.d.) It is widely regarded as one of the most successful digital card games and is relevant to Greedy Piggies primarily because of how it handles its shop system and card economy. (Slay the Spire Review - IGN, s.d.) In Slay the Spire, players visit a shop between combat encounters where they can spend gold to buy new cards, remove cards from their deck, or purchase relics. This directly parallels the shop mechanic we built into Greedy Piggies, where players can spend resources between rounds to acquire new cards or buffs.

![SlatTheSpireCombat](https://cdn.mos.cms.futurecdn.net/34pQ4ggkqocbB2W6j3cF2B-650-80.jpg.webp)
*Figure 3 - Slay the Spire Combat* (Kinglink, 2019)

The game also demonstrates how card abilities and combinations can be layered to create depth and replayability. Individual cards in Slay the Spire are straightforward on their own, but they become much more powerful when built around synergies. (Slay the Spire | Complete Beginner’s Guide and Beyond | Silent - Ascension 5 | Act 1, 2025) This influenced how we thought about the card abilities and archetype system in Greedy Piggies, where character archetypes change how certain cards behave and reward players for building around them rather than just playing whatever is available. 

---

#### Balatro


Balatro is a poker-based roguelike developed by LocalThunk. (Balatro, s.d.) It is directly relevant to Greedy Piggies because it uses the same standard 52-card deck as a foundation and layers additional ability cards on top of it. In Balatro these are called Jokers, and they fundamentally change how scoring works, for example a player might have a Joker that triples the value of flush hands, or one that scores bonus points for every card played of a specific suit. (Jokers, s.d.) This maps closely to how Greedy Piggies uses archetype cards that modify the base rules of play for each character.

![BalatroGameplay](https://static0.polygonimages.com/wordpress/wp-content/uploads/2024/11/GcrvGTWWYAAJ_b5.jpg?w=1200&h=675&fit=crop)
*Figure 4 - Balatro Gameplay* (Morley, 2024)


Balatro also shows how familiar hand rankings, pairs, three of a kind, straights, can be made fresh and interesting by adding modifiers on top of them rather than reinventing the underlying structure. Our scoring logic in `BPC_PlayCards` uses the same hand ranking foundation, calculating multipliers based on whether a player submits a pair or three of a kind, which is the same design approach Balatro takes.

![BalatroShop](https://static.wikia.nocookie.net/balatrogame/images/0/0f/Screenshot_in_shop.png/revision/latest/scale-to-width-down/1200?cb=20250414054711)
*Figure 5 - Balatro Shop* (Balatro Wiki, 2025)

---

#### Neon White

![NeonWhiteGameplay](https://www.psu.com/wp/wp-content/uploads/2022/12/Neon-White-Review-1-e1671143257719.jpg)
*Figure 6 - Neon White Gameplay image showing cards in hand* (Diaz, 2022)

Neon White is an action game developed by Angel Matrix where cards are the entire gameplay system. (Neon White - Annapurna Interactive, s.d.) Every card in Neon White serves two purposes: it can be used as a weapon to eliminate enemies, or discarded to activate a movement ability. This discard mechanic is particularly relevant to Greedy Piggies because it shows how choosing not to play a card can be just as meaningful as playing it. In our game, the decision of which cards to submit versus which to hold back has a similar strategic weight.

Neon White also demonstrates how a card system can feel natural and responsive in a real-time context. (Neon White Review - IGN, s.d.) While Greedy Piggies is turn-based rather than real-time, the principle that cards should feel like a direct extension of player intent rather than a menu system was something we thought about when designing how cards are selected and submitted.

![NeonWhiteGameplayGif](https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExYXh5bHBhYWlqb3p6M3ZzdWJ3c2Jma2tlcTNrbHJnaW53cm53eGMzaSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/jNCRVDSX6cN0HXWoh7/giphy.gif)

*Figure 7 - Neon White Gameplay* (Fps Platformer GIF by Annapurna Interactive - Find & Share on GIPHY, s.d.)

---

#### Poker

![PokerHandRankings](https://blog-contents.com/wp-content/uploads/2023/10/poker-hands-rankings.jpg)
*Figure 8 - Poker Hand Rankings* (Poker Hand Rankings: Complete Guide to Hold’em, Short Deck & Lowball, s.d.)

Poker is the game that Greedy Piggies draws most directly from in terms of structure. It is a centuries-old card game built around hand rankings, bluffing, and reading other players, all of which are central to how Greedy Piggies works. The auditing mechanic in our game where players can call out a bluff and trigger a review of what was actually submitted is a direct digital interpretation of the bluffing and calling mechanic that poker is built on.

![RealLifePokerGame](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/PokerTableBradley.jpg)
*Figure 9 - Professional Poker Game being played by myself*

Poker also validated our use of standard hand rankings as a scoring foundation. Pairs and three of a kind are poker concepts that most players already understand intuitively, which meant we could build complexity on top of familiar rules rather than having to teach an entirely new system. The longevity of poker as a game also showed that a relatively simple ruleset around hidden information and social deduction can sustain long-term interest when the player interactions are engaging enough.

---

## Implementation

### What was your development process and how did decisions evolve?

#### Project Coordination

Alongside another project coordinator I was responsible for managing the team throughout development. This involved assigning tasks to developers based on what needed doing at each stage of the project, checking in on progress, and making sure work wasn't being blocked or duplicated. Having two coordinators meant we could split the workload and keep on top of both the technical side and the organisational side at the same time, with my contributions leaning more into the technical side of things.

Part of this coordination role tied directly into the Git management work. With multiple developers working on different features at the same time across different branches, keeping the repository clean and making sure people weren't going to lose their work when branches were merged was something I focused on throughout the whole project rather than just at the end.

![Git Branches](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/GitBranches.gif)

*Figure 10 - Gif of the Greedy Piggies Git branches* 

#### Asset Scanner Tool


I built an asset scanner that runs inside the UE5 editor using the Python scripting plugin. (Scripting the Unreal Editor Using Python | Unreal Engine 5.7 Documentation | Epic Developer Community, s.d.) The purpose of the tool was to give the team a way to check their assets against a set of agreed quality thresholds before those assets were used in the game. (UE5 Optimization | Community tutorial, 2025) Without something like this it was easy for assets to slip through that were too high poly, missing LODs, had textures that were too large, or had file sizes that would cause problems further down the line.

The scanner checks every Static Mesh and Texture2D in a designated drop-off folder called `/Game/DropOff` and flags anything that breaks one of four rules.

```python
MAX_TRIANGLES     
MAX_TEXTURE_SIZE  
MIN_LODS          
MAX_ASSET_SIZE_MB 
```

![DropOff2D](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/DropOff2D.png)
*Figure 11 - Screenshot of the 2D DropOff folder in UE5 Editor*

![DropOff3D](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/DropOff3D.png)
*Figure 12 - Screenshot of the 3D DropOff folder in UE5 Editor*

When the scan finishes it prints a summary to the UE5 Output Log and writes two output files. The first is a CSV containing every flagged asset, and the second is a Markdown report that organises the issues into sections so they are easy to read and share. (csv — CSV File Reading and Writing, s.d.) 

```python
all_flagged = scan_meshes() + scan_textures()
print_and_export(all_flagged)
```

![LogOutput](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/UE5OutputLog.png)
*Figure 13 - Screenshot of the UE5 Output Log showing the scan results*

I also built a companion script called `generate_report.py` that runs outside the editor. It reads the CSV, validates the data, generates graphs using matplotlib, and rebuilds the Markdown report with those graphs embedded in it. (Using Matplotlib — Matplotlib 3.10.8 documentation, s.d.) This meant the team could get a visual breakdown of the issues at a glance rather than having to read through a table to understand the scale of the problems.

![Scan Results](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/scan_results.png)
*Figure 14 - Matplotlib graph showing the scan results*

The tool was useful to the team because it gave everyone a shared reference point. Rather than the QA process being informal or inconsistent, there was a script that anyone could run which would produce the same report every time based on the same thresholds. Artists knew what the standards were and could check their own work before submitting, and the QA lead could run the scanner across all submitted assets and have a report ready to review without having to manually inspect everything.

![Asset Audit Output](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/AssetAuditOutput.gif)

*Figure 15 - Gif of the Asset Audit Tool markdown output*

I used Sphinx (Sphinx — Sphinx documentation, s.d.) to create a more in depth technical documentation for the tool which can be found here:  https://bradleycurtisdev.github.io/ToolsAndProduction/index.html

<img src="https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/AssetScannerQRCode.png" alt="AssetScannerQRCode" width="200"/>

*Figure 16 - QR Code to the Asset Audit Tool technical documentation*

#### Multiplayer Systems

![BP Dealer Overview](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/BP_DealerOverviewImage.png)

*Figure 17 - Screenshot of the BP_Dealer blueprint*

My work on the multiplayer side of Greedy Piggies started around the 13th of March. At that point I had got both players showing up on each other's screens, but the client player still couldn't see their own cards. The main blueprints I was working with were `BP_Dealer`, `BP_FirstPersonCharacter_HarryTesting`, `BPC_PlayCards`, and the multiplayer game mode `GM_Multiplayer`.

The replication architecture across these blueprints followed a consistent pattern. (Replication Graph overview and proper replication methods, s.d.) All player actions originate from Enhanced Input Actions inside `BP_FirstPersonCharacter_HarryTesting`. These input events are gated behind an `IsLocallyControlled` check so they only fire on the pawn the player actually owns. From there, each action calls a Server RPC which runs exclusively on the server and makes the authoritative change to game state. The Server RPCs I implemented or fixed in `BP_FirstPersonCharacter_HarryTesting` were:

- `ServerPlayCards` — notifies the server the player has played their cards
- `ServerSubmitCards` — confirms final card submission from the client
- `ServerAuditYes` / `ServerAuditNo` — sends the player's audit vote to the server
- `ServerCardSelectionLeft` / `ServerCardSelectionRight` — syncs card scroll input server-side
- `ServerBluffValue` — sends the declared bluff value to the server

![ServerExecutedCustomEvents](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/ServerExecutedCustomEvents.png)

*Figure 18 - Screenshot of how we had to create server replicated custom events to get gameplay working across multiple instances*

Once the server receives one of these RPCs it calls into `BP_Dealer`, which is the authoritative manager of all game state. `BP_Dealer` contains the core game flow events including `StartGame`, `DealCard`, `StartingDeal`, `AddToHands`, `Turn`, `AuditPhase`, `NewAuditPhase`, `AuditInput`, `RefillHand`, `UpdateAllScores`, and `ServerIsAuditing`. Because `BP_Dealer` only executes on the server, game state can only be changed through it, which kept things consistent across all connected clients.

![IsLocallyControlledExample](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/IsLocallyControlledExample.png)

*Figure 19 - Screenshot of IsLocallyControlled node to get who is currently playing*

To push results back out to all players, `BPC_PlayCards` uses Multicast events. (Networking and Multiplayer in Unreal Engine | Unreal Engine 5.7 Documentation | Epic Developer Community, s.d.) These included `AuditDecision`, `RemoveAuditWBP`, `CreateDeclareValueWBP`, and `CreateShopWidget`, which handle showing and hiding UI widgets on every player's screen at the right moment. Character archetypes were synced to all clients using a `Multicast_ApplyArchetype` call from `BP_ArchetypeComponent`.

`GM_Multiplayer` handled the session side. It fired a `K2_PostLogin` event each time a player joined and used `BP_PlayerState` to assign each player their index. It tracked `TotalPlayers` and `ReadyPlayers` variables and used a `CheckAllPlayersReady` server function to decide when to start the game. `HasAuthority` checks gated any logic that should only run on the server. A `Muticast Join` event from `GS_Multiplayer` notified all clients when a new player connected. (Networking and Multiplayer in Unreal Engine | Unreal Engine 5.7 Documentation | Epic Developer Community, s.d.)

The first thing I focused on was getting `BP_Dealer` to correctly read card submissions from the server side, because up to that point the server wasn't picking them up at all. After that I worked on the broader gameplay loop and tried to get turn order and auditing functional across all connected players.

The trickiest problem was getting card submission to work for the client player specifically. The input had originally been checked using a Make Literal Text node to detect the enter key, which works fine locally but cannot be replicated in Unreal's networking model. Because you cannot create a custom event from a Make Literal Text node, clients had no way to trigger the submission. I flagged this in a commit message at the time, noting the system would need a proper rework.

I had the auditing mechanic working across all players and had resolved the input issues, including a separate bug that was preventing four player sessions from starting correctly.


![HandValueInputFix](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/CardValueFix.png)

*Figure 20 - Screenshot of the fixed card value input by using a widget blueprint rather than taking raw keyboard inputs from the player.* 

### What creative or technical methods did you try?

Most of my work was technical rather than creative. The main challenge was understanding how Unreal's replication model works and why certain approaches that worked in single player couldn't just be copied over to a multiplayer context. Learning that some nodes simply don't replicate and that you have to route actions through the server using RPCs was something I had to work out through trial and error during this project.

### Did you experience any technical challenges?

The Make Literal Text input issue was the main technical challenge. Because the node type doesn't support custom events, there was no way to make it work on a client without rethinking the system. (Text Localization in Unreal Engine | Unreal Engine 5.7 Documentation | Epic Developer Community, s.d.) Unreal's networking model requires that any client-initiated action goes through a server RPC, and the original implementation didn't account for that at all.

---

## Testing

### What testing methods did you use?

Testing for the multiplayer systems was done by running sessions directly inside the UE5 editor using the standalone game mode with multiple player windows. To set this up I went to the play settings in the editor toolbar, set the number of players to four, and set the net mode to Play As Listen Server. This launched one window as the server host and three additional windows as clients, all running simultaneously on the same machine. This let me test the full session without needing multiple computers or a dedicated server build.

![4GameInstances](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/Running4GameInstances.png)

*Figure 21 - Screenshot of of how to run the game with 4 instances, one as the server host and three as clients.*

![In Game Screenshot](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/InGameScreenshot.png)

*Figure 22 - In game image of the level layout.*

Running it this way meant I could watch all four windows at the same time and see exactly where things were breaking. For example, when the Make Literal Text input bug was present I could see the host submitting cards fine while the client windows showed no response at all, which confirmed the issue was on the client side rather than server side. After fixing `ServerSubmitCards` and switching to the Enhanced Input approach I could verify that card submission triggered correctly in all four windows.

For the auditing mechanic I checked that `AuditDecision` multicast events were firing correctly by watching whether the audit UI appeared on all client windows at the same time when a player triggered it. Similarly for the `BPC_CheckAuditWinner` logic I verified that the outcome was calculated once on the server and then reflected correctly across all connected players without any desync.

Bugs were identified by running the game, observing where it broke, and then tracing the issue back through the relevant blueprints — checking whether the problem was a missing `IsLocallyControlled` guard, an RPC not being marked correctly, or a function executing on the wrong side of the server/client boundary.

For the asset scanner, testing was done by running the script against assets in the drop-off folder and checking that the output matched what was expected. I also built automated validation into `generate_report.py` which runs every time the script is executed and checks that the CSV data is well-formed and that every flagged value genuinely violates its threshold.

---

## Critical Reflection

### What went well?

Getting the auditing mechanic working across all players felt like a good result, especially given how much trouble the input system gave me earlier in the process. The merge management also went well in the sense that the team didn't lose much work at all during the project, which was something I was conscious of throughout given how messy Unreal binary asset conflicts can get. The asset scanner ended up being a genuinely useful tool, especially for the art leads, and gave everyone a consistent way to check their work against the same standards.

### What could be improved or done differently next time?

The input system for card submission should have been set up with networking in mind from the start. If I were doing it again I would make sure any player input that needs to reach the server is routed through a proper input action and server RPC from the beginning, rather than discovering partway through that the existing approach couldn't work on a client. Planning the replication architecture before building the gameplay systems would have saved a significant amount of time.

---

## Bibliography

Morley, G. (2024) Balatro cast a magic spell that made me like math. At: https://www.polygon.com/reviews/24084564/balatro-review-poker-game-deck-building-roguelite/ (Accessed 14/02/2026).

Balatro (s.d.) Balatro: Deck-Building Roguelite. At: https://www.playbalatro.com/ (Accessed 14/02/2026).

csv — CSV File Reading and Writing (s.d.) At: https://docs.python.org/3/library/csv.html (Accessed 28/03/2026).

Fps Platformer GIF by Annapurna Interactive - Find & Share on GIPHY (s.d.) At: https://giphy.com/gifs/annapurnainteractive-speedrunning-speedrunner-neon-white-jNCRVDSX6cN0HXWoh7 (Accessed 21/02/2026).

Games - Mega Crit Games (s.d.) At: https://www.megacrit.com/games/ (Accessed 13/02/2026).

Greedy Piggies on Steam (s.d.) At: https://store.steampowered.com/app/4463930/Greedy_Piggies/ (Accessed 11/02/2026).

Jokers (s.d.) At: https://balatrogame.fandom.com/wiki/Jokers (Accessed 17/02/2026).

Neon White - Annapurna Interactive (s.d.) At: https://annapurnainteractive.com/en/games/neon-white (Accessed 24/02/2026).

Diaz, A. (2022) Neon White isn’t just for ‘freaks,’ it made me into one. At: https://www.polygon.com/23179286/neon-white-first-person-shooter-speedrun-impressions/ (Accessed 22/02/2026).

Neon White Review - IGN (s.d.) At: https://www.ign.com/articles/neon-white-review (Accessed 23/02/2026).

Networking and Multiplayer in Unreal Engine | Unreal Engine 5.7 Documentation | Epic Developer Community (s.d.) At: https://dev.epicgames.com/documentation/unreal-engine/networking-and-multiplayer-in-unreal-engine (Accessed 19/03/2026).

Poker Hand Rankings: Complete Guide to Hold’em, Short Deck & Lowball (s.d.) At: https://ggpoker.com/blog/holdem-and-short-deck-and-more-oh-my/ (Accessed 07/03/2026).

Replication Graph overview and proper replication methods (s.d.) At: https://www.unrealengine.com/tech-blog/replication-graph-overview-and-proper-replication-methods (Accessed 22/03/2026).

Scripting the Unreal Editor Using Python | Unreal Engine 5.7 Documentation | Epic Developer Community (s.d.) At: https://dev.epicgames.com/documentation/unreal-engine/scripting-the-unreal-editor-using-python (Accessed 05/03/2026).

Kinglink (2019) Slay the Spire – Review – Just one more run… just one more. At: https://kinglink-reviews.com/2019/08/25/slay-the-spire-review/ (Accessed 16/02/2026).

Slay the Spire | Complete Beginner’s Guide and Beyond | Silent - Ascension 5 | Act 1 (2025) Directed by Dr. Incompetent. At: https://www.youtube.com/watch?v=K-FuktUH1Sg (Accessed 17/02/2026).

Slay the Spire Review - IGN (s.d.) At: https://www.ign.com/articles/2019/01/25/slay-the-spire-review (Accessed 15/02/2026).

Sphinx — Sphinx documentation (s.d.) At: https://www.sphinx-doc.org/en/master/ (Accessed 01/04/2026).

Store - Slay the Spire (s.d.) At: https://interfaceingame.com/screenshots/slay-the-spire-store/ (Accessed 16/02/2026).

Text Localization in Unreal Engine | Unreal Engine 5.7 Documentation | Epic Developer Community (s.d.) At: https://dev.epicgames.com/documentation/unreal-engine/text-localization-in-unreal-engine (Accessed 25/03/2026).

UE5 Optimization | Community tutorial (2025) At: https://dev.epicgames.com/community/learning/tutorials/7K4a/unreal-engine-ue5-optimization (Accessed 08/04/2026).

Using Matplotlib — Matplotlib 3.10.8 documentation (s.d.) At: https://matplotlib.org/stable/users/index.html (Accessed 12/03/2026).


---

## Declared Assets

This document was modified and formatted with the use of:

- Claude Sonnet 4.6 (Claude, s.d.)

Claude (s.d.) At: https://claude.ai/login?from=logout (Accessed  22/04/2026).


- Google Gemini 3.1 Pro (Google Gemini, s.d.)

At: https://gemini.google.com (Accessed  22/04/2026).
