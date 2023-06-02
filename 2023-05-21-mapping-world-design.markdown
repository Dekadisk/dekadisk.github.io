---
layout: post
title:  "World Design, level design, scripting, and more"
date:   2023-05-21 12:00:01 -0300
categories: "video_games"
img: Thumbnail_UE.png
weight: 99
---
<style>body {text-align: justify}</style>
_Please note that this text is available only in English. I am french, though, so some untranslated words might be on some of my drawings._

_This page also features a lot of images (including GIFs), **which might take some time to load**, depending on your connection._

**If you've received a link to this website as a part of my motivation letter, please keep in mind that my resume is available on [LinkedIn](https://www.linkedin.com/in/julien-leonard/). Some projects are not referenced there though, but can be found on this website by clicking the purple "DEKADISK" above. Thank you!**

# Introduction

This document is divided into three parts: the first one details the design of a game map (with level design, blocking, AI scripting), while the second one presents a game made in LUA (used for scripting). The third one presents TTRPG creations related to world design.

## Designing a map
### Introduction

My objective here was to create a map that could form one of the levels of an immersive sim game (involving several paths to reach the objective, and involving stealth, parkour, etc.). This project features level design (with blocking, mainly) and AI scripting in Unreal Engine 5 (for more AI-related stuff, please read [this article](https://dekadisk.gitlab.io/video_games/2021/06/01/prisonniersdessonges-trailer.html), on this very website, which presents one of my academic projects). I chose to use Unreal Engine 5 as it is one of the two game engines I'm the most familiar with - the other being Unity.

### Results first

<iframe width="560" height="315" src="https://www.youtube.com/embed/E72-AQVyEOI" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Reference Material

I started this project by looking for pictures which could act as sources of inspiration. I knew I wanted my map to be Morocco-themed, but I needed architectural references. One of the main examples of Morocco-themed games is the Dust 2 map from Counter-Strike, that I kept in mind for the whole process. Of course, I also looked at some cities of Morocco for inspiration - mainly Fez.

<img style="float: center;" src="https://dekadisk.gitlab.io/assets/References.png">

### Drafts: paper time and story

I started by drawing a few parts of the map, then the whole level, taking into account what I wanted the player to feel. I wanted this map to be a barricaded part of a bigger Morrocan city: as such, it can perfectly be a part of a bigger open world (for example, in an Assassin's Creed-like game), or stand on its own (in a Dishonored-like game). By barricading it, I also wanted to make this level much more stressful for the players who cannot flee, as they are trapped in their enemies' territory.

I went back to my sheets of paper a few times before settling on a layout that I liked. The map underwent significant changes from the initial draft to its final design. Initially, it featured two parallel roads — a main one that remained in the final version, along with a back alley on its right. However, I later opted to include several closed shops and stalls in the map to portray the entire district as being under lockdown. These elements are situated in a small square (visible in the sketches below), which replaced the back alley. 

As I contemplated the notion of a locked-down district, I devised a brief and straightforward backstory for the villain who resides there: he serves as the leader of a militia that governs this barricaded area and its inhabitants. For this level, the player character has infiltrated this barricaded district and must take down the leader, in his house. Once the leader is dead, a cutscene would then show the player escaping via a door in his hous, thanks to key carried by the leader.


_(Click the pictures to see bigger versions!)_

[<img width="50%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/MappingMap.jpg">](https://dekadisk.gitlab.io/assets/MappingMap.jpg)
[<img width="50%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/MappingSquare.jpg">](https://dekadisk.gitlab.io/assets/MappingSquare.jpg)
[<img width="50%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/MappingObjectiveInView.jpg">](https://dekadisk.gitlab.io/assets/MappingObjectiveInView.jpg)

I wanted the player to see where their goal - the head of the milicia - was as soon as they spawned. The target's house is located on a hill, heavily guarded, and emanates an ominous presence. With its size and its many archs, it looks like no other.

### Blocking and iterating

Note that I used the "White Box" philosophy while creating this map, starting from simple geometric shapes, and then only adding details - for example, windows, bins, etc. I didn't detail most of the inacessible buildings: those only act as landscape.
While I did use some external meshes for some elements (street lights, fountains, cars), most of the blocking was made using Unreal Engine's BSP (which were later converted to static meshes), and its modeling tools, introduced in Unreal Engine 5. Those are perfect for level designing, allowing elements to be modified in-engine!
To make the blocking clearer, I used Unreal Engine materials from Quixel.
[<img width="80%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.github.io/assets/SC.png">](https://dekadisk.github.io/assets/SC.png)
[<img width="80%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/UEMAP.png">](https://dekadisk.gitlab.io/assets/UEMAP.png)
![](https://dekadisk.gitlab.io/assets/ExploreMap.mp4)

As said earlier, I changed the layout a few times, including in this phase. For example, the locked doors (from area B to C and the one in the target's house) were added in the latest iterations.

[<img width="50%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.github.io/assets/RedDoor.png">](https://dekadisk.gitlab.io/github/RedDoor.png)

### Details 

[<img width="80%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/UEMAP_1.png">](https://dekadisk.gitlab.io/assets/UEMAP_1.png)
[<img width="80%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/Infos.png">](https://dekadisk.gitlab.io/assets/Infos.png)
Three paths are available for the players: __rushing through the main gate__ is possible, but will lead to the spawn of more enemies in area C, who will rush towards the player. The latter can also decide to __go to point 2__. Going there trigger the __apparition of an enemy carrying a box, who opens a door__ - this is used to __show the player__ that some doors (with padlocks on them) can be opened. Searching the area, the player can discover that one of the enemies is __carrying a key__. Taking it by getting close (or by looting the enemy's corpse) makes the player able to use a safe path in a building, which leads to the __area C__. However, point 2.a shows that while opening the door is possible, the player can also decide to climb the building to reach a vantage point in the next area (see the "Rewarding vantage point" part below). Shooting in area B also lead to the apparition of more enemies.

The target is on the first floor of the biggest building in area C (4). It can be reached thanks to some parkour on the right, or from the ground on the left, which is more risky because of the guards. Once killed, the target can be looted, giving the player a key that can be used to escape through a door in the enemy's house (visible under the stairs in the showcase video).


### Level design techniques

#### Rewarding vantage point

[<img width="80%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/IA_PatrolPointOfView.gif">](https://dekadisk.gitlab.io/assets/IA_PatrolPointOfView.gif)
[<img width="80%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/POV.png">](https://dekadisk.gitlab.io/assets/POV.png)

The player can enter some areas from an elevated position, helping him/her assess the situation (see where the enemies are). These elevated positions act as rewards: they're not hidden, but aren't on the main path.

#### Framing, contrast and colors

As said earlier, the target is in a house visible from the start: the player's eyes are guided by the street and buildings towards the objective. Its material (from Quixel, available in UE5), darker than the other houses', also grab the player's attention - and from the very beginning, it can be seen that one of the windows of this house is open, making the player think about how to get there.

[<img width="80%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/Funnel.png">](https://dekadisk.gitlab.io/assets/Funnel.png)

Colors and contrast are also used to highlight useful parts of the environnement - to show a path to the bad guy's house's second floor, for example!

[<img width="80%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/Parkour.png">](https://dekadisk.gitlab.io/assets/Parkour.png)
<iframe width="560" height="315" src="https://www.youtube.com/embed/Nh-UYfGHvVY" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

#### Showing where the player can go organically and giving them choices

[<img width="50%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/IA_DoorEnemy.gif">](https://dekadisk.gitlab.io/assets/IA_DoorEnemy.gif)

As said before, going to area B triggers the __apparition of an enemy carrying a box, who opens a door__ - this is used to __show the player__ that some doors (with padlocks on them) can be opened. This whole area can be move through in several ways : stealthily (behind stalls), with parkours (on top of the archways), or in a more brutal way, which will lead to new enemies coming from behind the locked door.

[<img width="50%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/Info2.png">](https://dekadisk.gitlab.io/assets/Info2.png)

### Scripting : doors

[<img width="50%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/OpenDoor.gif">](https://dekadisk.gitlab.io/assets/OpenDoor.gif)
Padlocks can only be opened by specific keys ; the door allowing the player to escape can only be unlocked with the red key carried by the target.

### AI Scripting : patrols and behaviour trees

I created a patrol system, allowing me to set paths for my characters using "Patrol nodes". This helps make the world more dynamic and therefore alive, but also make the enemies much more threatening! Moreover, making the enemies move make them easier to notice for the players (especially on the villain's house's balcony)! My patrol system uses Unreal Engine 5's behaviour trees.

[<img width="80%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/IA_Patrol.gif">](https://dekadisk.gitlab.io/assets/IA_Patrol.gif)
[<img width="80%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/IA_PatrolBox.gif">](https://dekadisk.gitlab.io/assets/IA_PatrolBox.gif)
_This brown thing on this GIF is supposed to be the back of a car!_

I also added the possibility to link tasks to "Patrol nodes", as seen in the previous GIF. Thanks to this, some guards can now pick up crates and drop them somewhere else.

[<img width="80%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/Renfocement.gif">](https://dekadisk.gitlab.io/assets/Renfocement.gif)

After a few shots, more enemies are spawned in two areas of the map - depending on the location of the player. Indeed, shooting at enemies while in area B will make enemies appear from behind the locked door. Otherwise, the appear in front of a door in area C - meaning that a player rushing through the main gates will first have to fight a wave of enemies.


### Conclusion

Of course, this map is far from finished, as no asset is finished - but that's the point of the blocking phase! However, with a bit more time, I would probably make this map a night-time level ; this would require the guard to have torchlights, which would make them more visible, aiding players in comprehending the enemies' field of vision through the illumination cones. Moreover, I would expand the overall size of the map slightly, adding one or two escape roads that would replace the locked door in the villain's house.

## Using LUA to create games

While I used Blueprints to script behaviours in the previous map in UE5, I can also use scripting languages such as LUA. Here are two games made in LUA, using the Love2D game engine, to showcase this. The first one is a very simple shoot-em-up, while the other one is a platformer.

[<img width="50%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/Shmup_LUA.gif">](https://dekadisk.gitlab.io/assets/Shmup_LUA.gif)
[<img width="80%" style="display:block; margin-left:auto; margin-right:auto" src="https://dekadisk.gitlab.io/assets/LUAGame2.gif">](https://dekadisk.gitlab.io/assets/LUAGame2.gif)

I also know C++, C#, C, Java, Python (and a few others). Please have a look at my resume or the rest of this website to see my academic projects using these programming languages!

## World design in TTRPGS

As you may know if you've already looked at the rest of this website, I'm a fan of TTRPGS, such as Call of Cthulhu or Dungeons & Dragons. However, if I am sometimes a player, I am a Game Master much more often! Which is great, as I love creating and designing worlds for my players. I'm currently mastering a homebrew D&D 5th edition campaign - which is to say, I created all of it! I'm currently writing a short campaign book, but here is a PDF showing a part of it (description of a district : its history and a few Non-Playable Characters).

<embed src="https://dekadisk.gitlab.io/assets/Intrigues_Coldcoast_Rats_EN.pdf" type="application/pdf" style="min-height:100vh;width:100%"/>

