# SMTracker

![smtracker](https://user-images.githubusercontent.com/7599538/40287366-e061480a-5c7a-11e8-87af-d3e78f321de6.png)

SMtracker is a simple tracker for Super Metroid, suitable for Metroid Randomizer or 100% playthroughs. It was created with the intent of being used with an ALTTP tracker for playing ALTTP + SM Randomizer.

This is a very quick and fast job made in Scirra Construct Classic. As such it'd almost impossible to make meaningful pull requests, though you can either send me a modified cap or just a screenshot of the changes if they're simple enough.

## Configuration/Logic

Items.cfg defines the location and requirements for all the item pips on the map. Lets use this as an example.

***[brinstar-mockball-missiles2]
X=104
Y=211
1=10,CanOpenRedDoors,CanDestroyBombWalls,SpeedBooster,CanBomb
2=9,CanOpenRedDoors,CanDestroyBombWalls,CanBomb***

**[brinstar-mockball-missiles2]** is an arbitrary name tag that can be anything. I tried to name item locations in a way that was as understandable as possible but it's still a challenge. This can be changed without consequence as long as names are different.

**X** and **Y** are of course the x and y coordinates. You can change these, but unless the tracker starts allowing custom maps, there is no reason to do so.

**1**, **2**, **3** represent attempts at determining the clearability of an item. They don't have to be numeric -- they go in order --  but they have to be different and after **X** and **Y**. Lets look at the individual lines.

**10**,**CanOpenRedDoors**,**CanDestroyBombWalls**,**SpeedBooster**,**CanBomb**

So **10** in this represents the obtainability rating. 10 gives a nice green box to tell the player they can get the item. The rest of the line is requirements. ALL of these must be true for the rating to take effect. 

**SpeedBooster** is an item check. It checks to see if an item is collected by the player. These item names are hardcoded.

**CanOpenRedDoors,CanDestroyBombWalls,CanBomb** are all meta tags -- combinations of items and boss requirements that are defined in **meta.cfg**.

The following line is a 9. Right now this currently defines 'glitches' or exploit. In this case it's saying "Hey, if you can do a mockball you can get this". These are marked as yellow for players. This number doesn't have to go down either. You can (and often need to) have multiple **10** obtainability ratings to define when an item can be awared (though meta tags help keep this down). You can define an arbitrary amount of obtainability definitions. It's best to go from highest to lowest, as the engine won't even bother checking definitions if the rating is lower than one that has already come back as true.

meta.cfg works similarly but slightly differently. For example

**[CanGrapple]
data=GrappleBeam,SpaceJump**

The **[CanGrapple]** is the name you would like to use to reference this tag. It can be anything, but keeping it clear and readable is important.

**data** works slightly differently. Instead of having *1=*, *2=1* and *3=1*, different definitions are broken up with a **|**, functioning as an *or* statement. Why is this different? It was easier and I'm lazy. Anyways, CanGrapple is used to cover any situation where a Grappling Hook or Space Jump can solve a problem. Since this is a common case, it got a meta tag. In situations like the Maridia Springball item entrance, you would use the item name **GrappleBeam** instead.

Metatags can reference each other, like in this example...

**[CanDefeatBotwoon]
Data=CanAccessInnerMaridia,IceBeam|CanAccessInnerMaridia,SpeedBooster**

This allows definitions to be a lot cleaner and shorter. New meta tags can be defined arbitrarily. I based mine off the SM Randomizer's code but added more of my own.


##Item List

**Nothing,ChargeBeam,IceBeam,WaveBeam,Spazer,Plasma,VariaSuit,GravitySuit,MorphBall,Bombs,SpringBall,ScrewAttack,HiJumpBoots,SpaceJump,Missiles,SuperMissiles,PowerBombs,GrappleBeam,XRay,BeatKraid,BeatPhantoon,BeatDraygon,BeatRidley**

While some of these are not items, they're treated as such intentionally.
