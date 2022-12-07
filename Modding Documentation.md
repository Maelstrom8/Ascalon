
I will cover a lot of things involving how to mod the game, how mods interact, what the effects are, and other things. It will be a bit long so get a drink or something.

## Dragon's Dogma & Mod Organizer 2

Dragon's Dogma: Dark Arisen is not like other games, especially when managed through Mod Organizer 2. The game data is in the form of archives (.arc files) that need to be unpacked, edited and then repacked.

Mod Organizer 2 can actually manage the game fairly well, and the mods for DD:DA are split into two groups, which is honestly just overwriting arc file(s)

1) Mods that start with a directory of /rom/ which will overwrite smaller arcs 
2) The "mod" or what I call the output, which is a directory of /rom/ and contain a lot the main game files such as game_main.arc, title.arc, bbs_rpg.arc etc

## Archive Files, Mods and You

You will see a lot of outfit and armor texture mods that are enabled. They overwrite smaller individual .arc files, they are typically textures or other things. These mods work as intended when enabled.

And then we have the ARCTool Output. This consists of these main archives: bbs_rpg.arc, bbsrpg_core.arc, game_main.arc and title.arc. It is essentially where the rest of the mods get merged into. Here is some examples of what is currently inside these, and which one represents in terms of what they do or contain typically.

- 10th Anniversary Loading Screen is located under bbs_rpg.arc and bbsrpg_core.arc. Advanced: `bbs_rpg\id\DDN\load\load01_ID.tex' & 'bbsrpg_core\id\DDN\load\load01_ID.tex`
- Easy Clothing ID with HD Icons is located under game_main.arc. Advanced: `game_main\dl1\id\common\item\combinedItemIcon_ID.tex`
- Cleaner Female/Male Body Textures is located under game_main.arc and title.arc. Advanced: `game_main\models\` & `title\models\` (there are too many to list)

**Some of the "enabled" mods do not do anything in Mod Organizer 2 if they are purely in loose form, as in they are an archive file unpacked - they are already merged, please don't touch any of them unless you know what you are doing**

### A Deeper Look Into Archives

Here are some examples of what is possible to edit when unpacking some of these archives. The archive file "game_main.arc" contains the following from my knowledge:

- Modifying Item Icons - `game_main\dl1\id\common\item\combinedItemIcon_ID.tex & .dds` - PAWN SAFE
- Modifying Quest Rewards - `game_main\etc\questReward\questReward.qr (.xml)` - PAWN SAFE
- Modifying Augment Effects - `game_main\param\pl\other\PlAbilityParam.ablparam (.xml)` - THIS INVALIDATES PAWNS WHEN THEIR STATUE IS SET TO ONLINE
- Modifying DP Cost for Vocation Ranks - `game_main\param\pl\JobLevel\JobLvFighter.joblvl (.xml)` - There are nine of these, this is for Fighter. THIS MAY INVALIDATE A PAWN.
- Modifying Jump Height - `game_main\param\pl\other\PIJumpParam.ablparam (.xml)` - AFFECTS PAWNS BUT UNTESTED IN AN ONLINE SENSE
- Modifying Carry Weight - `game_main\param\pl\weight\manyfileshere.plw` - AFFECTS PAWNS BUT UNTESTED IN AN ONLINE SENSE
- Modifying Stamina Drain While Sprinting - `game_main\param\pl\stamina\PlStaminaDash.stm & PLSDAssassin.stm (.xml)` - DOESN'T AFFECT PAWNS BECAUSE THEY DON'T USE STAMINA WHILE RUNNING
- Modifying Experience Rate - `game_main\param\pl\level\exp.plexp (.xml)` - THIS IS COMPLICATED TO EXPLAIN, NOT RECOMMENDED CHANGING
- Modifying Weal and Prosperity - `game_main\param\status\player.statusparam (.xml)` - LINES 289 AND 297, DEFAULT 300 (5 MINUTES)
- Modifying Stat Growth for Vocations - `game_main_param\pl\pl\level\LvFighter.lvl (.xml)` - There are nine of these, this is for Fighter. THESE INVALIDATES PAWNS IF YOU CHANGE STATE GROWTH FOR ANY OF THE 6 VOCATIONS THEY SHARE WITH THE PLAYER

I'm dead now from all that.

## Adding Mods to Ascalon

At this moment, I included a folder called `Modding Templates` it contains *some* of the mods above, but in different versions - in loose file form. I will teach you how to apply one of these to your game, but before that.. Go to your modlist directory, under `/tools` is a file called "ARCTool (Simplified).rar" - extract this to any folder, this is where you will *unpack* and *repack* archive files - you will see several bat files and your two main bat files, XFS_Extract & XFS_Repack.

### Adding Mods to Ascalon cont.

Let's say that you hate sprinting costing Stamina, and you want it infinite. Head to `Modding Templates` and find the folder `Stamina Drain While Sprinting` - pick the last folder labelled `Sprinting no longer costs Stamina`. Keep this explorer window active, but go to your ARCTool Output, find the **game_main.arc** file, copy it. Paste it into your folder you created for the ARCTool file and the other bat files. Double-click XFS_Extract, it should create a folder called game_main, a log folder, and another file for game_main responsible for telling itself how it's structured.

Go to the other explorer window for the `Sprinting no longer costs Stamina`, open it until you see **game_main** in folder form, copy this folder, paste it into the one you unpacked. It should overwrite the param files for Sprinting. Now double-click XFS_Repack. Wait. Take the newly created game_main.arc and replace it with the one in the output, done. 

## Warnings - Mods & Pawns

I will cover which mods are safe for pawns, and which ones are not + which ones I am unsure about. In Dragon's Dogma, you can create companions called pawns, and you can share them online, where other people can rent them out and use them - which can benefit you the player as pawns have many mechanics to them. Most mods will affect pawns as they do you, because they use some of the same vocations, skills and systems. 

Any modifications done to a pawn that is considered "not-achievable" by legitimate means will result in a pawn being invalidated or basically, the pawn will show up as corrupt data and cannot be hired. You must start a new game to get around this.

- Changing Augments (eg Vigilance 100HP > 300HP) will invalidate your pawn
- Changing the Stat Growth of the six default vocations will invalidate your pawn
- Changing or giving max Knowledge will invalidate a pawn
- Changing the cost of Augments has not been confirmed
- Changing the DP cost for Vocation Ranks has not been confirmed
- Changing Carry Weight / Jump Height / Stamina Drain does not seem to put your pawn in danger
- Changing Quest Rewards does not affect pawns in any way
- Using dinput8.dll could possibly invalidate your pawn

Invalidation of a pawn is only caused if you are playing with *these* mods and have your pawn-sharing-status set to Online. How the detection roughly works is that if you are not using a list, and are using for example.. an Augment tweak mod, it is totally fine client-side. The augments only change on your end, but once you send the pawn back, no mods are going through the server.

NOW - Here's the funny thing. You are not safe to use these mods if someone hiring your pawn also has the mod. To explain further on that, if I decided to make tweaks to the Augments, and release it in a list, for those who are wanting to share your pawns with others using the list - it is a game of how long until someone else using the list finds your pawn and immediately gets it corrupted!

If you're using dangerous mods, just set to pawn to private! This should cover everything but don't be afraid to ask questions.