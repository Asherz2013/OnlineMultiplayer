# Online-Examples
 Sandbox to test out Networking features

## Relevancy
 Took a door blue print and changed the different ways it can replicate over the network. This also used an INTERFACE to help with "Interactions"
  Always - As the name suggests, this is done all the time, regardless of how far the user is from the actor
  Only Relevant Owner - This will only show to the Client who instigated the action
  Net Use Owner - If we have an owner it will use their relevancy to determine who should see this happen.
  Net Cull Distance changed - Lowered the Net Cull Distance to show that once everything is setup correctly, nothing will happen until the player is within a certain range.

## Rep Notify
 Created a "Random number wall" which picks a random number every second.
  To start off with this just sent a number to the text widget, which was different for Client and Server
  Made the "Update Text" function "Run on Server", which meant that only the server would see the text update, not the clients.
  Turned the var I was using into "Rep Notify", then on the new function updated the text. This then propergates to all clients the same number as the SERVER, so stays in sync.
  
## Character Manipulation
### Sprinting
 How do we replicate that the user is Sprinting?
  Simply just updating the user Character Movemement component isn't enough, as this just updates it on the client.
  Make Custom Events which run on the server and call those. Does good, but has some stuttering on the client as the server has changed and NOT the client.
  Finally perform both of the above to get the user moving as expected.

### Animation
 Making sure Animations replicate as expected.
  Setting up the Anim Blue print alone isnt enough. We need to make certain variables Replicate.
  For instance, Jumping, will need a Bool Var, which is replicated, then used in the animation BP to dictate when to jump.
  Updated the Anim BP to have a "Blend Poses by Bool" node, to switch between Aiming and Not
  Within the Thirdperson Character. Made use of the same technic above for Sprinting to resolve Aiming and Jumping.
  
### Montages
 How to make everyone see that a user is firing a gun from a montage...
  Inital setup and making Cache Poses and using "Layered Blend per Bone" node to make sure we can show the correct animation given the correct "Slot (upperbody) was in use.
  <Update a bit more here on what I did before the below>
  Had to use a Remote Procedure Call (RPC) to then call a Multicast, which sends out the information that this user was playing a particular animation.
 
### Shooting
 How do we deal DAMAGE to a player?
  Had to make a new "Health" variable
  After pressing the "Shoot" button, we call another RPC to make sure everything runs on the Server. Don't want clients cheating now do we...
  This then fires off a line trace and if it hits somthing call the "Apply Point Damage", which is a SERVER ONLY command. We pass in the person who done the damage, how much damage, what direction did this damage come from, the Hit Info from the line trace, who did the damage.
  This then sends out a Event called "Point Damage" which we can then apply damage to the use on the server.
  
## Scoring Points


## HUD updating
