CHATPILOT
===============================

INSTALL
-------
1. Copy chatpilot-1.2.1.jar to your .minecraft/mods folder.
2. Make sure these mods are also in mods/:
     - Fabric API (matching 1.21.4 build)
     - Baritone API Fabric 1.13.1 (the libs/ jar in this zip is built and
       linked at compile time; if you want runtime Baritone you also need
       baritone-fabric on the client. The Baritone jar that the client
       runs is whatever you already had working in v1.1.0; nothing changed
       there.)
3. Launch Minecraft 1.21.4 with Fabric.
4. Look for "chatpilot 1.2.1" in the in-game mods list.

CONFIG NEW KEYS
---------------
config/chatpilot/config.json gets these on first run after the upgrade:

  miningOreQuotaEmerald: 4
  miningOreQuotaGold:    8
  miningOreQuotaCoal:    16

  beehiveAvoidanceRadius: 6

  fishingCatchTarget:        8
  fishingWaterScanRadius:    16
  fishingMaxWaitTicks:       600       (30 seconds, recast on timeout)
  fishingSettleTicks:        14
  fishingBiteVelocityY:      -0.04     (more negative = stricter bite)

  trashItemIds:  [the default trash list, editable]

Old keys miningOreQuotaCopper / miningOreQuotaLapis / miningOreQuotaIron
and woodLogQuota are still parsed for backward compat but unused.

GOTCHAS
-------
* The fishing bobber uses the FishingBobberEntity exposed by the player.
  Catch detection is "bobber Y velocity dipped below threshold". Vanilla
  bobbers occasionally bob naturally; the threshold is set conservatively
  (-0.04) plus a 30-tick guard window after each cast to avoid false
  positives from the cast settling. Real catches blow past -0.1 easily.

* The cactus drop step uses SlotActionType.THROW with button=1 (whole
  stack) on the player's own screen handler. No GUI is opened. Item
  entities spawn forward of the player in the look direction with a small
  random spread, so aiming AT the cactus while standing 2-3 blocks back
  reliably lands them on the cactus side or top. Items dropped onto the
  cactus get destroyed within a few seconds.

* If you re-enable wood gathering, beehive avoidance is on by default.
  No extra config needed.
