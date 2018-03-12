# Destruction
Destruction Game Mode for Squad
Gameplay: Teams fighting over objectives, where one team need to destroy weapon caches, and other need to protect them.
Game consist of multiple phases, with 2 objectives in each phase.

-----------------------------------------------------------------------------------------------------
##### Content description

* Content/Deployables - Custom versions of FOBs and Ammocrates blueprints, needed for technical reasons.
* Content/Gameplay - Gameplay specific actor classes
* Content/Layers - Layers for maps
* Content/Teams - Custom Teams Info blueprints
* Content/UI - Custom versions of radial menu, needed to use custom versions of FOBs and Ammocrates

-----------------------------------------------------------------------------------------------------

##### Gameplay specific classes 

* /Content/Gameplay
  * BP_GameMode_Destruction - game mode blueprint, that makes use of default rulesets for scoring, as well as BP_Destruction_Ruleset 
  * BP_Destruction_Ruleset - game defining class. Makes the work of initializing game mode logic actor, adjusting tickets, showing rules to joined players and handles match ending conditions
  * BP_Destruction_PhaseDirector - contains all top-level game mode logic. such as : managing phases, activating new objectives, checking current active objectives, and generating events for other actors and game mode.
  * BP_Destruction_ObjectiveArea - class that represents single objective. contains logic for randomizing cache position.
  * BP_Destruction_TempSpawn - class for temporary spawn, that activates on certain phase. Relies on Phase Director.
  * BP_NoDeployZone_Custom - custom version of NoDeployZone, that restricts placement of FOBs in it.Can only restrict placement of custom FOBs, located in Deployables folder. Removes itself on certain phase.
  * BP_Destruction_AttackMarker - class of interactive attack marker, that disappears upon enemy player getting close.
  * DestructionPhase - structure that defines which objectives belong to which phase. Used by PhaseDirector.

* /Content/Gameplay/Caches - contains blueprints of weapon caches
  * BP_DestructionCache - base version of weapon cache, uses Russian-specific model.
  * BP_DestructionCache_MIL - Militia version of weapon cache
  * BP_DestructionCache_US - US version of weapon cache

* Content/Gameplay/MapPaint - contains classes responsible for painting objective areas on the map
  * BP_DrawedSpline - actor that have a spline component, that defines the shape that should be painted on map
  * BP_MapPainter_V2 - actor that responsible for painting DrawedSplines on the map
