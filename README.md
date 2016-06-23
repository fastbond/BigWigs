# BigWigs
BigWigs is a World of Warcraft AddOn to predict certain AI behaviour to improve the players performance.<br \>
This Modification is build for Patch 1.12.1 and its content for use on the <b>Classic-WoW</b> private Server.

The adjustments were originally made by LYQ.<br \>
Adjustments for Classic-WoW made by Dorann.<br \>
<b><a href="github.com/xorann/BigWigs">Please refer to this repository for more information.</a></b>

# Download
PLEASE NOTE THIS IS STILL A WORK IN PROGRESS <br>
<b><a href="https://github.com/xorann/BigWigs/releases">Download the latest Release here</a></b>

## How to install
<b>a)</b> If you choose to download the .rar file all you have to do is extract the archive in your /World of Warcraft/Interface/AddOns/ directory.<br />
<b>b)</b> If you download the raw code from GitHub (<b>Download ZIP</b>) you'll have to unzip the downloaded archive and rename the folder from 'BigWigs-master' to 'BigWigs' and place it in your /World of Warcraft/Interface/AddOns/ directory.

## Wiki
<b><a href="https://github.com/xorann/BigWigs/wiki">For more information or help please visit the Wiki</a></b>

## Included AddOns/Plugins
I've included several other BigWigs AddOns in this repository, so you only need to download and use the 'BigWigs' folder from this repository. If you happen to have any of the listed AddOns seperately I suggest removing them - in case I adjusted some of those in this repository as well.
<ul>
    <li><b>BigWigs_CommonAuras</b> <br \>  ( keeps track of certain Buffs eg. Fear Ward and Tank cooldowns )</li>
    <li><b>BigWigs_NefCount</b> <i>deactivated atm (NEEDS REWORK)</i> <br \>  ( improved mechanism for Nefarian phase 1, keeps track of the Adds killed since that triggers phase 2 )
    <li><b>BigWigs_ZombieFood</b> <i>modified</i> <br>  ( announces if a player is getting dazed )</li>
    <li><b>BigWigs_LoathebTactical</b> <br>  ( Spore and Consumable warnings for Loatheb )</li>
    <li><b>BigWigs_RespawnTimers</b> <i>(NEEDS REWORK)</i> <br>  ( Trash respawn timers )</li>
    <li><b>WarnIcon</b>  <i>own development</i> <br> ( Displays important SpellIcons in the center of your screen. Eg. if you're standing in Rain of Fire at Gehennas or if you're a Hunter and Magmadar/Flamegor/Chromaggus is Frenzied and you need to Tranq )</li>
    <li><b>BossRecords</b>  <i>own development</i> <br> ( This Plugin will keep record of your time used in bossfights and compare it to your fastest )</li>
    <li><b>AutoReply</b>  <i>own development (WORK IN PROGRESS)</i> <br> ( This Plugin will answer whispers received during BossFights )</li>
    <li><b>ReadyCheck</b>  <i>own development (WORK IN PROGRESS)</i> <br> ( This Plugin will implement the needed code for the 'ReadyCheck' button from Blizzward which is in visible in the RaidFrame. Since the missing code was related to missing AddOn communication this Plugin will only work for RaidMembers with one of LYQs BigWigs Version )</li>
    <li><b>RaidOfficer</b>  <i>own development</i> <br> ( This Plugin will enable for Raid Assistants dragging Players of one Raid-subgroup to another. This was on vanilla previously only enabled for RaidLeaders but the API allows Assistants to do so too )</li>
    <li><b>AFKick</b>  <i>own development (CONCEPT IN PROGRESS)</i> <br> ( The concept of this Plugin is yet not fully made and can still be cancelled entirely. The Idea of this was from Sulfuras/Feenix Mesmerize version which in that version could get abused. The intent is to give RaidLeaders and Officers the possibility to force Raidmembers to logout IF those players are AFK and are basically blocking one raidslot not just in the raidgroup but the raid instance as such. If I reimplement such feature it will have multiple safety measures which should prevent all kinds of abuse. )</li>
</ul>

## Raid Adjustments
If you want to browse through all the changes and their status regarding each encounter in the Raid specific README files. On there you can also see whether changes are untested, working perfectly or working as good as they can be.
<ul>
    <li><a href="Raids/MC/"><b>(MC)</b> Molten Core</a></li>
    <li><a href="Raids/Onyxia/"><b>(ONY)</b> Onyxia</a></li>
    <li><a href="Raids/BWL/"><b>(BWL)</b> Blackwing Lair</a></li>
    <li><a href="Raids/ZG/"><b>(ZG)</b> Zul'Gurub</a></li>
    <li><a href="Raids/AQ20/"><b>(AQ20)</b> Ruins of Ahn'Qiraj</a></li>
    <li><a href="Raids/AQ40/"><b>(AQ40)</b> Temple of Ahn'Qiraj</a></li>
    <li><a href="Raids/Naxxramas/"><b>(NAXX)</b> Naxxramas</a></li>
</ul>


## Core/General Adjustments
- <b>(100%)</b> Engage Syncs are now working perfectly on every encounter and do allow communication between clients of different language packs.
- <b>(100%)</b> Bosskill Syncs were added for every encounter dynamically and do also support communication of different language packs.
- <b>(QA)</b> BossWipe Syncs were remodelled and added dynamically for every encounter.
- <b>(100%)</b> KTM compatibility - Bossmodules are now able to set the MasterTarget, reset the Threat or Clear the Master Target. RaidOfficers do need to have this version for that.
- <b>()</b> to be completed later..

# Provided API
<a href="http://wow.gamepedia.com/BigWigs/API">BigWigs API</a>

function BigWigs.modulePrototype:Bar(text, length, icon, otherColor, c1, c2, c3, c4, c5, c6, c7, c8, c9, c10)
	self:TriggerEvent("BigWigs_StartBar", self, text, time, icon, otherc, c1, c2, c3, c4, c5, c6, c7, c8, c9, c10)
end
function BigWigs.modulePrototype:DelayedBar(text, length, icon, otherColor, c1, c2, c3, c4, c5, c6, c7, c8, c9, c10)
	return self:ScheduleEvent("BigWigs_StartBar", delay, self, text, time, icon, otherc, c1, c2, c3, c4, c5, c6, c7, c8, c9, c10)
end

## :Bar(text, length, icon, otherColor, ...)
Starts a timer bar that counts down for the specified length of time.

### Arguments
<ul>
	<li><b>text</b> string<br />The text to show on the bar.</li>
	<li><b>length</b> number<br />The length of the bar in seconds.</li>
	<li><b>icon</b> string<br />What icon to show on the bar.</li>
	<li><b>otherColor</b> boolean<br />Optional, if not specified, the configured colors will be used. If specified, you must provide 1 to 10 colors to use as arguments after otherColor.</li>
	<li><b>...</b> color<br />Optional, if otherColor is specified, you must provide 1 to 10 colors.</li>
</ul>
### Returns
Nothing
		
###	Remarks
"Interface\\Icons\\" is automatically pre-pended to the icon path. If you have to show a bar with an icon that is not part of the default icons provided by WoW, this is still possible using the self:TriggerEvent("BigWigs_StartBar", ...) syntax.
		
### Example
self:Bar("Adds incoming!", 30, "Spell_Nature_Web")
self:Bar("Testing Colors!", 60, "Spell_Nature_Web", true, "red", "yellow", "green")


## :Icon(name, iconnumber)
Puts the specified raid icon on the specified player, only works if you are promoted in the raid or the raid leader.

### Arguments
<ul>
	<li><b>name</b> string<br />The name of the player you want to put an icon on.</li>
	<li><b>iconnumber</b> number<br />Optional, if not specified, the configured default raid icon will be used. If specified, this raid icon will be used. 1: Yellow Star, 2: Orange Circle, 3: Purple Diamond, 4: Green Triangle, 5: White Moon, 6: Blue Square, 7: Red Cross, 8: Skull</li>
</ul>

### Returns
Nothing.
		
###	Remarks
If you use GenericBossDeath or CheckForWipe the icon is removed automatically. If not, you should clear it yourself.
		
### Example
self:Icon("SomePlayer")


## :Message(text, priority, noRaidSay, sound, broadcastOnly)
Displays a message in the configured message frame (defaults to BigWigs' own message frame) with the color configured for the given priority.

### Arguments
<ul>
	<li><b>text</b> string<br />The message to show.</li>
	<li><b>priority</b> string<br />Optional, one of "Important", "Personal", "Urgent", "Attention", "Positive", "Bosskill" or "Core".</li>
	<li><b>noRaidSay</b> boolean<br />Optional, if this is non-nil, the message will not be relayed to raid warning channel, even if that option is enabled.</li>
	<li><b>sound</b> string or boolean<br />Optional, if this is a string, it must be a valid sound name (see :Sound). If 'true' is passed, the default "RaidWarning" sound provided by WoW will be played.</li>
	<li><b>broadcastOnly</b> boolean<br />Optional, if this is provided, the message will only be broadcasted to the raid warning channel (if that option is enabled), and not shown locally.</li>
</ul>
### Returns
Nothing.
		
###	Remarks
You should almost always provide a priority - if not, the message will be white. Remember that you should NOT surround the text with "***".
Also note that priority can be a RGB tuple, like {r=1.0,g=0,b=0}, and also just a color name, like "Yellow".
		
### Example
self:Message("Fear in 2sec!", "Important")
self:Message("You have the plague", "Personal", true, "Info")

## :DelayedMessage(delay, ...)
This will schedule a delayed message to be printed after delay seconds.

### Arguments
<ul>
	<li><b>delay</b> number<br />The number of seconds to wait before printing the message.</li>
	<li><b>...</b><br />The rest of the arguments are exactly like the ones for :Message.</li>
</ul>

### Returns
The scheduled event ID, which is useful if you may want to cancel the scheduled message later.
		
### Example
self:DelayedMessage(55, "Something happens in 5sec!", "Important")
		
local x = self:DelayedMessage(55, "Something happens in 5sec!", "Important")
-- Then, a bit later, the boss enters phase 2, and you no langer want this message to display
self:CancelScheduledEvent(x)


## :Sync(sync)
Sends a communication sync to the other BigWigs users in the group.

### Arguments
<ul>
	<li><b>sync</b> string<br />The synchronization token to send to the other people in your group. Note that these tokens are recieved by all the BigWigs modules, so you should make sure you pick something unique.</li>
</ul>
### Returns
Nothing.
		
###	Remarks
The tokens we use are typically prefixed by some portion of the boss name, like "HyakissWeb". When sending a sync, if you want to send more data (this will be provided by the second argument to :BigWigs_RecvSync, detailed later), you have to use string concatenation; "HyakissWeb" .. playerName (which would bekome "HyakissWeb MyToon").
Note that synchronization throttling is done only on the first part, not the additional information you include in the sync.
Of course, sync messages are sent using SendAddonMessage, and as such there are some restrictions inherited. Take a look at Wowpedia for more information.
		
### Example
self:Sync("BossAbility")
self:Sync("BossTargettedAbility " .. player)