---
ns: GRAPHICS
apiset: client
---
## CREATE_CHECKPOINT

```c
// 0x0134F0835AB6BFCB 0xF541B690
int CREATE_CHECKPOINT(int type, float posX1, float posY1, float posZ1, float posX2, float posY2, float posZ2, float radius, int red, int green, int blue, int alpha, int reserved);
```

```
Creates a checkpoint. Returns the handle of the checkpoint.
20/03/17 : Attention, checkpoints are already handled by the game itself, so you must not loop it like markers.

Parameters:
* type - The type of checkpoint to create. See below for a list of checkpoint types.
* pos1 - The position of the checkpoint.
* pos2 - The position of the next checkpoint to point to.
* radius - The radius of the checkpoint.
* color - The color of the checkpoint.
* reserved - Special parameter, see below for details. Usually set to 0 in the scripts.

Checkpoint types:
0-4---------- Cylinder: 1 arrow, 2 arrow, 3 arrows, CycleArrow, Checker
5-9---------- Cylinder: 1 arrow, 2 arrow, 3 arrows, CycleArrow, Checker (Z is on ground)
10-14-------- Ring: 1 arrow, 2 arrow, 3 arrows, CycleArrow, Checker
15-19-------- 1 arrow, 2 arrow, 3 arrows, CycleArrow, Checker      
20-24-------- Cylinder: 1 arrow, 2 arrow, 3 arrows, CycleArrow, Checker 
25-29-------- Cylinder: 1 arrow, 2 arrow, 3 arrows, CycleArrow, Checker    
30-34-------- Cylinder: 1 arrow, 2 arrow, 3 arrows, CycleArrow, Checker 
35-38-------- Ring: Airplane Up, Left, Right, UpsideDown
39----------- none
40----------- Ring: just a ring
41----------- none
42-44-------- Cylinder w/ number (uses 'reserved' parameter)
* changing reserved value:
	- 0-99 numbers
	- 100-109 arrow + number
	- 110-119 double arrow + number
	- 120-129 triple arrow + number
	- 130-139 ground big circle + number
	- 140-149 cycle + number
	- 150-159 ground slim circle + number
	- 160-169 ground circle with arrow + number
	- 170-179 ground circle with spaces + number
	- 180-189 world sphere + number
	- 190-199 dollar
	- 200-209 lines
	- 210-219 wolf
	- 220-229 ?
	- 230-239 plane
	- 240-249 helicopter
	- 250-255 boat
* restart at 256
45-47-------- Cylinder no arrow or number
48-51-------- none
52----------- ring with dollar inside
53----------- ring with wolf inside
54----------- ring with ? inside
55----------- ring with plane inside
56----------- ring with helicopter inside
57----------- ring with boat inside
58----------- ring with car inside
59----------- ring with motorbike inside
60----------- ring with bike inside
61----------- ring with truck inside
62----------- ring with parachute inside
63----------- ring with jetpack inside
64----------- ring with hurricane? inside 
```

## Examples
```lua
local checkpointId = CreateCheckpoint(markerType, pos1.x, pos1.y, pos1.z, pos2.x, pos2.y, pos2.z, radius, r, g, b, alpha, (reserved or 0)) -- this creates a marker
CreateThread(function()
  while true do
    local diff = (vec(pos2.x, pos2.y, pos2.z) - vec(pos1.x, pos1.y, pos1.z))
    if Vdist2(GetEntityCoords(PlayerPedId()), vec(pos1.x-diff.x, pos1.y-diff.y, pos1.z-diff.z)) <= radius then -- this gets the center of the marker
        -- stuff when inside the marker
    end
    Wait(0)
  end
end)
DeleteCheckpoint(checkpointId) -- this removes the marker
```

## Parameters
* **type**: 
* **posX1**: 
* **posY1**: 
* **posZ1**: 
* **posX2**: 
* **posY2**: 
* **posZ2**: 
* **radius**: 
* **red**: 
* **green**: 
* **blue**: 
* **alpha**: 
* **reserved**: 

## Return value
