Logic points:

1. Player Speed (main mechanic the game is centered around) specifically gaining and losing speed and if pausing the game could mess with it.  
2. Using the charge ability  (player using and gaining at the same exact time.)  
3. Collision. 

1.Speed (for this example lets say max speed is 150.):

| Boundary input | Why test |
| :---- | :---- |
| \-1 | Right under the minimum and if something is not working could result in the player going backwards. |
| 0 | Minimum value should mean that player died |
| 100 | About in the middle but is also the speed the player should always start at the beginning of a run. |
| 150 | At the intended maximum speed, going beyond this could result in unintended consequences.  (Possible to have future mechanics rely on this cap, say at max speed, getting hit results in losing half of the normal speed.) |
| 151 | Right above max speed the player should not be able to get to this point. |
| Gaining/losinging speed | This is where brakes would most likely come from /originate. Needs to be tested to ensure the correct math is in play.  |

2.Charges (for example max charges is 5\)

| input | Why test |
| :---- | :---- |
| \-1 | Under the minimum if entered could allow for infinite charges or crash. |
| 0 | Is the minimum/ no charge Should not be able to use the ability if they have no charge. |
| 5 | Is the max and tested to see if it can / will go over. |
| 6 | Above max |
| Using/gaining charge | This is where brakes would most likely come from /originate. Needs to be tested to ensure the correct math is in play.  |
| Losing charge | If something other than the player drains a charge it could cause it to go under. |

3.Volume ():

| input | Why test |
| :---- | :---- |
| \-1 | Below the minimum most likely causing a runtime error or an overflow. |
| 0 | Is the min but also should result in no noise from the game  |
| 50 | Right in the middle and gives  a general test to make sure it works. |
| 100 | Max volume also should be a reasonable noise level. |
| 101 | Above max could cause an overflow error or give someone Tinnitus or another hearing problem if is able to go beyond this like 1000 or something.  |

Step 3 testing

1.Speed (for this example lets say max speed is 150.):

| Boundary input | test |
| :---- | :---- |
| \-1 | Have the player get hit with something that would make them lose speed while their speed is 0\. Or the amount they lose is greater than the max. |
| 0 | Create a temp entity that sets the speed to 0 |
| 100 | Call launch player func |
| 150 | Set launch value to 150 or Create a temp entity that sets the speed to 150 |
| 151 | Have the player get hit with something that would make them gain speed while their speed is 150\. Or the amount they gain is greater than the max. |

2.Charges (for example max charges is 5\)

| input | test |
| :---- | :---- |
| \-1 | Have the player get hit with something that would make them lose charge at 0 charges.  |
| 0 | Have this be the starting value 1.Add 1 or more chargers through entity happens normally  2\. Attempt to use at 0  3\. Try to subtract charge wail at 0 say there is a trap that decreases your charges |
| 5 | Set are starting charges amount  Repeat steps from 0 |
| 6 | entity that would give more than 1 charge or another meaning of getting 2 at the same time. |

3.Volume ():

| input | Why test |
| :---- | :---- |
| \-1 | Players mess with inputs or just make a mistake.  |
| 0 | Tries to mute game. |
| 50 | Doing a goldidy lox thing. |
| 100 | Wants the game to be loud and tries to set it to the max volume. |
| 101 | Messes up with volume adjusting, miss click ect.   |

Step 4:  
Speed

| input | Test Data | Expected output. | Possible bugged output |
| :---- | :---- | :---- | :---- |
| \-1 | Have the player get hit with something that would make them lose speed while their speed is 0\. Or the amount they lose is greater than the max. | Speed should be set to 0 and the player (character) dies. | The player starts to move the opposite direction Or underflow |
| 0 | Create a temp entity that sets the speed to 0\. | DEATH\! And the player character should stop moving | The player keeps moving or the die func does not run. |
| 100 | Launching player | Player moves at that speed | I am not sure. |
| 150 | Set launch value to 150 or Create a temp entity that sets the speed to 150 | Player moves at that speed no grater | Going to fast, overflow  |
| 151 | Have the player get hit with something that would make them gain speed while their speed is 150\. Or the amount they gain is greater than the max. | Speed stays/ is set to 150 | Overflow/unexpected death or gaining infinite speed. |

| input | Test Data | Expected output. | Possible bugged output |
| :---- | :---- | :---- | :---- |
| \-1 | Have the player get hit with something that would make them lose charge at 0 charges.  | Charges are set to 0 | Infinite uses, underflow, or crash. |
| 0 | Have this be the starting value 1.Add 1 or more chargers through entity happens normally  2\. Attempt to use at 0  3\. Try to subtract charge wail at 0 say there is a trap that decreases your charges | Unable to use charges | Going negative, crashes ext  |
| 5 | Set are starting charges amount  Repeat steps from 0 | Safely use charges not be able to gain more. | Exceeding max. |
| 6 | entity that would give more than 1 charge or another meaning of getting 2 at the same time. | Set charges to 5 | Overflow  |

volume;

| input | Test Data | Expected output. | Possible bugged output |
| :---- | :---- | :---- | :---- |
| \-1 | Players mess with inputs or just make a mistake.  | Should not happen or set to 0 | underflow, or crash. |
| 0 | Tries to mute game. | Silence  | Going negative, crashes ext  |
| 50 | Set volume to 50 | Audio played reflects set amount | Confusion,possible discomfort   |
| 100 | Set are starting charges amount  Repeat steps from 50 | Plays at max volume | Exceeding max. |
| 101 | Messes up with volume adjusting, miss click ect. | Set volume to 100 | Overflow, crash, giving the player Tinnitus  |

STEP 5 reflect;  
Which logic point feels most fragile? It’s speed it is changing the most and feels like the one most likely to have some math oversight   
What will I need to watch out for when coding this?: Adding /subtracting. Numbers that aren't guaranteed to be \+/- but one value (say increments of 1 or 10\) are the more likely to have something go wrong.

What will I need to watch out for when coding this?: To be honest ability charges I didn't really think about all of the possible braking points with that one immediately like 2 different \+1 cases at the same time.