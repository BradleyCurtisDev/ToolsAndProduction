# Greedy Piggies — Development Commentary

**Unit Name:** Tools and Production FGCT5017

**Student Name:** Bradley Curtis

**Student ID:** 2309516

**Total Word Count:** [XXXX]

**API Reference Link:** https://bradleycurtisdev.github.io/ToolsAndProduction/

**User Guide Link:** [URL]

**Build Link:** [URL or Embed]

**Video Demonstration Link:** [URL or Embed]

---

## Overview

![TitleScreen](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/GreddyPiggiesTitle.png)

For this project I worked on Greedy Piggies, a multiplayer card game built in Unreal Engine 5. I had three main responsibilities across the project. The first was acting as one of two development project coordinators, where I worked alongside another coordinator to manage the team, assign tasks, and keep development moving. The second was implementing and fixing the multiplayer gameplay systems, which included getting the auditing mechanic working across all players, fixing card submission so it worked correctly on both the server and client, and resolving input issues that were stopping players from being able to interact properly. The third was building a Python asset scanner tool that ran inside the UE5 editor to help the team check their assets met the project's quality standards before they were brought into the game. I also managed the team's Git repository throughout the project, handling merges between branches to make sure nobody lost their work.

---

## Research

### What sources or references have you identified as relevant to this task?

---

## Implementation

### What was your development process and how did decisions evolve?

#### Project Coordination

Alongside another project coordinator I was responsible for managing the team throughout development. This involved assigning tasks to developers based on what needed doing at each stage of the project, checking in on progress, and making sure work wasn't being blocked or duplicated. Having two coordinators meant we could split the workload and keep on top of both the technical side and the organisational side at the same time, with my contributions leaning more into the technical side of things.

Part of this coordination role tied directly into the Git management work. With multiple developers working on different features at the same time across different branches, keeping the repository clean and making sure people weren't going to lose their work when branches were merged was something I focused on throughout the whole project rather than just at the end.

![Git Branches](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/GitBranches.gif)

#### Asset Scanner Tool


I built an asset scanner that runs inside the UE5 editor using the Python scripting plugin. The purpose of the tool was to give the team a way to check their assets against a set of agreed quality thresholds before those assets were used in the game. Without something like this it was easy for assets to slip through that were too high poly, missing LODs, had textures that were too large, or had file sizes that would cause problems further down the line.

The scanner checks every Static Mesh and Texture2D in a designated drop-off folder called `/Game/DropOff` and flags anything that breaks one of four rules.

```python
MAX_TRIANGLES     
MAX_TEXTURE_SIZE  
MIN_LODS          
MAX_ASSET_SIZE_MB 
```

<!-- IMAGE NEEDED: A screenshot of the /Game/DropOff folder open in the UE5 Content Browser, showing the assets sitting inside it. This shows the actual folder the scanner targets. -->

When the scan finishes it prints a summary to the UE5 Output Log and writes two output files. The first is a CSV containing every flagged asset, and the second is a Markdown report that organises the issues into sections so they are easy to read and share.

```python
all_flagged = scan_meshes() + scan_textures()
print_and_export(all_flagged)
```

<!-- IMAGE NEEDED: A screenshot of the UE5 Output Log showing the scan summary being printed — the lines listing how many assets were flagged per category. This proves the script ran inside the editor. -->

I also built a companion script called `generate_report.py` that runs outside the editor. It reads the CSV, validates the data, generates graphs using matplotlib, and rebuilds the Markdown report with those graphs embedded in it. This meant the team could get a visual breakdown of the issues at a glance rather than having to read through a table to understand the scale of the problems.

![Scan Results](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/scan_results.png)

The tool was useful to the team because it gave everyone a shared reference point. Rather than the QA process being informal or inconsistent, there was a script that anyone could run which would produce the same report every time based on the same thresholds. Artists knew what the standards were and could check their own work before submitting, and the QA lead could run the scanner across all submitted assets and have a report ready to review without having to manually inspect everything.

![Asset Audit Output](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/AssetAuditOutput.gif)

I used Sphinx to create a more in depth technical documentation for the tool which can be found here:  https://bradleycurtisdev.github.io/ToolsAndProduction/index.html

<img src="https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/AssetScannerQRCode.png" alt="AssetScannerQRCode" width="200"/>

#### Multiplayer Systems

My work on the multiplayer side of Greedy Piggies started around the 13th of March. At that point I had got both players showing up on each other's screens, but the client player still couldn't see their own cards. The main blueprints I was working with were `BP_Dealer`, `BP_FirstPersonCharacter_HarryTesting`, `BPC_PlayCards`, and the multiplayer game mode `GM_Multiplayer`.

The replication architecture across these blueprints followed a consistent pattern. All player actions originate from Enhanced Input Actions inside `BP_FirstPersonCharacter_HarryTesting`. These input events are gated behind an `IsLocallyControlled` check so they only fire on the pawn the player actually owns. From there, each action calls a Server RPC which runs exclusively on the server and makes the authoritative change to game state. The Server RPCs I implemented or fixed in `BP_FirstPersonCharacter_HarryTesting` were:

- `ServerPlayCards` — notifies the server the player has played their cards
- `ServerSubmitCards` — confirms final card submission from the client
- `ServerAuditYes` / `ServerAuditNo` — sends the player's audit vote to the server
- `ServerCardSelectionLeft` / `ServerCardSelectionRight` — syncs card scroll input server-side
- `ServerBluffValue` — sends the declared bluff value to the server

<!-- IMAGE NEEDED: A screenshot of the My Blueprint panel in BP_FirstPersonCharacter_HarryTesting showing the Server RPC functions listed under Functions. This makes the list above tangible and shows the actual blueprint structure. -->

Once the server receives one of these RPCs it calls into `BP_Dealer`, which is the authoritative manager of all game state. `BP_Dealer` contains the core game flow events including `StartGame`, `DealCard`, `StartingDeal`, `AddToHands`, `Turn`, `AuditPhase`, `NewAuditPhase`, `AuditInput`, `RefillHand`, `UpdateAllScores`, and `ServerIsAuditing`. Because `BP_Dealer` only executes on the server, game state can only be changed through it, which kept things consistent across all connected clients.

![BP Dealer Overview](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/BP_DealerOverviewImage.png)

<!-- IMAGE NEEDED: A screenshot of the IsLocallyControlled node in the BP_FirstPersonCharacter event graph, ideally with the branch flowing into one of the Server RPC calls. This illustrates the client-side guard that prevents input firing on the wrong pawn. -->

To push results back out to all players, `BPC_PlayCards` uses Multicast events. These included `AuditDecision`, `RemoveAuditWBP`, `CreateDeclareValueWBP`, and `CreateShopWidget`, which handle showing and hiding UI widgets on every player's screen at the right moment. Character archetypes were synced to all clients using a `Multicast_ApplyArchetype` call from `BP_ArchetypeComponent`.

`GM_Multiplayer` handled the session side. It fired a `K2_PostLogin` event each time a player joined and used `BP_PlayerState` to assign each player their index. It tracked `TotalPlayers` and `ReadyPlayers` variables and used a `CheckAllPlayersReady` server function to decide when to start the game. `HasAuthority` checks gated any logic that should only run on the server. A `Muticast Join` event from `GS_Multiplayer` notified all clients when a new player connected.

The first thing I focused on was getting `BP_Dealer` to correctly read card submissions from the server side, because up to that point the server wasn't picking them up at all. After that I worked on the broader gameplay loop and tried to get turn order and auditing functional across all connected players.

The trickiest problem was getting card submission to work for the client player specifically. The input had originally been checked using a Make Literal Text node to detect the enter key, which works fine locally but cannot be replicated in Unreal's networking model. Because you cannot create a custom event from a Make Literal Text node, clients had no way to trigger the submission. I flagged this in a commit message at the time, noting the system would need a proper rework.

I had the auditing mechanic working across all players and had resolved the input issues, including a separate bug that was preventing four player sessions from starting correctly.

#### Multiplayer Input Fix

The fix was to replace the Make Literal Text detection with a proper Enhanced Input Action. I added `IA_PlayCard` as a dedicated input action in `BP_FirstPersonCharacter_HarryTesting`, using the same Enhanced Input system already in place for the other actions such as `IA_AuditYes`, `IA_AuditNo`, `IA_ScrollLeft`, `IA_ScrollRight`, and `IA_CallNewCards`. With a proper input action I could create `ServerSubmitCards` as a Server RPC. The input action fires locally on the client and the RPC carries the intent to the server, where `BP_Dealer` handles the actual state change. This meant card submission worked correctly for both the host and any connected client.

<!-- IMAGE NEEDED: A screenshot of the IA_PlayCard input action asset open in the editor, showing it is set up as an Enhanced Input Action. Ideally place it next to or above a screenshot of the ServerSubmitCards RPC node in the event graph so the reader can see how the two connect. -->

### What creative or technical methods did you try?

Most of my work was technical rather than creative. The main challenge was understanding how Unreal's replication model works and why certain approaches that worked in single player couldn't just be copied over to a multiplayer context. Learning that some nodes simply don't replicate and that you have to route actions through the server using RPCs was something I had to work out through trial and error during this project.

### Did you experience any technical challenges?

The Make Literal Text input issue was the main technical challenge. Because the node type doesn't support custom events, there was no way to make it work on a client without rethinking the system. Unreal's networking model requires that any client-initiated action goes through a server RPC, and the original implementation didn't account for that at all.

---

## Testing

### What testing methods did you use?

Testing for the multiplayer systems was done by running sessions directly inside the UE5 editor using the standalone game mode with multiple player windows. To set this up I went to the play settings in the editor toolbar, set the number of players to four, and set the net mode to Play As Listen Server. This launched one window as the server host and three additional windows as clients, all running simultaneously on the same machine. This let me test the full session without needing multiple computers or a dedicated server build.

<!-- IMAGE NEEDED: A screenshot of the UE5 play settings dropdown open in the editor toolbar, showing the Number of Players set to 4 and Net Mode set to Play As Listen Server. This is the exact setup described above and directly supports the explanation. -->

![In Game Screenshot](https://raw.githubusercontent.com/BradleyCurtisDev/ToolsAndProduction/refs/heads/main/Images/InGameScreenshot.png)

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

---

## Declared Assets

