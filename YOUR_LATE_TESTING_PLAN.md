Testing Plan — YOUR\_LATE

1\. Overview  
Describe in several sentences what this document is and what it will cover  
This document describes the testing for my game concept “YOUR\_LATE\!”  
Mechanics I am testing:

1. Speed/Gravity/Player movement, Ensuring that it acts appropriately.  
2. Ability and its charges  
3. Powerups (none in particular but how they could interact with the program.

Note for game overall: YOUR\_LATE\! It is meant to be a very fast paced game heavily inspired by the game Burrito Bison with it sharing most mechanics with that game.  
\---

2\. User Stories and Acceptance Criteria  
\<Speed/Movement/gravity\>  
User Story 1: Players feel like they are flying through the air at mock 1,000 without losing track of where they are.   
\- Acceptance Criterion 1: “Falling with style”, The speed value and the players actual speed match up, player should not be faster or slower than the speed value.   
    \- Requirement(s):Players speed value and their actual movement value should reflect each other, and should feel correct.  
    \- Purpose:Players should feel like they have a level of control and feel rewarded by maintaining as well as increasing their speed.  
    \- Test Cases:Both edge and boundary test.  
        a) Feature:Speed/Movement/gravity  
        b) Test:Boundary: Set staring speed to the value you need to test and/or make a temp “enemy” that sets the speed to a value when you collide with it.(only for testing)   
        c) Expected Result / Behavior:The Speed var and the actual Speed should match, and should only be moving up or down, and to the right at all times (unless dead). With the camera following the player.  
        d) Automation Candidate: Yes and NO. Explanation:This is essentially the first mechanic that would be made so no to the first few times. But as the game progresses how speed interacts other things like powerups and alternative damage sources(traps) can me automated.

\- Acceptance Criterion 2-Player should be punished Not maintaining speed:

    \- Requirement(s):Players can lose speed and should start to lose speed naturally if they are at say 80% (120) or more of the max speed.     \- Purpose:Encourages the player to maintain their speed even if they get to max  
    \- Test Case:Bounds  
        a) Feature:Lousing speed  
        b) Test: Bounds test of max, min along with at the brake point   
        c) Expected Result / Behavior: Should only drain if above 80% max speed (you have the normal max speed 120 then the actual max speed 150\)  
        d) Automation Candidate: Yes with regression testing (As new ways of gaining speed are added.)

User Story 2:Player should be able to pick up powerups that give them an opportunity to increase their speed if they do them well.  
\- Acceptance Criterion 1; Power up active the second the player collides with it and should not brake if the player somehow gets 2 at the same time  
    \- Requirement(s):   
\#Side note player should be able to pick up a different power up wail another is in use essentially switching from on to the other unless otherwise stated.  
    \- Purpose:Powerups don’t break the flow of the game and don’t brake it.  
    \- Test Case:Edge and bounds  
        a) Feature:Getting power up  
        b) Test: Getting 2 at once along with getting them at the speed bounds.  
        c) Expected Result / Behavior: Only 1 power up is pickup at a time and speed is not broken.  
        d) Automation Candidate: No

\- Acceptance Criterion 2 Powerups   
    \- Requirement(s):Powerups do not brake speed.  
    \- Purpose: Keeping game in check  
    \- Test Case:Boundary test  
        a) Feature:Speed increasing  
        b) Test:Give power up wail at X speed.  
        c) Expected Result / Behavior:Speed is still working  
        d) Automation Candidate: Y 

User Story 3:Ability /Jump    
\- Acceptance Criterion 1   
    \- Requirement(s): Ability charges are working correctly (increasing/decreasing) and UI reflects it.  
    \- Purpose:Ability works which give player more control and reward them for timing.  
    \- Test Case: Bound and a little bit of Edge  
        a) Feature:Gaining charge  
        b) Test: Do the standard bounds test But also test what happens if they get gain 2 charges at the same time when they can only 1 away from max(Say for example the max is 5 the player has 4 and is about to gain 2 at the same time because it is at that moment 4 (ie less than 5)Game thinks it’s ok to increase by 1\)  
        c) Expected Result / Behavior:Never goes above max or below min 0\.  
        d) Automation Candidate: No

\- Acceptance Criterion 2   
    \- Requirement(s):When player uses (or tries to use) ability it should use it and louse 1 charge unless it has no charges.  
    \- Purpose:Ability works as intended   
    \- Setup:Ability thing/code  
    \- Test Case: Bounds and edge  
        a) Feature:Using ability  
        b) Test:Bounds charge is spent correctly. Edge: Using an ability at the same time you gain a charge (especially if you have 1 or 0\)  
        c) Expected Result / Behavior:Only uses 1 charge and only when you have a charge.  
        d) Automation Candidate: Y you need to use a tool (Assuming you don’t want to go crazy trying to time things.) Func calls

\---

3\. Boundary and Edge Testing

Boundary / Edge 1:    
    \- Requirement(s):Speed does not result in Possible bugged output.  
    \- Purpose:Make sure that speed is working

| input | Test Data | Expected output. | Possible bugged output |  Automation Candidate: |
| ----- | ----- | ----- | ----- | :---- |
| \-1 | Have the player get hit with something that would make them lose speed while their speed is 0\. Or the amount they lose is greater than the max. | Speed should be set to 0 and the player (character) dies. | The player starts to move the opposite direction Or underflow | Y:Use a tool to set the speed manually.  |
| 0 | Create a temp entity that sets the speed to 0\. | DEATH\! And the player character should stop moving | The player keeps moving or the die func does not run. | Y:Use a tool to set the speed manually.  |
| 100 | Launching player | Player moves at that speed | I am not sure. | Y:Use a tool to set the speed manually.  |
| 150 | Set launch value to 150 or Create a temp entity that sets the speed to 150 | Player moves at that speed no grater | Going to fast, overflow | Y:Use a tool to set the speed manually.  |
| 151 | Have the player get hit with something that would make them gain speed while their speed is 150\. Or the amount they gain is greater than the max. | Speed stays/ is set to 150 | Overflow/unexpected death or gaining infinite speed. | Y:Use a tool to set the speed manually.  |

Boundary / Edge 2: Abbily and charges   
    \- Requirement(s):   
    \- Purpose:     

| input | Test Data | Expected output. | Possible bugged output | Audimate |
| ----- | ----- | ----- | ----- | ----- |
| \-1 | Have the player get hit with something that would make them lose charge at 0 charges. | Charges are set to 0 | Infinite uses, underflow, or crash. | Y with func tool |
| 0 | Have this be the starting value 1.Add 1 or more chargers through entity happens normally 2\. Attempt to use at 0 3\. Try to subtract charge wail at 0 say there is a trap that decreases your charges | Unable to use charges | Going negative, crashes ext | Y with func tool |
| 5 | Set are starting charges amount Repeat steps from 0 | Safely use charges not be able to gain more. | Exceeding max. | Y with func tool |
| 6 | entity that would give more than 1 charge or another meaning of getting 2 at the same time. | Set charges to 5 | Overflow | Y with func tool |
| Edge: Gaining multiple at the same time | Collect 2 or more at the same time (item that add a charge stack 2 on top of eachother.) | Does not go over 5 | Overflow/ having to many charges | N manual test. |

Boundary / Edge 3:    
    \- Requirement(s):Powerups don’t brake previous established rules  
    \- Purpose:Powerups are fun to use and don’t brake the game

    \- Test Case 1:

| input | Test Data | Expected output. | Possible bugged output |
| ----- | ----- | ----- | ----- |
| \-1 | Using a tool then to set speed and give powerup. (func call) | Unable to pick up powerup | The player starts to move the opposite direction Or underflow Unexpected revive/zombie apocalypse or crash. |
| 0 | Using a tool then to set speed and give powerup. (func call) | DEATH\! And the player character should stop moving and Unable to pick up powerup | Unexpected revive/zombie apocalypse or crash |
| 100 | Using a tool then to set speed and give powerup. (func call) | Powerup acts as normal | I am not sure. |
| 150 | Using a tool then to set speed and give powerup. (func call) | Powerup doesn't further increase speed. | Going to fast, overflow, powerup not working |
| 151 | Using a tool then to set speed and give powerup. (func call) | Speed stays/ is set to 150 and Powerup doesn't further increase speed. | Overflow/unexpected death or gaining infinite speed. |

        d) Automation Candidate: Y use a tool to control speed.

    \- Test Case 2: Edge  
        a) input: Gaining 2 powerups at the same time.  
        c) Expected Result / Behavior: Only one is activated/used.  
        d) Automation Candidate: N Manual test.

\---

4\. Automated Test List  
Which tests were candidates for Automation?    
Basic value increases to speed charges. However strange logic/edge cases like gaining 2 or powerups at the same time.

