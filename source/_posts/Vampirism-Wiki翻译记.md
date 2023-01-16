---
title:  Vampirism-Wiki翻译记
date: 2020-02-27 12:12:00
categories: 
tags:

---
What's past is prologue.

<!--more-->

### Troubleshooting（排错）

####No vampires are spawning
没有吸血鬼生成

Custom Mob Spawner / Mo's creatures
自定义怪物的生成/Mo模组下的生物

Custom Mob Spawner replaces the vanilla spawning algorithm and does not properly handle Vampirism's creatures.
Custom Mob Spawner代替了原版生成算法，因此无法正确生成吸血鬼生物。

As a workaround: Go to your config directory and look for the CustomSpawner directory. In there you should find a overworld folder with a Creatures subfolder. Edit the DE.cfg file and look for vampire and vampire baron. Change canSpawn to true and the type to MONSTER. With that I was able to see some vampires spawn. However, I do not know if this is reset on certain occasions.
解决方法：在'config'文件夹中找到'CustomSpawner'文件夹，然后找到`overworld`这个配置生物的子文件夹.编辑'DE.cfg'文件，找到'vampire'和'vampire baron'.将'canSpawn'后的'false'改为'true'.并且将'type'设置为'MONSTER'.如此你便可看到吸血鬼生成在世界上。但是，并不能确保这些是否会在某些情况下重置。

#### Thaumcraft - Can't get Examine Fire closely research

As a workaround you can go to your config directory (or use the GUI Main Menu -> Mods -> Vampirsm -> Config -> Balance) and open the Balance - vampire_player.cfg (Vampire Player General) and change fire_vulnerability_type to 0 and fire_vulnerability_max_mod to 1. Thereby the increased fire vulnerability added by Vampirism is deactivated.
解决方法：转到配置目录（或使用在游戏中打开主菜单GUI>Mods>Vampirsm>Config>Balance）,然后打开'Balance - vampire_player.cfg'(Vampire Player General)，并将'fire_vulnerability_type'设置为0，将'fire_vulnerability_max_mod'设置为1.

<br>
<br>
----------
###Biteable Creatures
可以从中吸血的生物

In Vampirism you can bite several creatures to get blood.
Sometimes they even become vampires and act different.
在吸血鬼中，你可以通过咬几种动物来获取血液。
又是被咬的生活也会变成吸血鬼，变得与众不同。

####Dynamically calculated values
动态计算

Starting with Vampirism 1.4 values for unknown animals (instanceof EntityAnimal) are dynamically calculated during runtime.
自吸血鬼模组1.4开始，会自动动态获取未知生物的'instanceof EntityAnimal'值.

Thereby creatures from most other mods should be biteable.
因此，大部分动物是可以被吸血鬼咬的。

The values are calculated based on the entities (collision box) size. However, there is a minimum size requirement for making a creature biteable. Also the values are capped at a certain values and set lower slightly than the hardcoded values to avoid explits.
这些值是基于实体（区块）的大小来计算的。但是，要使生物可以被吸血，有一个最小的尺寸要求。此外，这些值会被限定在一定范围内，并设置为比硬编码的值低一点去避免调用.

Value are indirectly synced between server and client and also stored with the entity itself (so changed values only affect newly spawned creatures).
值会在服务端和客户端之间同步，并和实体本身一起被储存起来。（因此更改后的配置只会影响新生成的生物）.

Dynamically calculated values are saved to and loaded from (world/vampirism/dynamic-blood-values.txt).
动态计算的值将保存到'world/vampirism/dynamic-blood-values.txt'中，并且模组会从中调用加载.

####Adjusting the values / Adding new biteable creatures / Preventing dynamic calculation
调整值/添加新的可以被吸血的生物/防止动态计算

Users and mod pack creator
玩家和整合包制作者

If you want to adjust the amount of blood a creature gives, follow these instructions
如果要调整生物的血液提供量的大小，请遵循以下说明：

Go to your .minecraft/config/vampirism directory
打开'.minecraft/config/vampirism directory'

Create a vampirism_blood_values.txt file
创建一个'vampirism_blood_values.txt'文件（txt类型）

Set a blood value by adding a line "entity_name=value" (e.g minecraft:cow=5)
通过添加一行'entity_name=value'代码来设置生物可以提供的血液量.
例子：minecraft:cow=5

To find out an entity's name, spawn one and use the "/vampirism-test entity" command near to it. One or more names should pop up, choose the one that sounds right.
若要获取一个实体的名称，请生成一个实体，然后在它旁边使用命令'/vampirism-test entity'.
之后会应该会显示一个或多个名称，自行选择一个看起来正确的名称。

You also can change the blood value of all creatures (including modded) at once by changing minecraft:multiplier=10 to something else (must be an integer). All blood values are multiplied by this divided by 10. This does not affect dynamically calculated ones.
你还可以将'minecraft:multiplier=10'中的10修改为其他值（必须为整数）来一次性更改所有生物（包括修改过的生物）的血液值.（即咬它一次能够获得的血液的值）所有血液值能够被*10或者/10.这不会影响动态计算的值.（不会影响它获取，调用）

These values will overwrite any default values or dynamically calculated values. The resulting file should look similar to here.
这些值将会覆盖所有的默认值或者动态计算后的值。生成的文件应该类似于这样：
```
#General Multiplier. Is divided by 10.
minecraft:multiplier=10

#Vanilla
minecraft:cow=10
minecraft:horse=10
minecraft:villager=15
minecraft:pig=5
minecraft:sheep=5
minecraft:ocelot=5
minecraft:wolf=5
minecraft:mooshroom=10
minecraft:polar_bear=10
minecraft:rabbit=2
minecraft:llama=8

#MCA
mca:EntityHuman=15
```

If you have added values for a larger count of modded mobs, please send them to us so we can add them as defaults.
如果你为大量模组生物添加了血液提供值，请将其发给作者，方便作者将此添加为默认值。

To prevent a creature from having a dynamic value assigned set it's blood value to 0 here.
为了防止将生物的血液值设定为动态计算后的值，请在此处将血液值设置为0.

Mod authors
模组作者们

If you want to add blood values for your creatures, you can either use the API or (starting with Vampirism 1.4) send a Inter-Mod-Communication-Message via Forge:
如果要为作者的生物添加血液值，，啧可以使用API（从吸血鬼模组1.4开始）或通过Forge发送一个
'Inter-Mod-Communication-Message'.

#### Adding a new convertible creature
添加新的可以变为吸血鬼的生物

If you want a certain creature to be convertible to a vampire version, follow these instructions. You first need to create a overlay image. It has to have the size of entity's texture and has to be see-though. Anything in this image will be rendered over the original entity texture.
Example (Cow): Image
如果你想让某个生物变成吸血鬼，请按照以下说明进行操作。首先要画一个这个生物的吸血鬼的皮肤，必须是实体，而且必须是透明的。此图片上的任何内容都将在原始实体的纹理上进行渲染.
（如要允许马变成吸血鬼，就画一个马的吸血鬼的图片，那么'原始实体'便是'马'.）
例子：
牛的吸血鬼皮肤：
（想要什么生物变成吸血鬼就需要按照这个皮肤一样来创建吸血鬼皮肤）
![1][1]

First get the texture of the creature (either it is available e.g. on Github, or you have to open the mod file (as zip, e.g. using 7zip, or by changing the file ending to .zip) and navigate to 'resources/assets...').
首先获取生物的皮肤（从Github上找例子，或者通过压缩文件打开模组（也可以通过将模组扩展名改为.zip实现），然后在'resources/assets'中找到皮肤）

Then the file with an image tool that supports layers (e.g. GIMP or Photoshop). Create a new transparent layer and draw the 'converted changes' (e.g. red eyes) into this layer.
然后用能够支持图片编辑的软件（例如GIMP/Photoshop）。
创建一个新的透明图层将'converted changes'(于原本的皮肤不同的地方)（如画个红眼睛）绘制到该图层中。

然后将图层设置为“不可见”，并导出保存。然后将图片发送给作者（vampirism@maxanier.de）

PS：
这段是给模组作者写的，大概就是说，若是模组作者想要自己的生物也能够在作者的吸血鬼模组中有“一席之地”的话,即自己的生物在官方吸血鬼模组中默认带有吸血鬼皮肤，那么就需要自己创建一个自己生物的“吸血鬼类型”的皮肤。然后将自己的生物皮肤以及自己的生物吸血鬼类型的皮肤发到作者的邮箱里。

If you want to test how it looks in-game beforehand, you can save the complete image (with base layer) and put it into a resource pack (at the same path as you found it in the mod's file).
如果你想测试这个皮肤在游戏里的最终效果，可以保存完整的图像（带有基础图层），（PS:类似于上方那个牛的皮肤）并将其放入到材质包中。（路径一定要相同）

Then contact the mod authors of Vampirism (e.g. send the image to vampirism@maxanier.de). If you are a mod author consider making your modded creatures convertible using the API.
然后与吸血鬼模组的作者联系（例如，将图片发送到vampirism@maxanier.de）
如果你是MOD开发者，请考虑使用API使您模组下的生物能够转换为吸血鬼类型。

### Structures
结构

#### Important structures
重要遗迹

There are new structures generated in the world. Here is a list of the most important ones:
世界上生成了新的遗迹，以下是最重要的几个：

Hunter Trainer house
培养猎人的小屋

Generated in some villages.
会在某些村庄中生成。

Has some garlic growing outside.
会有一些大蒜在其周边生成

Home of a Hunter Trainer.
是猎人教官的家。

Church
教堂

Generated in some villages.
会在某些村庄中生成。

Looks like a normal church. Has a Altar of Cleansing which can be used to cure you from vampirism
看上去像一个普通教堂。拥有一个可以净化吸血鬼的净化祭坛。


//TODO more
//其他的正在制作


#### Submit your own structures
提交自己的遗迹

It is possible to submit your own structure suggestions which might be included in future versions of the mod.
可以提交您有关遗迹的一些建议。该遗迹可能会在未来mod的某个版本中实现。

Read this.
请阅读这个(https://github.com/TeamLapen/Vampirism/wiki/Submit-your-own-structures)

###Multiplayer
多人游戏

This mod should play well on multiplayer servers. Players can choose to join the vampire faction or the the hunter faction or even mostly ignore this mod if they want.
这个模组应该可以在多人服务器中正常运行。玩家可以选择加入吸血鬼派系或者猎人派系。甚至如果玩家愿意，可以选择忽略该模组。

#### PVP

You can disable PVP within factions, so only players from different factions can hurt each other and the war between vampires and humans can take place organized.
你可以选择是否开启各个派系中的pvp选项。这样来自不同派系的玩家才能互相伤害，并且吸血鬼与人类之间的战争可以有组织，有预谋的进行着。

#### Difficulty
困难

Most hostile creatures appear in different levels.
大多数敌对生物会以不同等级生成.

The strength of a spawned creature is affected by the level of nearby players. Around strong vampire players, strong hunters will spawn, but around normal humans (not hunter/not vampire) only weak vampires will appear.
生物的攻击力会受附近玩家等级的影响。在强大的吸血鬼玩家周围将会出现强大的猎人，但是在正常人（即不是猎人也不是吸血鬼）的周围只会出现弱小的吸血鬼。

#### Commands
指令

When using command blocks or similar for things you can use the included entity selectors to filter between hunters/vampire, levels etc. in most commands.
当使用命令方块或者命令的时候，您可以使用模组自带的实体选择器然后自定义是否在大多数命令中忽略掉猎人/吸血鬼以及自定义他们的的等级等。
PS：即模组提供了一个实体选择器，可以设置在使用命令调整实体的时候是否忽略掉猎人/吸血鬼，即排除在外，不会影响到他们，以及能够自定义他们的等级之类。

#### Utility
一些实用设置

Sundamage
减少阳光伤害

For common places (e.g. spawn) you can place (cheat only) sunscreen beacons, so vampires can visit them during the day without taking sun damage.
对于一些常见吸血鬼的地方，你可以放置防晒信标（仅限作弊模式下）。这样子的话吸血鬼在白天就不会受到阳光伤害，不会因为在阳光底下而扣血。

Sleep
睡眠

There also is a Morpheus like config option, where you can specify which percentage of players have to be in a coffin to make it night.
你可以指定必须要在棺.材中睡觉的玩家的百分比。通过修改config中的'Morpheus'实现。

Infection
感染

Also interesting might be the config option to allow/deny players from infecting other human players with vampirism (hunters are immune anyway due to their garlic injection).
允许/禁止 吸血鬼玩家感染人类玩家.（猎人因为注射过大蒜试剂而免疫）（PS：因为猎人吃过大蒜而免疫？总之是因为猎人有“大蒜”而造成的免疫）

###Commands and Cheats
指令与作弊选项

It is obviously not recommend to use these commands during regular gameplay, since they might destroy your experience. Therefore most of them can only be used as an OP or in creative-mode. But for creating videos or solving problems caused by a bug or testing the alpha versions the following commands might be helpful.
无疑，对于这些命令，在正常游玩中是不太建议去使用的。因为它们可能会破坏你的游戏体验。正是因此，大多数命令只能在有管理员权限或者在创造模式下才能使用。但是在拍摄视频/bug引起的一些问题/测试Alpha版本时，以下命令可能会对你有一点帮助。

#### /vampirism

checkForVampireBiome
检查吸血鬼生物群系

Checks if there is a vampire biome somewhere in the world. Be careful with this since it will pause the server's game loop until it is finished. Usage: /vampirism checkForVampireBiome
检查主世界上是否存在吸血鬼生物群系。请注意这一点，使用这条命令时它将暂停服务器，直到完成。指令：/vampirism checkForVampireBiome

Use /vampirism level Vampire 10 to become a vampire of level 10. or /vampirism level Hunter 4 to become a hunter level 4.
使用指令：/vampirism level Vampire 10，能够将吸血鬼等级变成10级
使用指令：/vampirism level Hunter 4，能够使猎人等级变成4级。

help
帮助

Show all subcommands
显示所有子命令（显示所有命令的意思）

/vampirism-test

emptyBloodBar
即：/vampirism-test emptyBloodBar
Empties your blood bar
清空血量

help
帮助
即：/vampirism-test help
Show all subcommands
显示所有子命令

#### Entity selectors (as of version 1.1)
实体选择器（在1.1之后的版本中添加）

Vampirism adds a few custom entity selectors, which can be used together with the vanilla ones in commands ("@e[...]").
吸血鬼模组添加了一些可自定义的实体选择器，这些选择器支持命令方块中的("@e[...]").

Faction - 'vampirism:faction'
派系-'吸血鬼派系'

Select all entities that belong to a given faction. Can be 
inverted.
选择派系，可以倒置。（选择这些命令对哪些派系有效果，指定这些命令在对哪些派系生效）
Example: "/kill @e[vampirism:faction=vampire]"
Kills all vampire players and vampire mobs. Example 2: "/kill @e[vampirism:faction=!vampire]"
Kills all non vampire players and non vampire mobs.
例子1：/kill @e[vampirism:faction=vampire]
杀死所有吸血鬼玩家和吸血鬼小怪
例子2：/kill @e[vampirism:faction=!vampire]
杀死所有非吸血鬼的玩家和生物

Level - 'vampirism:level'
等级

Selects all players that are on the given level
选择指定等级上的所有玩家

Example: "/kill @a[vampirism:level=5,vampirism:faction=vampire]"
Kills all vampire players on level 5.
例子：/kill @a[vampirism:level=5,vampirism:faction=vampire]
杀死等级为5的所有吸血鬼玩家

MinLevel/MaxLevel - 'vampirism:minLevel'/'vampirism:maxLevel'
最小/最大等级

Selects all players that are at least on the given level/at max on the given level.
选择在指定等级之上/之下的玩家
（PS：max是之下，比如指定7级，那么就是对所有七级之下的玩家生效，七级以上的没有任何影响）

Example: "/kill @e[vampirism:minLevel=7]"
Kills all players that are level 7 or higher (vampire and hunter)
例子：/kill @e[vampirism:minLevel=7]
杀死所有七级以上的玩家（吸血鬼和猎人）


[1]: https://raw.githubusercontent.com/TeamLapen/Vampirism/aec60d2086c88093f7cf854e0327e98295994201/src/main/resources/assets/vampirism/textures/entity/vanilla/cow_overlay.png