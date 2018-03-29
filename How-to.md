#### Placing game mode specific actors

1. Place BP_Destruction_ObjectiveArea actors in general location of objectives. 
2. Place BP_NoDeployZone_Custom actors around objective areas. You should not place them around phase 1 objectives.
3. Place BP_MapPainter_V2 actor in the world. 
4. Place BP_DrawedSpline actors for each objective and NoDeployZone. 
5. Place BP_Destruction_TempSpawn actors where you want the defenders to spawn between phases.
6. Place a BP_PhaseDirector anywhere in the world.

#### World Setting setup
1. Set the game mode to BP_GameMode_Destruction
2. Set the attackers team to gamemode-specific version (Currently there is only US faction supported as attackers, so use BP_TeamInfo_D_USA)
3. Place gamemode-specific version of ammocrates at the main bases (Currently only US team supported, so use BP_US_Ammocrate_D) 
4. Set tickets amount for each team. Recommended values are 350 for attackers and 1000 for defenders.

#### Objectives setup 
1. Set up each ObjectiveArea actor. Things you will need to change: 
"Ticket adjustment by Opposing Team upon objective being met" - This is how much tickets attackers will gain upon cache destruction on this objective. 
Recommended values: 50 for Phase 1 objective, 75 for Phase 2, 100 for Phase 3. 
"Use Fake Markers" - if this is set to True, objective will use discoverable cache locations markers mechanic. If this is set to False, there will be only 1 regular marker at the position of this actor. 
"Number of spots" - number of markers to show, including the real one. Only relevant if "Use Fake Markers" is True. 
"Min Distance Between Spots" - minimal distance between the markers of possible cache spots. Only relevant if "Use Fake Markers" is True. 
You will need to tune this value based on your placement of possible cache spots. If you set it too high, there will be less than "Number of spots" cache spawns displayed on map. 
"Objective Tag" - string that identifies the cache spots to use for this objective. All cache spots actors should have same string in their "Tag" property. 
"Team" - irrelevant, it is set automatically by PhaseDirector. Just leave it as it is. 
"Objective area border" - should be set to reference the BP_DrawedSpline actor, that corresponds to that objective. 
 
2. Place BP_ObjectiveSpawnLocation (included in SDK) actors at locations, where you want possible cache spawn to be. Recommended to place at least 20 possible spots for each objective. 
Assign cache spawn locations to objectives by adding the value of "Objective Tag" property of corresponding ObjectiveArea actor to "Tag" property of spawn location actors. 
 
3. Set up the NoDeployZone actors, by: 
- setting the "Disallowed Team" to the value that corresponds to Attackers team 
- setting the "Remove on Phase" to the number of phase, at which it should be removed. You'd want this to be at least 2. 
- setting the "AreaBorder" to reference the the BP_DrawedSpline, that represents the border of this NoDeployZone on the map. 
 
4. Set up temporary spawns (BP_Destruction_TempSpawn actors) for defenders 
"Phase Number" - at which phase this spawn point should activate. 
"Activate on Phase start" - if this set to True, spawn point will be activated on phase start, otherwise it will activate on phase end. 
"Lifetime" - how long in seconds this spawn point should be active. Recommended value: 180 for spawns on Phase 1 objectives, 60 for all others. 
 
5. Set up BP_DrawedSpline actors, by: 
- changing the "Coloring" property. Recommended to use orange color for objective areas and red color for NoDeploy zones. 
- editing spline components, making their shape to be outline of corresponding area. Need to set it to be looped also.
 
6. Set up PhaseDirector, by : 
- setting "ObjectiveClass" to needed class, depending on which faction is set for defending team. Default is "BP_DestructionCache", which corresponds to Russian Armed Forces faction, and uses russian-specific cache model. 
- setting "Winning Team on Last Phase Complete" to value, corresponding to the Attackers team. 
- setting "Delay Between Phases" to how much time you want to pass, before next phase start. This affecting all phases except first one.
- assigning objectives to phases, by adding references to ObjectiveArea actors into "Phase objectives" property of each element of "Phases Setup" array. 
You can add how many objectives you want into each phase. 
Recommended to use 2 objectives per phase. 