# Theory Discipline Essay — Outline and Draft
## Greedy Piggies: Procedural Rhetoric, Virtual Economies, and the Ethics of Play

**Student:** Bradley Curtis | **ID:** 2309516 | **Unit:** FGCT5017 Tools and Production
**Word Target:** 1,750 words | **Deadline:** 24 April 2026

---

## Argument (Central Thesis)

Greedy Piggies makes arguments through its mechanics. The auditing mechanic procedurally encodes a claim about deception and accountability in competition. The shop system encodes a claim about resource accumulation and advantage. These arguments can be unpacked using Ian Bogost's concept of procedural rhetoric, and situated within the broader context of how games commodify player attention and construct in-game economies. Rather than exploiting an impatience economy in the way that freemium games do, Greedy Piggies operates as a single-purchase title on Steam and positions its economy entirely within the game world — a design decision with ethical implications that can be evaluated using the frameworks of Evans (2016) and Neely (2019).

---

## Essay Structure

---

### 01 — Introduction (~175 words)

**What to cover:**
- Introduce Greedy Piggies: a multiplayer card game developed in Unreal Engine 5, published on Steam, built around bluffing, auditing, card hand rankings, and a between-round shop system.
- State the essay's argument clearly: that Greedy Piggies communicates ideological claims through its rules rather than its narrative, and that these claims can be analysed using procedural rhetoric as a primary framework and money games theory as a secondary lens.
- Name the key sources you will draw on: Bogost (2007), Evans (2016), Neely (2019).
- Briefly name the reference games that informed the project: Balatro, Slay the Spire, and Poker.
- End with a signpost sentence outlining the structure of the essay.

**Key point to argue, not describe:** the reward structure of Greedy Piggies is already a set of arguments about competition, risk, and resource accumulation — and the essay will demonstrate what those arguments are.

---

### 02 — Literature Review (~440 words)

**What to cover:**

#### Procedural Rhetoric — Bogost (2007)
- Define procedural rhetoric using Bogost's own words: *"Procedural rhetoric is the practice of persuading through processes in general and computational processes in particular"* (Bogost, 2007, p.3).
- Explain the core idea: games do not argue through dialogue or cutscenes. They argue through what they allow, what they forbid, and what they make inevitable. As the seminar puts it, games say *"Try surviving this system"* rather than stating a position outright.
- Introduce Bogost's four questions for systems literacy: What are the rules? What is the significance of those rules? What claims about the world do they make? How do I respond to those claims? These are the analytical tools you will apply to Greedy Piggies in the case study section.
- Note that procedural rhetoric is not about storytelling or cutscenes — it is about the mechanics themselves. This is why the auditing mechanic, the scoring system, and the shop loop are the relevant objects of analysis, not the game's visual style or setting.

#### Money Games — Evans (2016), Neely (2019), Goldhaber (1997)
- Introduce Goldhaber's attention economy: *"We are drowning in information... There is something else that moves through the Net, flowing in the opposite direction from information, namely attention"* (Goldhaber, 1997). Human attention is scarce and therefore economically valuable.
- Introduce Evans' impatience economy: freemium games profit not just from when players play, but from the time in between. *"Play is interspersed with nonplay"* (Evans, 2016, p.569). Waiting timers create impatience, and impatience is then monetised. Money flows from frustration rather than enjoyment.
- Introduce Neely's taxonomy of microtransactions: cosmetics only (ethical), fixed-cost functional shortcuts (conditional), pay-to-win (problematic), loot boxes with random reward (contested). Neely argues that *"fixed-cost functional items can be ethical if they function essentially as shortcuts to attaining items available in the game"* (Neely, 2019).
- Use these three frameworks to set up a question you will answer in the case study: where does Greedy Piggies sit within these frameworks, and what does its monetisation model argue about games and fairness?

---

### 03 — Case Studies (~700 words)

Three reference games followed by Greedy Piggies itself as the primary case study.

---

#### Case Study 1: Balatro — Procedural Rhetoric of Accumulation (~150 words)

- Balatro is a poker-based roguelike built on a standard 52-card deck with Joker cards layered on top. Each Joker fundamentally changes how hand rankings score.
- Apply Bogost's framework: the mechanics reward the player for identifying and building around multiplier synergies. The game does not say "compound advantage matters" — but the scoring system makes this inevitable. A player who ignores Joker synergies and plays random hands will always lose to one who compounds modifiers.
- Procedural argument: **advantage compounds; optimisation is rewarded over improvisation.**
- **Link to Greedy Piggies:** the archetype system in Greedy Piggies functions similarly to Joker cards. Character archetypes modify the base rules for that player, creating asymmetric advantages that reward players who understand how archetypes interact with the hand ranking system. The scoring multipliers for pairs and three of a kind in BPC_PlayCards directly mirror Balatro's hand ranking foundation.

---

#### Case Study 2: Slay the Spire — The Shop as a Procedural System (~150 words)

- Slay the Spire's shop allows players to spend gold accumulated during runs on new cards, card removals, and relics. The shop is a mechanic, not a store — it encodes a resource management argument.
- Apply Bogost's framework: the shop rewards players who conserve resources and make calculated purchases over those who spend freely. Removing bad cards from your deck is worth as much as adding good ones. The game makes a procedural argument: **a system's strength depends on removing weaknesses, not just adding power.**
- **Link to Greedy Piggies:** the between-round shop in Greedy Piggies operates on the same logic. Players who manage their resources across rounds and make deliberate shop decisions compound their advantage over players who spend reactively. The shop is not just a feature — it is a procedural argument about planning versus improvisation.

---

#### Case Study 3: Poker — Bluffing as Procedural Argument (~150 words)

- Poker is built around hidden information and the mechanics of bluffing and calling. A player cannot see another's hand; they can only infer from behaviour and act on that inference. The call mechanic — challenging a bluff — is the core procedural argument of the game.
- Apply Bogost's framework: poker does not say "deception exists in competitive environments and can be challenged." It makes you perform this truth. Every time a player calls a bluff, they are enacting the argument procedurally.
- **Link to Greedy Piggies:** the auditing mechanic is a direct digital translation of poker's call. When one player triggers an audit, they are challenging the claim that the submitted hand is what was declared. The ServerAuditYes and ServerAuditNo RPCs in the game's networking architecture implement this mechanic across all connected players. The game procedurally argues: **deception is available, but accountability is always possible.**

---

#### Case Study 4: Greedy Piggies — The Primary Case Study (~250 words)

Apply all three frameworks directly to Greedy Piggies.

**Procedural rhetoric of the auditing mechanic:**
- The rules allow a player to bluff by submitting a hand that does not match their declaration. The rules also allow any other player to call an audit. The outcome — who gains and who loses — is calculated on the server and broadcast to all players.
- Bogost's question: what claim does this make? The mechanic argues that in a competitive system built on declared value, trust is not given freely. Verification is built into the rules. The game does not lecture players about honesty — it makes dishonesty available and immediately answerable.

**Procedural rhetoric of the shop:**
- Between rounds, players spend accumulated resources on new cards or upgrades. This creates a compounding advantage mechanic. Players who have won previous rounds enter the shop with more purchasing power.
- This procedurally argues that early advantage compounds — wealth begets wealth — a claim that sits in tension with the bluffing mechanic, which gives any player the ability to disrupt an advantaged opponent through a successful audit.

**Money Games — where Greedy Piggies sits ethically:**
- Greedy Piggies is a single-purchase Steam title with no real-money shop, no loot boxes, and no microtransactions. Using Ash's (2015) framework, it operates as an attention economy product: it monetises player time through engaging mechanics rather than through psychological compulsion.
- Using Neely's (2019) taxonomy, the shop exists entirely within the game's virtual economy. No real money changes hands after purchase. This places Greedy Piggies at the ethical end of Neely's spectrum — closer to cosmetics-only than pay-to-win, because all shop items are achievable through play alone.
- Evans' impatience economy does not apply: there are no timers, no artificial nonplay phases, no waiting structures designed to produce frustration. The absence of these mechanics is itself a procedural argument — the game refuses to monetise impatience.

---

### 04 — Conclusion (~235 words)

**What to cover:**
- Draw together the argument: Greedy Piggies encodes two distinct procedural claims. The auditing mechanic argues that deception is available but accountability is always possible. The shop mechanic argues that early advantage compounds, but can be disrupted by the bluffing and auditing system.
- Reflect on what the case study comparisons revealed: Balatro showed how modifier stacking creates a procedural argument about optimisation; Slay the Spire showed how shop design encodes resource management logic; Poker showed how the call mechanic performs an argument about trust that Greedy Piggies directly inherits.
- Apply the money games lens as a closing argument: by choosing a single-purchase model with no real-money economy, Greedy Piggies sits in a different ethical position to freemium games that exploit Evans' impatience economy. The game makes money from player attention in the way Ash describes — through engaging mechanics — rather than from frustration.
- Offer a critical insight: the tension between the shop (which rewards accumulated advantage) and the auditing mechanic (which rewards challenge and disruption) is the game's most interesting procedural argument. It suggests that no advantage is permanent, and that the player with fewer resources always has a recourse. Whether this is a genuine equaliser or a rhetorical comfort is a question the game leaves open.

---

### 05 — Research Process (~200 words) ★ NEW REQUIREMENT

**What to cover:**
- Explain how you began research by identifying the three theoretical frameworks from the module seminars that were most relevant to the game's mechanics: procedural rhetoric, attention economies, and virtual economies and ethics.
- Explain that you started with Bogost (2007) as the primary source because it directly addresses how game mechanics carry meaning — and the auditing and shop mechanics in Greedy Piggies are the most analytically rich parts of the design.
- Explain that you then looked at Evans (2016) and Neely (2019) because the game has a shop system and is distributed commercially, so the money games frameworks offered a way to evaluate the design decisions ethically rather than just structurally.
- Note that the reference games — Balatro, Slay the Spire, and Poker — were identified during development as direct inspirations, which meant the research process involved reading back from the games to the theories rather than starting from theory and finding examples.
- Acknowledge the limitation: the Week 4 nature in games framework (Chang, 2019) was considered but set aside because Greedy Piggies has no natural environment — its procedural arguments operate entirely through its card economy and social dynamics rather than through landscape.

---

## Academic Sources to Use

These are the sources you must cite explicitly in the essay:

| Source | Where it appears |
|---|---|
| Bogost, I. (2007) *Persuasive Games.* MIT Press. (pp. 1–3) | Literature Review + all Case Studies |
| Evans, E. (2016) 'The economics of free: Freemium games, branding and the impatience economy.' *Convergence*, 22(6). | Literature Review + Greedy Piggies case study |
| Neely, E.L. (2019) 'Come for the Game, Stay for the Cash Grab.' *Games and Culture.* | Literature Review + Greedy Piggies case study |
| Goldhaber, M.H. (1997) 'The Attention Economy and the Net.' *First Monday.* 2. | Literature Review |
| Ash, J. (2015) *The Interface Envelope.* Bloomsbury Academic. | Greedy Piggies case study |

**Minimum three required — you have five. All are directly from the module readings.**

---

## Bibliography (for the final essay)

Ash, J. (2015) *The Interface Envelope: Gaming, Technology, Power.* Bloomsbury Academic.

Bogost, I. (2007) *Persuasive Games: The Expressive Power of Videogames.* Cambridge, MA: MIT Press.

Evans, E. (2016) 'The economics of free: Freemium games, branding and the impatience economy.' *Convergence,* 22(6). Available at: https://doi.org/10.1177/1354856514567052

Goldhaber, M.H. (1997) 'The Attention Economy and the Net.' *First Monday,* 2. Available at: https://firstmonday.org/article/view/519/440

Neely, E.L. (2019) 'Come for the Game, Stay for the Cash Grab: The Ethics of Loot Boxes, Microtransactions, and Freemium Games.' *Games and Culture.* Available at: https://doi.org/10.1177/1555412019887658

---

## Final Checklist

- [ ] 1,750 words (±10% = 1,575–1,925 words)
- [ ] Reference to creative project (Greedy Piggies) throughout
- [ ] Clear critical framework (procedural rhetoric as primary, money games as secondary)
- [ ] At least three academic sources (five identified above)
- [ ] Bibliography of explicitly cited works only
- [ ] 200-word research process section
- [ ] Argue, don't describe — each game is used as evidence, not summarised
- [ ] Connect to practice — Greedy Piggies treated with same rigour as the reference games

---

---

# ESSAY DRAFT

## Greedy Piggies: Procedural Rhetoric, Virtual Economies, and the Ethics of Play

**Student:** Bradley Curtis | **ID:** 2309516 | **Unit:** FGCT5017 Tools and Production
**Word Count:** ~1,750 words | **Deadline:** 24 April 2026

---

## Introduction

Greedy Piggies is a multiplayer card game developed in Unreal Engine 5 and published on Steam as the practical outcome of this module. Players compete across rounds using card hands drawn from a shared deck, with a bluffing and auditing mechanic at the centre of each turn and a between-round shop system that allows resources to compound across a session. The game did not emerge in isolation — its core mechanics were directly shaped by two established points of reference: *Slay the Spire* (Mega Crit, 2019), which informed the shop and resource accumulation loop, and Poker, which provided the structural model for bluffing and accountability.

This essay argues that critically examining those inspirations through academic frameworks reveals not only where Greedy Piggies' mechanics come from, but what arguments those mechanics make. Using Ian Bogost's procedural rhetoric as the primary analytical lens (Bogost, 2007), Elizabeth Evans' money games theory to evaluate the game's economic positioning (Evans, 2016), and Alenda Chang's nature in games framework to examine the closed resource system the game constructs (Chang, 2019), the essay demonstrates that the design decisions made during development encode ideological claims about competition, fairness, and accountability — claims that were absorbed from the reference games and reshaped in the process of building Greedy Piggies.

---

## Literature Review

### Procedural Rhetoric — Bogost (2007)

Ian Bogost defines procedural rhetoric as 'the practice of persuading through processes in general and computational processes in particular' (Bogost, 2007, p.3). The core insight is that games do not argue through dialogue or cutscenes — they argue through what they allow, what they forbid, and what they make inevitable. A game that penalises a player for poor resource management does not need to state that planning matters; it makes the player experience that consequence directly. Bogost proposes four questions for reading any game system: What are the rules? What is the significance of those rules? What claims about the world do they make? How do players respond to those claims? (Bogost, 2007). These questions structure the analysis applied to each case study in this essay.

The critical distinction procedural rhetoric draws is between *telling* and *doing*. A cutscene can tell a player that deception has consequences; a mechanic makes those consequences immediate and personal. This is why the auditing and shop mechanics in Greedy Piggies — rather than its visual style or setting — are the objects of analysis here.

### Money Games — Evans (2016) and Goldhaber (1997)

To evaluate the arguments a game makes through its economic model, a second framework is required. Michael Goldhaber's attention economy argues that in the digital age human attention is the truly scarce resource, and that platforms compete to capture and hold it rather than simply exchanging goods for money (Goldhaber, 1997). Elizabeth Evans extends this into the impatience economy, examining how freemium mobile games monetise not the time players spend engaged, but the time they spend waiting. Evans observes that in these games 'play is interspersed with stretches of non-play' (Evans, 2016, p.10) — artificial waiting periods are built into the design as a commercial strategy. Players are made to wait, frustration accumulates, and the ability to skip that waiting is sold back to them. Evans argues this structure is 'ultimately concerned with monetising a player's impatience and desire to avoid waiting for the game's progression' (Evans, 2016, p.27). These frameworks raise a key question: where does Greedy Piggies sit within this model, and what does its monetisation choice argue about fairness?

### Nature in Games — Chang (2019)

Alenda Chang's *Playing Nature* argues that video games model ecological systems and, in doing so, teach players to think systemically about resource cycles, interdependence, and the consequences of individual action within a shared environment (Chang, 2019). Chang's ecocritical framework was developed primarily through games with natural landscapes, but its core concern — how games construct closed systems of resource flow and scarcity — extends beyond the environmental. Greedy Piggies has no natural environment, but it builds a closed artificial ecology: chips and cards flow between players, are won and lost through competition, and the shop redistributes resources between rounds. Viewing this through Chang's lens reveals that the game's card economy functions as a systemic model of competitive resource management, where individual actions have consequences across the whole player group, and where scarcity is manufactured by the rules rather than by nature. The absence of a natural ecology in Greedy Piggies is itself meaningful: the game's resource system is entirely human-constructed, which makes its procedural arguments about fairness and advantage more deliberate and more accountable.

---

## Case Studies

### Slay the Spire — The Shop as Procedural System and Ecological Model

*Slay the Spire* (Mega Crit, 2019) was a direct inspiration for the shop system in Greedy Piggies, and critically examining it through the module's frameworks reveals precisely what was inherited — and what that inheritance means as a design choice. In *Slay the Spire*, players spend gold accumulated during combat runs on new cards, card removals, and relics between floors. Applying Bogost's framework, the shop does not simply offer upgrades — it makes a procedural argument. The system rewards deliberate resource conservation over reactive spending, and makes the counterintuitive claim that removing weak cards from a deck is worth as much as adding powerful ones (Bogost, 2007). Efficiency requires eliminating weakness, not only accumulating strength.

Viewed through Chang's ecological lens, *Slay the Spire*'s economy functions as a closed resource system: gold flows into the player's hands through combat and out through spending, and the rules punish both hoarding and recklessness with equal severity (Chang, 2019). This is systemic thinking applied to game design — understanding that individual spending decisions have cascading consequences across the run as a whole. The between-round shop in Greedy Piggies was built on this same logic. Players who manage resources deliberately across rounds compound their advantage, while reactive spenders gradually fall behind. Recognising this as a procedural argument — rather than simply a game feature — reveals that when the team designed the shop loop, they were encoding a claim about the value of planning within a shared competitive system.

### Poker — Bluffing as Procedural Argument

Poker provided the second major structural inspiration for Greedy Piggies, specifically its mechanic of hidden information and challenge. In poker, a player cannot see another's hand and can only infer intent from behaviour. The call mechanic — staking chips to challenge a bet — is the game's core procedural argument. As Bogost would frame it, poker does not tell players that deception exists in competitive environments and can be challenged; it makes players perform this truth across every hand (Bogost, 2007). Every call is a procedural enactment of an argument about trust, risk, and accountability under conditions of incomplete information.

This structure was the direct model for the auditing mechanic in Greedy Piggies. When a player submits a card hand, they declare its value to all connected players. Any other player may trigger an audit, challenging the declared value. The outcome — who gains and who loses chips — is resolved server-side and broadcast to all simultaneously. The inheritance from poker is not superficial or cosmetic: it is structural. By translating poker's call into a digital multiplayer audit, the development team imported poker's core procedural argument — that deception is always available, but accountability is always possible — into a new context with new stakes.

### Greedy Piggies — The Primary Case Study

Greedy Piggies did not simply borrow mechanics from *Slay the Spire* and Poker — it synthesised them into a new system, and in doing so created a set of procedural arguments that are distinct from either source. Critically examining that system through all three frameworks reveals what the game argues, what it inherits, and what design choices were made — consciously or otherwise — in the process of building it.

Applying Bogost's framework, the auditing mechanic encodes a claim about trust in competitive systems. In a game built on declared value, verification is embedded in the rules rather than assumed. The game makes dishonesty available — players can submit a hand that does not match their declaration — and makes that dishonesty immediately answerable. A successful bluff rewards the deceiver; a successful audit punishes them and compensates the challenger. Crucially, the mechanic does not lecture players about fairness. It does not need to. It makes fairness a live question in every round, performed through the decision to audit or to trust (Bogost, 2007). This is the argument the game makes procedurally: that accountability is not a moral ideal imposed from outside a competitive system, but a structural feature that can be built into its rules.

The shop mechanic encodes a second, partially conflicting argument: that early advantage compounds. Players who win rounds accumulate more chips, enter the shop with more purchasing power, and can acquire stronger cards that improve their future performance. This creates a feedback loop — wealth begets competitive strength, which begets more wealth. However, the auditing mechanic partially disrupts this loop. A well-timed audit can strip chips from a dominant player, giving a resource-poor player a meaningful recourse. Whether the audit functions as a genuine equaliser or merely as rhetorical reassurance — creating the impression of fairness without truly balancing the system — is a question the game deliberately leaves unresolved. That ambiguity is itself one of its most interesting procedural arguments (Bogost, 2007).

Chang's framework reveals a further dimension of the system that procedural rhetoric alone does not capture. The card economy in Greedy Piggies is a closed artificial ecology: every chip gained by one player is taken from another, every card in the shop is a finite resource governed entirely by the game's rules rather than introduced from outside the system (Chang, 2019). This manufactured scarcity is not incidental — it is the condition that makes every decision in the game meaningful. Players who understand the resource pool systemically, who track what other players have spent and what competitive advantages are likely to have been built, will consistently outperform those who play in isolation from the broader group dynamic. The game teaches ecological thinking about a human-made competitive environment, applying the same logic Chang identifies in games with natural settings to a purely social and economic one.

Applying Evans' impatience economy reveals what Greedy Piggies refuses to do — and why that refusal constitutes an argument. There are no timers, no enforced waiting periods, and no monetisation structures designed to produce and then exploit frustration (Evans, 2016). Greedy Piggies is a single-purchase Steam title with no real-money shop, no loot boxes, and no microtransactions. All competitive advantages are achievable through play alone. In the context of a games market where, as Evans documents, design and commercial strategy are increasingly inseparable — where waiting is engineered to produce impatience that can be sold back to the player — the decision to build a game without those structures is a design argument in itself. The game argues, through its absence of impatience mechanics, that a competitive multiplayer experience does not need to monetise the time between rounds to be commercially viable or engaging.

---

## Conclusion

This essay set out to examine how the games and media that informed Greedy Piggies can be critically contextualised using academic frameworks, and what that contextualisation reveals about the creative decisions made during development. The answer is that those decisions were not neutral — they were argumentative. By inheriting *Slay the Spire*'s shop logic and Poker's auditing structure, the development team imported specific procedural claims into Greedy Piggies and reshaped them into a new system with its own ideological position.

Bogost's framework reveals the specific claims the mechanics make: that accountability is a structural feature of competitive systems, that early advantage compounds, and that the tension between deception and fairness cannot be designed away — only staged (Bogost, 2007). Chang's framework reveals that the card economy functions as a closed artificial ecology, where systemic thinking about the resource pool is rewarded and individual decisions have consequences across the whole player group (Chang, 2019). Evans' framework reveals that by refusing the impatience economy model — no timers, no real-money shortcuts, no monetisation of frustration — Greedy Piggies makes an ethical argument through what it chooses not to do (Evans, 2016).

Together, these readings demonstrate that the inspirations behind a game are not simply sources of borrowed ideas. They are arguments that the developer inherits, consciously or otherwise, and that become embedded in the mechanics of whatever is built from them. Whether the auditing mechanic makes Greedy Piggies genuinely fair or only rhetorically so is the productive ambiguity the game leaves unresolved — and the most honest reflection of the competitive systems it draws from.

---

## Research Process

Research began from the overarching question: what games informed the development of Greedy Piggies, and how can those inspirations be critically explored using academic frameworks? The two primary reference games — *Slay the Spire* and Poker — were identified during development as direct structural influences, which meant the research process moved backwards from the games to the theories rather than forwards from theory to example. This made each case study's analysis precise: rather than selecting games to illustrate a pre-chosen argument, the mechanics of the reference games were examined first, and the frameworks that best explained those mechanics were then applied.

Bogost (2007) was selected as the primary framework because procedural rhetoric directly addresses how game mechanics carry meaning — and the auditing and shop systems are the analytically richest parts of Greedy Piggies' design. Evans (2016) was selected because the game is a commercial product distributed on Steam, making the money games framework essential for evaluating whether its economic model is ethically distinct from the freemium industry Evans analyses. Goldhaber (1997) provided the theoretical foundation that Evans builds on.

Chang (2019) was initially considered less applicable because Greedy Piggies has no natural landscape. However, Chang's core concern — how games model closed systems of resource flow and teach players to think about systemic interdependence — applies directly to the card economy. This reframing allowed Chang's framework to reveal something neither Bogost nor Evans could: the ecological logic of the game's resource pool, and what it means for players to think and act within it.

---

## Bibliography

Bogost, I. (2007) *Persuasive Games: The Expressive Power of Videogames.* Cambridge, MA: MIT Press.

Chang, A.Y. (2019) *Playing Nature: Ecology in Video Games.* Minneapolis: University of Minnesota Press.

Evans, E. (2016) 'The economics of free: Freemium games, branding and the impatience economy.' *Convergence,* 22(6). Available at: https://doi.org/10.1177/1354856514567052

Goldhaber, M.H. (1997) 'The Attention Economy and the Net.' *First Monday,* 2. Available at: https://firstmonday.org/article/view/519/440

Neely, E.L. (2019) 'Come for the Game, Stay for the Cash Grab: The Ethics of Loot Boxes, Microtransactions, and Freemium Games.' *Games and Culture.* Available at: https://doi.org/10.1177/1555412019887658
