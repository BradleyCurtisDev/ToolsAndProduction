bradl@Bradley_Curtis MINGW64 /c/users/bradl/onedrive/documents/github/greedy_piggies (Multiplayer/gameplay)
$ git log --author="Bradley Curtis" --stat
commit 2f0261e012df205c84ab5ed46d545e455e665a15
Author: Bradley Curtis <bradleycurtis2004@gmail.com>
Date:   Thu Mar 19 17:05:53 2026 +0000

    Auditing with multiple players works

 Content/PrototypeBlueprints/BP_Dealer.uasset | 4 ++--
 1 file changed, 2 insertions(+), 2 deletions(-)

commit 2fb6fd4ac6fb3664af7587e12b559651fb7a207a
Author: Bradley Curtis <161096639+lunaviadev@users.noreply.github.com>
Date:   Thu Mar 19 12:52:49 2026 +0000

    fixed input not working, fixed 4 player not working, auditing now works for all players, input now works for all players

 Content/BP_FirstPersonCharacter_HarryTesting.COPY  | 6849 ++++++++++++++++++++
 Content/PrototypeBlueprints/BP_Dealer.uasset       |    4 +-
 .../BP_FirstPersonCharacter_HarryTesting.uasset    |    4 +-
 3 files changed, 6853 insertions(+), 4 deletions(-)

commit eb0b8006dbda37b4ce07acf48e12c06f89955537
Author: Bradley Curtis <2309516@students.ucreative.ac.uk>
:...skipping...
commit 2f0261e012df205c84ab5ed46d545e455e665a15
Author: Bradley Curtis <bradleycurtis2004@gmail.com>
Date:   Thu Mar 19 17:05:53 2026 +0000

    Auditing with multiple players works

 Content/PrototypeBlueprints/BP_Dealer.uasset | 4 ++--
 1 file changed, 2 insertions(+), 2 deletions(-)

commit 2fb6fd4ac6fb3664af7587e12b559651fb7a207a
Author: Bradley Curtis <161096639+lunaviadev@users.noreply.github.com>
Date:   Thu Mar 19 12:52:49 2026 +0000

    fixed input not working, fixed 4 player not working, auditing now works for all players, input now works for all players

 Content/BP_FirstPersonCharacter_HarryTesting.COPY  | 6849 ++++++++++++++++++++
 Content/PrototypeBlueprints/BP_Dealer.uasset       |    4 +-
 .../BP_FirstPersonCharacter_HarryTesting.uasset    |    4 +-
 3 files changed, 6853 insertions(+), 4 deletions(-)

commit eb0b8006dbda37b4ce07acf48e12c06f89955537
Author: Bradley Curtis <2309516@students.ucreative.ac.uk>
Date:   Mon Mar 16 19:44:43 2026 +0000

    Made the client player inputs works. Having an issue where the client player cant submit cards

    Issue is that the enter key is checked by a make literal text node rather than a input key so i cant make it work client side. This system probably needs a rework since i dont think you can make a custom event for making literal text.

 Content/Multiplayer_Callum/GM_Multiplayer.uasset                      | 4 ++--
 Content/PrototypeBlueprints/BPC_PlayCards.uasset                      | 4 ++--
 Content/PrototypeBlueprints/BP_Dealer.uasset                          | 4 ++--
 .../PrototypeBlueprints/BP_FirstPersonCharacter_HarryTesting.uasset   | 4 ++--
 4 files changed, 8 insertions(+), 8 deletions(-)

commit f2745568883dbc2f7158994f44a5c2228e035f32
Author: Bradley Curtis <2309516@students.ucreative.ac.uk>
Date:   Mon Mar 16 16:50:37 2026 +0000

    updates so that the server can actual read when cards are submitted

 Content/PrototypeBlueprints/BP_Dealer.uasset | 4 ++--
 1 file changed, 2 insertions(+), 2 deletions(-)

commit ddb4c0211d722729b97b4a65666a5dca94ed696a
Author: Bradley Curtis <2309516@students.ucreative.ac.uk>
Date:   Mon Mar 16 15:08:06 2026 +0000

    trying to make gameplay loop work

 Content/PrototypeBlueprints/BP_Dealer.uasset                          | 4 ++--
 .../PrototypeBlueprints/BP_FirstPersonCharacter_HarryTesting.uasset   | 4 ++--
 2 files changed, 4 insertions(+), 4 deletions(-)

commit 614448c79b03d145d3c1628d13db4e1f3fb50dc6 (origin/Multiplayer/BugFixes&TurnOrder)
Author: Bradley Curtis <2309516@students.ucreative.ac.uk>
Date:   Fri Mar 13 15:12:52 2026 +0000

    Multiplayer updates.

    Both players visible on eachothers screens. Main issue is that client player cant see their cards

 Config/DefaultEngine.ini                           |    4 +-
 .../Level_Blockout_DylanM/DM_Final_Blockout.umap   |    4 +-
 Content/Multiplayer_Callum/GM_Multiplayer.uasset   |    4 +-
 Content/Multiplayer_Callum/PC_MainInstance.uasset  |    4 +-
 .../BPC_CheckAuditWinner.uasset                    |    4 +-
 Content/PrototypeBlueprints/BP_CardBase.uasset     |    4 +-
 Content/PrototypeBlueprints/BP_Dealer.uasset       |    4 +-
 .../BP_FirstPersonCharacter_HarryTesting.uasset    |    4 +-
 Content/PrototypeBlueprints/BP_Hand.uasset         |    4 +-
 Content/PrototypeBlueprints/GM_Prototype.uasset    |    4 +-
 Saved/Logs/Greedy_Piggies_2.log                    | 9663 ++++++++++++++++----
 11 files changed, 8140 insertions(+), 1563 deletions(-)

commit 024ecd1ad441bbc0d0f05382c7d6172c1ce3f258 (origin/merge/shopintoworking)
Author: Bradley Curtis <2309516@students.ucreative.ac.uk>
