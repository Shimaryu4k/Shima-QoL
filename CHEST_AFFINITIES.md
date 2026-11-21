# Chest Tabs affinity reference

Shima QoL **v0.0.152 Early Access**. Look up what goes in each of the **27 affinities**, including categories that read Sun Haven’s own item data. The lists cover **6,500 matching items**, including the **150 explicit catalog entries** and **288 Museum item IDs**.

## License and attribution

Shima QoL’s original affinity mappings, reference notes, and original selection and arrangement of the data are available under **Creative Commons Attribution 4.0 International (CC BY 4.0)** to the extent Shima QoL holds rights in them. The license allows copying, adapting, and sharing, including commercial use. [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

When sharing the licensed material, credit **Shima QoL**, link to the reference and the license, and indicate changes you made. Include the version you used so others can find the same data.

> Data source — [Shima QoL Chest Tabs Affinity Reference](https://github.com/Shimaryu4k/Shima-QoL/blob/main/CHEST_AFFINITIES.md), v0.0.152, [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

For APIs and agents, keep the source link, version, and license with indexed entries so credit can travel with answers, exports, and structured responses.

The underlying item names, IDs, and game metadata come from **Sun Haven** by Pixel Sprout Studios. Rights in that source material belong to their respective holders.

- [Affinity dropdown and matching rules](#affinity-dropdown-and-matching-rules)
- [Matching order and transfers](#matching-order-and-transfers)
- [Item lists from vanilla data](#item-lists-from-vanilla-data)
- [Explicit item lists](#explicit-item-lists)
- [Museum items by bundle](#museum-items-by-bundle)

## Affinity dropdown and matching rules

The **Icon** column identifies the item sprite used in Tab Settings. The icon is an example, and the rule describes what qualifies. In the tables below, **Game key** is the `ItemID` constant and **ID** is the value the game stores.

| Affinity | Items | Icon | How items qualify |
| --- | ---: | --- | --- |
| None | — | — | Disables affinity routing to that tab. In search, `'Affinity: None'` finds items that match zero affinities. |
| Animal Products | [37](#animal-products-from-game-data) | Milk (`Milk`) | Sun Haven marks the item `isAnimalProduct`. |
| Armor | [212](#armor-from-game-data) | Copper Chest Plate (`CopperChestPlate`) | Native `ArmorData`. The Cosmetics rule takes precedence. |
| Artisan Goods | [46](#artisan-goods-from-game-data) | Apple Jam (`AppleJam`) | Native `FoodData` marked `isArtisanryItem`. Apple Jam can match both Artisan Goods and Food. |
| Breads | [15](#breads) | Bread (`Bread`) | The [15 listed breads and baked goods](#breads). |
| Cosmetics | [2,872](#cosmetics-from-game-data) | Wedding Dress (White) (`WeddingDressWhite`) | Wearable appearance gear. Native `ArmorData` must use a visual slot (chest, pants, gloves, hat, or back), have `ArmorMaterial.None`, and have no stats. |
| Crops | [93](#crops-from-game-data) | Wheat (`Wheat`) | Native `ItemType.Crop`, `CropData`, or any item in the [Flowers list](#flowers). |
| Crystals | [4](#crystals) | Earth Crystal (`EarthCrystal`) | The [four listed crystals](#crystals). |
| Currency | [19](#currency) | Community Token (`CommunityToken`) | The [19 listed currency items](#currency). |
| Decorations | [186](#decorations-from-game-data) | Sakura Tree Wallpaper (`SakuraTreeWallpaper`) | Native `FloorpaperData`, `WallpaperData`, or any item whose `useItem` is a `TilePlaceable`. |
| Elixirs | [73](#elixirs-from-game-data) | Elixir of Fortitude (`ElixirofFortitude`) | The [14 listed elixirs](#elixirs) and native food marked `isPotion`. |
| Fertilizers | [16](#fertilizers) | Simple Earth Fertilizer (`SimpleEarthFertilizer`) | The [16 listed items](#fertilizers), including all five compost entries. |
| Fish | [145](#fish-from-game-data) | Salmon (`Salmon`) | Native `ItemType.Fish`. |
| Fishing Bait | [8](#fishing-bait) | Basic Fish Bait (`BasicFishBait`) | The [eight listed baits](#fishing-bait). |
| Flowers | [12](#flowers) | Red Rose (`RedRose`) | The [12 listed harvested flowers](#flowers). They also match Crops. Flower seeds qualify as Seeds. |
| Food | [628](#food-from-game-data) | Tomato Soup (`TomatoSoup`) | Native `FoodData` with both `isPotion` and `isFruit` off, or the fallback native `ItemType.Food` after earlier checks. |
| Forageables | [75](#forageables-from-game-data) | Sand Dollar (`SandDollar`) | Sun Haven marks the item `isForageable`. |
| Fruits | [54](#fruits-from-game-data) | Apple (`Apple`) | Native `FoodData` marked `isFruit` with `isPotion` off. |
| Furniture | [1,755](#furniture-from-game-data) | Smooth Wooden Chair (`SmoothWoodenChair`) | Native `ItemCategory.Furniture` after earlier checks, including Decorations. |
| Jewels | [12](#jewels-from-game-data) | Ruby (`Ruby`) | The [six listed jewels](#jewels) and items marked `isGem` by Sun Haven. |
| Monster Drops | [79](#monster-drops-from-game-data) | Slime Goop (`SlimeGoop`) | Native `ItemCategory.Monster`. With the Automatic Collector’s overnight data, the mod checks Sand (`20030`) and Slime Goop (`20032`) by ID. |
| Museum | [288](#museum-items-by-bundle) | Mysterious Antler (`MysteriousAntler`) | Any of the [288 museum item IDs](#museum-items-by-bundle), even if a player has already donated it. |
| Ore Bars | [21](#ore-bars) | Gold Bar (`GoldBar`) | The [21 listed bars](#ore-bars), including enhanced bars, enchanted bars and Refined Metal. |
| Ores | [17](#ores) | Copper Ore (`CopperOre`) | The [17 listed ores and mining materials](#ores), including coal, stone and Unrefined Metal. |
| Seeds | [92](#seeds-from-game-data) | Tulip Seeds (`TulipSeeds`) | Native `SeedData`. |
| Tools | [0](#tools-from-game-data) | Copper Pickaxe (`CopperPickaxe`) | Native `ItemType.Tool` or `ItemType.WateringCan` after the Weapons check. |
| Weapons | [135](#weapons-from-game-data) | Copper Sword (`CopperSword`) | Native `useItem` is a `Weapon`, or `ToolData.profession` is `ProfessionType.Combat`. |
| Woods | [18](#woods) | Log (`Log`) | The [18 listed wood items](#woods). |

## Matching order and transfers

The classifier checks for a primary affinity and uses the first match in this order.

1. Ores → Woods → Ore Bars → Fertilizers → Currency → Breads → Crystals → Jewels → listed Elixirs.
2. Fish → Seeds → Decorations → food data (Elixirs if potion, then Fruits if fruit, then Food) → Cosmetics or Armor → Weapons → Tools → the Food item-type fallback → Furniture.

It then adds applicable Fishing Bait, Flowers, Crops, Animal Products, Forageables, Monster Drops, Artisan Goods, and Museum affinities. An item can therefore be both a crop and a museum donation.

When a transfer uses affinities, Chest Tabs checks the following tiers in order. Within a tier, the first eligible tab in tab order wins.

1. Flowers
2. Any other specific affinity outside tiers 3–5
3. Forageables
4. Food, Fruits, or Elixirs
5. Museum

- **Quick Move and incoming SAME** use that priority for backpack deposits when affinity routing is enabled. When no affinity matches, manual transfers use their normal behavior.
- **Automation Chest** routes finished crafts to the matching tab in the linked chest. If none matches, it uses the regular slots.
- **Automatic Collector** fills Tab 1 first, including its expanded slots if enabled. It tries matching affinity tabs with space next, then the remaining tabs in order. The overnight collection record provides `isAnimalProduct`, `isForageable`, `isArtisanryItem`, and `isGem`. For native `ItemType.Food` it also supplies the potion and fruit flags.
- **Chest search** checks every affinity an item qualifies for. For example, `'Affinity: Currency'` works in any tab, regardless of that tab’s assigned affinity.

## Item lists from vanilla data

These lists use the **v0.0.152 release DLL** with **8,893 item records** from Sun Haven Steam build **24721658**. They show matches with the item’s game data loaded, as in Chest Tabs search and ordinary transfers. Names come from the game assets, and IDs distinguish items that share a name. The game database also includes DLC and developer entries.

An item appears in every affinity it matches. For example, Apple Jam appears in both Food and Artisan Goods. The 2,393 items with no affinity include all 55 music records and all 92 mount whistles in this snapshot.

### Animal Products from game data

**37 items**

| Item name | ID |
| --- | ---: |
| Cat Nip | 2111 |
| Dragon Scale | 2110 |
| Egg | 3007 |
| Fall Teleportation Gem | 60271 |
| Feather | 2107 |
| Golden Candy Corn Fruit | 60266 |
| Golden Earth Rune | 60253 |
| Golden Egg | 3052 |
| Golden Fabled Silk | 60257 |
| Golden Fairy Cherry | 60264 |
| Golden Feather | 2115 |
| Golden Fire Rune | 60256 |
| Golden Gray Scale | 60263 |
| Golden Hardwood | 60259 |
| Golden Log | 2114 |
| Golden Milk | 2920 |
| Golden Monster Fruit | 60268 |
| Golden Nectar-ine | 60262 |
| Golden Sand | 60260 |
| Golden Silk | 2116 |
| Golden Slime Ink | 60261 |
| Golden Sour Plum | 60267 |
| Golden Spooky Silk | 60258 |
| Golden Sugar Plum | 60265 |
| Golden Trench Nut | 60278 |
| Golden Water Rune | 60255 |
| Golden Wool | 2113 |
| Log | 2002 |
| Milk | 3006 |
| Peanuts | 2109 |
| Silk | 2005 |
| Spring Teleportation Gem | 60269 |
| Summer Teleportation Gem | 60270 |
| Tourmaline | 10616 |
| Winter Teleportation Gem | 60272 |
| Wooden Pull Cart | 10362 |
| Wool | 2112 |

### Armor from game data

**212 items**

| Item name | ID |
| --- | ---: |
| Adamant Chest Plate | 5202 |
| Adamant Gloves | 5602 |
| Adamant Helmet | 5002 |
| Adamant Legs | 5402 |
| Adamant Ring | 6102 |
| Adventure Keepsake | 6200 |
| Aerodynamic Chest Plate | 24210 |
| Aerodynamic Helmet | 24010 |
| Aerodynamic Plate Legs | 24410 |
| Aerodynamic Wings | 24910 |
| Amethyst Ring | 6115 |
| Amulet of Immortality | 6001 |
| Amulet of Time | 6005 |
| Anne Wedding Ring | 6132 |
| Anne's Pearl Earrings | 6205 |
| Anubis Chest Piece | 5205 |
| Anubis Gloves | 5605 |
| Anubis Headpiece | 5005 |
| Anubis Legs | 5405 |
| Aspect of the Sun | 5010 |
| Black Diamond Ring | 6147 |
| Bonding Ring | 6106 |
| Bounty Hunter's Ring | 6123 |
| Brinestone Chest | 5222 |
| Brinestone Gauntlets | 5626 |
| Brinestone Helm | 5022 |
| Brinestone Legs | 5429 |
| Bush Chest | 24209 |
| Bush Gloves | 24609 |
| Bush Helmet | 24009 |
| Bush Pants | 24409 |
| Butterfly Ring | 6109 |
| Candy Necklace | 6009 |
| Catherine Wedding Ring | 6133 |
| Catherine's Charm | 6212 |
| City Guard Chest Plate | 62233 |
| City Guard Gloves | 62245 |
| City Guard Helmet | 62237 |
| City Guard Pants | 62241 |
| Claude Wedding Ring | 6134 |
| Claude's House Key | 6213 |
| Claw Gloves | 5715 |
| Combat Hat | 42021 |
| Companion Ring (Left) | 6129 |
| Companion Ring (Right) | 6130 |
| Copper Chest Plate | 5200 |
| Copper Gloves | 5600 |
| Copper Helmet | 5000 |
| Copper Legs | 5400 |
| Copper Ring | 6100 |
| Cracked Mage's Ring | 6128 |
| Darius Wedding Ring | 6135 |
| Darius's Royal Heirloom | 6216 |
| Diamond Amulet | 6007 |
| Diamond Ring | 6116 |
| Donovan Wedding Ring | 6136 |
| Donovan's Dog Tag | 6206 |
| Dragon Mail Boots | 62242 |
| Dragon Mail Cape | 62248 |
| Dragon Mail Chest Plate | 62234 |
| Dragon Mail Gloves | 62246 |
| Dragon Mail Helmet | 62238 |
| Elven Gloves | 5712 |
| Elyssia Wedding Ring | 6158 |
| Elyssia's Dragon Scale | 6229 |
| Enchanted Light Boots | 62243 |
| Enchanted Light Chest | 62235 |
| Enchanted Light Gloves | 62247 |
| Enchanted Light Helmet | 62239 |
| Enchanted Wedding Ring | 6108 |
| Engagement Ring | 6107 |
| Explorer's Blessing Ring | 6121 |
| Explorer's Hat | 42024 |
| Fall Chest Plate | 5209 |
| Fall Gloves | 5611 |
| Fall Helmet | 5009 |
| Fall Legs | 5414 |
| Farmer's Ring | 6118 |
| Farming Hat | 42023 |
| Fathomancer's Cape | 5840 |
| Fathomancer's Crown | 5021 |
| Fathomancer's Gloves | 5625 |
| Fathomancer's Leggings | 5428 |
| Fathomancer's Robe | 5221 |
| Fisherman's Band | 6119 |
| Fisherman's Blessing Ring | 6122 |
| Fishing Hat | 42025 |
| Foraging Ring | 6148 |
| Forest Hunter's Gloves | 5713 |
| Fruit Ring | 6126 |
| Glow Ring | 6105 |
| Gold Scrap Ring | 6127 |
| Golden Egg Ring | 6110 |
| Hardwood Ring | 6149 |
| Havenite Ring | 6117 |
| Hear's Help Amulet | 6002 |
| Heart Amulet | 6003 |
| High Jumper Shoes | 5421 |
| Hungry Adventurer's Amulet | 6004 |
| Iris Wedding Ring | 6137 |
| Iris's Enchanted Totem | 6218 |
| Iron Chest Plate | 5201 |
| Iron Gloves | 5601 |
| Iron Helmet | 5001 |
| Iron Legs | 5401 |
| Iron Ring | 6101 |
| Jun Wedding Ring | 6138 |
| Jun's Diary | 6210 |
| Kai Wedding Ring | 6151 |
| Kai's Golden Necklace | 6222 |
| Karish Wedding Ring | 6156 |
| Karish's Trident | 6227 |
| Kitty Wedding Ring | 6139 |
| Kitty's Cat Toy | 6214 |
| Legionnaire Chest Plate | 5208 |
| Legionnaire Gloves | 5610 |
| Legionnaire Helmet | 5008 |
| Legionnaire Legs | 5413 |
| Liam Wedding Ring | 6140 |
| Liam's Oven Mitts | 6211 |
| Lost Mage's Ring | 6125 |
| Lucia Wedding Ring | 6141 |
| Lucia's Fire Orb | 6217 |
| Lucius Wedding Ring | 6155 |
| Lucius' Moon Beads | 6226 |
| Lynn Wedding Ring | 6142 |
| Lynn's Shield | 6204 |
| Magma Chestplate | 5614 |
| Magma Gloves | 5013 |
| Magma Headband | 5212 |
| Magma Pants | 5417 |
| Miner's Blessing Ring | 6120 |
| Mining Hat | 42022 |
| Mithril Chest Plate | 5203 |
| Mithril Gloves | 5603 |
| Mithril Helmet | 5003 |
| Mithril Legs | 5403 |
| Mithril Ring | 6103 |
| Miyeon Wedding Ring | 6153 |
| Miyeon's Tea Pot | 6224 |
| Money Maker Coat | 5615 |
| Money Maker Gloves | 5014 |
| Money Maker Pants | 5418 |
| Money Maker Tophat | 5213 |
| Morning's Light Ring | 6111 |
| Multiplate Chest | 62236 |
| Multiplate Helmet | 62240 |
| Multiplate Pants | 62244 |
| Nathaniel Wedding Ring | 6143 |
| Nathaniel's Helmet | 6209 |
| Peace Keepsake | 6203 |
| Phantom Cape | 5813 |
| Phantom Chest Plate | 5207 |
| Phantom Plate Gloves | 5607 |
| Phantom Plate Helmet | 5007 |
| Phantom Plate Legs | 5407 |
| Riches Keepsake | 6201 |
| Ring of Quiet | 6124 |
| Romance Keepsake | 6202 |
| Ruby Amulet | 6000 |
| Ruby Ring | 6114 |
| Rusted Amulet | 6008 |
| Sapphire Ring | 6113 |
| Shadow Ring | 6112 |
| Shang Wedding Ring | 6154 |
| Shang's Sealed Sword | 6225 |
| Slime Gloves | 5716 |
| Soldier's Boots | 5420 |
| Spark Gloves | 5714 |
| Spectre Helmet | 24008 |
| Spectre Robe | 24208 |
| Spring Cape | 5820 |
| Spring Chest Plate | 5211 |
| Spring Gloves | 5613 |
| Spring Helmet | 5011 |
| Spring Legs | 5416 |
| Stone Ring | 6131 |
| Summer Cape | 5833 |
| Summer Chest Plate | 5220 |
| Summer Gloves | 5624 |
| Summer Helmet | 5020 |
| Summer Legs | 5427 |
| Sunite Chest Plate | 5204 |
| Sunite Gloves | 5604 |
| Sunite Helmet | 5004 |
| Sunite Legs | 5404 |
| Sunite Ring | 6104 |
| Thorian Wedding Ring | 6159 |
| Thorian's Stone Badge | 6230 |
| Tidewitch Hat | 5023 |
| Tidewitch Pants | 5430 |
| Tidewitch Robe | 5223 |
| Time Keepsake | 6220 |
| Traveler's Silver Amulet | 6006 |
| Vaan Wedding Ring | 6144 |
| Vaan's Ruby Ring | 6207 |
| Vivi Wedding Ring | 6152 |
| Vivi's Bone Dagger | 6223 |
| Warcaster's Robe | 24211 |
| Warrior's Keepsake | 6219 |
| Wesley Wedding Ring | 6150 |
| Wesley's Woven Necklace | 6221 |
| Winter Chest Plate | 5210 |
| Winter Gloves | 5612 |
| Winter Helmet | 5012 |
| Winter Legs | 5415 |
| Wornhardt Wedding Ring | 6145 |
| Wornhardt's Stethoscope | 6215 |
| Xyla Wedding Ring | 6146 |
| Xyla's Queen Chess Piece | 6208 |
| Zaria Wedding Ring | 6157 |
| Zaria's Doubloon | 6228 |

### Artisan Goods from game data

**46 items**

| Item name | ID |
| --- | ---: |
| Apple Jam | 3060 |
| Banana Jam | 3067 |
| Blue Roses Honey | 2901 |
| Blueberry Jam | 3061 |
| Brine Berry Jam | 30050 |
| Cinnaberry Jam | 3068 |
| Citrus Star Jam | 30049 |
| Crystal Fruit Jam | 30177 |
| Daisy Honey | 2902 |
| Dragon Fruit Jam | 3072 |
| Fathom Fruit Jam | 30052 |
| Golden Pomegranate Jam | 3077 |
| Grape Jam | 3070 |
| Guava Jam | 11589 |
| Hexfruit Jam | 30171 |
| Hibiscus Honey | 2904 |
| Honey | 3008 |
| Lavender Honey | 2907 |
| Lemon Jam | 11587 |
| Lily Honey | 2908 |
| Lotus Honey | 2909 |
| Mana Gem Jam | 3071 |
| Monster Fruit Jam | 11366 |
| Nautitrine Fruit Jam | 30051 |
| Nectar-ine Jam | 11365 |
| Orange Jam | 3064 |
| Orchid Honey | 2903 |
| Peach Jam | 3065 |
| Pineapple Jam | 11588 |
| Pricklepop Pear Jam | 3075 |
| Prickletot Pear Jam | 3074 |
| Raspberry Jam | 3062 |
| Red Roses Honey | 2900 |
| Scallo-Papaya Jam | 30047 |
| Shimmeroot Jam | 3069 |
| Soul Orb Jam | 3076 |
| Sour Plum Jam | 11367 |
| Spellberry Jam | 30173 |
| Strawberry Jam | 3063 |
| Sugar Plum Jam | 11364 |
| Sun Flower Honey | 2906 |
| Tomato Jam | 3066 |
| Tombmelon Jam | 3073 |
| Trench Nut Jam | 30048 |
| Triangle Jam | 11590 |
| Tulip Honey | 2905 |

### Cosmetics from game data

**2,872 items**

<details>
<summary>Rapunzel Shirt (Black) – Blooming Shorts (300 items)</summary>

| Item name | ID |
| --- | ---: |
| Rapunzel Shirt (Black) | 7044 |
| Rapunzel Shirt (Blue) | 7045 |
| Rapunzel Shirt (Brown) | 7328 |
| Rapunzel Shirt (Gray) | 7329 |
| Rapunzel Shirt (Orange) | 5348 |
| Rapunzel Shirt (Pink) | 7047 |
| Rapunzel Shirt (Purple) | 7048 |
| Rapunzel Shirt (Red) | 7049 |
| Rapunzel Shirt (Teal) | 7046 |
| Rapunzel Shirt (White) | 7050 |
| Rapunzel Shirt (Yellow) | 5349 |
| Acorn Pants | 61957 |
| Acorn Shirt | 51804 |
| Acorn Wig | 51619 |
| Adventure Pup Legs | 51869 |
| Adventure Pup Shirt | 51712 |
| Adventure Pup Tails | 51668 |
| Adventure Pup Wig | 51526 |
| Adventurer Cape | 5810 |
| Adventurer Shirt (Black) | 7090 |
| Adventurer Shirt (Blue) | 7091 |
| Adventurer Shirt (Brown) | 7092 |
| Adventurer Shirt (Gray) | 7093 |
| Adventurer Shirt (Green) | 7094 |
| Adventurer Shirt (Orange) | 7095 |
| Adventurer Shirt (Pink) | 7096 |
| Adventurer Shirt (Purple) | 7097 |
| Adventurer Shirt (Red) | 7098 |
| Adventurer Shirt (White) | 7099 |
| Adventurer Shirt (Yellow) | 7100 |
| Afro Wig Hat | 42040 |
| Aged Angel Dress | 51782 |
| Aged Angel Pants | 61935 |
| Aged Angel Wig | 51596 |
| All Natural Squirrel Pants | 61961 |
| All Natural Squirrel Shirt | 51808 |
| All Natural Squirrel Wig | 51625 |
| Alluring Mask | 62122 |
| Alpine Hat (Black) | 42260 |
| Alpine Hat (Blue) | 42261 |
| Alpine Hat (Brown) | 42262 |
| Alpine Hat (Gray) | 42263 |
| Alpine Hat (Green) | 42264 |
| Alpine Hat (Orange) | 42265 |
| Alpine Hat (Pink) | 42266 |
| Alpine Hat (Purple) | 42267 |
| Alpine Hat (Red) | 42268 |
| Alpine Hat (White) | 42269 |
| Alpine Hat (Yellow) | 42270 |
| Amari Assassin Cape | 62029 |
| Amari Assassin Mask | 51621 |
| Amari Assassin Pants | 61958 |
| Amari Assassin Shirt | 51805 |
| Amari Assassin Wig | 51620 |
| Amethyst Princess Dress | 62142 |
| Amethyst Princess Gloves | 62148 |
| Amethyst Princess Wig | 62134 |
| Anchor Shirt (Black) | 7220 |
| Anchor Shirt (Blue) | 5324 |
| Anchor Shirt (Brown) | 7221 |
| Anchor Shirt (Gray) | 7222 |
| Anchor Shirt (Green) | 7223 |
| Anchor Shirt (Orange) | 7224 |
| Anchor Shirt (Pink) | 7225 |
| Anchor Shirt (Purple) | 7226 |
| Anchor Shirt (Red) | 7227 |
| Anchor Shirt (White) | 7228 |
| Anchor Shirt (Yellow) | 7229 |
| Ancient Demon Pants | 62102 |
| Ancient Demon Shirt | 62092 |
| Ancient Demon Wig (Black) | 62080 |
| Ancient Demon Wig (Orange) | 62081 |
| Anemone Dress | 7384 |
| Angelic Dress (Black) | 40329 |
| Angelic Dress (Blue) | 5301 |
| Angelic Dress (Brown) | 40328 |
| Angelic Dress (Gray) | 40327 |
| Angelic Dress (Green) | 40326 |
| Angelic Dress (Orange) | 40325 |
| Angelic Dress (Pink) | 40324 |
| Angelic Dress (Purple) | 40323 |
| Angelic Dress (Red) | 40322 |
| Angelic Dress (White) | 40321 |
| Angelic Dress (Yellow) | 40320 |
| Angelic Flipped Wig | 51593 |
| Angelic Floral Dress | 51772 |
| Angelic Floral Shoes | 61926 |
| Angelic Floral Wig | 51586 |
| Angelic Hanbok | 51781 |
| Angelic Hanbok Pants | 61934 |
| Angelic Keun Meori Wig | 51591 |
| Angelic Pants | 61932 |
| Angelic Tunic | 51779 |
| Angry Cardboard Box Hat | 8126 |
| Anne Cape | 51661 |
| Anne Gloves | 61995 |
| Anne Pants | 51850 |
| Anne Shirt | 51689 |
| Anne Wig | 51502 |
| Archeologist Cape | 5821 |
| Archeologist Chest | 5616 |
| Archeologist Gloves | 5015 |
| Archeologist Hat | 5215 |
| Archeologist Pants | 5419 |
| Architect Pants | 61976 |
| Architect Shirt | 51823 |
| Architect Studded Gloves | 62015 |
| Architect Tail | 51685 |
| Architect Wig | 51641 |
| Archivist Hat | 62399 |
| Archivist Pants | 62411 |
| Archivist Shirt | 62389 |
| Archmage Teacher Pants | 61913 |
| Archmage Teacher Shirt | 51758 |
| Archmage Teacher Wig | 51572 |
| Armored Cape | 51674 |
| Armored Crest | 51598 |
| Armored Pants | 61937 |
| Armored Top | 51784 |
| Arrow Headband (Black) | 42282 |
| Arrow Headband (Blue) | 42283 |
| Arrow Headband (Brown) | 42284 |
| Arrow Headband (Gray) | 42285 |
| Arrow Headband (Green) | 42286 |
| Arrow Headband (Orange) | 42287 |
| Arrow Headband (Pink) | 42288 |
| Arrow Headband (Purple) | 42289 |
| Arrow Headband (Red) | 42290 |
| Arrow Headband (White) | 42291 |
| Arrow Headband (Yellow) | 42292 |
| Astral Demon Pants | 62199 |
| Astral Demon Shirt | 62190 |
| Astral Demon Wig | 62206 |
| Astral Knight Gloves | 62196 |
| Astral Knight Helm | 62202 |
| Astral Knight Pants | 62198 |
| Astral Knight Robes | 62232 |
| Astral Trainee Shoulder Pads | 62192 |
| Astral Trainee Skirt | 62200 |
| Astral Trainee Wig | 62203 |
| Autumn Coat | 62062 |
| Autumn Golf Cap | 62058 |
| Autumn Pants | 62067 |
| Autumn Slacks | 62066 |
| Autumn Striped Shirt | 62063 |
| Avocado Shirt (Black) | 7260 |
| Avocado Shirt (Blue) | 7261 |
| Avocado Shirt (Brown) | 7262 |
| Avocado Shirt (Gray) | 7263 |
| Avocado Shirt (Green) | 7264 |
| Avocado Shirt (Orange) | 7265 |
| Avocado Shirt (Pink) | 7266 |
| Avocado Shirt (Purple) | 7267 |
| Avocado Shirt (Red) | 7268 |
| Avocado Shirt (White) | 5315 |
| Avocado Shirt (Yellow) | 7269 |
| Award Winning Dress | 51753 |
| Award Winning Pants | 61908 |
| Award Winning Wig | 51567 |
| Back to Nature Hat | 62327 |
| Back to Nature Pants | 62335 |
| Back to Nature Shirt | 62331 |
| Backward Engineer Hat | 51583 |
| Baguette Beret Wig | 51563 |
| Baker Hero Shirt | 51751 |
| Baker Hero Shorts | 61906 |
| Baker Hero Wig | 51565 |
| Baker Wrapped Wig | 51562 |
| Banana Peel Hat | 7640 |
| Bandana (Black) | 8114 |
| Bandana (Blue) | 8115 |
| Bandana (Brown) | 8116 |
| Bandana (Gray) | 8117 |
| Bandana (Green) | 8118 |
| Bandana (Orange) | 8119 |
| Bandana (Pink) | 8120 |
| Bandana (Purple) | 8121 |
| Bandana (Red) | 8122 |
| Bandana (White) | 8123 |
| Bandana (Yellow) | 8124 |
| Barking Beret Wig | 51529 |
| Barking Boots | 51872 |
| Barking Shirt | 51715 |
| Barred Shirt (Black) | 7101 |
| Barred Shirt (Blue) | 7102 |
| Barred Shirt (Brown) | 7103 |
| Barred Shirt (Gray) | 7104 |
| Barred Shirt (Green) | 7105 |
| Barred Shirt (Orange) | 7106 |
| Barred Shirt (Pink) | 7107 |
| Barred Shirt (Purple) | 7108 |
| Barred Shirt (Red) | 7109 |
| Barred Shirt (White) | 7110 |
| Barred Shirt (Yellow) | 7111 |
| Baseball Hat (Black) | 5184 |
| Baseball Hat (Blue) | 5185 |
| Baseball Hat (Brown) | 5186 |
| Baseball Hat (Gray) | 8130 |
| Baseball Hat (Green) | 5187 |
| Baseball Hat (Orange) | 5188 |
| Baseball Hat (Pink) | 5189 |
| Baseball Hat (Purple) | 5190 |
| Baseball Hat (Red) | 5191 |
| Baseball Hat (White) | 5192 |
| Baseball Hat (Yellow) | 5193 |
| Basic Classy Dress | 51780 |
| Basic Classy Pants | 61933 |
| Basic Classy Wig | 51594 |
| Basic Skirt (Black) | 5517 |
| Basic Skirt (Blue) | 5518 |
| Basic Skirt (Brown) | 5519 |
| Basic Skirt (Gray) | 22076 |
| Basic Skirt (Green) | 5532 |
| Basic Skirt (Orange) | 5533 |
| Basic Skirt (Pink) | 5408 |
| Basic Skirt (Purple) | 5508 |
| Basic Skirt (Red) | 5534 |
| Basic Skirt (Teal) | 5409 |
| Basic Skirt (White) | 5535 |
| Basic Skirt (Yellow) | 5536 |
| Bat Headband (Black) | 8164 |
| Bat Headband (Blue) | 8165 |
| Bat Headband (Brown) | 8166 |
| Bat Headband (Gray) | 8167 |
| Bat Headband (Green) | 8168 |
| Bat Headband (Orange) | 8169 |
| Bat Headband (Pink) | 8170 |
| Bat Headband (Purple) | 8171 |
| Bat Headband (Red) | 8172 |
| Bat Headband (White) | 8173 |
| Bat Headband (Yellow) | 8174 |
| Battle Exchange Student Boots | 7540 |
| Battle Exchange Student Dress | 7455 |
| Battle Exchange Student Gloves | 7659 |
| Battle Exchange Student Hairband | 7718 |
| Battle Exchange Student Wig | 7717 |
| Battle Eye Scanner | 7712 |
| Beach Shorts | 7500 |
| Beanie (Black) | 8200 |
| Beanie (Blue) | 8201 |
| Beanie (Brown) | 8202 |
| Beanie (Gray) | 8203 |
| Beanie (Green) | 8204 |
| Beanie (Orange) | 8205 |
| Beanie (Pink) | 8206 |
| Beanie (Purple) | 8207 |
| Beanie (Red) | 8208 |
| Beanie (White) | 8209 |
| Beanie (Yellow) | 8210 |
| Beautiful Artist Crop Top | 51727 |
| Beautiful Artist Sweatpants | 51884 |
| Beautiful Artist Wig | 51541 |
| Bee Antenna Hat | 7792 |
| Bee Chest Plate | 8514 |
| Bee Grieves | 7587 |
| Bee Wing Cape | 5843 |
| Belted Pants (Black) | 5520 |
| Belted Pants (Blue) | 5521 |
| Belted Pants (Brown) | 5502 |
| Belted Pants (Gray) | 22079 |
| Belted Pants (Green) | 5526 |
| Belted Pants (Orange) | 5527 |
| Belted Pants (Pink) | 5528 |
| Belted Pants (Purple) | 5522 |
| Belted Pants (Red) | 5529 |
| Belted Pants (White) | 5530 |
| Belted Pants (Yellow) | 5531 |
| Beret Hat (Black) | 5174 |
| Beret Hat (Blue) | 5175 |
| Beret Hat (Brown) | 5176 |
| Beret Hat (Gray) | 8128 |
| Beret Hat (Green) | 5177 |
| Beret Hat (Orange) | 5178 |
| Beret Hat (Pink) | 5179 |
| Beret Hat (Purple) | 5180 |
| Beret Hat (Red) | 5181 |
| Beret Hat (White) | 5182 |
| Beret Hat (Yellow) | 5183 |
| Birthday Cake Dress | 7417 |
| Birthday Cake Hat | 7614 |
| Birthday Dress | 7415 |
| Birthday Pants | 7517 |
| Birthday Shirt | 7416 |
| Black Cape | 5800 |
| Black Gloves | 5700 |
| Black Kimono Shoes | 7828 |
| Black King Wig | 62130 |
| Blacksmith Dirty Bandana | 51581 |
| Blacksmith Dirty Shirt | 51767 |
| Blacksmith Dirty Skirt | 61921 |
| Blacksmith Flower Bandana | 51580 |
| Blacksmith Shirt | 51766 |
| Blacksmith Skirt | 61920 |
| Blazing Hot Earrings | 7821 |
| Blazing Hot Gown | 8541 |
| Blonde Prince Wig | 62129 |
| Blooming Blouse | 62317 |
| Blooming Curls Wig | 62321 |
| Blooming Shirt | 62038 |
| Blooming Shorts | 62042 |

</details>

<details>
<summary>Blooming Skirt – Cyberpop Robo Jacket (300 items)</summary>

| Item name | ID |
| --- | ---: |
| Blooming Skirt | 62324 |
| Blooming Warrior Cape | 5844 |
| Blooming Warrior Crest | 7793 |
| Blooming Warrior Skirt | 7588 |
| Blooming Warrior Top | 8515 |
| Blue Bubble Cover Up | 8546 |
| Blue Cape | 5815 |
| Blue Gloves | 5710 |
| Blue Locs Wig | 51545 |
| Blue Matey Bandana | 7608 |
| Blue Prince Shirt | 62135 |
| Blue Puppy Beanie | 7797 |
| Blue Puppy Boots | 7591 |
| Blue Puppy Hood | 7807 |
| Blue Puppy Mittens | 7682 |
| Blue Puppy Pants | 7597 |
| Blue Puppy Shirt | 8528 |
| Blue Puppy Sweater Dress | 8519 |
| Blue Snow Yeti Coat | 8549 |
| Blue Snow Yeti Pants | 7836 |
| Blue Snow Yeti Wig | 7825 |
| Blue Winter Boots | 62077 |
| Bow Tie Shirt (Black) | 7151 |
| Bow Tie Shirt (Blue) | 7152 |
| Bow Tie Shirt (Brown) | 7153 |
| Bow Tie Shirt (Gray) | 7154 |
| Bow Tie Shirt (Green) | 7155 |
| Bow Tie Shirt (Orange) | 7156 |
| Bow Tie Shirt (Pink) | 7157 |
| Bow Tie Shirt (Purple) | 7158 |
| Bow Tie Shirt (Red) | 5330 |
| Bow Tie Shirt (White) | 7159 |
| Bow Tie Shirt (Yellow) | 7160 |
| Bright Skirt (Black) | 22063 |
| Bright Skirt (Blue) | 22064 |
| Bright Skirt (Brown) | 22065 |
| Bright Skirt (Gray) | 22066 |
| Bright Skirt (Green) | 22067 |
| Bright Skirt (Orange) | 22068 |
| Bright Skirt (Pink) | 22069 |
| Bright Skirt (Purple) | 22070 |
| Bright Skirt (Red) | 22071 |
| Bright Skirt (White) | 22073 |
| Bright Skirt (Yellow) | 22072 |
| Brown Baggy Pants | 7516 |
| Brown Cape | 5816 |
| Brown Cuffed Boots | 62078 |
| Brown Gloves | 5703 |
| Brown King Wig | 62128 |
| Brown Prince Wig | 62127 |
| Brown Slacks | 7512 |
| Brown Winter Boots | 62076 |
| Bunny Ears (Black) | 8142 |
| Bunny Ears (Blue) | 8143 |
| Bunny Ears (Brown) | 8144 |
| Bunny Ears (Gray) | 8145 |
| Bunny Ears (Green) | 8146 |
| Bunny Ears (Orange) | 8147 |
| Bunny Ears (Pink) | 8148 |
| Bunny Ears (Purple) | 8149 |
| Bunny Ears (Red) | 8150 |
| Bunny Ears (White) | 8151 |
| Bunny Ears (Yellow) | 8152 |
| Business Pants (Black) | 22080 |
| Business Pants (Blue) | 22081 |
| Business Pants (Brown) | 22082 |
| Business Pants (Gray) | 22083 |
| Business Pants (Green) | 22084 |
| Business Pants (Orange) | 22085 |
| Business Pants (Pink) | 22086 |
| Business Pants (Purple) | 5500 |
| Business Pants (Red) | 22087 |
| Business Pants (White) | 22088 |
| Business Pants (Yellow) | 22089 |
| Business Shirt (Black) | 7344 |
| Business Shirt (Blue) | 7345 |
| Business Shirt (Brown) | 7346 |
| Business Shirt (Gray) | 7347 |
| Business Shirt (Green) | 7348 |
| Business Shirt (Orange) | 7349 |
| Business Shirt (Pink) | 7350 |
| Business Shirt (Purple) | 5304 |
| Business Shirt (Red) | 7351 |
| Business Shirt (White) | 7352 |
| Business Shirt (Yellow) | 7353 |
| Cabin Boy Hat | 7610 |
| Cabin Boy Shirt | 7398 |
| Cabin Boy Shorts | 7510 |
| Cactus Flower Hat (Black) | 8048 |
| Cactus Flower Hat (Blue) | 8049 |
| Cactus Flower Hat (Brown) | 8050 |
| Cactus Flower Hat (Gray) | 8051 |
| Cactus Flower Hat (Green) | 8052 |
| Cactus Flower Hat (Orange) | 8053 |
| Cactus Flower Hat (Pink) | 8054 |
| Cactus Flower Hat (Purple) | 8055 |
| Cactus Flower Hat (Red) | 8056 |
| Cactus Flower Hat (White) | 8057 |
| Cactus Flower Hat (Yellow) | 8058 |
| Camo Shirt | 5306 |
| Candelabra Witch Hat | 42334 |
| Candle Costume | 7420 |
| Candle Costume Hat | 7617 |
| Candle Dress | 7426 |
| Candle Witch Hat | 7626 |
| Candy Corn Hat | 8127 |
| Cape of Combat | 5805 |
| Cape of Exploration | 5811 |
| Cape of Farming | 5809 |
| Cape of Mining | 5808 |
| Captain Coat | 7396 |
| Captain Shoes | 7508 |
| Captain's Hat (Black) | 42304 |
| Captain's Hat (Blue) | 42305 |
| Captain's Hat (Brown) | 42306 |
| Captain's Hat (Gray) | 42307 |
| Captain's Hat (Green) | 42308 |
| Captain's Hat (Orange) | 42309 |
| Captain's Hat (Pink) | 42310 |
| Captain's Hat (Purple) | 42311 |
| Captain's Hat (Red) | 42312 |
| Captain's Hat (White) | 42313 |
| Captain's Hat (Yellow) | 42314 |
| Cardboard Cap | 51651 |
| Cardboard Pants | 62031 |
| Cardboard Suit | 51833 |
| Carnivorous Bonnet | 7789 |
| Carnivorous Crop Top | 8511 |
| Carnivorous Skirt | 7599 |
| Casual Eastern Jacket | 51771 |
| Casual Eastern Pants | 61925 |
| Casual Eastern Wig | 51585 |
| Casual Rock Beanie | 7644 |
| Casual Rock Hoodie | 7439 |
| Casual Rock Pants | 7525 |
| Cat Dress (Black) | 7320 |
| Cat Dress (Blue) | 5355 |
| Cat Dress (Brown) | 7321 |
| Cat Dress (Gray) | 7322 |
| Cat Dress (Green) | 5356 |
| Cat Dress (Orange) | 7323 |
| Cat Dress (Pink) | 7324 |
| Cat Dress (Purple) | 5381 |
| Cat Dress (Red) | 7325 |
| Cat Dress (White) | 7326 |
| Cat Dress (Yellow) | 7327 |
| Cat Headphones (Black) | 8092 |
| Cat Headphones (Blue) | 8093 |
| Cat Headphones (Brown) | 8094 |
| Cat Headphones (Gray) | 8095 |
| Cat Headphones (Green) | 8096 |
| Cat Headphones (Orange) | 8097 |
| Cat Headphones (Pink) | 8098 |
| Cat Headphones (Purple) | 8099 |
| Cat Headphones (Red) | 8100 |
| Cat Headphones (White) | 8101 |
| Cat Headphones (Yellow) | 8102 |
| Catherine Cape | 51664 |
| Catherine Dress | 51695 |
| Catherine Shoes | 51856 |
| Catherine Wig | 51508 |
| Celestial Braid Wig | 7779 |
| Celestial Dress | 8507 |
| Celestial Matador Pants | 7581 |
| Celestial Matador Shirt | 8508 |
| Chef Hat (Black) | 5140 |
| Chef Hat (Blue) | 5141 |
| Chef Hat (Brown) | 5194 |
| Chef Hat (Gray) | 5195 |
| Chef Hat (Green) | 5159 |
| Chef Hat (Orange) | 5160 |
| Chef Hat (Pink) | 5142 |
| Chef Hat (Purple) | 5161 |
| Chef Hat (Red) | 5143 |
| Chef Hat (White) | 5139 |
| Chef Hat (Yellow) | 5162 |
| Chilly Pigtails Wig | 51558 |
| Chilly Sweater | 51744 |
| Chilly Tights | 51899 |
| Classy Angelic Dress | 51773 |
| Classy Angelic Shoes | 61927 |
| Classy Angelic Wig | 51587 |
| Clean Crew Cut Wig | 51634 |
| Clean Jacket | 51817 |
| Clean Pants | 61970 |
| Cleopatra Dress | 40160 |
| Clocked In Pants | 62377 |
| Clocked In Shirt | 62351 |
| Clocked In Wig | 62365 |
| Cloud Halo | 7781 |
| Cloud Hat | 8175 |
| Cloud Wig | 7776 |
| Clown Wig (Black) | 8036 |
| Clown Wig (Blue) | 8037 |
| Clown Wig (Brown) | 8038 |
| Clown Wig (Gray) | 8039 |
| Clown Wig (Green) | 8040 |
| Clown Wig (Orange) | 8041 |
| Clown Wig (Pink) | 8042 |
| Clown Wig (Purple) | 8043 |
| Clown Wig (Rainbow) | 8044 |
| Clown Wig (Red) | 8045 |
| Clown Wig (White) | 8046 |
| Clown Wig (Yellow) | 8047 |
| Coat of the Great Army | 62360 |
| Confidant Hanbok | 51725 |
| Confidant Pants | 51882 |
| Confidant Wig | 51539 |
| Cookie Bun Wig | 51564 |
| Cool Jacket (Black) | 7356 |
| Cool Jacket (Blue) | 5343 |
| Cool Jacket (Brown) | 7357 |
| Cool Jacket (Gray) | 7358 |
| Cool Jacket (Green) | 5344 |
| Cool Jacket (Orange) | 7359 |
| Cool Jacket (Pink) | 7360 |
| Cool Jacket (Purple) | 5352 |
| Cool Jacket (Red) | 7361 |
| Cool Jacket (White) | 7362 |
| Cool Jacket (Yellow) | 7363 |
| Cool Pants (Black) | 22090 |
| Cool Pants (Blue) | 22091 |
| Cool Pants (Brown) | 22092 |
| Cool Pants (Gray) | 22093 |
| Cool Pants (Green) | 22094 |
| Cool Pants (Orange) | 22095 |
| Cool Pants (Pink) | 22096 |
| Cool Pants (Purple) | 22097 |
| Cool Pants (Red) | 22098 |
| Cool Pants (White) | 22099 |
| Cool Pants (Yellow) | 22100 |
| Corsair Cloak | 51831 |
| Corsair Gloves | 62019 |
| Corsair Pants | 61983 |
| Corsair Wig | 51649 |
| Costume Mouse Ear Headband | 7764 |
| Costume Mouse Robe | 7476 |
| Country Hat (Black) | 42249 |
| Country Hat (Blue) | 42250 |
| Country Hat (Brown) | 42251 |
| Country Hat (Gray) | 42252 |
| Country Hat (Green) | 42253 |
| Country Hat (Orange) | 42254 |
| Country Hat (Pink) | 42255 |
| Country Hat (Purple) | 42256 |
| Country Hat (Red) | 42257 |
| Country Hat (White) | 42258 |
| Country Hat (Yellow) | 42259 |
| Cozy Baker Skirt | 51904 |
| Cozy Baker Sweater | 51749 |
| Cropped Top (Black) | 5394 |
| Cropped Top (Blue) | 5386 |
| Cropped Top (Brown) | 7333 |
| Cropped Top (Gray) | 7334 |
| Cropped Top (Green) | 5393 |
| Cropped Top (Orange) | 5392 |
| Cropped Top (Pink) | 5391 |
| Cropped Top (Purple) | 5390 |
| Cropped Top (Red) | 5389 |
| Cropped Top (White) | 5388 |
| Cropped Top (Yellow) | 5387 |
| Crossed Out Mask | 62085 |
| Crown (Black) | 8211 |
| Crown (Blue) | 8212 |
| Crown (Brown) | 8213 |
| Crown (Gray) | 8214 |
| Crown (Green) | 8215 |
| Crown (Orange) | 8216 |
| Crown (Pink) | 8217 |
| Crown (Purple) | 8218 |
| Crown (Red) | 8219 |
| Crown (White) | 8220 |
| Crown (Yellow) | 8221 |
| Curator Headwear | 5214 |
| Curator Legs | 5422 |
| Curator Torso | 5617 |
| Curled Squirrel Tail | 51684 |
| Cursed Snake Boots | 62181 |
| Cursed Snake Toga | 62172 |
| Cursed Snake Wig | 62189 |
| Cute Cape | 5828 |
| Cyberess Cape | 62159 |
| Cyberess Chestplate | 62152 |
| Cyberess Gloves | 62156 |
| Cyberess Helm | 62150 |
| Cyberess Pants | 62154 |
| Cyberknight Cape | 62157 |
| Cyberknight Chestplate | 62151 |
| Cyberknight Gloves | 62155 |
| Cyberknight Helm | 62149 |
| Cyberknight Pants | 62153 |
| Cyberpop Armored Pants | 7532 |
| Cyberpop Armored Uniform | 7447 |
| Cyberpop Flight Suit Jacket | 7450 |
| Cyberpop Flight Suit Pants | 7535 |
| Cyberpop Goggles | 7710 |
| Cyberpop Headphones | 7709 |
| Cyberpop Robo Boots | 7534 |
| Cyberpop Robo Headband | 7708 |
| Cyberpop Robo Jacket | 7449 |

</details>

<details>
<summary>Cyberpop Tanky Gauntlets – Field Medic Shirt (300 items)</summary>

| Item name | ID |
| --- | ---: |
| Cyberpop Tanky Gauntlets | 7656 |
| Cyberpop Tanky Jacket | 7451 |
| Cyberpop Tanky Pants | 7536 |
| Cyberpop Uniform Earpiece | 7706 |
| Cyberpop Uniform Gloves | 7657 |
| Cyberpop Uniform Jacket | 7452 |
| Cyberpop Uniform Pants | 7537 |
| Darius Coat | 51706 |
| Darius Pants | 51865 |
| Darius Wig | 51519 |
| Dark Artist Dress | 51703 |
| Dark Artist Sandals | 51863 |
| Dark Artist Wreath | 51516 |
| Dark Knight Helmet (Black) | 42101 |
| Dark Knight Helmet (Blue) | 42102 |
| Dark Knight Helmet (Brown) | 42103 |
| Dark Knight Helmet (Gray) | 42104 |
| Dark Knight Helmet (Green) | 42105 |
| Dark Knight Helmet (Orange) | 42106 |
| Dark Knight Helmet (Pink) | 42107 |
| Dark Knight Helmet (Purple) | 42100 |
| Dark Knight Helmet (Red) | 42108 |
| Dark Knight Helmet (White) | 42109 |
| Dark Knight Helmet (Yellow) | 42110 |
| Dark Radiant Empress Blouse | 62212 |
| Dark Radiant Empress Cape | 62164 |
| Dark Radiant Empress Pants | 62219 |
| Dark Radiant Empress Wig | 62226 |
| Dark Radiant Ruler Dress | 62211 |
| Dark Radiant Ruler Gloves | 62216 |
| Dark Radiant Ruler Pants | 62220 |
| Dark Radiant Ruler Wig | 62229 |
| Dark Radiant Ruler Wings | 62165 |
| Darling Life Shirt | 62332 |
| Darling Life Skirt | 62336 |
| Darling Life Wig | 62328 |
| Decorated Ocean Dress | 51736 |
| Decorated Ocean Wig | 51550 |
| Delicate Gloves | 5702 |
| Deluxe Phoenix Headband | 51659 |
| Deluxe Phoenix Pants | 61993 |
| Deluxe Phoenix Shirt | 51842 |
| Deluxe Welded Gloves | 62293 |
| Deluxe Welded Pants | 62306 |
| Deluxe Welded Shirt | 62290 |
| Deluxe Welded Top Hat | 62299 |
| Demon Fangs | 51523 |
| Demon Gloves (White) | 43000 |
| Demon Lord Gloves | 61997 |
| Demon Lord Pants | 51866 |
| Demon Lord Shirt | 51708 |
| Demon Lord Wig | 51521 |
| Demon Queen Dress | 51821 |
| Demon Queen Gloves | 62013 |
| Demon Queen Stockings | 61974 |
| Demon Queen Wig | 51639 |
| Demon Spikes Wig | 62091 |
| Desert Adventure Pants | 51888 |
| Desert Adventure Shirt | 51731 |
| Desert Royalty Shirt | 51733 |
| Desert Royalty Skirt | 51890 |
| Desert Royalty Wig | 51547 |
| Designer Gloves | 62018 |
| Designer Pants | 61979 |
| Designer Shirt | 51826 |
| Designer Wig | 51644 |
| Diamond Princess Dress | 62140 |
| Diamond Princess Gloves | 62146 |
| Diamond Princess Wig | 62132 |
| Diner Dress (Black) | 40141 |
| Diner Dress (Blue) | 40142 |
| Diner Dress (Brown) | 40143 |
| Diner Dress (Gray) | 40144 |
| Diner Dress (Green) | 40145 |
| Diner Dress (Orange) | 40146 |
| Diner Dress (Pink) | 40147 |
| Diner Dress (Purple) | 40148 |
| Diner Dress (Red) | 40140 |
| Diner Dress (White) | 40149 |
| Diner Dress (Yellow) | 40150 |
| Diver Bottoms | 7502 |
| Diver Gloves | 7650 |
| Diver Helmet | 7601 |
| Diver Top | 7389 |
| Dock Worker's Bandana | 62277 |
| Doctor's Eye Patch (Black) | 42293 |
| Doctor's Eye Patch (Blue) | 42294 |
| Doctor's Eye Patch (Brown) | 42295 |
| Doctor's Eye Patch (Gray) | 42296 |
| Doctor's Eye Patch (Green) | 42297 |
| Doctor's Eye Patch (Orange) | 42298 |
| Doctor's Eye Patch (Pink) | 42299 |
| Doctor's Eye Patch (Purple) | 42300 |
| Doctor's Eye Patch (Red) | 42301 |
| Doctor's Eye Patch (White) | 42302 |
| Doctor's Eye Patch (Yellow) | 42303 |
| Dog Hat (Spotted) | 43230 |
| Dolphin Runway Tail | 62027 |
| Dolphin Tail Runway Dress | 51738 |
| Dono-Dog Costume | 51717 |
| Dono-Dog Pants | 51874 |
| Dono-Dog Wig | 51531 |
| Donovan Gloves | 62000 |
| Donovan Pants | 51873 |
| Donovan Shirt | 51716 |
| Donovan Tails | 51669 |
| Donovan Wig | 51530 |
| Dragging Wings | 51848 |
| Dragon Onesie Gloves | 62361 |
| Dragon Onesie Hood | 62366 |
| Dragon Onesie Pants | 62378 |
| Dragon Onesie Shirt | 62352 |
| Dragon Onesie Tail | 62343 |
| Dragon Onesie Wings | 62342 |
| Dragoness Horns | 62363 |
| Dragoness Pants | 62375 |
| Dragoness Shirt | 62349 |
| Dragoness Tail | 62339 |
| Dragoness Wings | 62338 |
| Dragonfly Antenna Headband | 7788 |
| Dragonfly Pants | 7583 |
| Dragonfly Shirt | 8510 |
| Dragonfly Wing Cape | 5841 |
| Dreamy Ram Hat | 7641 |
| Dress of Life | 62309 |
| e-Battler Headphones | 7716 |
| e-Battler Uniform Jacket | 7454 |
| e-Battler Uniform Pants | 7539 |
| e-Battler Wig | 7715 |
| Eastern Region Hat | 51582 |
| Eastern Region Jacket | 51768 |
| Eastern Region Pants | 61922 |
| Edgy Pants (Black) | 5553 |
| Edgy Pants (Blue) | 5554 |
| Edgy Pants (Brown) | 5555 |
| Edgy Pants (Gray) | 22077 |
| Edgy Pants (Green) | 5556 |
| Edgy Pants (Orange) | 5557 |
| Edgy Pants (Pink) | 5558 |
| Edgy Pants (Purple) | 5559 |
| Edgy Pants (Red) | 5560 |
| Edgy Pants (White) | 5561 |
| Edgy Pants (Yellow) | 5562 |
| Elder in Training Coat | 51812 |
| Elder in Training Pants | 61965 |
| Elder in Training Wig | 51629 |
| Elder Merchant Cape | 62026 |
| Elder Merchant Pants | 51851 |
| Elder Merchant Shirt | 51690 |
| Elder Merchant Wig | 51503 |
| Elder of the Phoenix Cape | 51907 |
| Elder of the Phoenix Headdress | 51656 |
| Elder of the Phoenix Pants | 61990 |
| Elder of the Phoenix Shirt | 51839 |
| Elegant Bowl Cut | 51597 |
| Elegant Earth Mage Dress | 8538 |
| Elegant Earth Mage Gloves | 7689 |
| Elegant Earth Mage Wig | 7817 |
| Elegant Emerald Armored Gloves | 7687 |
| Elegant Emerald Helm | 7814 |
| Elegant Emerald Pants | 7831 |
| Elegant Emerald Tunic | 8535 |
| Elegant Flowy Pants | 61936 |
| Elegant Flowy Top | 51783 |
| Elegant Halo | 62024 |
| Elegant Queen Dress | 8540 |
| Elegant Queen Gloves | 7691 |
| Elegant Queen Wig | 7819 |
| Elegant Tiara (Black) | 42216 |
| Elegant Tiara (Blue) | 42217 |
| Elegant Tiara (Brown) | 42218 |
| Elegant Tiara (Gray) | 42219 |
| Elegant Tiara (Green) | 42220 |
| Elegant Tiara (Orange) | 42221 |
| Elegant Tiara (Pink) | 42222 |
| Elegant Tiara (Purple) | 42223 |
| Elegant Tiara (Red) | 42224 |
| Elegant Tiara (White) | 42225 |
| Elegant Tiara (Yellow) | 42226 |
| Elios Tiki Mask | 7999 |
| Elite Platinum Boots | 62108 |
| Elite Silver Boots | 62109 |
| Elven Enchanter Cape | 51670 |
| Elven Enchanter Crop Top | 51721 |
| Elven Enchanter Pants | 51878 |
| Elven Enchanter Wig | 51535 |
| Elven Enchantress Gloves | 62001 |
| Elven Enchantress Shirt | 51723 |
| Elven Enchantress Shorts | 51880 |
| Elven Enchantress Wig | 51537 |
| Elven Space Bun Wig | 51577 |
| Elven Space Pants | 61918 |
| Elven Space Shirt | 51763 |
| Elyssia Boots | 62381 |
| Elyssia Dress | 62355 |
| Elyssia Wig | 62369 |
| Emerald Bounty Hunter Armor | 8537 |
| Emerald Bounty Hunter Gloves | 7688 |
| Emerald Bounty Hunter Pants | 7833 |
| Emerald Bounty Hunter Wig | 7816 |
| Emerald Edgy Gloves | 7690 |
| Emerald Edgy Pants | 7830 |
| Emerald Edgy Robe | 8539 |
| Emerald Edgy Wig | 7818 |
| Emerald Otter Boots | 7832 |
| Emerald Otter Mask | 7815 |
| Emerald Robe | 8536 |
| Emo Violinist Pants | 51862 |
| Emo Violinist Shirt | 51701 |
| Emo Violinist Wig | 51514 |
| Enchanted Braided Wig | 51510 |
| Enchanted Overall Pants | 51858 |
| Enchanted Overall Top | 51697 |
| Engineer Gloves | 62003 |
| Engineer Pants | 61923 |
| Engineer Shirt | 51769 |
| Eye Patch (Black) | 42271 |
| Eye Patch (Blue) | 42272 |
| Eye Patch (Brown) | 42273 |
| Eye Patch (Gray) | 42274 |
| Eye Patch (Green) | 42275 |
| Eye Patch (Orange) | 42276 |
| Eye Patch (Pink) | 42277 |
| Eye Patch (Purple) | 42278 |
| Eye Patch (Red) | 42279 |
| Eye Patch (White) | 42280 |
| Eye Patch (Yellow) | 42281 |
| Fake Slug Hat | 5024 |
| Fall Boots | 62065 |
| Fall Dress | 62060 |
| Fall Newsboy Hat | 62057 |
| Fall Sun Hat | 62056 |
| Fall Tights | 62064 |
| Famous Band Pants | 51860 |
| Famous Band Shirt | 51699 |
| Famous Band Wig | 51512 |
| Famous Musician Dress | 51702 |
| Famous Musician Wig | 51515 |
| Fancy Frond Pants | 62323 |
| Fancy Frond Shirt | 62316 |
| Fancy Frond Wig | 62320 |
| Fancy Mage Hat | 62256 |
| Fancy Mage Pants | 62270 |
| Fancy Mage Robe | 62264 |
| Fancy Pants (Black) | 5501 |
| Fancy Pants (Blue) | 22101 |
| Fancy Pants (Brown) | 22102 |
| Fancy Pants (Gray) | 22103 |
| Fancy Pants (Green) | 22104 |
| Fancy Pants (Orange) | 22105 |
| Fancy Pants (Pink) | 22106 |
| Fancy Pants (Purple) | 22107 |
| Fancy Pants (Red) | 22108 |
| Fancy Pants (White) | 22109 |
| Fancy Pants (Yellow) | 22110 |
| Fancy Vest (Black) | 5302 |
| Fancy Vest (Blue) | 7364 |
| Fancy Vest (Brown) | 7365 |
| Fancy Vest (Gray) | 7366 |
| Fancy Vest (Green) | 5350 |
| Fancy Vest (Orange) | 7367 |
| Fancy Vest (Pink) | 7368 |
| Fancy Vest (Purple) | 5351 |
| Fancy Vest (Red) | 7369 |
| Fancy Vest (White) | 7370 |
| Fancy Vest (Yellow) | 7371 |
| Fang Mask | 62088 |
| Fantasy Dress (Green) | 40080 |
| Fashionably Oversized Shirt | 7414 |
| Feather Circlet (Gold Black) | 5144 |
| Feather Circlet (Gold Blue) | 5130 |
| Feather Circlet (Gold Brown) | 5196 |
| Feather Circlet (Gold Gray) | 5197 |
| Feather Circlet (Gold Green) | 5132 |
| Feather Circlet (Gold Orange) | 5145 |
| Feather Circlet (Gold Pink) | 5133 |
| Feather Circlet (Gold Purple) | 5146 |
| Feather Circlet (Gold Red) | 5134 |
| Feather Circlet (Gold White) | 5147 |
| Feather Circlet (Gold Yellow) | 5131 |
| Feather Circlet (Silver Black) | 5148 |
| Feather Circlet (Silver Blue) | 5135 |
| Feather Circlet (Silver Brown) | 5198 |
| Feather Circlet (Silver Gray) | 5199 |
| Feather Circlet (Silver Green) | 5136 |
| Feather Circlet (Silver Orange) | 5149 |
| Feather Circlet (Silver Pink) | 5137 |
| Feather Circlet (Silver Purple) | 5150 |
| Feather Circlet (Silver Red) | 5138 |
| Feather Circlet (Silver White) | 5152 |
| Feather Circlet (Silver Yellow) | 5151 |
| Feather Flight Headband | 51613 |
| Feather Flight Pants | 61951 |
| Feather Flight Tunic | 51798 |
| Feathered Rocker Headpiece | 51513 |
| Feathered Rocker Pants | 51861 |
| Feathered Rocker Shirt | 51700 |
| Field Medic Mask | 51637 |
| Field Medic Pants | 61972 |
| Field Medic Shirt | 51819 |

</details>

<details>
<summary>Field Medic Wig – Hood (Yellow) (300 items)</summary>

| Item name | ID |
| --- | ---: |
| Field Medic Wig | 51636 |
| Fingerless Gloves | 62101 |
| Fire Mage Cape | 51673 |
| Fire Mage Pants | 61909 |
| Fire Mage Shirt | 51754 |
| Fire Mage Wig | 51568 |
| Fire Wizard Hat | 51657 |
| Fire Wizard Pants | 61991 |
| Fire Wizard Shirt | 51840 |
| First Mate Dress | 7391 |
| First Mate Hat | 7609 |
| Fish Hat (Black) | 8153 |
| Fish Hat (Blue) | 8154 |
| Fish Hat (Brown) | 8155 |
| Fish Hat (Gray) | 8156 |
| Fish Hat (Green) | 8157 |
| Fish Hat (Orange) | 8158 |
| Fish Hat (Pink) | 8159 |
| Fish Hat (Purple) | 8160 |
| Fish Hat (Red) | 8161 |
| Fish Hat (White) | 8162 |
| Fish Hat (Yellow) | 8163 |
| Fish Shirt (Black) | 7250 |
| Fish Shirt (Blue) | 5313 |
| Fish Shirt (Brown) | 7251 |
| Fish Shirt (Gray) | 7252 |
| Fish Shirt (Green) | 7253 |
| Fish Shirt (Orange) | 7254 |
| Fish Shirt (Pink) | 7255 |
| Fish Shirt (Purple) | 7256 |
| Fish Shirt (Red) | 7257 |
| Fish Shirt (White) | 7258 |
| Fish Shirt (Yellow) | 7259 |
| Fishy Pirate Pants | 61980 |
| Fishy Pirate Shirt | 51827 |
| Fishy Pirate Wig | 51645 |
| Flame Jester Hat | 7820 |
| Flame Jester Pants | 7834 |
| Flame Jester Shirt | 8542 |
| Flaming Feather Cape | 5849 |
| Flaming Feather Hat | 7822 |
| Flaming Pinstripe Pants | 7835 |
| Flaming Pinstripe Suit Jacket | 8543 |
| Flawless Paper Bag Disguise | 42028 |
| Flightmaster's Wig | 62276 |
| Floppy Rose Sun Hat | 62273 |
| Floral Beach Dress | 7382 |
| Floral Shirt | 7386 |
| Flower Headband (Black) | 42323 |
| Flower Headband (Blue) | 42324 |
| Flower Headband (Brown) | 42325 |
| Flower Headband (Gray) | 42326 |
| Flower Headband (Green) | 42327 |
| Flower Headband (Orange) | 42328 |
| Flower Headband (Pink) | 42329 |
| Flower Headband (Purple) | 42330 |
| Flower Headband (Red) | 42331 |
| Flower Headband (White) | 42332 |
| Flower Headband (Yellow) | 42333 |
| Flower Shirt (Black) | 5340 |
| Flower Shirt (Blue) | 7242 |
| Flower Shirt (Brown) | 7243 |
| Flower Shirt (Gray) | 7244 |
| Flower Shirt (Green) | 5341 |
| Flower Shirt (Orange) | 7245 |
| Flower Shirt (Pink) | 7246 |
| Flower Shirt (Purple) | 5342 |
| Flower Shirt (Red) | 7247 |
| Flower Shirt (White) | 7248 |
| Flower Shirt (Yellow) | 7249 |
| Fluffy Dress (Black) | 40041 |
| Fluffy Dress (Blue) | 40040 |
| Fluffy Dress (Brown) | 40042 |
| Fluffy Dress (Gray) | 40043 |
| Fluffy Dress (Green) | 40044 |
| Fluffy Dress (Orange) | 40045 |
| Fluffy Dress (Pink) | 40046 |
| Fluffy Dress (Purple) | 40047 |
| Fluffy Dress (Red) | 40048 |
| Fluffy Dress (White) | 40049 |
| Fluffy Dress (Yellow) | 40050 |
| Fluffy Feathered Wings | 51846 |
| Fluffy Pet Lover Coat | 8527 |
| Fluffy Pet Lover Pants | 7596 |
| Folded Tight Wings | 51845 |
| Folk Shirt (Black) | 7131 |
| Folk Shirt (Blue) | 7132 |
| Folk Shirt (Brown) | 7133 |
| Folk Shirt (Gray) | 7134 |
| Folk Shirt (Green) | 5307 |
| Folk Shirt (Orange) | 7135 |
| Folk Shirt (Pink) | 7136 |
| Folk Shirt (Purple) | 7137 |
| Folk Shirt (Red) | 7138 |
| Folk Shirt (White) | 7139 |
| Folk Shirt (Yellow) | 7140 |
| Fool's Royal Coat | 51741 |
| Fool's Royal Pants | 51896 |
| Fool's Royal Wig | 51555 |
| Formal Elven Pants | 61919 |
| Formal Elven Top Hat | 51578 |
| Formal Elven Vest | 51764 |
| Formal Gloves (White) | 43020 |
| Frightening Mask | 62120 |
| Frilly Apron Skirt | 51903 |
| Frilly Apron Top | 51748 |
| Frog Hood | 8222 |
| Frog Pal (Black) | 42205 |
| Frog Pal (Blue) | 42206 |
| Frog Pal (Brown) | 42207 |
| Frog Pal (Gray) | 42208 |
| Frog Pal (Green) | 42209 |
| Frog Pal (Orange) | 42210 |
| Frog Pal (Pink) | 42211 |
| Frog Pal (Purple) | 42212 |
| Frog Pal (Red) | 42213 |
| Frog Pal (White) | 42214 |
| Frog Pal (Yellow) | 42215 |
| Froggy Dress | 7402 |
| Froggy Hat (Black) | 42120 |
| Froggy Hat (Blue) | 42121 |
| Froggy Hat (Brown) | 42122 |
| Froggy Hat (Gray) | 42123 |
| Froggy Hat (Green) | 42124 |
| Froggy Hat (Orange) | 42125 |
| Froggy Hat (Pink) | 42126 |
| Froggy Hat (Purple) | 42127 |
| Froggy Hat (Red) | 42128 |
| Froggy Hat (White) | 42129 |
| Froggy Hat (Yellow) | 42130 |
| Froggy Overall Bottoms | 7515 |
| Froggy Overall Top | 7407 |
| Fur Lined Boots | 7523 |
| Fur Lined Vest | 7437 |
| Galaxy Halo | 7782 |
| Galaxy Wig | 7777 |
| Galaxy Witch Hat | 7780 |
| Garden Party Dress | 62315 |
| Garden Party Hat | 62319 |
| Gardening Dress | 62036 |
| Gardening Hat | 62032 |
| Gardening Slippers | 62040 |
| Gas Mask (Black) | 42181 |
| Gas Mask (Blue) | 42182 |
| Gas Mask (Brown) | 42183 |
| Gas Mask (Gray) | 42184 |
| Gas Mask (Green) | 42185 |
| Gas Mask (Orange) | 42186 |
| Gas Mask (Pink) | 42187 |
| Gas Mask (Purple) | 42188 |
| Gas Mask (Red) | 42189 |
| Gas Mask (White) | 42190 |
| Gas Mask (Yellow) | 42191 |
| Gear Grinder Chestplate | 62288 |
| Gear Grinder Gloves | 62292 |
| Gear Grinder Legs | 62304 |
| Gear Grinder Mask | 62297 |
| Gear Maiden Wig | 62280 |
| Generic Pants (Black) | 5563 |
| Generic Pants (Blue) | 5564 |
| Generic Pants (Brown) | 5565 |
| Generic Pants (Gray) | 22078 |
| Generic Pants (Green) | 5566 |
| Generic Pants (Orange) | 5567 |
| Generic Pants (Pink) | 5568 |
| Generic Pants (Purple) | 5569 |
| Generic Pants (Red) | 5570 |
| Generic Pants (White) | 5571 |
| Generic Pants (Yellow) | 5572 |
| Generic Shirt (Red) | 40300 |
| Ghost Costume Gloves | 7654 |
| Ghost Costume Mask | 7619 |
| Ghost Costume Robe | 7422 |
| Gilded Pauldrons | 51735 |
| Gilded Skirt | 51892 |
| Gilded Updo Wig | 51549 |
| Gladiator's Chest | 62174 |
| Glimmering Sprout Pants | 51877 |
| Glimmering Sprout Shirt | 51720 |
| Glimmering Sprout Wig | 51534 |
| Gloves of the Dead | 62310 |
| Goggles (Black) | 42227 |
| Goggles (Blue) | 42228 |
| Goggles (Brown) | 42229 |
| Goggles (Gray) | 42230 |
| Goggles (Green) | 42231 |
| Goggles (Orange) | 42232 |
| Goggles (Pink) | 42233 |
| Goggles (Purple) | 42234 |
| Goggles (Red) | 42235 |
| Goggles (White) | 42236 |
| Goggles (Yellow) | 42237 |
| Gold Chef Hat | 8197 |
| Gold Embossed Shirt | 62099 |
| Gold X Shirt | 62100 |
| Golden Feather Winged Cape | 5834 |
| Golden Gloves | 7652 |
| Golden King Pants | 62144 |
| Golden King Shirt | 62136 |
| Golden Leaf Crown | 42131 |
| Golden Princess Dress | 62139 |
| Golden Princess Gloves | 62158 |
| Golden Princess Wig | 62131 |
| Golden Ram Horns | 7615 |
| Golden Silk Scarf | 5835 |
| Golden Spooky Silk Robes | 7418 |
| Graffiti Artist Boots | 62107 |
| Graffiti Artist Helmet | 62089 |
| Graffiti Artist Shirt | 62098 |
| Grand Tree Shirt | 51813 |
| Grand Tree Skirt | 61966 |
| Grand Tree Vine Headband | 51630 |
| Gray Cape | 5804 |
| Great Detective Dress | 62356 |
| Great Detective Pants | 62382 |
| Great Detective Tail | 62345 |
| Great Detective Wig | 62370 |
| Great Detective Wings | 62344 |
| Green Cape | 5801 |
| Green Gloves | 5704 |
| Hair Roller Wig | 7823 |
| Hakama (Black) | 7372 |
| Hakama (Blue) | 7373 |
| Hakama (Brown) | 7374 |
| Hakama (Gray) | 7375 |
| Hakama (Green) | 7376 |
| Hakama (Orange) | 7377 |
| Hakama (Pink) | 7378 |
| Hakama (Purple) | 7379 |
| Hakama (Red) | 40200 |
| Hakama (White) | 7380 |
| Hakama (Yellow) | 7381 |
| Happy Pumpkin Hat | 7621 |
| Healing Touch Dress | 51818 |
| Healing Touch Fingerless Gloves | 62010 |
| Healing Touch Sandals | 61971 |
| Healing Touch Wig | 51635 |
| Heart Shirt (Black) | 7281 |
| Heart Shirt (Blue) | 7282 |
| Heart Shirt (Brown) | 7283 |
| Heart Shirt (Gray) | 7284 |
| Heart Shirt (Green) | 7285 |
| Heart Shirt (Orange) | 7286 |
| Heart Shirt (Pink) | 5318 |
| Heart Shirt (Purple) | 7287 |
| Heart Shirt (Red) | 7288 |
| Heart Shirt (White) | 7289 |
| Heart Shirt (Yellow) | 7290 |
| Heroic Champion Chest | 62173 |
| Heroic Champion Sandals | 62177 |
| Hidden Magic Hood Wig | 51536 |
| Hidden Magic Hoodie | 51722 |
| Hidden Magic Shorts | 51879 |
| High Kanzashi Bun Wig | 7811 |
| High Mage Cape | 62281 |
| High Mage Crest | 62250 |
| High Mage Dress | 62258 |
| High Sea Loops Wig | 51607 |
| High Sea Shirt | 51793 |
| High Sea Skirt | 61946 |
| High Society Cap | 62255 |
| High Society Pants | 62269 |
| High Society Vest | 62263 |
| Historian Gloves | 62007 |
| Historian Pants | 61967 |
| Historian Poncho | 51814 |
| Historian Wig | 51631 |
| Historian's Pants | 62410 |
| Historian's Shirt | 62388 |
| Historian's Sunglasses | 62398 |
| Historic Investigator Coat | 62393 |
| Historic Investigator Hat | 62404 |
| Historic Investigator Skirt | 62415 |
| Historically Accurate Shirt | 62392 |
| Historically Accurate Skirt | 62414 |
| Historically Accurate Wig | 62403 |
| Holiday Dress (Black) | 40261 |
| Holiday Dress (Blue) | 40262 |
| Holiday Dress (Brown) | 40263 |
| Holiday Dress (Gray) | 40264 |
| Holiday Dress (Green) | 40265 |
| Holiday Dress (Orange) | 40266 |
| Holiday Dress (Pink) | 40267 |
| Holiday Dress (Purple) | 40268 |
| Holiday Dress (Red) | 40260 |
| Holiday Dress (White) | 40269 |
| Holiday Dress (Yellow) | 40270 |
| Home Made Hoodie | 51743 |
| Homemade Pants | 51898 |
| Hood (Black) | 8081 |
| Hood (Blue) | 8082 |
| Hood (Brown) | 8083 |
| Hood (Gray) | 8084 |
| Hood (Green) | 8085 |
| Hood (Orange) | 8086 |
| Hood (Pink) | 8087 |
| Hood (Purple) | 8088 |
| Hood (Red) | 8089 |
| Hood (White) | 8090 |
| Hood (Yellow) | 8091 |

</details>

<details>
<summary>Hooded Traveler Cape – Moon Dress (White) (300 items)</summary>

| Item name | ID |
| --- | ---: |
| Hooded Traveler Cape | 51671 |
| Hooded Traveler Shirt | 51734 |
| Hooded Traveler Skirt | 51891 |
| Hooded Traveler Wig | 51548 |
| Hoodie (Black) | 7025 |
| Hoodie (Blue) | 5372 |
| Hoodie (Brown) | 7336 |
| Hoodie (Gray) | 5373 |
| Hoodie (Green) | 7026 |
| Hoodie (Orange) | 5374 |
| Hoodie (Pink) | 7027 |
| Hoodie (Purple) | 7028 |
| Hoodie (Red) | 5375 |
| Hoodie (White) | 7029 |
| Hoodie (Yellow) | 5376 |
| Horn Headband (Black) | 42159 |
| Horn Headband (Blue) | 42160 |
| Horn Headband (Brown) | 42161 |
| Horn Headband (Gray) | 42162 |
| Horn Headband (Green) | 42163 |
| Horn Headband (Orange) | 42164 |
| Horn Headband (Pink) | 42165 |
| Horn Headband (Purple) | 42166 |
| Horn Headband (Red) | 42167 |
| Horn Headband (White) | 42168 |
| Horn Headband (Yellow) | 42169 |
| Hot Dog Hat | 8020 |
| Huge Snaccoon Pal Wig | 62113 |
| Huge Snaccoon Pigtails Wig | 62112 |
| Ice Cream Dress (Blue) | 7469 |
| Ice Cream Dress (Pink) | 7467 |
| Ice Cream Gloves | 7667 |
| Ice Cream Hat (Black) | 8010 |
| Ice Cream Hat (Blue) | 8011 |
| Ice Cream Hat (Brown) | 8012 |
| Ice Cream Hat (Gray) | 8129 |
| Ice Cream Hat (Green) | 8013 |
| Ice Cream Hat (Orange) | 8014 |
| Ice Cream Hat (Pink) | 8016 |
| Ice Cream Hat (Purple) | 8015 |
| Ice Cream Hat (Red) | 8017 |
| Ice Cream Hat (White) | 8018 |
| Ice Cream Hat (Yellow) | 8019 |
| Ice Cream Leggings (Pink) | 7552 |
| Ice Cream Twin Tail Wig (Blue) | 7757 |
| Ice Cream Twin Tail Wig (Pink) | 7755 |
| Ice Fist Helmet | 7744 |
| Ice Spike Buns Wig | 7742 |
| Improved Paper Bag Disguise | 42027 |
| Inaugural Archmage Pants | 61912 |
| Inaugural Archmage Robe | 51757 |
| Inaugural Archmage Wig | 51571 |
| Ingenious Dress | 62285 |
| Ingenious Top Hat | 62295 |
| Innocent Flower Shirt | 62175 |
| Innocent Flower Skirt | 62182 |
| Innocent Flower Wig | 62186 |
| Inventor Dress | 62262 |
| Inventor Goggles | 62254 |
| Iris Shirt | 51719 |
| Iris Skirt | 51876 |
| Iris Wig | 51533 |
| Island Boots | 62055 |
| Island Hat | 62047 |
| Island Shirt | 62051 |
| Jellyfish Dress | 8504 |
| Jellyfish Hat | 7773 |
| Jester Hat (Black) | 8021 |
| Jester Hat (Green) | 8023 |
| Jester Hat (Pink) | 8022 |
| Jester Shirt (Green) | 7186 |
| Jester Shirt (Pink) | 7187 |
| Jester Shirt (Red) | 5309 |
| Jester Shirt (White) | 7189 |
| Jester Shirt (Yellow) | 7188 |
| Jet Black Kimono | 8532 |
| Jun Hanbok | 51724 |
| Jun Pants | 51881 |
| Jun Wig | 51538 |
| Kai Pants | 51887 |
| Kai Snake Shirt | 51730 |
| Kai Wig | 51544 |
| Kanmuri Wig | 7810 |
| Karish Shirt | 51740 |
| Karish Shorts | 51895 |
| Karish Wig | 51554 |
| Kelp Wig | 42060 |
| Kimono (Black) | 40021 |
| Kimono (Blue) | 40022 |
| Kimono (Brown) | 40023 |
| Kimono (Gray) | 40024 |
| Kimono (Green) | 40025 |
| Kimono (Orange) | 40026 |
| Kimono (Pink) | 40027 |
| Kimono (Purple) | 40028 |
| Kimono (Red) | 40020 |
| Kimono (White) | 40029 |
| Kimono (Yellow) | 40030 |
| King of the Merchants Pants | 51852 |
| King of the Merchants Shirt | 51691 |
| King of the Merchants Wig | 51504 |
| Kitty Bandeau | 8524 |
| Kitty Ear Headband | 7802 |
| Kitty Gloves | 7685 |
| Kitty Mascot Head | 7799 |
| Kitty Mascot Robe | 8521 |
| Kitty Paw Skirt | 7594 |
| Kitty Pop Pants | 51902 |
| Kitty Pop Shirt | 51747 |
| Kitty Pop Wig | 51561 |
| Kitty Shirt | 51745 |
| Kitty Skirt | 51900 |
| Kitty Tail | 51672 |
| Kitty Wig | 51559 |
| Knightly Wig | 51603 |
| Knitted Cap | 62069 |
| Knitted Winter Sweater | 62073 |
| Kraken Eye Wig | 51552 |
| Leaf Cape | 5827 |
| Letterman Jacket (Black) | 7036 |
| Letterman Jacket (Blue) | 5322 |
| Letterman Jacket (Brown) | 7330 |
| Letterman Jacket (Gray) | 7331 |
| Letterman Jacket (Green) | 7037 |
| Letterman Jacket (Orange) | 7038 |
| Letterman Jacket (Pink) | 7039 |
| Letterman Jacket (Purple) | 7040 |
| Letterman Jacket (Red) | 7041 |
| Letterman Jacket (White) | 7042 |
| Letterman Jacket (Yellow) | 7043 |
| Liam Shirt | 51752 |
| Liam Shorts | 61907 |
| Liam Wig | 51566 |
| Light Brown Slacks | 7514 |
| Lily Blossom Cape | 5845 |
| Lily Blossom Hat | 7795 |
| Lily Blossom Pants | 7589 |
| Lily Blossom Robe | 8517 |
| Lilypad Cape | 5824 |
| Lilypad Dress | 7429 |
| Lilypad Hat | 7628 |
| Long Elvish Twintails Wig | 7760 |
| Long Green Striped Sweater | 7408 |
| Long Sleeve Crop Striped Sweater | 7409 |
| Long Sleeve Shirt (Black) | 7079 |
| Long Sleeve Shirt (Blue) | 7080 |
| Long Sleeve Shirt (Brown) | 7081 |
| Long Sleeve Shirt (Gray) | 7335 |
| Long Sleeve Shirt (Green) | 7082 |
| Long Sleeve Shirt (Orange) | 7083 |
| Long Sleeve Shirt (Pink) | 7084 |
| Long Sleeve Shirt (Purple) | 7085 |
| Long Sleeve Shirt (Red) | 7086 |
| Long Sleeve Shirt (White) | 7087 |
| Long Sleeve Shirt (Yellow) | 7088 |
| Long Tuxedo (Black) | 5377 |
| Long Tuxedo (Blue) | 7161 |
| Long Tuxedo (Brown) | 7162 |
| Long Tuxedo (Gray) | 7163 |
| Long Tuxedo (Green) | 5378 |
| Long Tuxedo (Orange) | 7164 |
| Long Tuxedo (Pink) | 7165 |
| Long Tuxedo (Purple) | 7166 |
| Long Tuxedo (Red) | 5379 |
| Long Tuxedo (White) | 5380 |
| Long Tuxedo (Yellow) | 7167 |
| Loose Wavy Bun Wig | 51501 |
| Loose Wavy Cape | 62025 |
| Loose Wavy Pants | 51849 |
| Loose Wavy Shirt | 51688 |
| Lost Bloom Jacket | 62395 |
| Lost Bloom Pants | 62417 |
| Lost Bloom Scarf | 62407 |
| Lost Bloom Wig | 62406 |
| Lost King's Sandals | 62180 |
| Lost King's Toga | 62171 |
| Lost Musician Dress | 51704 |
| Lost Musician Veil Wig | 51517 |
| Lost Seedling Coat | 62390 |
| Lost Seedling Pants | 62412 |
| Lost Seedling Scarf | 62401 |
| Lost Seedling Wig | 62400 |
| Lotus Clip | 7629 |
| Lotus Kimono | 7430 |
| Lover's Kiss Dress | 62169 |
| Lover's Kiss Tiara | 62184 |
| Lover's Kiss Wig | 62188 |
| Lucia Cape | 62028 |
| Lucia Pants | 61914 |
| Lucia Shirt | 51759 |
| Lucia Wig | 51573 |
| Lucius Shirt | 51761 |
| Lucius Shoes | 61916 |
| Lucius Wig | 51575 |
| Lynn Gloves | 62004 |
| Lynn Pants | 61924 |
| Lynn Shirt | 51770 |
| Lynn Wig | 51584 |
| Mage Master Coat | 51756 |
| Mage Master Pants | 61911 |
| Mage Master Wig | 51570 |
| Mage Student Pants | 61910 |
| Mage Student Shirt | 51755 |
| Mage Student Wig | 51569 |
| Magic Circlet (Black) | 5116 |
| Magic Circlet (Blue) | 5117 |
| Magic Circlet (Brown) | 5125 |
| Magic Circlet (Gray) | 5126 |
| Magic Circlet (Green) | 5112 |
| Magic Circlet (Orange) | 5113 |
| Magic Circlet (Pink) | 5118 |
| Magic Circlet (Purple) | 5115 |
| Magic Circlet (Red) | 5114 |
| Magic Circlet (White) | 5119 |
| Magic Circlet (Yellow) | 5120 |
| Magic Gloves | 5711 |
| Magic Shirt (Black) | 7051 |
| Magic Shirt (Blue) | 7052 |
| Magic Shirt (Brown) | 5335 |
| Magic Shirt (Gray) | 7332 |
| Magic Shirt (Green) | 5333 |
| Magic Shirt (Orange) | 5334 |
| Magic Shirt (Pink) | 7053 |
| Magic Shirt (Purple) | 5336 |
| Magic Shirt (Red) | 5332 |
| Magic Shirt (White) | 7054 |
| Magic Shirt (Yellow) | 7055 |
| Magic Skirt (Black) | 5593 |
| Magic Skirt (Blue) | 5512 |
| Magic Skirt (Brown) | 5594 |
| Magic Skirt (Gray) | 5598 |
| Magic Skirt (Green) | 5513 |
| Magic Skirt (Orange) | 5514 |
| Magic Skirt (Pink) | 5595 |
| Magic Skirt (Purple) | 5516 |
| Magic Skirt (Red) | 5515 |
| Magic Skirt (White) | 5596 |
| Magic Skirt (Yellow) | 5597 |
| Majestic Cape | 5812 |
| Mantis Antenna Headband | 7790 |
| Mantis Cloak | 8512 |
| Mantis Pants | 7584 |
| Mask of the Dead | 62311 |
| Matey Pants | 7504 |
| Matey Shirt | 7392 |
| Mechanical Pilot Coat | 62289 |
| Mechanical Pilot Helmet | 62298 |
| Mechanical Pilot Pants | 62305 |
| Medic's Gloves | 62009 |
| Medic's Pants | 61969 |
| Medic's Shirt | 51816 |
| Medic's Twintail Wig | 51633 |
| Member of the Gear Cape | 62283 |
| Member of the Gear Hood | 62294 |
| Member of the Gear Pants | 62301 |
| Member of the Gear Shirt | 62284 |
| Mermaid Crown | 7771 |
| Mermaid Dress | 8502 |
| Messenger Cape | 62231 |
| Messenger Crown | 62183 |
| Messenger Toga | 62166 |
| Messy Doll Hair Wig | 7770 |
| Messy Short Wig | 51595 |
| Metal Dragon Chest Plate | 7443 |
| Metal Dragon Greaves | 7529 |
| Metal Dragon Helm | 7648 |
| Metal Gladiator Helm | 7646 |
| Metal Gladiator Shirt | 7441 |
| Metal Gladiator Shorts | 7527 |
| Metal Opera Dress | 7446 |
| Metal Opera Tiara | 7701 |
| Metal Skull Chestplate | 7445 |
| Metal Skull Greaves | 7531 |
| Metal Skull Mask | 7700 |
| Milkmaid Dress | 62330 |
| Milkmaid Shoes | 62334 |
| Milkmaid Wig | 62326 |
| Mod Demon Pants | 62103 |
| Mod Demon Shirt (Blue) | 62094 |
| Mod Demon Shirt (Green) | 62093 |
| Mod Demon Wig (Blue) | 62083 |
| Mod Demon Wig (Green) | 62082 |
| Monster Boots | 62106 |
| Monster Crop Top | 62096 |
| Monster Gogo Boots | 62105 |
| Monster Wing Wig | 62086 |
| Monster Workout Shirt | 62097 |
| Monster Workout Wig | 62087 |
| Moon Crest | 7783 |
| Moon Dress | 40000 |
| Moon Dress (Black) | 40001 |
| Moon Dress (Blue) | 40002 |
| Moon Dress (Brown) | 40003 |
| Moon Dress (Gray) | 40004 |
| Moon Dress (Green) | 40005 |
| Moon Dress (Orange) | 40006 |
| Moon Dress (Pink) | 40007 |
| Moon Dress (Purple) | 40008 |
| Moon Dress (Red) | 40009 |
| Moon Dress (White) | 40010 |

</details>

<details>
<summary>Moon Dress (Yellow) – Pop Sensation Emo Wig (300 items)</summary>

| Item name | ID |
| --- | ---: |
| Moon Dress (Yellow) | 40011 |
| Moon Elf Pants | 61917 |
| Moon Elf Pleather Hat | 51576 |
| Moon Elf Sweater | 51762 |
| Moon Forehead Marking | 7786 |
| Moon Shirt (Black) | 7017 |
| Moon Shirt (Blue) | 7018 |
| Moon Shirt (Brown) | 7340 |
| Moon Shirt (Gray) | 7341 |
| Moon Shirt (Green) | 7019 |
| Moon Shirt (Orange) | 7020 |
| Moon Shirt (Pink) | 7021 |
| Moon Shirt (Purple) | 5316 |
| Moon Shirt (Red) | 7022 |
| Moon Shirt (White) | 7023 |
| Moon Shirt (Yellow) | 7024 |
| Moon Temple Dress | 51765 |
| Moon Temple Headband | 51579 |
| Moon Temple Shoes | 62030 |
| Moonlight Cape | 5806 |
| Morning Dew Dress | 51718 |
| Morning Dew Shoes | 51875 |
| Morning Dew Wig | 51532 |
| Moth Antenna Headband | 7796 |
| Moth Chest Plate | 8518 |
| Moth Grieves | 7590 |
| Moth Wing Cape | 5846 |
| Muscle Shirt (Brown) | 5365 |
| Muscle Shirt (Gray) | 5368 |
| Muscle Shirt (Orange) | 5367 |
| Muscle Shirt (White) | 5366 |
| Mush Hat | 7611 |
| Mushette Hat | 7613 |
| Mushroom Baggy Pants | 7511 |
| Mushroom Coat | 7405 |
| Mushroom Dress | 7406 |
| Mushroom Dress Coat | 7401 |
| Mushroom Hat (Black) | 8070 |
| Mushroom Hat (Blue) | 8071 |
| Mushroom Hat (Brown) | 8072 |
| Mushroom Hat (Gray) | 8073 |
| Mushroom Hat (Green) | 8074 |
| Mushroom Hat (Orange) | 8075 |
| Mushroom Hat (Pink) | 8076 |
| Mushroom Hat (Purple) | 8077 |
| Mushroom Hat (Red) | 8078 |
| Mushroom Hat (White) | 8079 |
| Mushroom Hat (Yellow) | 8080 |
| Mushroom Jersey | 62061 |
| Mushroom Slacks | 7513 |
| Mushroom Sweater | 7403 |
| Mushroom Vest | 7410 |
| Mushroom Vest Dress | 7411 |
| Mushroom Witch Hat | 7612 |
| Music Note Shirt (Black) | 5312 |
| Music Note Shirt (Blue) | 7291 |
| Music Note Shirt (Brown) | 7292 |
| Music Note Shirt (Gray) | 7293 |
| Music Note Shirt (Green) | 7294 |
| Music Note Shirt (Orange) | 7295 |
| Music Note Shirt (Pink) | 7296 |
| Music Note Shirt (Purple) | 7297 |
| Music Note Shirt (Red) | 7298 |
| Music Note Shirt (White) | 7299 |
| Music Note Shirt (Yellow) | 7300 |
| Musical Maid Dress | 51705 |
| Musical Maid Headdress | 51518 |
| Musical Maid Shoes | 51864 |
| Nathaniel Wig | 51600 |
| Nature Prince Cape | 51665 |
| Nature Prince Gloves | 61996 |
| Nature Prince Pants | 51857 |
| Nature Prince Shirt | 51696 |
| Nature Witch Boots | 51854 |
| Nature Witch Dress | 51693 |
| Nature Witch Pigtail Wig | 51506 |
| Nature's Gift Headdress | 51614 |
| Nature's Gift Pants | 61952 |
| Nature's Gift Shirt | 51799 |
| Nel'Varian Fall Feather | 51616 |
| Nel'Varian Fall Shirt | 51801 |
| Nel'Varian Fall Skirt | 61954 |
| Neon Punk Shirt | 62095 |
| Neon Punk Skirt | 62104 |
| Neon Punk Wig | 62084 |
| Newly Invented Goggles | 62296 |
| Newly Invented Pants | 62303 |
| Newly Invented Shirt | 62287 |
| Nurse Dress | 51820 |
| Nurse Gloves | 62012 |
| Nurse Shoes | 61973 |
| Nurse Wig | 51638 |
| Nya Pants | 51901 |
| Nya Shirt | 51746 |
| Nya Wig | 51560 |
| Ocean Beauty Dress | 51830 |
| Ocean Beauty Wig | 51648 |
| Oceanic Desert Dweller Shirt | 51732 |
| Oceanic Desert Dweller Skirt | 51889 |
| Oceanic Desert Dweller Wig | 51546 |
| Octopus Dress | 7385 |
| Octopus Hat | 7775 |
| Officer Uniform Shirt | 5314 |
| Orange Cape | 5802 |
| Orange Gloves | 5705 |
| Orange Tiger Pants | 61944 |
| Orange Tiger Shirt | 51791 |
| Orange Tiger Tail | 51676 |
| Orange Tiger Wig | 51605 |
| Orange Tigress Skirt | 61948 |
| Orange Tigress Tail | 51678 |
| Orange Tigress Top | 51795 |
| Orange Tigress Wig | 51609 |
| Overall Pants | 22111 |
| Overall Top | 5397 |
| Oversized Winter Sweater | 62072 |
| Pants of the Dead | 62313 |
| Paper Bag Disguise | 42026 |
| Paper Mache Skeleton Hat | 7625 |
| Party Hat (Black) | 8059 |
| Party Hat (Blue) | 8060 |
| Party Hat (Brown) | 8061 |
| Party Hat (Gray) | 8062 |
| Party Hat (Green) | 8063 |
| Party Hat (Orange) | 8064 |
| Party Hat (Pink) | 8065 |
| Party Hat (Purple) | 8066 |
| Party Hat (Red) | 8067 |
| Party Hat (White) | 8068 |
| Party Hat (Yellow) | 8069 |
| Pastel Skirt (Black) | 5583 |
| Pastel Skirt (Blue) | 5584 |
| Pastel Skirt (Brown) | 5585 |
| Pastel Skirt (Gray) | 22075 |
| Pastel Skirt (Green) | 5586 |
| Pastel Skirt (Orange) | 5587 |
| Pastel Skirt (Pink) | 5588 |
| Pastel Skirt (Purple) | 5589 |
| Pastel Skirt (Red) | 5590 |
| Pastel Skirt (White) | 5591 |
| Pastel Skirt (Yellow) | 5592 |
| Patched Bucket Hat | 62059 |
| Patched Pants (Black) | 22040 |
| Patched Pants (Blue) | 22041 |
| Patched Pants (Brown) | 22042 |
| Patched Pants (Gray) | 22043 |
| Patched Pants (Green) | 22044 |
| Patched Pants (Orange) | 22045 |
| Patched Pants (Pink) | 22046 |
| Patched Pants (Purple) | 22047 |
| Patched Pants (Red) | 22048 |
| Patched Pants (White) | 22049 |
| Patched Pants (Yellow) | 22050 |
| Paw Shirt (Black) | 7123 |
| Paw Shirt (Blue) | 5359 |
| Paw Shirt (Brown) | 7124 |
| Paw Shirt (Gray) | 7125 |
| Paw Shirt (Green) | 5357 |
| Paw Shirt (Orange) | 5360 |
| Paw Shirt (Pink) | 7126 |
| Paw Shirt (Purple) | 7127 |
| Paw Shirt (Red) | 7128 |
| Paw Shirt (White) | 5382 |
| Paw Shirt (Yellow) | 5358 |
| Peace Cape | 5831 |
| Peasant Sailor Pants | 7509 |
| Peasant Sailor Shirt | 7397 |
| Petal Shirt (Pink) | 7089 |
| Petal Shirt (Black) | 7000 |
| Petal Shirt (Brown) | 7342 |
| Petal Shirt (Gray) | 7343 |
| Petal Shirt (Green) | 7001 |
| Petal Shirt (Orange) | 7002 |
| Petal Shirt (Purple) | 7003 |
| Petal Shirt (Red) | 7004 |
| Petal Shirt (Teal) | 7005 |
| Petal Shirt (White) | 7006 |
| Petal Shirt (Yellow) | 7007 |
| Petal Skirt (Black) | 5410 |
| Petal Skirt (Brown) | 22008 |
| Petal Skirt (Gray) | 22002 |
| Petal Skirt (Green) | 22003 |
| Petal Skirt (Orange) | 22004 |
| Petal Skirt (Pink) | 5505 |
| Petal Skirt (Purple) | 22005 |
| Petal Skirt (Red) | 22006 |
| Petal Skirt (Teal) | 5411 |
| Petal Skirt (White) | 22007 |
| Petal Skirt (Yellow) | 5412 |
| Phantom Monster Cape | 51667 |
| Phantom Monster Mask | 51524 |
| Phantom Monster Pants | 51868 |
| Phantom Monster Shirt | 51710 |
| Phoenix Caretaker Hat | 51908 |
| Phoenix Caretaker Pants | 61987 |
| Phoenix Caretaker Shirt | 51836 |
| Phoenix Guardian Cape | 51906 |
| Phoenix Guardian Chest | 51834 |
| Phoenix Guardian Helm | 51652 |
| Phoenix Guardian Pants | 61985 |
| Phoenix Prince Crown | 51654 |
| Phoenix Prince Pants | 61988 |
| Phoenix Prince Shirt | 51837 |
| Phoenix Princess Boots | 61986 |
| Phoenix Princess Dress | 51835 |
| Phoenix Princess Headband | 51653 |
| Phoenix Princess Tail | 51686 |
| Phoenix Queen Crest | 51660 |
| Phoenix Queen Dress | 51843 |
| Pink Bathrobe | 8547 |
| Pink Bubble Cover Up | 8545 |
| Pink Cape | 5817 |
| Pink Gloves | 5706 |
| Pink Kitty Beanie | 7798 |
| Pink Kitty Boots | 7592 |
| Pink Kitty Hood | 7808 |
| Pink Kitty Pants | 7598 |
| Pink Kitty Shirt | 8529 |
| Pink Kitty Sweater Dress | 8520 |
| Pink Kitty Sweater Mittens | 7683 |
| Pink Snow Yeti Coat | 8550 |
| Pink Snow Yeti Pants | 7837 |
| Pink Snow Yeti Wig | 7826 |
| Pirate Captain Hat | 7604 |
| Pirate Coat | 7393 |
| Pirate Dress (Black) | 40061 |
| Pirate Dress (Blue) | 40062 |
| Pirate Dress (Brown) | 40063 |
| Pirate Dress (Gray) | 40064 |
| Pirate Dress (Green) | 40065 |
| Pirate Dress (Orange) | 40066 |
| Pirate Dress (Pink) | 40067 |
| Pirate Dress (Purple) | 40068 |
| Pirate Dress (Red) | 40060 |
| Pirate Dress (White) | 40069 |
| Pirate Dress (Yellow) | 40070 |
| Pirate Hat (Black) | 8000 |
| Pirate Hat (Blue) | 8001 |
| Pirate Hat (Brown) | 8002 |
| Pirate Hat (Gray) | 8035 |
| Pirate Hat (Green) | 8003 |
| Pirate Hat (Orange) | 8004 |
| Pirate Hat (Pink) | 8005 |
| Pirate Hat (Purple) | 8006 |
| Pirate Hat (Red) | 8007 |
| Pirate Hat (White) | 8008 |
| Pirate Hat (Yellow) | 8009 |
| Pirate Pants | 7505 |
| Polkadot Shirt (Black) | 7210 |
| Polkadot Shirt (Brown) | 7211 |
| Polkadot Shirt (Gray) | 7212 |
| Polkadot Shirt (Green) | 7213 |
| Polkadot Shirt (Orange) | 7214 |
| Polkadot Shirt (Pink) | 7215 |
| Polkadot Shirt (Purple) | 7216 |
| Polkadot Shirt (Red) | 5329 |
| Polkadot Shirt (Teal) | 7217 |
| Polkadot Shirt (White) | 7218 |
| Polkadot Shirt (Yellow) | 7219 |
| Pom Pom Hat | 62068 |
| Poofy Pants (Black) | 22029 |
| Poofy Pants (Blue) | 22030 |
| Poofy Pants (Brown) | 22031 |
| Poofy Pants (Gray) | 22032 |
| Poofy Pants (Green) | 22033 |
| Poofy Pants (Orange) | 22034 |
| Poofy Pants (Pink) | 22035 |
| Poofy Pants (Purple) | 22036 |
| Poofy Pants (Red) | 22037 |
| Poofy Pants (White) | 22038 |
| Poofy Pants (Yellow) | 22039 |
| Poofy Shirt (Black) | 5339 |
| Poofy Shirt (Brown) | 7311 |
| Poofy Shirt (Gray) | 7312 |
| Poofy Shirt (Green) | 7313 |
| Poofy Shirt (Orange) | 7314 |
| Poofy Shirt (Pink) | 7315 |
| Poofy Shirt (Purple) | 5338 |
| Poofy Shirt (Red) | 7316 |
| Poofy Shirt (Teal) | 7317 |
| Poofy Shirt (White) | 7318 |
| Poofy Shirt (Yellow) | 7319 |
| Pop Sensation Cool Gloves | 7672 |
| Pop Sensation Cool Hat | 7721 |
| Pop Sensation Cool Jacket | 7482 |
| Pop Sensation Cool Pants | 7563 |
| Pop Sensation Cool Wig | 7732 |
| Pop Sensation Cute Gloves | 7673 |
| Pop Sensation Cute Microphone | 7727 |
| Pop Sensation Cute Shirt | 7483 |
| Pop Sensation Cute Skirt | 7564 |
| Pop Sensation Dancer Gloves | 7674 |
| Pop Sensation Dancer Pants | 7565 |
| Pop Sensation Dancer Shirt | 7484 |
| Pop Sensation Dancer Wig | 7730 |
| Pop Sensation Emo Gloves | 7675 |
| Pop Sensation Emo Headgear | 7728 |
| Pop Sensation Emo Jacket | 7485 |
| Pop Sensation Emo Pants | 7566 |
| Pop Sensation Emo Wig | 7735 |

</details>

<details>
<summary>Pop Sensation Heart Barrette – Slash Tank Top (Red) (300 items)</summary>

| Item name | ID |
| --- | ---: |
| Pop Sensation Heart Barrette | 7722 |
| Pop Sensation Heartthrob Gloves | 7676 |
| Pop Sensation Heartthrob Horns | 7724 |
| Pop Sensation Heartthrob Pants | 7567 |
| Pop Sensation Heartthrob Shirt | 7486 |
| Pop Sensation Heartthrob Tail | 5839 |
| Pop Sensation Heartthrob Wig | 7736 |
| Pop Sensation Lead Skirt | 7568 |
| Pop Sensation Lead Sweater | 7487 |
| Pop Sensation Lead Wig | 7729 |
| Pop Sensation Performance Gloves | 7677 |
| Pop Sensation Performance Microphone | 7726 |
| Pop Sensation Performance Pants | 7569 |
| Pop Sensation Performance Shirt | 7488 |
| Pop Sensation Serious Dress | 7489 |
| Pop Sensation Serious Shoes | 7570 |
| Pop Sensation Serious Wig | 7733 |
| Pop Sensation Singer Glasses | 7725 |
| Pop Sensation Singer Gloves | 7678 |
| Pop Sensation Singer Pants | 7571 |
| Pop Sensation Singer Shirt | 7490 |
| Pop Sensation Singer Wig | 7731 |
| Pop Sensation Weeb Gloves | 7679 |
| Pop Sensation Weeb Headphones | 7723 |
| Pop Sensation Weeb Shirt | 7491 |
| Pop Sensation Weeb Skirt | 7572 |
| Pop Sensation Weeb Wig | 7734 |
| Powerful Mask | 62121 |
| Prince Cape | 51666 |
| Prince Charming Pants | 62143 |
| Prince Gloves | 61998 |
| Prince of the Barracks Coat | 51788 |
| Prince of the Barracks Crown | 51602 |
| Prince of the Barracks Pants | 61941 |
| Prince Pants | 51867 |
| Prince Shirt | 51709 |
| Prince Wig | 51522 |
| Princess Masquerade Dress | 51711 |
| Princess Masquerade Mask | 51525 |
| Princess of the Barracks Dress | 51785 |
| Princess of the Barracks Shoes | 61938 |
| Princess of the Barracks Tiara | 51599 |
| Prize Winning Dress | 62286 |
| Prize Winning Shoes | 62302 |
| Proper Dress (Black) | 40180 |
| Puffer Wig | 51553 |
| Pumpkin Beanie | 42203 |
| Pumpkin Bobble Headband | 42204 |
| Pumpkin Costume | 7419 |
| Pumpkin Costume Hat | 7616 |
| Pumpkin Dress | 7428 |
| Pumpkin Helmet | 42132 |
| Pumpkin Polo Pants | 7518 |
| Pumpkin Polo Shirt | 7423 |
| Pumpkin Witch Hat | 7620 |
| Puppy Bandana | 8523 |
| Puppy Ear Headband | 7801 |
| Puppy Gloves | 7684 |
| Puppy Mascot Head | 7800 |
| Puppy Mascot Robe | 8522 |
| Puppy Paw Pants | 7593 |
| Purple Cape | 5814 |
| Purple Curled Wig | 51509 |
| Purple Gloves | 5707 |
| Quartz Princess Dress | 62141 |
| Quartz Princess Gloves | 62147 |
| Quartz Princess Wig | 62133 |
| Queen's Gambit Dress | 51825 |
| Queen's Gambit Horns | 51643 |
| Queen's Gambit Pants | 61978 |
| Queen's Gambit Sleeves | 62017 |
| Radiant Queen Dress | 62209 |
| Radiant Queen Wig | 62227 |
| Radiant Ribbon Cape | 62163 |
| Radiant Ribbon Gloves | 62215 |
| Radiant Ribbon Hat | 62223 |
| Radiant Ribbon Mask | 62225 |
| Radiant Ribbon Pants | 62218 |
| Radiant Ribbon Shirt | 62213 |
| Radiant Royalty Cape | 62162 |
| Radiant Royalty Chest Plate | 62208 |
| Radiant Royalty Gloves | 62214 |
| Radiant Royalty Helmet | 62224 |
| Radiant Royalty Pants | 62217 |
| Radiant Royalty Princess Dress | 62210 |
| Radiant Royalty Princess Wig | 62228 |
| Raggedy Doll Wig | 7769 |
| Rags to Riches Wig | 62275 |
| Rainbow Shell Hat | 8223 |
| Rainbow Shirt (Black) | 7301 |
| Rainbow Shirt (Blue) | 7302 |
| Rainbow Shirt (Brown) | 7303 |
| Rainbow Shirt (Gray) | 7304 |
| Rainbow Shirt (Green) | 7305 |
| Rainbow Shirt (Orange) | 7306 |
| Rainbow Shirt (Pink) | 7307 |
| Rainbow Shirt (Purple) | 7308 |
| Rainbow Shirt (Red) | 7309 |
| Rainbow Shirt (White) | 5331 |
| Rainbow Shirt (Yellow) | 7310 |
| Rainy Day Hat | 62035 |
| Rainy Day Pants | 62043 |
| Rainy Day Sweater | 62039 |
| Ram Rocking Helm | 7645 |
| Ramberry Wool Hat | 51626 |
| Ramberry Wool Pants | 61962 |
| Ramberry Wool Shirt | 51809 |
| Rapunzel Skirt (Black) | 5545 |
| Rapunzel Skirt (Blue) | 5546 |
| Rapunzel Skirt (Brown) | 22061 |
| Rapunzel Skirt (Gray) | 22062 |
| Rapunzel Skirt (Green) | 5550 |
| Rapunzel Skirt (Orange) | 5547 |
| Rapunzel Skirt (Pink) | 5551 |
| Rapunzel Skirt (Purple) | 5506 |
| Rapunzel Skirt (Red) | 5548 |
| Rapunzel Skirt (White) | 5549 |
| Rapunzel Skirt (Yellow) | 5552 |
| Red Cape | 5803 |
| Red Gloves | 5708 |
| Red Matey Bandana | 7603 |
| Red Prince Shirt | 62137 |
| Red Shimmer Dress | 40240 |
| Referee Shirt | 5308 |
| Retro Cheer Skirt | 51897 |
| Retro Cheer Top | 51742 |
| Retro Cheer Wig | 51556 |
| Ribbon Hat | 7600 |
| Ripped Jeans (Black) | 5509 |
| Ripped Jeans (Blue) | 22051 |
| Ripped Jeans (Brown) | 22052 |
| Ripped Jeans (Gray) | 22053 |
| Ripped Jeans (Green) | 22054 |
| Ripped Jeans (Orange) | 22055 |
| Ripped Jeans (Pink) | 22056 |
| Ripped Jeans (Purple) | 22057 |
| Ripped Jeans (Red) | 22058 |
| Ripped Jeans (White) | 22059 |
| Ripped Jeans (Yellow) | 22060 |
| Risen Phoenix Hood | 51655 |
| Risen Phoenix Pants | 61989 |
| Risen Phoenix Shirt | 51838 |
| Rising Sun Dress | 51776 |
| Rising Sun Shoes | 61930 |
| Rising Sun Wig | 51590 |
| Rock 'n' Roll Mohawk Wig (Black) | 7705 |
| Rock 'n' Roll Mohawk Wig (White) | 7704 |
| Rock 'n' Roll Wig (Black) | 7703 |
| Rock 'n' Roll Wig (Red) | 7702 |
| Rocker Belted Shirt | 7438 |
| Rocker Ski Mask | 7643 |
| Rocker Spiked Pants | 7524 |
| Rocketship Shirt (Black) | 7230 |
| Rocketship Shirt (Blue) | 5317 |
| Rocketship Shirt (Purple) | 7231 |
| Rocking Chest Belts | 7440 |
| Rocking Spiked Boots | 7526 |
| Royal Blossom Dress | 8516 |
| Royal Blossom Hairpiece | 7794 |
| Royal Cape | 5830 |
| Royal Dress (Black) | 40380 |
| Royal Dress (Blue) | 40381 |
| Royal Dress (Brown) | 40382 |
| Royal Dress (Gray) | 40383 |
| Royal Dress (Green) | 40384 |
| Royal Dress (Orange) | 40385 |
| Royal Dress (Pink) | 40386 |
| Royal Dress (Purple) | 40387 |
| Royal Dress (Red) | 40388 |
| Royal Dress (White) | 40389 |
| Royal Dress (Yellow) | 40390 |
| Royal Robe Pants | 62179 |
| Royal Robe Top | 62176 |
| Sad Cardboard Box Hat | 8125 |
| Sailor Shirt (Black) | 7141 |
| Sailor Shirt (Blue) | 5321 |
| Sailor Shirt (Brown) | 7142 |
| Sailor Shirt (Gray) | 7143 |
| Sailor Shirt (Green) | 7144 |
| Sailor Shirt (Orange) | 7145 |
| Sailor Shirt (Pink) | 7146 |
| Sailor Shirt (Purple) | 7147 |
| Sailor Shirt (Red) | 7148 |
| Sailor Shirt (White) | 7149 |
| Sailor Shirt (Yellow) | 7150 |
| Scale Cape | 5829 |
| Scale Protecting Earmuffs | 62373 |
| Scale Protecting Pants | 62385 |
| Scale Protecting Sweater | 62359 |
| Scary Pumpkin Hat | 7623 |
| School Shirt (Black) | 7200 |
| School Shirt (Blue) | 7201 |
| School Shirt (Brown) | 7202 |
| School Shirt (Gray) | 7203 |
| School Shirt (Green) | 5323 |
| School Shirt (Orange) | 7204 |
| School Shirt (Pink) | 7205 |
| School Shirt (Purple) | 7206 |
| School Shirt (Red) | 7207 |
| School Shirt (White) | 7208 |
| School Shirt (Yellow) | 7209 |
| Seaside Dress | 7383 |
| Seaweed Shirt | 51829 |
| Seaweed Skirt | 61982 |
| Self Cut Ponytail Wig | 51557 |
| Setting Sun Boots | 61929 |
| Setting Sun Dress | 51775 |
| Setting Sun Wig | 51589 |
| Shang Pants | 61947 |
| Shang Shirt | 51794 |
| Shang Wig | 51608 |
| Shanty Boots | 7506 |
| Shanty Hat | 7605 |
| Shanty Top | 7394 |
| Sharp Angelic Wings | 51847 |
| Shattered Spirit Helm | 7632 |
| Shattered Spirit Shorts | 7520 |
| Shattered Spirit Vest | 7435 |
| Sheer Green Crop Sweater | 7412 |
| Sheer Green Sweater | 7413 |
| Shell-tastic Wig | 51647 |
| Sheriff Hat (Black) | 5107 |
| Sheriff Hat (Blue) | 5153 |
| Sheriff Hat (Brown) | 5106 |
| Sheriff Hat (Gray) | 5099 |
| Sheriff Hat (Green) | 5154 |
| Sheriff Hat (Orange) | 5155 |
| Sheriff Hat (Pink) | 5108 |
| Sheriff Hat (Purple) | 5156 |
| Sheriff Hat (Red) | 5157 |
| Sheriff Hat (White) | 5109 |
| Sheriff Hat (Yellow) | 5158 |
| Shiny Cape | 5825 |
| Shiny Mask | 62124 |
| Shirt of the Dead | 62308 |
| Shocked Pumpkin Hat | 7622 |
| Shoes of Life | 62314 |
| Shooting Star Halo | 62023 |
| Shooting Star Shaw | 51774 |
| Shooting Star Skirt | 61928 |
| Shooting Star Wig | 51588 |
| Short Squirrel Tail | 51683 |
| Shorts | 5507 |
| Sick Tilted Top Hat | 7649 |
| Sick Trench Coat Bottom | 7530 |
| Sick Trench Coat Top | 7444 |
| Side Cape Pants | 61939 |
| Side Cape Shirt | 51786 |
| Silver Tiger Pants | 61945 |
| Silver Tiger Shirt | 51792 |
| Silver Tiger Tail | 51677 |
| Silver Tiger Wig | 51606 |
| Silver Tigress Skirt | 61949 |
| Silver Tigress Tail | 51679 |
| Silver Tigress Wig | 51610 |
| Simple Angelic Coat | 51778 |
| Simple Angelic Pants | 61931 |
| Simple Fur Shirt | 51728 |
| Simple Jellyfish Hat | 8224 |
| Simple Mask | 62123 |
| Simple Octopus Dress | 8506 |
| Simple Phoenix Headband | 51658 |
| Simple Phoenix Pants | 61992 |
| Simple Phoenix Shirt | 51841 |
| Simple Seller Cape | 51662 |
| Simple Seller Pants | 51853 |
| Simple Seller Shirt | 51692 |
| Simple Seller Wig | 51505 |
| Simple Sun Halo | 62021 |
| Simple Sun Wig | 51592 |
| Simple Sweatpants | 51885 |
| Simple Sweep Wig | 51542 |
| Simple Wonders Hat | 62278 |
| Skater Pants (Black) | 22009 |
| Skater Pants (Blue) | 22010 |
| Skater Pants (Brown) | 22011 |
| Skater Pants (Gray) | 22012 |
| Skater Pants (Green) | 22013 |
| Skater Pants (Orange) | 22014 |
| Skater Pants (Pink) | 22015 |
| Skater Pants (Purple) | 22016 |
| Skater Pants (Red) | 22017 |
| Skater Pants (White) | 22018 |
| Skater Pants (Yellow) | 22019 |
| Skeleton Polo Pants | 7519 |
| Skeleton Polo Shirt | 7425 |
| Skeleton Shirt | 5325 |
| Skipper Dress | 7388 |
| Skipper Pants | 7501 |
| Skipper Shirt | 7387 |
| Skirt of the Great Army | 62386 |
| Slash Tank Top (Black) | 7008 |
| Slash Tank Top (Blue) | 7010 |
| Slash Tank Top (Brown) | 7354 |
| Slash Tank Top (Gray) | 7355 |
| Slash Tank Top (Green) | 7011 |
| Slash Tank Top (Orange) | 7012 |
| Slash Tank Top (Pink) | 7013 |
| Slash Tank Top (Purple) | 7014 |
| Slash Tank Top (Red) | 7015 |

</details>

<details>
<summary>Slash Tank Top (White) – Striped Shirt 1 (Red) (300 items)</summary>

| Item name | ID |
| --- | ---: |
| Slash Tank Top (White) | 7009 |
| Slash Tank Top (Yellow) | 7016 |
| Sleepy Kitty Hat | 7806 |
| Sleepy Puppy Hat | 7805 |
| Slick Squirrel Tail | 51681 |
| Slime Hat (Black) | 8195 |
| Slime Hat (Blue) | 8194 |
| Slime Hat (Brown) | 8193 |
| Slime Hat (Gray) | 8192 |
| Slime Hat (Green) | 8191 |
| Slime Hat (Orange) | 8190 |
| Slime Hat (Pink) | 8189 |
| Slime Hat (Purple) | 8186 |
| Slime Hat (Red) | 8188 |
| Slime Hat (Yellow) | 8187 |
| Smuggler's Coat | 51828 |
| Smuggler's Pants | 61981 |
| Smuggler's Wig | 51646 |
| Snaccoon Gloves | 7651 |
| Snaccoon Hat | 7602 |
| Snaccoon Pal Pants | 62119 |
| Snaccoon Pal Shirt | 62116 |
| Snaccoon Pal Tail | 62118 |
| Snaccoon Pal Wig | 62111 |
| Snaccoon Pants | 7503 |
| Snaccoon Rider Blouse | 62114 |
| Snaccoon Rider Gloves | 62117 |
| Snaccoon Rider Pigtails Wig | 62110 |
| Snaccoon Riding Skirt | 62115 |
| Snaccoon Shirt | 7390 |
| Snaccoon Tail | 5832 |
| Snow Day Baggy Pants | 7573 |
| Snow Day Beanie | 7740 |
| Snow Day Beauty Tiara | 7738 |
| Snow Day Buttoned Skirt | 7576 |
| Snow Day Casual Pants | 7578 |
| Snow Day Cozy Shirt | 7497 |
| Snow Day Crop Top | 7496 |
| Snow Day Dress | 7495 |
| Snow Day Hood | 7739 |
| Snow Day Hoodie | 7493 |
| Snow Day Horns Hat | 7741 |
| Snow Day Long Coat | 7492 |
| Snow Day Long Skirt | 7575 |
| Snow Day Ninja Pants | 7577 |
| Snow Day Ninja Scarf | 5847 |
| Snow Day Ninja Top | 7498 |
| Snow Day Pants | 7579 |
| Snow Day Puff Ball Mittens | 7681 |
| Snow Day School Dress | 8501 |
| Snow Day Shawl | 7494 |
| Snow Day Sleeves | 7680 |
| Snow Day Sweater Dress | 8500 |
| Snow Day Thermal Pants | 7574 |
| Snow Day V Coat | 7499 |
| Snow Day Windswept Wig | 7743 |
| Snow Jacket (Black) | 7190 |
| Snow Jacket (Blue) | 5303 |
| Snow Jacket (Brown) | 7191 |
| Snow Jacket (Gray) | 7192 |
| Snow Jacket (Green) | 7193 |
| Snow Jacket (Orange) | 7194 |
| Snow Jacket (Pink) | 7195 |
| Snow Jacket (Purple) | 7196 |
| Snow Jacket (Red) | 7197 |
| Snow Jacket (White) | 7198 |
| Snow Jacket (Yellow) | 7199 |
| Snowflake Hair Piece | 7737 |
| Snowflake Shirt (Black) | 7270 |
| Snowflake Shirt (Blue) | 5310 |
| Snowflake Shirt (Brown) | 7271 |
| Snowflake Shirt (Gray) | 7272 |
| Snowflake Shirt (Green) | 7273 |
| Snowflake Shirt (Orange) | 7274 |
| Snowflake Shirt (Pink) | 7275 |
| Snowflake Shirt (Purple) | 7276 |
| Snowflake Shirt (Red) | 7277 |
| Snowflake Shirt (White) | 7278 |
| Snowflake Shirt (Yellow) | 7279 |
| Solar Delight Coat | 62354 |
| Solar Delight Pants | 62380 |
| Solar Delight Wig | 62368 |
| Space Demon Cape | 62160 |
| Space Demon Pants | 62197 |
| Space Demon Ponytail Wig | 62204 |
| Space Demon Shirt | 62193 |
| Space Princess Bow Wig | 62205 |
| Space Princess Shirt | 62194 |
| Space Princess Skirt | 62201 |
| Space Queen Dress | 62191 |
| Space Queen Wig | 62207 |
| Space Queen Wings | 62161 |
| Space Wig (Black) | 42134 |
| Space Wig (Blue) | 42135 |
| Space Wig (Brown) | 42136 |
| Space Wig (Gray) | 42138 |
| Space Wig (Green) | 42137 |
| Space Wig (Light Purple) | 42141 |
| Space Wig (Orange) | 42139 |
| Space Wig (Pink) | 42140 |
| Space Wig (Purple) | 42133 |
| Space Wig (Red) | 42142 |
| Space Wig (Teal) | 42143 |
| Space Wig (White) | 42144 |
| Space Wig (Yellow) | 42145 |
| Spare Crown | 62126 |
| Sparkling Sun Chest Plate | 5206 |
| Sparkling Sun Dress | 5383 |
| Sparkling Sun Gauntlets | 5606 |
| Sparkling Sun Gloves | 5701 |
| Sparkling Sun Helmet | 5006 |
| Sparkling Sun Legs | 5406 |
| Spiked Cowboy Hat | 7642 |
| Spiked Leather Pants | 7528 |
| Spiked Leather Vest | 7442 |
| Spiked Top Hat | 7647 |
| Spirit Blunt Bangs Wig | 7638 |
| Spirit Bun Wig | 7637 |
| Spirit Half Robe | 7433 |
| Spirit Lilypad Wig | 7639 |
| Spirit Mask | 7634 |
| Spirit Moon Belted Skirt | 7521 |
| Spirit Moon Clip | 7633 |
| Spirit Moon Cropped Top | 7436 |
| Spirit Orb Dress | 7431 |
| Spirit Orb Hat | 7630 |
| Spirit Protector Hat | 7631 |
| Spirit Protector Robe | 7432 |
| Spirit Ruffle Bracelets | 7655 |
| Spirit Ruffle Cropped Top | 7434 |
| Spirit Side Mask | 7635 |
| Spirit Split Dye Wig | 7636 |
| Spirit Tied Skirt | 7522 |
| Spooky Gloves | 7653 |
| Spooky Hair Bow (Black) | 8024 |
| Spooky Hair Bow (Blue) | 8025 |
| Spooky Hair Bow (Brown) | 8026 |
| Spooky Hair Bow (Gray) | 8027 |
| Spooky Hair Bow (Green) | 8028 |
| Spooky Hair Bow (Orange) | 8029 |
| Spooky Hair Bow (Pink) | 8030 |
| Spooky Hair Bow (Purple) | 8031 |
| Spooky Hair Bow (Red) | 8032 |
| Spooky Hair Bow (White) | 8033 |
| Spooky Hair Bow (Yellow) | 8034 |
| Spooky Hood | 7618 |
| Spooky Robe | 7421 |
| Spooky Top Hat (Black) | 8131 |
| Spooky Top Hat (Blue) | 8132 |
| Spooky Top Hat (Brown) | 8133 |
| Spooky Top Hat (Gray) | 8134 |
| Spooky Top Hat (Green) | 8135 |
| Spooky Top Hat (Orange) | 8136 |
| Spooky Top Hat (Pink) | 8137 |
| Spooky Top Hat (Purple) | 8138 |
| Spooky Top Hat (Red) | 8139 |
| Spooky Top Hat (White) | 8140 |
| Spooky Top Hat (Yellow) | 8141 |
| Sport Jersey (Black) | 40340 |
| Sport Jersey (Blue) | 5305 |
| Sport Jersey (Brown) | 40341 |
| Sport Jersey (Gray) | 40342 |
| Sport Jersey (Green) | 40343 |
| Sport Jersey (Orange) | 40344 |
| Sport Jersey (Pink) | 40345 |
| Sport Jersey (Purple) | 40346 |
| Sport Jersey (Red) | 40347 |
| Sport Jersey (White) | 40348 |
| Sport Jersey (Yellow) | 40349 |
| Spotted Dress (Black) | 40221 |
| Spotted Dress (Blue) | 40222 |
| Spotted Dress (Brown) | 40223 |
| Spotted Dress (Gray) | 40224 |
| Spotted Dress (Green) | 40225 |
| Spotted Dress (Orange) | 40226 |
| Spotted Dress (Pink) | 40227 |
| Spotted Dress (Purple) | 40228 |
| Spotted Dress (Red) | 40220 |
| Spotted Dress (White) | 40229 |
| Spotted Dress (Yellow) | 40230 |
| Sprout Hat (Black) | 42170 |
| Sprout Hat (Blue) | 42171 |
| Sprout Hat (Brown) | 42172 |
| Sprout Hat (Gray) | 42173 |
| Sprout Hat (Green) | 42174 |
| Sprout Hat (Orange) | 42175 |
| Sprout Hat (Pink) | 42176 |
| Sprout Hat (Purple) | 42177 |
| Sprout Hat (Red) | 42178 |
| Sprout Hat (White) | 42179 |
| Sprout Hat (Yellow) | 42180 |
| Star Earrings | 7785 |
| Star Glasses | 7784 |
| Star Shirt (Black) | 7232 |
| Star Shirt (Blue) | 5320 |
| Star Shirt (Brown) | 7233 |
| Star Shirt (Gray) | 7234 |
| Star Shirt (Green) | 7235 |
| Star Shirt (Orange) | 7236 |
| Star Shirt (Pink) | 7237 |
| Star Shirt (Purple) | 7238 |
| Star Shirt (Red) | 7239 |
| Star Shirt (White) | 7240 |
| Star Shirt (Yellow) | 7241 |
| Starlight Amethyst Dress | 7457 |
| Starlight Amethyst Gloves | 7662 |
| Starlight Amethyst Pants | 7544 |
| Starlight Amethyst Wig | 7750 |
| Starlight Armored Chest | 7458 |
| Starlight Armored Pants | 7549 |
| Starlight Champion Cape | 5838 |
| Starlight Champion Coat | 7462 |
| Starlight Champion Pants | 7546 |
| Starlight Coat | 7465 |
| Starlight Emerald Boots | 7543 |
| Starlight Emerald Cloak | 7460 |
| Starlight Emerald Gloves | 7661 |
| Starlight Emerald Wig | 7749 |
| Starlight Gloves | 7666 |
| Starlight Head Wings | 7745 |
| Starlight Lapis Boots | 7548 |
| Starlight Lapis Cloak | 7464 |
| Starlight Lapis Gloves | 7665 |
| Starlight Lapis Wig | 7753 |
| Starlight Leader Boots | 7542 |
| Starlight Leader Dress | 7459 |
| Starlight Leader Gloves | 7660 |
| Starlight Leader Wig | 7748 |
| Starlight Mascot Hat | 7747 |
| Starlight Mascot Pants | 7551 |
| Starlight Mascot Shirt | 7466 |
| Starlight Pants | 7562 |
| Starlight Pink Boots | 7547 |
| Starlight Pink Dress | 7463 |
| Starlight Pink Gloves | 7664 |
| Starlight Pink Wig | 7752 |
| Starlight Ruby Gloves | 7663 |
| Starlight Ruby Pants | 7545 |
| Starlight Ruby Shirt | 7461 |
| Starlight Ruby Wig | 7751 |
| Starlight Streak Wig | 7754 |
| Starlight Tiara | 7746 |
| Starlight Wings | 5836 |
| Starry Night Wig | 7778 |
| Steampunk Gauntlets | 62272 |
| Steampunk Jacket | 62261 |
| Steampunk Pants | 62268 |
| Steampunk Top Hat | 62253 |
| Stitched Robe | 7427 |
| Stitched Top (Black) | 7112 |
| Stitched Top (Blue) | 7113 |
| Stitched Top (Brown) | 7114 |
| Stitched Top (Gray) | 7115 |
| Stitched Top (Green) | 7116 |
| Stitched Top (Orange) | 7117 |
| Stitched Top (Pink) | 7118 |
| Stitched Top (Purple) | 7119 |
| Stitched Top (Red) | 7120 |
| Stitched Top (White) | 7121 |
| Stitched Top (Yellow) | 7122 |
| Stitched Top Hat | 7627 |
| Stitched Witch Dress | 7424 |
| Stitched Witch Hat | 7624 |
| Straw Farmers Hat (Black) | 42238 |
| Straw Farmers Hat (Blue) | 42239 |
| Straw Farmers Hat (Brown) | 42240 |
| Straw Farmers Hat (Gray) | 42241 |
| Straw Farmers Hat (Green) | 42242 |
| Straw Farmers Hat (Orange) | 42243 |
| Straw Farmers Hat (Pink) | 42244 |
| Straw Farmers Hat (Purple) | 42245 |
| Straw Farmers Hat (Red) | 42246 |
| Straw Farmers Hat (White) | 42247 |
| Straw Farmers Hat (Yellow) | 42248 |
| Straw Hat | 42000 |
| Strawberry Party Dress | 7468 |
| Strawberry Party Shoes | 7553 |
| Strawberry Party Wig | 7756 |
| Street Pants (Black) | 5573 |
| Street Pants (Blue) | 5574 |
| Street Pants (Brown) | 5575 |
| Street Pants (Gray) | 22074 |
| Street Pants (Green) | 5576 |
| Street Pants (Orange) | 5577 |
| Street Pants (Pink) | 5578 |
| Street Pants (Purple) | 5579 |
| Street Pants (Red) | 5580 |
| Street Pants (White) | 5581 |
| Street Pants (Yellow) | 5582 |
| Striped Button Up Shirt | 7404 |
| Striped Dress | 7400 |
| Striped Shirt 1 (Black) | 40360 |
| Striped Shirt 1 (Blue) | 40361 |
| Striped Shirt 1 (Brown) | 40362 |
| Striped Shirt 1 (Gray) | 40363 |
| Striped Shirt 1 (Green) | 5327 |
| Striped Shirt 1 (Orange) | 40364 |
| Striped Shirt 1 (Pink) | 40365 |
| Striped Shirt 1 (Purple) | 40366 |
| Striped Shirt 1 (Red) | 40367 |

</details>

<details>
<summary>Striped Shirt 1 (White) – Vest Shirt (Black) (300 items)</summary>

| Item name | ID |
| --- | ---: |
| Striped Shirt 1 (White) | 40368 |
| Striped Shirt 2 (Black) | 7078 |
| Striped Shirt 2 (Blue) | 7077 |
| Striped Shirt 2 (Brown) | 7076 |
| Striped Shirt 2 (Gray) | 7337 |
| Striped Shirt 2 (Green) | 7075 |
| Striped Shirt 2 (Orange) | 7074 |
| Striped Shirt 2 (Pink) | 7073 |
| Striped Shirt 2 (Purple) | 7072 |
| Striped Shirt 2 (Red) | 5326 |
| Striped Shirt 2 (White) | 7071 |
| Striped Shirt 2 (Yellow) | 7070 |
| Student Windswept Wig | 7711 |
| Summer Beach Shoes | 62054 |
| Summer Casual Shirt | 62049 |
| Summer Cropped Shirt | 62048 |
| Summer Flower Headpiece | 62044 |
| Summer Grass Skirt | 62052 |
| Summer Head Scarf | 62046 |
| Summer Snorkel | 62045 |
| Summer Sun Dress | 62050 |
| Summer Trunks | 62053 |
| Sun Dress (Black) | 7030 |
| Sun Dress (Blue) | 7031 |
| Sun Dress (Brown) | 5300 |
| Sun Dress (Gray) | 7339 |
| Sun Dress (Green) | 5361 |
| Sun Dress (Orange) | 7032 |
| Sun Dress (Pink) | 5362 |
| Sun Dress (Purple) | 7033 |
| Sun Dress (Red) | 7035 |
| Sun Dress (White) | 7034 |
| Sun Dress (Yellow) | 5384 |
| Sun Rising Halo | 62020 |
| Sun Setting Halo | 62022 |
| Sun Shirt | 5311 |
| Sunny Overall Bottom | 62041 |
| Sunny Overall Top | 62037 |
| Sunray Boots | 62384 |
| Sunray Dress | 62358 |
| Sunray Horns Headband | 62372 |
| Sunray Tail | 62348 |
| Sunray Wings | 62347 |
| Sunset Cape | 5807 |
| Super Cape | 5822 |
| Swashbuckler Bottoms | 7507 |
| Swashbuckler Headband | 7606 |
| Swashbuckler Top | 7395 |
| Sweeping Cape Pants | 61942 |
| Sweeping Cape Shirt | 51789 |
| Tall Captain Hat | 7607 |
| Tank Top (Black) | 40101 |
| Tank Top (Blue) | 40102 |
| Tank Top (Brown) | 40103 |
| Tank Top (Gray) | 40104 |
| Tank Top (Green) | 40105 |
| Tank Top (Orange) | 40106 |
| Tank Top (Pink) | 40107 |
| Tank Top (Purple) | 40108 |
| Tank Top (Red) | 40100 |
| Tank Top (White) | 40109 |
| Tank Top (Yellow) | 40110 |
| Teacher's Ponytail Wig | 51543 |
| Teacher's Shirt | 51729 |
| Teacher's Skirt | 51886 |
| Teal Kimono | 8531 |
| Teal King Pants | 62145 |
| Teal King Shirt | 62138 |
| Tech Academia Student Glasses | 7720 |
| Tech Academia Student Pants | 7541 |
| Tech Academia Student Shirt | 7456 |
| Tech Academia Student Wig | 7719 |
| Techy Shirt (Blue) | 7280 |
| Techy Shirt (Green) | 5319 |
| Temple Spirit Robe | 8533 |
| Temple Spirit Sleeves | 7686 |
| Temple Spirit Wig | 7813 |
| Tengu Helmet | 7809 |
| Tengu Pants | 7829 |
| Tengu Shirt | 8534 |
| Tengu Wings | 5848 |
| Thick Brim Sun Hat | 62034 |
| Thorian Coat | 62387 |
| Thorian Pants | 62409 |
| Thorian Wig | 62397 |
| Throwback Hat | 62405 |
| Throwback Pants | 62416 |
| Throwback Shirt | 62394 |
| Thundering Wisdom Sandals | 62178 |
| Thundering Wisdom Toga | 62168 |
| Thundering Wisdom Wig | 62187 |
| Tiara of the Great Army | 62374 |
| Tie Dye Shirt (Black) | 40121 |
| Tie Dye Shirt (Blue) | 40122 |
| Tie Dye Shirt (Brown) | 40123 |
| Tie Dye Shirt (Gray) | 40124 |
| Tie Dye Shirt (Green) | 40125 |
| Tie Dye Shirt (Orange) | 40126 |
| Tie Dye Shirt (Pink) | 40127 |
| Tie Dye Shirt (Purple) | 40128 |
| Tie Dye Shirt (Rainbow) | 40120 |
| Tie Dye Shirt (Red) | 40129 |
| Tie Dye Shirt (White) | 40130 |
| Tie Dye Shirt (Yellow) | 40131 |
| Timeless Mage Dress | 62357 |
| Timeless Mage Shoes | 62383 |
| Timeless Mage Tail | 62346 |
| Timeless Mage Wig | 62371 |
| Timeless Pants | 62376 |
| Timeless Shirt | 62350 |
| Timeless Tail | 62341 |
| Timeless Wig | 62364 |
| Timeless Wings | 62340 |
| Tinkerer's Top Hat | 62274 |
| Tis the Season Baker Dress | 7472 |
| Tis the Season Beanie Wig | 7758 |
| Tis the Season Boots | 7556 |
| Tis the Season Dress | 7473 |
| Tis the Season Elvish Bob Wig | 7762 |
| Tis the Season Gloves | 7668 |
| Tis the Season Holly Buns Wig | 7761 |
| Tis the Season Long Johns | 7555 |
| Tis the Season Mini Wings | 5837 |
| Tis the Season Overall Pants | 7554 |
| Tis the Season Reindeer Overall Top | 7475 |
| Tis the Season Reindeer Wig | 7759 |
| Tis the Season Top Elf Coat | 7474 |
| Tis the Season Top Elf Pants | 7557 |
| Tis the Season Trench Coat | 7471 |
| Tis the Season Ugly Sweater Dress | 7470 |
| Tis the Season Wool Skirt | 7558 |
| Top Hat (Black) | 8103 |
| Top Hat (Blue) | 8104 |
| Top Hat (Brown) | 8105 |
| Top Hat (Gray) | 8106 |
| Top Hat (Green) | 8107 |
| Top Hat (Orange) | 8108 |
| Top Hat (Pink) | 8109 |
| Top Hat (Purple) | 8110 |
| Top Hat (Red) | 8111 |
| Top Hat (White) | 8112 |
| Top Hat (Yellow) | 8113 |
| Torn Cape | 5823 |
| Torn Dress (Black) | 7062 |
| Torn Dress (Blue) | 7063 |
| Torn Dress (Brown) | 7064 |
| Torn Dress (Gray) | 7338 |
| Torn Dress (Green) | 7069 |
| Torn Dress (Orange) | 7065 |
| Torn Dress (Pink) | 7066 |
| Torn Dress (Purple) | 5353 |
| Torn Dress (Red) | 5354 |
| Torn Dress (White) | 7067 |
| Torn Dress (Yellow) | 7068 |
| Towel Turban Wrap | 7824 |
| Towel Wrap | 8548 |
| Toy Bear Gloves | 7669 |
| Toy Bear Hat | 7763 |
| Toy Bear Pants | 7561 |
| Toy Bear Shirt | 7479 |
| Toy Cat Dress | 8525 |
| Toy Cat Mask | 7803 |
| Toy Dog Mask | 7804 |
| Toy Dog Shorts | 7595 |
| Toy Dog Vest | 8526 |
| Toy Phone Costume | 7478 |
| Toy Phone Hat | 7768 |
| Toy Potato Costume | 7477 |
| Toy Potato Wig and Mustache | 7767 |
| Toy Robot Boots | 7559 |
| Toy Robot Gloves | 7670 |
| Toy Robot Helmet | 7765 |
| Toy Robot Shirt | 7480 |
| Toy Soldier Gloves | 7671 |
| Toy Soldier Helmet | 7766 |
| Toy Soldier Pants | 7560 |
| Toy Soldier Shirt | 7481 |
| Traditional Angelic Gown | 51777 |
| Traditional Hakama | 7827 |
| Traditional Winter Gloves | 62006 |
| Traditional Winter Hat | 51628 |
| Traditional Winter Pants | 61964 |
| Traditional Winter Poncho | 51811 |
| Traditional Yukata | 8530 |
| Training Pants | 61956 |
| Training Shirt | 51803 |
| Training Wig | 51618 |
| Trash Bag Helm | 51528 |
| Trash Gloves | 61999 |
| Trash Pants | 51871 |
| Trash Shirt | 51714 |
| Troublemaker Backward Hat | 7707 |
| Troublemaker Jacket | 7448 |
| Troublemaker Pants | 7533 |
| Tuxedo (Black) | 5337 |
| Tuxedo (Blue) | 7168 |
| Tuxedo (Brown) | 7169 |
| Tuxedo (Gray) | 7170 |
| Tuxedo (Green) | 7171 |
| Tuxedo (Orange) | 7172 |
| Tuxedo (Pink) | 7173 |
| Tuxedo (Purple) | 7174 |
| Tuxedo (Red) | 5364 |
| Tuxedo (White) | 5363 |
| Tuxedo (Yellow) | 7175 |
| Tuxedo Pants (Black) | 22020 |
| Tuxedo Pants (Blue) | 22021 |
| Tuxedo Pants (Brown) | 22022 |
| Tuxedo Pants (Gray) | 22023 |
| Tuxedo Pants (Green) | 22024 |
| Tuxedo Pants (Orange) | 22025 |
| Tuxedo Pants (Pink) | 22026 |
| Tuxedo Pants (Purple) | 22027 |
| Tuxedo Pants (Red) | 5510 |
| Tuxedo Pants (White) | 5511 |
| Tuxedo Pants (Yellow) | 22028 |
| TV Hat (Broken) | 42321 |
| TV Hat (Error) | 42315 |
| TV Hat (Eyeball) | 42317 |
| TV Hat (Happy) | 42318 |
| TV Hat (Heart) | 42319 |
| TV Hat (Heartbeat) | 42020 |
| TV Hat (Scenic) | 42320 |
| TV Hat (Signal) | 42322 |
| TV Hat (Static) | 42316 |
| Twin Kanzashi Bun Wig | 7812 |
| Twisted Mask | 62125 |
| Underwater Warrior Pants | 51894 |
| Underwater Warrior Pauldrons | 51739 |
| Unicorn Wig (Black) | 42146 |
| Unicorn Wig (Blue) | 42147 |
| Unicorn Wig (Brown) | 42148 |
| Unicorn Wig (DarkBlue) | 42149 |
| Unicorn Wig (Gray) | 42150 |
| Unicorn Wig (Green) | 42151 |
| Unicorn Wig (LightBlue) | 42152 |
| Unicorn Wig (Orange) | 42153 |
| Unicorn Wig (Pink) | 42154 |
| Unicorn Wig (Purple) | 42155 |
| Unicorn Wig (Rainbow) | 42080 |
| Unicorn Wig (Red) | 42156 |
| Unicorn Wig (White) | 42157 |
| Unicorn Wig (Yellow) | 42158 |
| Urban Artist Hoodie | 51726 |
| Urban Artist Pants | 51883 |
| Urban Artist Wig | 51540 |
| Urban Stripe Shirt (Black) | 7176 |
| Urban Stripe Shirt (Blue) | 5328 |
| Urban Stripe Shirt (Brown) | 7177 |
| Urban Stripe Shirt (Gray) | 7178 |
| Urban Stripe Shirt (Green) | 7179 |
| Urban Stripe Shirt (Orange) | 7180 |
| Urban Stripe Shirt (Pink) | 7181 |
| Urban Stripe Shirt (Purple) | 7182 |
| Urban Stripe Shirt (Red) | 7183 |
| Urban Stripe Shirt (White) | 7184 |
| Urban Stripe Shirt (Yellow) | 7185 |
| Vaan Shirt | 51802 |
| Vaan Shorts | 61955 |
| Vaan Wig | 51617 |
| Valkyrie Crest | 51601 |
| Valkyrie Dress | 51787 |
| Valkyrie Pants | 61940 |
| Vampire Cape | 5826 |
| Vampire Gloves (Black) | 43040 |
| Vampire Gloves (Blue) | 43041 |
| Vampire Gloves (Green) | 43042 |
| Vampire Gloves (Orange) | 43043 |
| Vampire Gloves (Pink) | 43044 |
| Vampire Gloves (Purple) | 43045 |
| Vampire Gloves (Red) | 43046 |
| Vampire Gloves (White) | 43047 |
| Vampire Gloves (Yellow) | 43048 |
| Vampire Shirt (Black) | 5371 |
| Vampire Shirt (Blue) | 7056 |
| Vampire Shirt (Brown) | 7129 |
| Vampire Shirt (Gray) | 7130 |
| Vampire Shirt (Green) | 7057 |
| Vampire Shirt (Orange) | 7058 |
| Vampire Shirt (Pink) | 7059 |
| Vampire Shirt (Purple) | 7060 |
| Vampire Shirt (Red) | 5369 |
| Vampire Shirt (White) | 5370 |
| Vampire Shirt (Yellow) | 7061 |
| Vampire Skirt (Black) | 5538 |
| Vampire Skirt (Blue) | 5539 |
| Vampire Skirt (Brown) | 22000 |
| Vampire Skirt (Gray) | 22001 |
| Vampire Skirt (Green) | 5540 |
| Vampire Skirt (Orange) | 5537 |
| Vampire Skirt (Pink) | 5541 |
| Vampire Skirt (Purple) | 5542 |
| Vampire Skirt (Red) | 5503 |
| Vampire Skirt (White) | 5543 |
| Vampire Skirt (Yellow) | 5544 |
| Venus Fly Trap Cape | 5842 |
| Venus Fly Trap Hood | 7791 |
| Venus Fly Trap Shawl | 8513 |
| Venus Fly Trap Skirt | 7586 |
| Vest Shirt (Black) | 5347 |

</details>

<details>
<summary>Vest Shirt (Green) – Zeppelin Pilot&#x27;s Pants (172 items)</summary>

| Item name | ID |
| --- | ---: |
| Vest Shirt (Green) | 5345 |
| Vest Shirt (Purple) | 5346 |
| Veteran Battle Star Clip | 7714 |
| Veteran Battle Star Long Gloves | 7658 |
| Veteran Battle Star Shoes | 7538 |
| Veteran Battle Star Uniform | 7453 |
| Veteran Battle Star Wig | 7713 |
| Vexxed Pants | 51859 |
| Vexxed Shirt | 51698 |
| Vexxed Wig | 51511 |
| Vine Crown | 51611 |
| Vintage Cropped Swimsuit | 62396 |
| Vintage Snorkel Mask | 62402 |
| Vintage Swim Cap | 62408 |
| Vintage Swim Shorts | 62418 |
| Vintage Swimsuit Bottom | 62413 |
| Vintage Swimsuit Top | 62391 |
| Vivi Mask | 51623 |
| Vivi Pants | 61959 |
| Vivi Shirt | 51806 |
| Vivi Tail | 51682 |
| Vivi Wig | 51622 |
| Warm Heart Pants | 51905 |
| Warm Heart Scarf Shirt | 51750 |
| Warrior Spirit Dress | 62167 |
| Wasp Chest Plate | 8509 |
| Wasp Grieves | 7582 |
| Wasp Helmet | 7787 |
| Wavy Deluxe Dress | 51687 |
| Wavy Deluxe Sleeves | 61994 |
| Wavy Deluxe Wig | 51500 |
| Web Woven Boots | 62230 |
| Web Woven Crown | 62185 |
| Web Woven Dress | 62170 |
| Wedding Dress (Vintage) | 5396 |
| Wedding Dress (White) | 5395 |
| Welded Earrings | 62300 |
| Welded Gown | 62291 |
| Welded Pants | 62307 |
| Wesley's Coat | 51810 |
| Wesley's Pants | 61963 |
| Wesley's Wig | 51627 |
| Western Hat (Black) | 5103 |
| Western Hat (Blue) | 5163 |
| Western Hat (Brown) | 5102 |
| Western Hat (Gray) | 5098 |
| Western Hat (Green) | 5164 |
| Western Hat (Orange) | 5165 |
| Western Hat (Pink) | 5104 |
| Western Hat (Purple) | 5166 |
| Western Hat (Red) | 5167 |
| Western Hat (White) | 5105 |
| Western Hat (Yellow) | 5168 |
| Wetsuit Pants | 7580 |
| Wetsuit Scuba Goggles | 7772 |
| Wetsuit Top | 8503 |
| White Bathrobe | 8544 |
| White Cape | 5818 |
| Wicker Pants | 62337 |
| Wicker Sweater Vest | 62333 |
| Wicker Wig | 62329 |
| Wide Spread Wings | 51844 |
| Wig of Life | 62312 |
| Wild Adventurer Cloak | 51737 |
| Wild Adventurer Pants | 51893 |
| Wild Mermaid Dress | 8505 |
| Wild Mermaid Kelp Wig | 7774 |
| Wild Squirrel Tail | 51680 |
| Wild Wiggling Wig | 51551 |
| Wild Wind Poncho | 51797 |
| Wild Wind Sandals | 61950 |
| Wild Wind Wig | 51612 |
| Wilting Feather Top Hat | 62279 |
| Wind Mage Pants | 61953 |
| Wind Mage Poncho | 51800 |
| Wind Mage Wig | 51615 |
| Winter Beanie | 62071 |
| Winter Hunting Coat | 62074 |
| Winter Hunting Hat | 62070 |
| Winter Moon Gloves | 62002 |
| Winter Moon Pants | 61915 |
| Winter Moon Sweater | 51760 |
| Winter Moon Wig | 51574 |
| Winter Pants | 62079 |
| Winter Rabbit Hood | 51507 |
| Winter Rabbit Pants | 51855 |
| Winter Rabbit Shirt | 51694 |
| Winter Rabbit Tail | 51663 |
| Winter Striped Sweater | 62075 |
| Winter Tiger Hood | 51604 |
| Winter Tiger Jacket | 51790 |
| Winter Tiger Pants | 61943 |
| Winter Tiger Tail | 51675 |
| Winter Warmth Gloves | 62362 |
| Winter Warmth Hat | 62367 |
| Winter Warmth Pants | 62379 |
| Winter Warmth Sweater | 62353 |
| Witch Hat (Black) | 5123 |
| Witch Hat (Blue) | 5121 |
| Witch Hat (Brown) | 8198 |
| Witch Hat (Gray) | 8199 |
| Witch Hat (Green) | 5169 |
| Witch Hat (Orange) | 5170 |
| Witch Hat (Pink) | 5171 |
| Witch Hat (Purple) | 5124 |
| Witch Hat (Red) | 5172 |
| Witch Hat (White) | 5122 |
| Witch Hat (Yellow) | 5173 |
| Wither Punk Pants | 51870 |
| Wither Punk Shirt | 51713 |
| Wither Punk Wig | 51527 |
| Withercouncil Coat | 51824 |
| Withercouncil Gloves | 62016 |
| Withercouncil Pants | 61977 |
| Withercouncil Wig | 51642 |
| Withergate Braids Wig | 62090 |
| Withergate Mask | 5100 |
| Withergate Queen Dress | 51707 |
| Withergate Queen Wig | 51520 |
| Withergate Tiara (Black) | 42192 |
| Withergate Tiara (Blue) | 42193 |
| Withergate Tiara (Brown) | 42194 |
| Withergate Tiara (Gray) | 42195 |
| Withergate Tiara (Green) | 42196 |
| Withergate Tiara (Orange) | 42197 |
| Withergate Tiara (Pink) | 42198 |
| Withergate Tiara (Purple) | 42199 |
| Withergate Tiara (Red) | 42200 |
| Withergate Tiara (White) | 42201 |
| Withergate Tiara (Yellow) | 42202 |
| Wooly Winter Gloves | 62005 |
| Wooly Winter Hood | 51624 |
| Wooly Winter Pants | 61960 |
| Wooly Winter Sweater | 51807 |
| Wornhardt Gloves | 62008 |
| Wornhardt Pants | 61968 |
| Wornhardt Shirt | 51815 |
| Wornhardt Wig | 51632 |
| Woven Sun Hat | 62033 |
| Woven Wood Pants | 62325 |
| Woven Wood Shirt | 62318 |
| Woven Wood Wig | 62322 |
| Wrapped Dress (Black) | 40281 |
| Wrapped Dress (Blue) | 40282 |
| Wrapped Dress (Brown) | 40283 |
| Wrapped Dress (Gray) | 40284 |
| Wrapped Dress (Green) | 40285 |
| Wrapped Dress (Orange) | 40286 |
| Wrapped Dress (Pink) | 40280 |
| Wrapped Dress (Purple) | 40287 |
| Wrapped Dress (Red) | 40288 |
| Wrapped Dress (White) | 40289 |
| Wrapped Dress (Yellow) | 40290 |
| Xyla Pants | 61975 |
| Xyla Shirt | 51822 |
| Xyla Sleeves | 62014 |
| Xyla Wig | 51640 |
| Yellow Cape | 5819 |
| Yellow Gloves | 5709 |
| Young Mage Hat | 62249 |
| Young Mage Robe | 62257 |
| Young Mage Skirt | 62265 |
| Young Wizard Hat | 62251 |
| Young Wizard Pants | 62266 |
| Young Wizard Robe | 62259 |
| Zaria Pants | 61984 |
| Zaria Shirt | 51832 |
| Zaria Wig | 51650 |
| Zeppelin Pilot's Coat | 62260 |
| Zeppelin Pilot's Gloves | 62271 |
| Zeppelin Pilot's Hat | 62252 |
| Zeppelin Pilot's Pants | 62267 |

</details>

### Crops from game data

**93 items**

| Item name | ID |
| --- | ---: |
| Acorn | 11031 |
| Armoranth | 11053 |
| Balloon Fruit | 11063 |
| Barley | 11045 |
| Beet | 12080 |
| Blizzard Berry | 11068 |
| Blue Moon Fruit | 11064 |
| Blue Rose | 11108 |
| Brr-Nana | 12082 |
| Butternut | 11044 |
| Candy Cane | 11077 |
| Carrot | 11006 |
| Cat Tail | 11032 |
| Chocoberry | 11054 |
| Cinnaberry | 11012 |
| Clover | 11055 |
| Coffee Bean | 11059 |
| Corn | 11001 |
| Cotton | 11075 |
| Cranberry | 11070 |
| Daisy | 11130 |
| Darkness Crop | 11034 |
| Demon Orb | 11004 |
| Dragon Fruit | 11027 |
| Durian | 11062 |
| Eggplant | 11015 |
| Fire Fruit | 11024 |
| Fizzy Fruit | 11039 |
| Garlic | 11060 |
| Ghost Pepper | 11049 |
| Grapes | 11022 |
| Green Beans | 11072 |
| Greenroot | 11010 |
| Guava Berry | 11035 |
| Heart Berry | 11058 |
| Heat Fruit | 11041 |
| Hexagon Berry | 11065 |
| Hibiscus | 11103 |
| Honey Flower | 11101 |
| Honeysuckle | 11076 |
| Hops | 11037 |
| Indiglow | 11030 |
| Kale | 11050 |
| Kiwi Berry | 11071 |
| Kraken Kale | 11016 |
| Lavender | 11102 |
| Lemon | 11052 |
| Lettuce | 11013 |
| Lily | 11104 |
| Lotus | 11110 |
| Mana Gem | 11033 |
| Mango | 11061 |
| Marshmallow Bean | 11042 |
| Melon | 11057 |
| Moon Fruit | 11043 |
| Moonplant | 11017 |
| Onion | 11009 |
| Orchid | 11105 |
| Peas | 11073 |
| Pepper | 11008 |
| Pineapple | 11056 |
| Potato | 11002 |
| Pumpkin | 11036 |
| Purple Eggplant | 12081 |
| Pythagorean Berry | 11069 |
| Razorstalk | 11020 |
| Red Rose | 11107 |
| Rice | 11014 |
| Rock Fruit | 11025 |
| Shiiwalki Mushroom | 11029 |
| Shimmeroot | 11007 |
| Snappy Plant | 11005 |
| Snow Ball Crop | 11067 |
| Snow Pea | 11078 |
| Soda Pop Crop | 11038 |
| Soul Orb | 11021 |
| Star Fruit | 11066 |
| Stormelon | 11051 |
| Suckerstem | 11018 |
| Sugar Cane | 12079 |
| Sun Orb | 11083 |
| Sunflower | 11106 |
| Tea Leaves | 11048 |
| Tomato | 11003 |
| Tombmelon | 11019 |
| Tulip | 11109 |
| Turnip | 11040 |
| Walk Choy | 11028 |
| Water Fruit | 11023 |
| Watermelon | 11074 |
| Wheat | 11000 |
| Wind Chime | 11026 |
| Yam | 11047 |

### Decorations from game data

**186 items**

| Item name | ID |
| --- | ---: |
| Arcade Flooring | 9724 |
| Arcade Wallpaper | 9648 |
| Art Deco Purple Wallpaper | 9625 |
| Astral Flooring | 13014 |
| Astral Wallpaper | 13013 |
| Barn Wallpaper | 9628 |
| Basic Wallpaper | 9600 |
| Basic Wooden Flooring | 9700 |
| Beach Sand Floor Tile | 17016 |
| Black and White Marble Tile Flooring | 9705 |
| Black Skull Floor Tile | 17023 |
| Blue Camo Wallpaper | 9644 |
| Blue Diamond Wallpaper | 9610 |
| Blue Mismatched Tile Flooring | 9719 |
| Blue Skull Floor Tile | 17022 |
| Blue Striped Wallpaper | 9619 |
| Blue Tiled Wallpaper | 9647 |
| Bolted Steel Flooring | 9725 |
| Brick Floor Tile | 17007 |
| Brine Stones Floor Tile | 17012 |
| Bronze Inventor's Flooring | 14065 |
| Brown Brick Wallpaper | 9614 |
| Brown Tiled Floor Tile | 17029 |
| Bunny Wallpaper | 9611 |
| Candy Bone Flooring | 9746 |
| Card Deck Wallpaper | 4352 |
| Checkered Fake Grass Flooring | 9715 |
| Cherry and Strawberry Floor Tile | 17021 |
| Chicken Coop Wallpaper | 9632 |
| Chiseled Floral Stone Floor Tile | 17032 |
| Clean Wooden Board Flooring | 9702 |
| Colorful Puzzle Flooring | 9709 |
| Contemporary Flooring | 14066 |
| Contemporary Wallpaper | 14054 |
| Cream Brick Wallpaper | 14056 |
| Cross Bone Flooring | 9747 |
| Cute Bat Wallpaper | 4350 |
| Daisy Field Wallpaper | 4257 |
| Dark Floral Stone Floor Tile | 17036 |
| Deluxe Wooden Patterned Flooring | 9703 |
| Demonic Suits Wallpaper | 4347 |
| Diagonal Dark Oak Floor Tile | 17024 |
| Earthy Grid Wallpaper | 9604 |
| Expensive Red Stone Flooring | 9716 |
| Exposed Gear Wallpaper | 14055 |
| Eyeball Wallpaper | 4346 |
| Fake Grass Flooring | 9713 |
| Fall Crosshatch Flooring | 9740 |
| Fall Leaves Wallpaper | 4306 |
| Feathered Wallpaper | 9637 |
| Festive Flooring | 9744 |
| Festive Wallpaper | 4334 |
| Fish Scale Flooring | 9708 |
| Floor Tile 1 | 17003 |
| Floor Tile 2 | 17004 |
| Floor Tile 3 | 17005 |
| Flower Field Flooring | 9735 |
| Flower Wallpaper | 9601 |
| Forest Floor Wallpaper | 4307 |
| Galaxy Flooring | 9723 |
| Galaxy Wallpaper | 9641 |
| Garden Festival Wallpaper | 4258 |
| Golden Moon Floor Tile | 17018 |
| Grassy Flower Floor Tile | 17033 |
| Grassy Stoney Floor Tile | 17034 |
| Gray Brick Wallpaper | 9622 |
| Gray Stone Flooring | 9727 |
| Great City Brick Flooring | 14067 |
| Green Bamboo Wallpaper | 9645 |
| Green Diagonal Plank Flooring | 9736 |
| Green Sun Wallpaper | 4284 |
| Heart Checkered Floor Tile | 17041 |
| Heart Checkered Flooring | 9722 |
| Hearth Wooden Flooring | 9745 |
| Ice Brick Flooring | 9743 |
| Ice Flooring | 9711 |
| Industrial Brick Wallpaper | 9635 |
| Lava Flooring | 9720 |
| Lavender Plant Wallpaper | 9636 |
| Light Floral Stone Floor Tile | 17031 |
| Love Snaccoon Wallpaper | 4374 |
| Mismatched Wooden Checkered Flooring | 9701 |
| Mismatched Wooden Floor Tile | 17045 |
| Modern Marble Flooring | 9706 |
| Monster Sigil Flooring | 9748 |
| Moon and Stars Wallpaper | 4621 |
| Mottled Brown Stone Floor Tile | 17027 |
| Mottled Pink Stone Floor Tile | 17028 |
| Mushroom Spotted Wallpaper | 4308 |
| Natural Diagonal Plank Flooring | 9739 |
| Navy Withergate Wallpaper | 9624 |
| Nel'Vari Treehouse Flooring | 9733 |
| Nel'Vari Treehouse Wallpaper | 9627 |
| Nel'Vari Workshop Wallpaper | 9630 |
| Nice Blue Wallpaper | 9615 |
| Nice Green Wallpaper | 9616 |
| Nice Ivory Wallpaper | 9617 |
| Nice Light Blue Wallpaper | 9618 |
| Night Forest Wallpaper | 3623 |
| Oak Plank Floor Tile | 17010 |
| Ocean Brick Floor Tile | 17011 |
| Ocean Flooring | 9737 |
| Orange Gilded Floor Tile | 17044 |
| Ornate Tatami Wallpaper | 9634 |
| Overgrown Pink Brick Floor Tile | 17025 |
| Overgrown Wooden Slat Floor Tile | 17038 |
| Painted Bamboo Wallpaper | 9646 |
| Parchment Wallpaper | 9608 |
| Patterned Floor Tile | 17009 |
| Pink Bow Wallpaper | 9640 |
| Pink Brick Floor Tile | 17026 |
| Pink Rosebud Wallpaper | 9605 |
| Purple Checkered Flooring | 9734 |
| Purple Fluffy Tiled Flooring | 9749 |
| Purple Gilded Wallpaper | 9638 |
| Purple Gold Arch Wallpaper | 9621 |
| Purple Grid Wallpaper | 9606 |
| Purple Moon Floor Tile | 17019 |
| Purple Scale Flooring | 9750 |
| Purple Striped Wallpaper | 9607 |
| Purple Vintage Wallpaper | 9612 |
| Radiant Royalty Flooring | 13024 |
| Radiant Royalty Wallpaper | 13025 |
| Rainbow Floor Tile | 17014 |
| Red Brick Wallpaper | 9613 |
| Red Carpet Flooring | 9707 |
| Red Cobblestone Wallpaper | 9639 |
| Red Sun Wallpaper | 4285 |
| Red Wooden Flooring | 9738 |
| Retro Striped Wallpaper | 9609 |
| Rose Stone Floor Tile | 17040 |
| Rose Stone Flooring | 9712 |
| Rounded Stone Floor Tile | 17035 |
| Sakura Tree Wallpaper | 4256 |
| Sand Floor TIle | 17013 |
| Seashell Checkered Floor Tile | 17015 |
| Shed Wallpaper | 9629 |
| Simple Stones Floor Tile | 17030 |
| Simple Woven Floor Tile | 17039 |
| Slime Wallpaper | 4349 |
| Small Marble Tile Flooring | 9717 |
| Snaccoon Fur Carpet Flooring | 9751 |
| Snaccoon Head Wallpaper | 4373 |
| Snowflake Wallpaper | 4332 |
| Spider Wallpaper | 4351 |
| Spiderweb Flooring | 9721 |
| Spooky Floor Tile | 17020 |
| Stained Glass Purple Wallpaper | 9623 |
| Starfish Wallpaper | 4281 |
| Steel Panel Flooring | 9726 |
| Steel Plate Floor Tile | 17046 |
| Stepping Stone Floor Tile | 17037 |
| Stitched Spooky Floor Tile | 17043 |
| Stone Floor Tile | 17001 |
| Straw Mat Flooring | 9731 |
| Summer Island Wallpaper | 4280 |
| Summer Ocean Wallpaper | 4282 |
| Summer Snaccoon Wallpaper | 4375 |
| Sun Haven Workshop Wallpaper | 9633 |
| Sunrise Forest Wallpaper | 3624 |
| Swirling Void Wallpaper | 4348 |
| Tatami Mat Flooring | 9730 |
| Teal Carpet Flooring | 9718 |
| Teal Woven Wallpaper | 9643 |
| Teddy Bear Floor Tile | 17017 |
| Thick Chevron Wooden Flooring | 9728 |
| Thin Chevron Wooden Flooring | 9714 |
| Ugly Sweater Wallpaper | 4333 |
| Uneven Striped Wallpaper | 9642 |
| Vintage Wallpaper | 9603 |
| Wade Pool Wallpaper | 4283 |
| Warehouse Wallpaper | 9631 |
| Well Worn Red Flooring | 9742 |
| White Stone Floor Tile | 17008 |
| Withergate Apartment Flooring | 9732 |
| Withergate Apartment Wallpaper | 9626 |
| Withergate Royalty Wallpaper | 9620 |
| Withergate Wallpaper | 9602 |
| Wood Floor Tile | 17000 |
| Wooden Honeycomb Flooring | 9704 |
| Wooden Overgrowth Flooring | 9741 |
| Wooden Plank Floor Tile | 17006 |
| Wooden Puzzle Flooring | 9710 |
| Wooden Stepping Stone Floor Tile | 17042 |
| Workshop Floor Tile | 17002 |
| Woven Wooden Flooring | 9729 |

### Elixirs from game data

**73 items**

| Item name | ID |
| --- | ---: |
| Advanced Attack Potion | 3085 |
| Advanced Defense Potion | 3086 |
| Advanced Fish Bait | 4510 |
| Advanced Spell Damage Potion | 3087 |
| Amazing Elixir of Farming | 30140 |
| Amazing Elixir of Fishing | 30142 |
| Amazing Elixir of Mining | 30141 |
| Attack Potion | 3082 |
| Basic Fish Bait | 4509 |
| Blueberry Candy Drop | 11556 |
| Briny Mage's Potion | 30028 |
| Cake Pop | 3839 |
| Carrot Cake | 3849 |
| Carrot Juice | 3892 |
| Chilly Fishing Bait | 4512 |
| Dead Eye Shrimp Cocktail | 11220 |
| Defense Potion | 3084 |
| Devilishly Good Stew | 11229 |
| Dumbo Octopus Takoyaki | 11218 |
| Electric Eel Sushi | 11221 |
| Elixir of Arcane Might | 3093 |
| Elixir of Combat | 18108 |
| Elixir of Exploration | 18106 |
| Elixir of Farming | 18105 |
| Elixir of Ferocity | 3094 |
| Elixir of Fishing | 18109 |
| Elixir of Fortitude | 3090 |
| Elixir of Iron Will | 3095 |
| Elixir of Mind | 3091 |
| Elixir of Mining | 18107 |
| Elixir of Speed | 3092 |
| Espresso | 30117 |
| Extraordinary Speed Potion | 30138 |
| Glass of Pure Water | 3899 |
| Grape Juice | 3895 |
| Grape Taffy | 11551 |
| Health Potion | 3081 |
| Healthy Seafarer's Potion | 30031 |
| Hearty Armor Pie | 3837 |
| Incredible Attack Potion | 3767 |
| Incredible Defense Potion | 3768 |
| Incredible Spell Damage Potion | 3766 |
| Kraken Stew | 11224 |
| Large Magic Potion | 11214 |
| Large Mana Potion | 11212 |
| Legendary Fish Bait | 4511 |
| Lucky Fish Bait | 4516 |
| Magic Potion | 11213 |
| Mana Potion | 3080 |
| Mango Taffy | 11550 |
| Medium Mana Potion | 11211 |
| Mini Jawbreaker | 11549 |
| Monster Fruit Fuel | 11380 |
| Monster Fruit Mocha | 11373 |
| Nectar-ine Smoothie | 11368 |
| Oceanic Hero's Potion | 30030 |
| Orange Candy Drop | 11555 |
| Pet Festival Ice Pop | 30080 |
| Raspberry Taffy | 11552 |
| Really Spicy Fishing Bait | 4514 |
| Sea Explorer's Potion | 30027 |
| Small Mana Potion | 11200 |
| Sour Plum Soda | 11381 |
| Sour Plum Tea | 11374 |
| Speed Potion | 3083 |
| Spell Damage Potion | 11215 |
| Spicy Fishing Bait | 4513 |
| Strawberry Candy Drop | 11554 |
| Sugar Plum Juice | 11371 |
| Sweet Fish Bait | 4515 |
| Watery Protector's Potion | 30029 |
| Wheat Grass Juice | 3901 |
| Withergate Mining Potion | 3769 |

### Fish from game data

**145 items**

| Item name | ID |
| --- | ---: |
| Acorn Anchovy | 15128 |
| Albascroll | 15140 |
| Albino Squid | 15079 |
| Alchemyjack | 15141 |
| Angel Fish | 15005 |
| Angelfin | 15059 |
| Archerfish | 15145 |
| Autumn Leaf Sole | 15135 |
| Averagemouth Bass | 15020 |
| Axolotl | 15055 |
| Bark Fish | 15038 |
| Bashful Pike | 15015 |
| Bitterling | 15081 |
| Black Bass | 15084 |
| Blazeel | 15104 |
| Blazing Herring | 15102 |
| Blooming Bass | 15115 |
| Blue Gill | 15009 |
| Blue Tang | 15003 |
| Blunted Swordfish | 15017 |
| Bomb Fish | 15091 |
| Bonemouth Bass | 15028 |
| Brain Jelly | 15068 |
| Bubblefish | 15060 |
| Bucketfish | 15138 |
| Butterflyfish | 15117 |
| Carp | 15010 |
| Catfish | 15018 |
| Christmas Lightfish | 15095 |
| Chromafin | 15025 |
| Clown Fish | 15083 |
| Coalfish | 15103 |
| Coducopia | 15125 |
| Crab | 15001 |
| Creepfish | 15064 |
| Crystal Tetra | 15044 |
| Cuddlefish | 15022 |
| Deadeye Shrimp | 15033 |
| Devilfin | 15080 |
| Dorado | 15000 |
| Dragon Gulper | 15040 |
| Dumbo Octopus | 15062 |
| Duorado | 15027 |
| Earlygator | 15137 |
| Eel | 15002 |
| Eel-Like-Thing | 15078 |
| Electric Eel | 15066 |
| Eyelotl | 15144 |
| Flame Ray | 15111 |
| Flamefish | 15036 |
| Floral Trout | 15119 |
| Flower Flounder | 15114 |
| Frilled Betta | 15054 |
| Frostfin | 15094 |
| Frozen Tuna | 15098 |
| Fungus Fish | 15052 |
| Geometric Squid | 15146 |
| Ghostfish | 15132 |
| Ghosthead Tuna | 15073 |
| Ghoul Fish | 15063 |
| Globfish | 15072 |
| Goblin Shark | 15074 |
| Gold Fish | 15008 |
| Golden Carp | 15026 |
| Haloopbut | 15139 |
| Hayfish | 15127 |
| Hearth Angler | 15106 |
| Heatfin | 15100 |
| Hocus-Puffus | 15142 |
| Holly Carp | 15096 |
| Horsefish | 15053 |
| Icicle Carp | 15101 |
| Inferno Guppy | 15105 |
| Ironhead Sturgeon | 15024 |
| Jack'o'fin | 15034 |
| Jingle Bass | 15097 |
| Kelp Eel | 15045 |
| King Salmon | 15126 |
| Koi Fish | 15090 |
| Kraken | 15070 |
| Leaf Sole | 15051 |
| Living Jelly | 15031 |
| Lobster | 15088 |
| Magma Star | 15108 |
| Molten Slug | 15112 |
| Moonfish | 15076 |
| Mud Catfish | 15120 |
| Mummy Trout | 15069 |
| Neapolitan Fish | 15056 |
| Neon Tetra | 15121 |
| Northern Pike | 15093 |
| Painted Egg | 15123 |
| Pirate Perch | 15134 |
| Popeye Goldfish | 15082 |
| Princely Frog | 15058 |
| Prism Minnow | 15147 |
| Pufferfish | 15007 |
| Pumpkin Jelly | 15133 |
| Purrmaid | 15037 |
| Pygmy Tuna | 15023 |
| Pyrelus | 15110 |
| Rainbow Trout | 15004 |
| Raincloud Ray | 15118 |
| Red Snapper | 15011 |
| Red Tie Guppy | 15019 |
| Redeye Piranha | 15016 |
| Redfinned Pincher | 15067 |
| Ribbon Eel | 15089 |
| Robed Parrotfish | 15041 |
| Rock Bass | 15092 |
| Royal Herring | 15021 |
| Royal Koi | 15057 |
| Salmon | 15085 |
| Sandstone Fish | 2118 |
| Scarffish | 15099 |
| Scorching Squid | 15107 |
| Sea Bass | 15006 |
| Sea Bat | 15071 |
| Seahorse | 15122 |
| Searback | 15113 |
| Shadow Tuna | 15029 |
| Silver Carp | 15012 |
| Sky Ray | 15046 |
| Slime Leech | 15035 |
| Snobfish | 15042 |
| Spectral Drifter | 15143 |
| Spiked Salmon | 15061 |
| Squawkmouth Bass | 15136 |
| Streamline Cod | 15014 |
| Sunfish | 15116 |
| Tadpole | 15124 |
| Tiger Trout | 15086 |
| Tinder Turtle | 15109 |
| Toothy Angler | 15030 |
| Trick or Trout | 15130 |
| Tuna | 15087 |
| Turkeyfish | 15129 |
| Unicornfish | 15039 |
| Vampire Piranha | 15131 |
| Vampire Squid | 15075 |
| Velveteen Betta | 15043 |
| Viperfish | 15077 |
| Water Bear | 15065 |
| Whitebelly Shark | 15013 |
| Zombie Fish | 15032 |

### Food from game data

**628 items**

<details>
<summary>Acai Bowl – Leaf Wrapped Bashful Pike (300 items)</summary>

| Item name | ID |
| --- | ---: |
| Acai Bowl | 3732 |
| Acorn Milk | 11272 |
| Advanced Attack Damage Tome | 18113 |
| Advanced Health Tome | 18115 |
| Advanced Spell Damage Tome | 18111 |
| Albascroll Sashimi | 30190 |
| Albino Squid Rings | 11228 |
| Alchemyjack Sashimi | 30191 |
| Apple Cake | 3840 |
| Apple Cider | 3700 |
| Apple Crisp Ice Cream | 3868 |
| Apple Jam | 3060 |
| Apple Juice | 3890 |
| Apple Pie | 3831 |
| Apple Sauce | 3728 |
| Arcane Essence | 3755 |
| Archerfish Roll | 30192 |
| Avocado Ice Cream | 30175 |
| Avocado Smoothie | 30180 |
| Baby Food | 31021 |
| Bacon Burger | 3935 |
| Bag of Jelly Beans | 11547 |
| Baked Beans | 3932 |
| Banana Jam | 3067 |
| Banana Peel Pie | 3612 |
| Beach Sand Mixer | 30024 |
| Bear-y Cute Burger | 30113 |
| Beginner's Apple Pie | 3029 |
| Berry Cake | 3844 |
| Berry Fruit Salad | 3880 |
| Berry Ice Cream | 3871 |
| Berry Pie | 3836 |
| Bewitching Fruit Tray | 30162 |
| Birthday Cake | 3944 |
| Bitter Seltzer | 3912 |
| Black Forest Cake | 3845 |
| Blizzard Berry Stew | 11585 |
| BLT | 3025 |
| Blue Rose Cake | 3856 |
| Blue Roses Honey | 2901 |
| Blueberry Cake | 3841 |
| Blueberry Ice Cream | 3869 |
| Blueberry Jam | 3061 |
| Blueberry Muffin | 3702 |
| Blueberry Pie | 3832 |
| Blueberry Salad | 3037 |
| Blueberry Smoothie | 3902 |
| Brain Jelly Salad | 11223 |
| Brine Berry Jam | 30050 |
| Brine Berry Salad | 30032 |
| Brine Berry Sorbet | 30041 |
| Brineapple Punch | 30025 |
| Brined Coconut Water | 30022 |
| Brinestone Boil | 30046 |
| Briney Surprise | 30023 |
| Brisket | 11557 |
| Brr-nana Smoothie | 3907 |
| Bubble Tea | 11274 |
| Bucketfish Sashimi | 30070 |
| Burger with Mana Sauce | 30114 |
| Butter | 3820 |
| Butternut Mac and Cheese | 11579 |
| Cake Mix | 3829 |
| California Roll | 3709 |
| Candied Yams | 3888 |
| Candy Apple | 3610 |
| Candy Corn Fruit Pop | 11379 |
| Candy Corn Fruit Smoothie | 11372 |
| Candy Kebab | 3613 |
| Candycorn Popcorn | 11385 |
| Caramel | 3822 |
| Caramel Apple | 3609 |
| Caramel Creme Brulee | 3866 |
| Caribbean Green Soup | 3016 |
| Catch of the Day | 11564 |
| Catsup | 11266 |
| Charcuterie Board | 11583 |
| Cheese | 3013 |
| Cheese Dip | 11567 |
| Cheese Souffle | 3864 |
| Cheeseburger | 3022 |
| Cheesecake | 3010 |
| Cheesecake Ice Cream | 3876 |
| Chicken Bastilla | 3747 |
| Chicken Noodle Soup | 3020 |
| Chicken Tenders | 11559 |
| Chicken Wings | 11566 |
| Chili | 11582 |
| Chipped Java Blast | 30112 |
| Chocolate | 3823 |
| Chocolate Cake | 3848 |
| Chocolate Cupcake | 3851 |
| Chocolate Ice Cream | 3875 |
| Chocolate Milk | 3885 |
| Chocolate Mousse Cake | 30125 |
| Chocolate Pudding | 3859 |
| Chocolate Tart | 3865 |
| Chow Mein | 3699 |
| Churros | 3743 |
| Cinnaberry Jam | 3068 |
| Cinnamon | 3821 |
| Cinnamon Apple Pie | 3030 |
| Cinnamon Cake | 3857 |
| Cinnamon Ice Cream | 3878 |
| Cinnamon Spice Latte | 3916 |
| Citrus Salad | 3733 |
| Citrus Star Jam | 30049 |
| Citrus Star Juice | 30043 |
| Citrus Star Soup | 30036 |
| Citrus Star Tart | 30038 |
| Clam Chowder | 3015 |
| Classic Golden Burger | 30115 |
| Cobb Salad | 11561 |
| Coconut Water | 3943 |
| Cod Sashimi | 11519 |
| Coffee | 3051 |
| Conch Cone | 30019 |
| Conjurmelon Bruschetta | 30150 |
| Conjurmelon Juice | 30170 |
| Conjurmelon Sorbet | 30176 |
| Cookie Spider | 11545 |
| Cookies | 3031 |
| Cooled Lava Honey | 3919 |
| Corn Dog | 3604 |
| Corn Flour | 3745 |
| Cotton Candy | 3617 |
| Crab Roll | 11520 |
| Cream Seltzer | 3913 |
| Creamy Beef Stew | 3018 |
| Creamy Mushroom Soup | 3711 |
| Creme Brulee | 3858 |
| Croquembouche | 30121 |
| Crystal Fruit Energy Bar | 30152 |
| Crystal Fruit Ice Cream | 30172 |
| Crystal Fruit Jam | 30177 |
| Crystal Fruit Mousse | 30158 |
| Cucumber Sandwiches | 30127 |
| Cupcake Mix | 3827 |
| Custard | 3825 |
| Daisy Honey | 2902 |
| Decaf Mocha | 30119 |
| Defense Essence | 3756 |
| Demon Coffee | 11260 |
| Demon Drink | 11536 |
| Demon Energy Juice | 11262 |
| Demonsoul Latte | 11263 |
| Devil Donut | 3614 |
| Deviled Eggs | 11571 |
| Double Scoop Delight | 30133 |
| Double Scoop Monster | 11389 |
| Dough | 3824 |
| Dragon Fruit Jam | 3072 |
| Dragon Tea | 11267 |
| Drinking Chocolate | 11500 |
| Dumplings | 3748 |
| Duorado Double Roll | 11230 |
| Earlygator Roll | 30068 |
| Earth Dragon Tea | 11278 |
| Eclair | 3862 |
| Eel Roll | 11527 |
| Eel Skewer | 11540 |
| Egg | 3007 |
| Egg Hash | 3011 |
| Egg Ramen | 3687 |
| Egg Tarts | 3012 |
| Eggplant Cola | 11508 |
| Eggplant Ravioli | 11581 |
| Elemental Cocktail | 11264 |
| Elios Gingerbread Cookie | 11503 |
| Elven Forest Cake | 11383 |
| Energy Smoothie | 3043 |
| Extraordinary Health Potion | 30137 |
| Eyeball Cocktail | 11538 |
| Eyeball Pizza | 11534 |
| Fairy Cherry Ice Cream | 11388 |
| Fairy Cherry Juice | 11369 |
| Fairy Cherry Water | 11376 |
| Fancy Grape Juice | 3918 |
| Fancy Hot Dog | 30108 |
| Fathom Fruit Jam | 30052 |
| Fathom Fruit Linguine | 30037 |
| Festive Oranges | 3684 |
| Figgy Pudding | 11506 |
| Fire Dragon Tea | 11277 |
| Fire Juice | 11269 |
| Fish and Chips | 3721 |
| Fish Roll | 30016 |
| Fish Taco | 3710 |
| Fish Tempura | 3050 |
| Fisherman's Essence | 3751 |
| Fizzy Fruit Fuel | 3909 |
| Fizzy Seltzer | 3910 |
| Flan | 3860 |
| Flour | 3003 |
| Fortitude Essence | 3753 |
| French Fries | 3601 |
| Fried Carp | 3036 |
| Fried Rice | 3035 |
| Frostfin Seltzer | 11584 |
| Fruit and Cheese Platter | 30126 |
| Fruit Blast Smoothie | 3906 |
| Fruit Cupcake | 11505 |
| Fruit Punch | 3703 |
| Fruit Snacks | 3734 |
| Fruit Tart | 3705 |
| Galaxy Smoothie | 11593 |
| Garden Festival Blooming Tea | 30077 |
| Garden Festival Dango | 30076 |
| Garden Festival Lamb Shanks | 30075 |
| Garden Festival Salad | 30072 |
| Garden Festival Souffle | 30073 |
| Geometric Squid Roll | 30193 |
| Ghosthead Tuna Sashimi | 11226 |
| Ghoul Fish Roll | 11217 |
| Ginger Juice | 3893 |
| Gingerbread House | 11532 |
| Gingerbread Man | 11529 |
| Gnocchi | 11580 |
| Golden Berry Porridge | 11351 |
| Golden Berry Smoothie | 11352 |
| Golden Brine Berry Pavlova | 30057 |
| Golden Brinestone Feast | 30059 |
| Golden Citrus Star Fruit Rice Bowl | 30056 |
| Golden Egg | 3052 |
| Golden Egg on Rice | 11353 |
| Golden Fathom Fruit Stirfry | 30053 |
| Golden Grilled Nautitrine and Pepper Salmon | 30058 |
| Golden Mac and Cheese | 11354 |
| Golden Macarons | 11350 |
| Golden Milk | 2920 |
| Golden Milk Cake | 11355 |
| Golden Mushroom Burger | 11356 |
| Golden Omelette | 11357 |
| Golden Pomegranate | 3053 |
| Golden Pomegranate Jam | 3077 |
| Golden Potato Salad | 11358 |
| Golden Sandwich | 11359 |
| Golden Scallo-Papaya Risotto | 30054 |
| Golden Scrambled Eggs | 11360 |
| Golden Slime Ink Pasta | 11361 |
| Golden Slime Ink Soup | 11362 |
| Golden Spicy Noodles | 11363 |
| Golden Upside Down Trench Nut Cake | 30055 |
| Grape Jam | 3070 |
| Gray Scale Smoothie | 11370 |
| Gray Scale Tea | 11377 |
| Greenspice | 3005 |
| Grilled Alchemyjack | 30183 |
| Grilled Archerfish | 30188 |
| Grilled Blue Tang | 11240 |
| Grilled Bucketfish | 30061 |
| Grilled Carp | 11241 |
| Grilled Catfish | 11242 |
| Grilled Cheese | 3723 |
| Grilled Conjurmelon | 30156 |
| Grilled Corn | 3936 |
| Grilled Crab | 11243 |
| Grilled Earlygator | 30060 |
| Grilled Frostfin | 11244 |
| Grilled Pineapple | 11576 |
| Grilled Whitebelly Shark | 11245 |
| Guacamole | 30161 |
| Guava Jam | 11589 |
| Haloopbut Sashimi | 30071 |
| Hard Butterscotch Gem | 3760 |
| Hearty Pie | 3834 |
| Hexfruit Jam | 30171 |
| Hexfruit Wizard's Bowl | 30151 |
| Hibiscus Honey | 2904 |
| Hibiscus Tea | 30118 |
| Holiday Hot Cocoa | 11504 |
| Honey | 3008 |
| Honeybrew | 11594 |
| Honeycomb Cake | 3855 |
| Honeyglazed Apple | 3027 |
| Hot Chocolate | 3915 |
| Hot Dog | 3931 |
| Hummus | 11573 |
| Hydrangea Cupcake | 3746 |
| Ice Cream | 3718 |
| Ice Cream Base | 3826 |
| Ice Cream Sandwich | 3615 |
| Ice Cream Whip | 3940 |
| Indiglow Tea | 11265 |
| Island Punch | 3941 |
| Island Skewer | 3938 |
| Jack'o'fin Sashimi | 11219 |
| Jawbreaker Gem | 3761 |
| Jelly Pop | 30017 |
| Just Peachy Double Scoop | 11391 |
| Kale Juice | 3896 |
| Kelp Soup | 30012 |
| Kettle Chips | 3600 |
| Kiwi Juice | 11591 |
| Kraken Cola | 11513 |
| Lasagna | 3716 |
| Lava Brew | 30111 |
| Lavender Honey | 2907 |
| Leaf Wrapped Averagemouth Bass | 11246 |
| Leaf Wrapped Bashful Pike | 11247 |

</details>

<details>
<summary>Leaf Wrapped Blue Gill – Triangle Jam (300 items)</summary>

| Item name | ID |
| --- | ---: |
| Leaf Wrapped Blue Gill | 11248 |
| Leaf Wrapped Cuddlefish | 11249 |
| Leaf Wrapped Haloopbut | 30062 |
| Leaf Wrapped Ribbon Eel | 11250 |
| Leaf Wrapped Searback | 11251 |
| Leaf Wrapped Silver Carp | 11252 |
| Leaf Wrapped Squawkmouth Bass | 30063 |
| Leaf Wrapped Tiger Trout | 11253 |
| Leaf-Wrapped Geometric Squid | 30187 |
| Leaf-Wrapped Hocus-Puffus | 30182 |
| Lemon Cake | 3850 |
| Lemon Jam | 11587 |
| Lemon Meringue | 3838 |
| Lemonade | 3897 |
| Lily Honey | 2908 |
| Linguine with Clams | 3706 |
| Living Jelly Salad | 11227 |
| Loaded Fries | 30116 |
| Loaded Hot Dog | 30107 |
| Lobster Bisque | 3722 |
| Lobster Roll | 3714 |
| Lobster Sushi | 11528 |
| Lotus Honey | 2909 |
| Macarons | 30123 |
| Mage's Mana Brew | 30110 |
| Magic Mana Boba | 30120 |
| Magical Water | 11270 |
| Magically Delicious Drink | 3917 |
| Mana Cone | 30132 |
| Mana Gem Jam | 3071 |
| Mana Water | 11268 |
| Marshmallow Ghost | 3606 |
| Mashed Potatoes | 3014 |
| Meat | 21005 |
| Meat Skewer | 3934 |
| Melting Mana Pop | 30135 |
| Microphone Ice Cream | 3925 |
| Milk | 3006 |
| Milk and Cookies | 11530 |
| Mind Essence | 3754 |
| Mining Essence | 3750 |
| Mixed Berry Smoothie | 3903 |
| Mochi | 3739 |
| Mochi Covered Strawberry | 3731 |
| Monster Burger | 11541 |
| Monster Fruit Granola Bar | 11386 |
| Monster Fruit Jam | 11366 |
| Moon Cake | 3688 |
| Moon Cream | 11539 |
| Moon Cream Pie | 3616 |
| Moonplant Cola | 11507 |
| Mulled Cider | 11501 |
| Mushroom Festival Apple Kebab | 30089 |
| Mushroom Festival Elote | 30087 |
| Mushroom Festival Peach Cobbler | 30086 |
| Mushroom Festival Pumpkin Pie | 30085 |
| Mushroom Festival Pumpkin Seeds | 30088 |
| Mushroom Pie | 3833 |
| Mushroom Risotto | 3738 |
| Mushroom Saute | 30129 |
| Mushroom Stroganoff | 3740 |
| Music Note Cupcake | 3923 |
| Music Note Dip | 3926 |
| Nachos | 3713 |
| Nautitrine Crab Kabob | 30034 |
| Nautitrine Fruit Jam | 30051 |
| Nautitrine Juice | 30045 |
| Nautitrine Sorbet | 30040 |
| Neapolitan Ice Cream | 3879 |
| Nectar-ine Crumble | 11384 |
| Nectar-ine Jam | 11365 |
| Nectar-ine Sorbet | 11387 |
| Nectar-ine Tea | 11375 |
| Noodles | 3004 |
| Omelet | 3720 |
| Onion Rings | 3724 |
| Orange Cream Cake | 3842 |
| Orange Jam | 3064 |
| Orange Juice | 3891 |
| Orchid Honey | 2903 |
| Overly Iced Cupcake | 3611 |
| Pad Thai | 3715 |
| Panettone | 11533 |
| Panna Cotta | 30122 |
| Peach Cobbler | 3034 |
| Peach Cream Cake | 3846 |
| Peach Jam | 3065 |
| Peaches and Cream | 3707 |
| Pepperoni Music Pizza | 3927 |
| Persian Love Cake | 3853 |
| Pet Festival Chocolate Ice Cream Taco | 30079 |
| Pet Festival Cucumber Sandwich | 30082 |
| Pet Festival Egg Salad Sandwich | 30083 |
| Pet Festival Strawberry Lemonade | 30078 |
| Pet Festival Watermelon Salad | 30081 |
| Piano Cake | 3929 |
| Piano Panini | 3924 |
| Pickled Veggie Salad | 3039 |
| Pie Crust | 3828 |
| Pina Colada | 3942 |
| Pineapple Jam | 11588 |
| Pineapple Juice | 3894 |
| Pink Lemon Coffeenade | 30109 |
| Pizza | 3024 |
| Plain Hot Dog | 30106 |
| Plain Tart | 3861 |
| Poached Trench Nut | 30035 |
| Poke Bowl | 3727 |
| Popcorn | 3028 |
| Pork Ramen | 3686 |
| Pot Pie | 3026 |
| Pot Roast | 11563 |
| Potato Salad | 3717 |
| Pricklepop Pear Jam | 3075 |
| Prickletot Pear Jam | 3074 |
| Princess Pop | 3908 |
| Pufferfish Sashimi | 11518 |
| Pulled Pork Sandwich | 11562 |
| Pumpkin Soda | 11511 |
| Purple Velvet Pancakes | 3928 |
| Rainbow Roll | 11524 |
| Raspberry Crepes | 3704 |
| Raspberry Doughnuts | 11531 |
| Raspberry Jam | 3062 |
| Raspberry Pie | 3867 |
| Raspberry Smoothie | 3904 |
| Raspberry Sorbet | 3872 |
| Ravioli | 30130 |
| Razor Stalk Tea | 11259 |
| Red Roses Honey | 2900 |
| Red Snapper Sashimi | 11525 |
| Red Veggie Soup | 3017 |
| Red Velvet Cake | 3920 |
| Red Velvet Cupcake | 3852 |
| Redfinned Pincher Sushi Roll | 11225 |
| Rice Ball Soup | 3749 |
| Rice Pilaf | 3882 |
| Roasted Albascroll | 30181 |
| Roasted Black Bass | 11233 |
| Roasted Dorado | 11234 |
| Roasted Earlygator | 30064 |
| Roasted Flower Flounder | 11235 |
| Roasted Hexfruit Salad | 30157 |
| Roasted Old Boot | 11236 |
| Roasted Prism Minnow | 30186 |
| Roasted Rainbow Trout | 11237 |
| Roasted Sea Bass | 11238 |
| Roasted Squawkmouth Bass | 30065 |
| Roasted Tuna | 11239 |
| Roasted Turnip | 3883 |
| Rock Candy Gem | 3759 |
| Rocky Road Smoothie | 11271 |
| Root Beer | 11558 |
| Salmon Roll | 11522 |
| Salsa | 3737 |
| Saltwater Lollipop | 30020 |
| Saltwater Taffy | 30021 |
| Sand Dollar Cookie | 30018 |
| Sandstone Sashimi | 11516 |
| Sandy Ice Cream | 3874 |
| Sausage | 3933 |
| Scallo-Papaya Fritters | 30033 |
| Scallo-Papaya Jam | 30047 |
| Scallo-Papaya Smoothie | 30042 |
| Scrambled Eggs | 11568 |
| Sea Salt Twist | 30015 |
| Seafood Gumbo | 3726 |
| Seared Acorn Anchovy | 11254 |
| Seared Bucketfish | 30067 |
| Seared Eyelotl | 30189 |
| Seared Haloopbut | 30066 |
| Seared Ironhead Sturgeon | 11255 |
| Seared Lobster | 11256 |
| Seared Pufferfish | 11257 |
| Seared Red Snapper | 11258 |
| Seared Spectral Drifter | 30184 |
| Seaweed | 3002 |
| Seaweed Ice Cream | 3873 |
| Sesame Rice Ball | 3041 |
| Shimmeroot Jam | 3069 |
| Shimmeroot Treat | 3042 |
| Short Ribs | 11575 |
| Shrimp Skewer | 3939 |
| Simple Attack Damage Tome | 18112 |
| Simple Health Tome | 18114 |
| Simple Spell Damage Tome | 18110 |
| Small Blue Glorite Crystal | 3762 |
| Small Glorite Crystal | 60252 |
| Small Magenta Glorite Crystal | 3764 |
| Small Purple Glorite Crystal | 3763 |
| Small Red Glorite Crystal | 3765 |
| Smoked Gouda Crepe | 30131 |
| Snaccoon Festival Dumpling | 30103 |
| Snaccoon Festival Gummy | 30104 |
| Snaccoon Festival Juice Box | 30101 |
| Snaccoon Festival Pancakes | 30105 |
| Snaccoon Festival Popsicle | 30102 |
| Snappy Juice | 11261 |
| Snow Cone | 11569 |
| Snow Festival Cranberry Juice | 30094 |
| Snow Festival Eggnog | 30093 |
| Snow Festival Frosted Donut | 30090 |
| Snow Festival Fruit Cake | 30092 |
| Snow Festival Ham | 30095 |
| Snow Festival Sugar Cookies | 30091 |
| Sombasu's Fortune #1 | 31001 |
| Sombasu's Fortune #10 | 31010 |
| Sombasu's Fortune #11 | 31011 |
| Sombasu's Fortune #12 | 31012 |
| Sombasu's Fortune #13 | 31013 |
| Sombasu's Fortune #14 | 31014 |
| Sombasu's Fortune #15 | 31015 |
| Sombasu's Fortune #16 | 31016 |
| Sombasu's Fortune #17 | 31017 |
| Sombasu's Fortune #2 | 31002 |
| Sombasu's Fortune #3 | 31003 |
| Sombasu's Fortune #4 | 31004 |
| Sombasu's Fortune #5 | 31005 |
| Sombasu's Fortune #6 | 31006 |
| Sombasu's Fortune #7 | 31007 |
| Sombasu's Fortune #8 | 31008 |
| Sombasu's Fortune #9 | 31009 |
| Souffle | 3863 |
| Soul Fizz | 11510 |
| Soul Orb Jam | 3076 |
| Sour Plum Jam | 11367 |
| Sour Plum Sorbet | 11390 |
| Spaghetti | 3023 |
| Spellberry Glazed Dorado | 30159 |
| Spellberry Jam | 30173 |
| Spellberry Juice | 30178 |
| Spellberry Tartlets | 30153 |
| Spiced Cider | 11502 |
| Spiced Cocoa | 3911 |
| Spicy Catsup | 11275 |
| Spicy Noodles | 11574 |
| Spicy Ramen | 3021 |
| Spicy Shrimp Ramen | 3685 |
| Spider Pie | 11535 |
| Spiked Salmon Sashimi | 11216 |
| Spikey Soda | 11509 |
| Spring Roll | 3040 |
| Squawkmouth Bass Roll | 30069 |
| Squid Tacos | 11577 |
| Steak | 3884 |
| Steamed Eggplant | 3889 |
| Strawberry Banana Smoothie | 3905 |
| Strawberry Cake | 3843 |
| Strawberry Ice Cream | 3870 |
| Strawberry Jam | 3063 |
| Strawberry Juice | 3922 |
| Strawberry Milk | 3701 |
| Strawberry Pie | 3835 |
| Strawberry Salad | 11570 |
| Strawberry Shortcake | 3730 |
| Strength Essence | 3757 |
| Stuffed Casserole | 3033 |
| Stuffed Peppers | 11578 |
| Sucker Soda | 11514 |
| Sugar | 3009 |
| Sugar Apple Brulee with Ice Cream | 30160 |
| Sugar Apple Herbal Soup | 30154 |
| Sugar Apple Ice Cream | 30179 |
| Sugar Apple Juice | 30174 |
| Sugar Cake | 3847 |
| Sugar Plum Jam | 11364 |
| Sugar Plum Pie | 11382 |
| Sugar Plum Tea | 11378 |
| Sugar Teeth | 11543 |
| Sugarcane Juice | 3898 |
| Sun Flower Honey | 2906 |
| Sundae Swirl | 30136 |
| Super Galaxy Smoothie | 11595 |
| Supper Skillet | 11565 |
| Sweet and Spicy Shrimp | 3725 |
| Sweet Melon Soda | 11515 |
| Swordfish Sashimi | 11523 |
| Tavern Burger | 11560 |
| Tea | 3914 |
| Tekka Maki | 11521 |
| Tentacle Fries | 11542 |
| Tentacle Kebab | 3602 |
| The Prehistoric Special | 3877 |
| Tiger Roll | 11526 |
| Tikka Masala | 3708 |
| Tomato Jam | 3066 |
| Tomato Juice | 3096 |
| Tomato Salad | 3038 |
| Tomato Soup | 3019 |
| Tombmelon Jam | 3073 |
| Tombmelon Soda | 11512 |
| Tooth Juice | 11537 |
| Tortilla | 3744 |
| Tortilla Chips | 3736 |
| Trail Mix | 3742 |
| Treasure-Finder's Breakfast | 30163 |
| Trench Nut Crumble | 30039 |
| Trench Nut Jam | 30048 |
| Trench Nut Milk | 30044 |
| Triangle Jam | 11590 |

</details>

<details>
<summary>Tropical Punch – Zaria&#x27;s Bucket (28 items)</summary>

| Item name | ID |
| --- | ---: |
| Tropical Punch | 3921 |
| Tropical Slime | 30026 |
| Tulip Honey | 2905 |
| Tuna Nigiri | 3735 |
| Tuna Sashimi | 11517 |
| Two Peas and a Pod | 3881 |
| Two-In-One Recovery Potion | 30139 |
| Veggie Kebab | 3729 |
| Veggie Wrap | 3741 |
| Viperfish Sashimi | 11232 |
| Waffles | 3712 |
| Water Bear Soup | 11231 |
| Water Dragon Tea | 11276 |
| Watermelon Juice | 11592 |
| Wind Chime Tea | 11273 |
| Witch's Fingers | 11548 |
| Withercake | 3854 |
| Withergate Ball Chocolate Banana | 30097 |
| Withergate Ball Elite Corndog | 30096 |
| Withergate Ball Glowing Boba Tea | 30098 |
| Withergate Ball Sweet Cream Pie | 30099 |
| Withergate Ball Taco | 30100 |
| Woodcutter's Essence | 3752 |
| Yam Fettuccine Alfredo | 11586 |
| Yogurt | 3886 |
| Yogurt Parfait | 3719 |
| Yucky Green Juice | 3900 |
| Zaria's Bucket | 21151 |

</details>

### Forageables from game data

**75 items**

| Item name | ID |
| --- | ---: |
| Apple | 3044 |
| Avocado | 30149 |
| Berry | 16500 |
| Berry Forageable | 16400 |
| Blueberry | 3046 |
| Brine Berry | 30009 |
| Citrus Star Fruit | 30001 |
| Clam | 2104 |
| Conjurmelon | 30143 |
| Crystal Fruit | 30146 |
| Dead Hardwood | 2012 |
| Dead Hardwood Plank | 2014 |
| Dead Log | 2011 |
| Dead Plank | 2013 |
| Driftwood | 2101 |
| Earth Crystal | 1111 |
| Earth Crystal Forageable | 16409 |
| Elven Health Book | 18024 |
| Fallen Log | 2106 |
| Fathom Fruit | 11399 |
| Fire Crystal | 1110 |
| Fire Crystal Forageable | 16408 |
| Golden Apple | 3054 |
| Golden Avocado | 30169 |
| Golden Berry | 3098 |
| Golden Blueberry | 3056 |
| Golden Brine Berry | 60277 |
| Golden Citrus Star Fruit | 60275 |
| Golden Conjurmelon | 30164 |
| Golden Crystal Fruit | 30166 |
| Golden Fabled Silk | 60257 |
| Golden Fathom Fruit | 60273 |
| Golden Hexfruit | 30165 |
| Golden Mushroom | 3099 |
| Golden Nautitrine Fruit | 60274 |
| Golden Orange | 3055 |
| Golden Peach | 3058 |
| Golden Raspberry | 3059 |
| Golden Scallo-Papaya | 60276 |
| Golden Silk | 2116 |
| Golden Spellberry | 30167 |
| Golden Spooky Silk | 60258 |
| Golden Strawberry | 3057 |
| Golden Sugar Apple | 30168 |
| Hardwood | 2007 |
| Hardwood Beam | 2009 |
| Hardwood Plank | 2008 |
| Hexfruit | 30145 |
| Large Mana Tome | 18004 |
| Log | 2002 |
| Mana Tome Forageable | 16404 |
| Money Bag Forageable | 16401 |
| Mushroom | 3001 |
| Nautitrine Fruit | 30002 |
| Ocean Treasure Chest | 2105 |
| Orange | 3045 |
| Peach | 3048 |
| Raspberry | 3049 |
| Red Mushroom Forageable | 16407 |
| Sand Dollar | 2102 |
| Scallo-Papaya | 30011 |
| Seaweed | 3002 |
| Seaweed Node | 2108 |
| Silk | 2005 |
| Small Mana Tome | 18003 |
| Small Money Bag | 18000 |
| Spellberry | 30147 |
| Starfish | 2103 |
| Strawberry | 3047 |
| Sugar Apple | 30148 |
| Trench Nut | 30010 |
| Water Crystal | 1112 |
| Water Crystal Forageable | 16420 |
| Wood Beam | 2010 |
| Wood Plank | 2003 |

### Fruits from game data

**54 items**

| Item name | ID |
| --- | ---: |
| Apple | 3044 |
| Avocado | 30149 |
| Berry | 16500 |
| Blueberry | 3046 |
| Brine Berry | 30009 |
| Candy Corn Fruit | 11396 |
| Citrus Star Fruit | 30001 |
| Conjurmelon | 30143 |
| Crystal Fruit | 30146 |
| Fairy Cherry | 11395 |
| Fathom Fruit | 11399 |
| Golden Apple | 3054 |
| Golden Avocado | 30169 |
| Golden Berry | 3098 |
| Golden Blueberry | 3056 |
| Golden Brine Berry | 60277 |
| Golden Candy Corn Fruit | 60266 |
| Golden Citrus Star Fruit | 60275 |
| Golden Conjurmelon | 30164 |
| Golden Crystal Fruit | 30166 |
| Golden Fairy Cherry | 60264 |
| Golden Fathom Fruit | 60273 |
| Golden Gray Scale | 60263 |
| Golden Hexfruit | 30165 |
| Golden Monster Fruit | 60268 |
| Golden Mushroom | 3099 |
| Golden Nautitrine Fruit | 60274 |
| Golden Nectar-ine | 60262 |
| Golden Orange | 3055 |
| Golden Peach | 3058 |
| Golden Raspberry | 3059 |
| Golden Scallo-Papaya | 60276 |
| Golden Sour Plum | 60267 |
| Golden Spellberry | 30167 |
| Golden Strawberry | 3057 |
| Golden Sugar Apple | 30168 |
| Golden Sugar Plum | 60265 |
| Golden Trench Nut | 60278 |
| Gray Scale | 11394 |
| Hexfruit | 30145 |
| Monster Fruit | 11398 |
| Mushroom | 3001 |
| Nautitrine Fruit | 30002 |
| Nectar-ine | 11393 |
| Orange | 3045 |
| Peach | 3048 |
| Raspberry | 3049 |
| Scallo-Papaya | 30011 |
| Sour Plum | 11397 |
| Spellberry | 30147 |
| Strawberry | 3047 |
| Sugar Apple | 30148 |
| Sugar Plum | 11392 |
| Trench Nut | 30010 |

### Furniture from game data

**1,755 items**

<details>
<summary>Acorn Moth – Contemporary Table (300 items)</summary>

| Item name | ID |
| --- | ---: |
| Acorn Moth | 21683 |
| Acorn Painting | 4304 |
| Acorn Plushie | 4296 |
| Air Hockey Table | 31200 |
| Alien Bed | 4232 |
| Alien Chair | 4233 |
| Alien Couch | 4226 |
| Alien End Table | 4231 |
| Alien Lamp | 4227 |
| Alien Rug | 4230 |
| Alien Table | 4229 |
| Alien Wardrobe | 4228 |
| All Seeing Window | 4345 |
| Angel Fox Plushie | 14035 |
| Angelic Floral Tea Pot | 21226 |
| Angelic Incense | 21227 |
| Angelic Lamp | 4446 |
| Angelic Stool | 4445 |
| Angelic Turtle Plush | 4443 |
| Angelic Vanity | 4447 |
| Angelic Window | 3954 |
| Angelic Wing Plush | 4444 |
| Angler Snaccoon Plush | 3779 |
| Anne Plushie | 21493 |
| Anne's Bed | 21489 |
| Anne's Candelabra | 21484 |
| Anne's Chair | 21482 |
| Anne's Couch | 21481 |
| Anne's Jewelry Display | 21487 |
| Anne's Night Stand | 21490 |
| Anne's Ottoman | 21491 |
| Anne's Rug | 21488 |
| Anne's Safe | 21486 |
| Anne's Sweet Table | 21492 |
| Anne's Vanity | 21485 |
| Anne's Wardrobe | 21483 |
| Anvil (Old) | 9352 |
| Apothecary Cabinet | 3812 |
| Arcade Rug | 4171 |
| Archeology Bed | 3964 |
| Archeology Chair | 3969 |
| Archeology Couch | 3966 |
| Archeology End Table | 3968 |
| Archeology Lamp | 3971 |
| Archeology Rug | 3967 |
| Archeology Table | 3965 |
| Archeology Wardrobe | 3970 |
| Artist Supply Bookshelf | 4599 |
| Artistic Kotatsu | 4423 |
| Artistic Lantern | 4422 |
| Auto-Mixer | 21218 |
| Baker's Meal Board | 4405 |
| Baker's Pie Table | 4404 |
| Baker's Pretzel Stool | 4403 |
| Bamboo Display | 4453 |
| Bamboo Door | 11720 |
| Bamboo Patio | 11721 |
| Bamboo Roof | 11722 |
| Bamboo Walls | 11723 |
| Bamboo Windows | 11724 |
| Barn Permit | 11113 |
| Baroque Fridge | 4626 |
| Baseball Set | 14028 |
| Basic Door | 11136 |
| Basic Patio | 11135 |
| Basic Roof | 11138 |
| Basic Walls | 11139 |
| Basic Windows | 11137 |
| Basket of Fruit | 3802 |
| Bat Shaped Window | 4344 |
| Beach Snaccoon Plush | 3777 |
| Bed | 9000 |
| Bed of Luxury | 4493 |
| Bee Box | 9360 |
| Bent Bar Window | 4131 |
| Berry Forageable | 16400 |
| Birdhouse Lamp | 21380 |
| Birthday Bed | 50465 |
| Birthday Chair | 50467 |
| Birthday Couch | 50468 |
| Birthday Lamp | 50471 |
| Birthday Place Settings | 50472 |
| Birthday Table | 50470 |
| Birthday Wardrobe | 50466 |
| Bitty Doll | 14019 |
| Black Bishop | 31219 |
| Black Display Katana | 21395 |
| Black King | 31227 |
| Black Knight | 31221 |
| Black Marble Counter | 4101 |
| Black Marble Vanity | 4190 |
| Black Pawn | 31223 |
| Black Queen | 31225 |
| Black Rook | 31217 |
| Blacksmith's Shield Display | 4441 |
| Blacksmith's Sword Display | 4442 |
| Bloom and Doom Bed | 21366 |
| Bloom and Doom Chair | 21372 |
| Bloom and Doom Couch | 21369 |
| Bloom and Doom End Table | 21371 |
| Bloom and Doom Lamp | 21373 |
| Bloom and Doom Record Player | 21374 |
| Bloom and Doom Rug | 21367 |
| Bloom and Doom Table | 21370 |
| Bloom and Doom Wardrobe | 21368 |
| Blooming Bunny Window | 4247 |
| Blooming Flower Arrangement | 14014 |
| Blue and Green Toy Dinosaurs | 4204 |
| Blue and Purple Beach Umbrella | 4018 |
| Blue Daisy Plushie | 4244 |
| Blue Display Katana | 21397 |
| Blue Lava Lamp | 31230 |
| Blue Polka Dot Door | 11785 |
| Blue Polka Dot Patio | 11786 |
| Blue Polka Dot Roof | 11787 |
| Blue Polka Dot Walls | 11788 |
| Blue Polka Dot Windows | 11789 |
| Blue Snow Globe Lamp | 21472 |
| Blue Snow Yeti Bean Bag Chair | 21469 |
| Blue Snow Yeti Chair | 21467 |
| Blue Snow Yeti Couch | 21470 |
| Blue Snow Yeti Lamp | 21468 |
| Blue Snow Yeti Lounge Chair | 21479 |
| Blue Striped Door | 11735 |
| Blue Striped Patio | 11736 |
| Blue Striped Roof | 11737 |
| Blue Striped Walls | 11738 |
| Blue Striped Windows | 11739 |
| Blue Tea Cushion | 21411 |
| Blue Tiled Door | 11150 |
| Blue Tiled Patio | 11151 |
| Blue Tiled Roof | 11152 |
| Blue Tiled Walls | 11153 |
| Blue Tiled Windows | 11154 |
| Blue Toy Dinosaur | 4207 |
| Blue Yeti Snow Globe | 21471 |
| Blue, Green, and Red Toy Dinosaurs | 4205 |
| Bonsai End Table | 21399 |
| Bonsai Lantern | 21417 |
| Branch Circle Window | 3962 |
| Bridge Customization Kit | 11123 |
| Bright Star Table | 4618 |
| Brinestone Statue | 31100 |
| Bronze Flower Sculpture | 14017 |
| Bronze Porthole Window | 4031 |
| Brown Cobblestone Door | 11485 |
| Brown Cobblestone Patio | 11486 |
| Brown Cobblestone Roof | 11487 |
| Brown Cobblestone Walls | 11488 |
| Brown Cobblestone Windows | 11489 |
| Brown Leather Couch | 50003 |
| Brown Stone Door | 11705 |
| Brown Stone Patio | 11706 |
| Brown Stone Roof | 11707 |
| Brown Stone Walls | 11708 |
| Brown Stone Windows | 11709 |
| Bubble Panic | 31203 |
| Budded Flower Arrangement | 14015 |
| Bunny Couch | 9007 |
| Bunny Lamp | 9022 |
| Bunny Side Table | 10007 |
| Bunny Snaccoon Plush | 3776 |
| Bunny Table | 9017 |
| Bunny Wardrobe | 10008 |
| Button Stool | 4590 |
| Cabin Bookshelf | 4600 |
| Cabin Couch | 4596 |
| Calico Cat Bed | 4115 |
| Calico Cat Chair | 4121 |
| Calico Cat Couch | 4119 |
| Calico Cat End Table | 4118 |
| Calico Cat Lamp | 4122 |
| Calico Cat Rug | 4117 |
| Calico Cat Table | 4120 |
| Calico Cat Tower | 4116 |
| Camper Snaccoon Plush | 3784 |
| Candle | 10004 |
| Candy Chair | 4593 |
| Captain's Chair | 4452 |
| Captain's Wall Art | 4451 |
| Cardboard Bed | 21740 |
| Cardboard Chair | 21738 |
| Cardboard Couch | 21744 |
| Cardboard Door | 11710 |
| Cardboard Dresser | 21737 |
| Cardboard End Table | 21743 |
| Cardboard Mailbox | 21742 |
| Cardboard Patio | 11711 |
| Cardboard Roof | 11712 |
| Cardboard Rug | 21741 |
| Cardboard Table | 21739 |
| Cardboard Wall Painting | 21736 |
| Cardboard Walls | 11713 |
| Cardboard Windows | 11714 |
| Carnival Balloons | 50005 |
| Carnival Bed | 4185 |
| Carnival Couch | 4181 |
| Carnival Lamp | 4183 |
| Carnival Rug | 4187 |
| Carnival Table | 4182 |
| Carnival Wardrobe | 4184 |
| Carved Kotatsu | 21424 |
| Carved Pumpkin Lamp | 4217 |
| Castle Door | 11490 |
| Castle Patio | 11491 |
| Castle Roof | 11492 |
| Castle Walls | 11493 |
| Castle Windows | 11494 |
| Cat Door | 11155 |
| Cat Patio | 11156 |
| Cat Roof | 11157 |
| Cat Scratcher | 21384 |
| Cat Scratching Post | 21217 |
| Cat Treat Rug | 21383 |
| Cat Walls | 11158 |
| Cat Windows | 11159 |
| Catherine Plushie | 21505 |
| Catherine's Bed | 21504 |
| Catherine's Cauldron | 21497 |
| Catherine's Chair | 21494 |
| Catherine's Couch | 21503 |
| Catherine's Decorative Mushroom Branch | 21499 |
| Catherine's Display Case | 21495 |
| Catherine's Gathering Basket | 21502 |
| Catherine's Low Table | 21498 |
| Catherine's Rug | 21500 |
| Catherine's Spell Book | 21501 |
| Catherine's Table | 21496 |
| Celestial Cauldron End Table | 21360 |
| Celestial Chair | 21362 |
| Celestial Couch | 21359 |
| Celestial Night Light | 21365 |
| Celestial Ram Bed | 21361 |
| Celestial Wardrobe | 21363 |
| Chaotic Painting | 4340 |
| Charming Door | 11480 |
| Charming Patio | 11481 |
| Charming Roof | 11482 |
| Charming Walls | 11483 |
| Charming Windows | 11484 |
| Checkered Stacked Storage Shelves | 21413 |
| Chess Bed | 31209 |
| Chess Board Rug | 31216 |
| Chess Chair | 31213 |
| Chess Couch | 31211 |
| Chess End Table | 31215 |
| Chess Lamp | 31212 |
| Chess Rug | 31210 |
| Chess Table | 31214 |
| Chess Wardrobe | 31208 |
| Chest | 10110 |
| Chick Plushie | 4242 |
| Chronologically Coordinated Clocks | 31104 |
| Circus Bigtop Rug | 4603 |
| Clam Shaped Window | 4272 |
| Clam Shell Bed | 4571 |
| Classic Barn Window | 4030 |
| Classic Beach Umbrella | 4017 |
| Classic Brick Door | 11700 |
| Classic Brick Patio | 11701 |
| Classic Brick Roof | 11702 |
| Classic Brick Walls | 11703 |
| Classic Brick Windows | 11704 |
| Classic Snowy Rug | 4316 |
| Classic Withergate Jester Plushie | 4338 |
| Claude Plushie | 21518 |
| Claude's Bed | 21517 |
| Claude's Candelabra | 21509 |
| Claude's Chair | 21506 |
| Claude's Couch | 21510 |
| Claude's Desk | 21508 |
| Claude's End Table | 21512 |
| Claude's Harp | 21513 |
| Claude's Ottoman | 21511 |
| Claude's Piano | 21515 |
| Claude's Rug | 21507 |
| Claude's Stool | 21514 |
| Claude's Wardrobe | 21516 |
| Closed Beach Cooler | 4555 |
| Cloudy Day End Table | 4619 |
| Cloudy Day Wardrobe | 4615 |
| Cluttered Apothecary Cabinet | 3813 |
| Cluttered Study Desk | 21393 |
| Cluttered Temple Wardrobe | 21430 |
| Coal Chair | 21448 |
| Coal Couch | 21445 |
| Coal End Table | 21454 |
| Coal Table | 21449 |
| Coal Wardrobe | 21452 |
| Cold Barbeque Grill | 4581 |
| Colorful Cat Tower | 4386 |
| Confetti Rug | 50469 |
| Conjured Brazier | 21221 |
| Contemporary Bed | 3981 |
| Contemporary Chair | 3987 |
| Contemporary Couch | 3980 |
| Contemporary End Table | 3985 |
| Contemporary Lamp | 3983 |
| Contemporary Rug | 3982 |
| Contemporary Table | 3986 |

</details>

<details>
<summary>Contemporary Wardrobe – Gilded Celestial Rug (300 items)</summary>

| Item name | ID |
| --- | ---: |
| Contemporary Wardrobe | 3984 |
| Coral Compass | 31102 |
| Cottage Core Door | 11475 |
| Cottage Core Patio | 11476 |
| Cottage Core Roof | 11477 |
| Cottage Core Walls | 11478 |
| Cottage Core Windows | 11479 |
| Cow Print Door | 11160 |
| Cow Print Patio | 11161 |
| Cow Print Roof | 11162 |
| Cow Print Walls | 11163 |
| Cow Print Windows | 11164 |
| Cowboy Snaccoon Plush | 3782 |
| Cozy Pet Bed | 4384 |
| Crafting Table (Old) | 9350 |
| Crissy Doll | 14022 |
| Cute Bunny Picture | 4431 |
| Cute Coat Rack | 4015 |
| Cute Cooking Rack | 4432 |
| Cute Dinosaur Bed | 4215 |
| Cute Dinosaur Blue Chair | 4209 |
| Cute Dinosaur Blue Rug | 4202 |
| Cute Dinosaur Brown Rug | 4203 |
| Cute Dinosaur Comfy Chair | 4212 |
| Cute Dinosaur Couch | 4211 |
| Cute Dinosaur Lamp | 4200 |
| Cute Dinosaur Red Chair | 4210 |
| Cute Dinosaur Table | 4201 |
| Cute Dinosaur Tall Statue | 4213 |
| Cute Dinosaur Toy Egg Nest | 4216 |
| Cute Dinosaur Wardrobe | 4199 |
| Cute Jam Rack | 4433 |
| Cute Vanity | 4434 |
| Cutesy Snaccoon Squishy Plushie | 4364 |
| Cyberpop Arc Capacitor | 21280 |
| Cyberpop Bed | 21276 |
| Cyberpop Bicycle | 21273 |
| Cyberpop Couch | 21277 |
| Cyberpop Desk | 21284 |
| Cyberpop Globe | 21283 |
| Cyberpop Hover Bike | 21274 |
| Cyberpop Motorcycle | 21275 |
| Cyberpop Record Player | 21281 |
| Cyberpop Rug | 21286 |
| Cyberpop Student Chair | 21282 |
| Cyberpop Student Chest | 21278 |
| Cyberpop Table | 21285 |
| Cyberpop Throne | 21272 |
| Cyberpop Wardrobe | 21279 |
| Daisy Screen Divider | 21406 |
| Darius Plushie | 21764 |
| Darius' Bed | 21758 |
| Darius' Candle Display | 21761 |
| Darius' Chair | 21755 |
| Darius' Couch | 21760 |
| Darius' Desk | 21756 |
| Darius' Romantic Bust | 21762 |
| Darius' Rug | 21759 |
| Darius' Single Rose | 21757 |
| Darius' Table | 21754 |
| Darius' Wardrobe | 21763 |
| Deadwood Chair | 4219 |
| Deadwood Chest | 4098 |
| Deadwood End Table | 4218 |
| Deadwood Lamp | 4221 |
| Deadwood Sign | 4223 |
| Deadwood Table | 4222 |
| Deadwood Torch | 4225 |
| Deadwood Vanity | 4188 |
| Deadwood Wardrobe | 4220 |
| Deep Conspiracy Board | 4428 |
| Deep Jaws | 4427 |
| Deep Rug | 4429 |
| Deep Sea Bed | 21352 |
| Deep Sea Clam Chair | 21346 |
| Deep Sea Door | 11835 |
| Deep Sea Nightstand | 21354 |
| Deep Sea Patio | 11836 |
| Deep Sea Roof | 11837 |
| Deep Sea Shell Bed | 4044 |
| Deep Sea Shell Chair | 4047 |
| Deep Sea Shell Couch | 4042 |
| Deep Sea Shell End Table | 4045 |
| Deep Sea Shell Lamp | 4048 |
| Deep Sea Shell Rug | 4043 |
| Deep Sea Shell Table | 4046 |
| Deep Sea Shell Wardrobe | 4148 |
| Deep Sea Table | 21355 |
| Deep Sea Walls | 11838 |
| Deep Sea Wardrobe | 21351 |
| Deep Sea Windows | 11839 |
| Deep Shark Plush | 4430 |
| Deeplight Lamp | 31101 |
| Deeps Treasure Map | 31103 |
| Delicate Hammer | 21225 |
| Delicious Bento Box | 21391 |
| Delicious Bread Display | 21219 |
| Deluxe Crown Jewels | 4401 |
| Deluxe Model Train Set | 14027 |
| Deluxe Nightstand | 4400 |
| Deluxe Tea Time | 4402 |
| Demolition Kit | 11120 |
| Demon Rising Painting | 4339 |
| Desert Royalty Bed | 4059 |
| Desert Royalty Chair | 4053 |
| Desert Royalty Couch | 4058 |
| Desert Royalty End Table | 4052 |
| Desert Royalty Lamp | 4054 |
| Desert Royalty Rug | 4056 |
| Desert Royalty Table | 4055 |
| Desert Royalty Wardrobe | 4057 |
| Designer Chess Board | 4470 |
| Designer Diary | 4469 |
| Designer Fabric | 4468 |
| Diamond Display | 21200 |
| Director Chair (Black) | 4176 |
| Director Chair (Blue) | 4175 |
| Director Chair (Green) | 4177 |
| Director Chair (Purple) | 4179 |
| Director Chair (Red) | 4174 |
| Director Chair (White) | 4178 |
| Director Chair (Yellow) | 4180 |
| Dog Biscuit Rug | 21382 |
| Donovan Plushie | 21529 |
| Donovan Town Flag | 21208 |
| Donovan's Bed | 21519 |
| Donovan's Broken Arcade Cabinet | 21520 |
| Donovan's Couch | 21526 |
| Donovan's End Table | 21521 |
| Donovan's Flaming Barrel | 21522 |
| Donovan's Junk Chair | 21527 |
| Donovan's Lockers | 21523 |
| Donovan's Rug | 21528 |
| Donovan's Table | 21524 |
| Donovan's TV | 21525 |
| Donut Plushie | 4337 |
| Dragon Claw Chair | 4025 |
| Dragon Claw Couch | 4023 |
| Dragon Claw Lamp | 4021 |
| Dragon Claw Table | 4024 |
| Dragon Claw Wardrobe | 4022 |
| Dried Herbs | 21203 |
| Dynus Bed | 4192 |
| Dynus Chair | 4193 |
| Dynus Couch | 4191 |
| Dynus End Table | 4196 |
| Dynus Lamp | 4197 |
| Dynus Rug | 4195 |
| Dynus Table | 4194 |
| Dynus Wall Jersey | 4103 |
| Dynus Wardrobe | 4198 |
| Eastern Door | 11715 |
| Eastern Patio | 11716 |
| Eastern Roof | 11717 |
| Eastern Walls | 11718 |
| Eastern Windows | 11719 |
| Edgy Coat Rack | 4102 |
| Elegant Bass | 21204 |
| Elegant Emerald Bed | 21431 |
| Elegant Emerald Chair | 21432 |
| Elegant Emerald Couch | 21438 |
| Elegant Emerald Cushion | 21433 |
| Elegant Emerald End Table | 21434 |
| Elegant Emerald Glowing Plant | 21441 |
| Elegant Emerald Lamp | 21437 |
| Elegant Emerald Leaf Rug | 21440 |
| Elegant Emerald Table | 21439 |
| Elegant Emerald Torch | 21436 |
| Elegant Emerald Vase | 21435 |
| Elios Bed | 4140 |
| Elios Chair | 4142 |
| Elios Couch | 4141 |
| Elios End Table | 4144 |
| Elios Lamp | 4147 |
| Elios Rug | 4146 |
| Elios Table | 4143 |
| Elios Wall Jersey | 4020 |
| Elios Wardrobe | 4145 |
| Elven Barn Permit | 11116 |
| Elven Barn Tier 2 Upgrade | 10063 |
| Elven Barn Tier 3 Upgrade | 10064 |
| Elven Coat Rack | 3814 |
| Elven Lore Tapestry | 21237 |
| Elven Wood Chair | 3996 |
| Elven Wood End Table | 3998 |
| Elven Wood Sign | 3994 |
| Elven Wood Table | 3995 |
| Elven Wood Torch | 3997 |
| Elven Wood Vanity | 3988 |
| Elven Wood Wardrobe | 3999 |
| Elvenwood Chest | 3790 |
| Elyssia Plushie | 14088 |
| Elyssia's Bed | 14097 |
| Elyssia's Bookshelf | 14089 |
| Elyssia's Chair | 14095 |
| Elyssia's Couch | 14091 |
| Elyssia's Desk | 14092 |
| Elyssia's End Table | 14093 |
| Elyssia's Lamp | 14087 |
| Elyssia's Rug | 14096 |
| Elyssia's Table | 14094 |
| Elyssia's Wardrobe | 14090 |
| Ember Chair | 21447 |
| Ember Couch | 21443 |
| Ember Rug | 21766 |
| Empty Pet Dish | 21378 |
| Enchanted Bench | 4418 |
| Enchanted Drawing | 4420 |
| Enchanted Mana Purifier | 4419 |
| Enchanted Pinwheel | 21233 |
| End Table of Luxury | 4490 |
| Entertainment Bar | 21240 |
| Even Window Trio | 4094 |
| Explorer Snaccoon Plush | 3774 |
| Extravagant Bamboo Wardrobe | 21401 |
| Fairy Painting | 4251 |
| Fall Bed | 4074 |
| Fall Chair | 4079 |
| Fall Couch | 4078 |
| Fall Door | 11850 |
| Fall End Table | 4081 |
| Fall Floral End Table | 4082 |
| Fall Flower Centerpiece | 4076 |
| Fall Forest Painting | 4302 |
| Fall Lamp | 4077 |
| Fall Leaf Window | 4299 |
| Fall Leaves Rug | 4550 |
| Fall Patio | 11851 |
| Fall Roof | 11852 |
| Fall Rug | 4075 |
| Fall Walls | 11853 |
| Fall Wardrobe | 4080 |
| Fall Windows | 11854 |
| Fancy Blue Dining Chair | 50004 |
| Fancy Tis the Season Wooden Table | 21338 |
| Fanned Fern of Luxury | 4492 |
| Farmer Snaccoon Plush | 3775 |
| Fed Snaccoon Plushie | 4399 |
| Festive Tree Painting | 4331 |
| Fire Lamp | 21455 |
| Fire Mage Couch | 4436 |
| Fire Mage Owl Statue | 4435 |
| Fire Mage Rug | 4437 |
| Flaming Book of Spells | 21220 |
| Flamingo Pool Float | 4557 |
| Flashlight Lamp | 21325 |
| Flower Field Painting | 4259 |
| Flower Power Rug | 4605 |
| Fluffy Bathroom Rug | 21465 |
| Flying Reindeer Decoration | 21344 |
| Folded Umbrella | 4551 |
| Foosball Table | 31201 |
| Forgotten Bouquet of Hyacinth | 14009 |
| Forgotten Bouquet of Orchids | 14008 |
| Forgotten Bouquet of Peonies | 14011 |
| Forgotten Bouquet of Roses | 14010 |
| Forgotten Bouquet of Tulips | 14006 |
| Formal Froggie Plushie | 14033 |
| Frozen Lamp Post | 4012 |
| Full Fall End Table | 4083 |
| Full Pet Dish | 21379 |
| Furnace (Old) | 9351 |
| Garden Festival Arm Chair | 4240 |
| Garden Festival Bed | 4234 |
| Garden Festival Couch | 4235 |
| Garden Festival Flower Display | 4239 |
| Garden Festival Flower Patch | 4396 |
| Garden Festival Lamp | 4238 |
| Garden Festival Rug | 4241 |
| Garden Festival Snaccoon | 4245 |
| Garden Festival Window | 4248 |
| Garden Party Chair | 14081 |
| Garden Party Lantern | 14085 |
| Garden Party Picnic | 14082 |
| Garden Party Potted Tree | 14083 |
| Garden Party String Light | 14084 |
| Garden Party Sweet Fern | 14086 |
| Gearwork Glamour Bed | 14076 |
| Gearwork Glamour Clock | 14080 |
| Gearwork Glamour Couch | 14075 |
| Gearwork Glamour Desk | 14073 |
| Gearwork Glamour Extraordinary Invention | 14079 |
| Gearwork Glamour Lamp | 14074 |
| Gearwork Glamour Rug | 14078 |
| Gearwork Glamour Stool | 14072 |
| Gearwork Glamour Table | 14071 |
| Gearwork Glamour Wardrobe | 14077 |
| Geode Muncher | 9358 |
| Ghost Bed | 4172 |
| Ghost Couch | 4173 |
| Ghost End Table | 4154 |
| Ghost Lamp | 4152 |
| Ghost Rug | 4151 |
| Ghost Snaccoon Plush | 3780 |
| Ghost Stool | 4153 |
| Ghost Table | 4150 |
| Ghost Wardrobe | 4149 |
| Giant Polar Bear Plushie | 4318 |
| Giant Tis the Season Snowglobe | 21337 |
| Gilded Celestial Rug | 21358 |

</details>

<details>
<summary>Gilded Celestial Table – Mitzy Doll (300 items)</summary>

| Item name | ID |
| --- | ---: |
| Gilded Celestial Table | 21364 |
| Gilded Moon Globe | 21357 |
| Gilded Rectangle Window | 14057 |
| Gilded Round Window | 14059 |
| Gilded Tall Lamp | 4629 |
| Gilded Woven Window | 4026 |
| Gingerbread Door | 11165 |
| Gingerbread Patio | 11166 |
| Gingerbread Roof | 11167 |
| Gingerbread Walls | 11168 |
| Gingerbread Windows | 11169 |
| Glass Lotus Lamp | 4040 |
| Glowing Flower Lights | 21211 |
| Golden Harp | 21205 |
| Golden Hutch | 4634 |
| Golden Vanity | 4633 |
| Gothic Chaise Couch | 50014 |
| Gothic Couch | 50013 |
| Gothic Fridge | 4625 |
| Gothic Hutch | 50015 |
| Grape Harvest Painting | 4305 |
| Great Army Guard Banner | 21228 |
| Great City Door | 14060 |
| Great City Patio | 14061 |
| Great City Roof | 14062 |
| Great City Walls | 14063 |
| Great City Windows | 14064 |
| Great Mage Fox Plushie | 14032 |
| Green Apple Window | 3963 |
| Green Display Katana | 21396 |
| Green Drawn Curtain Window | 3959 |
| Green Floral Bed | 4573 |
| Green Gummy Bear Plushie | 4335 |
| Green Lava Lamp | 31229 |
| Green Plank Door | 11170 |
| Green Plank Patio | 11171 |
| Green Plank Roof | 11172 |
| Green Plank Walls | 11173 |
| Green Plank Windows | 11174 |
| Green Polka Dot Door | 11790 |
| Green Polka Dot Patio | 11791 |
| Green Polka Dot Roof | 11792 |
| Green Polka Dot Walls | 11793 |
| Green Polka Dot Windows | 11794 |
| Green Runner Tea Table | 21388 |
| Green Striped Door | 11740 |
| Green Striped Patio | 11741 |
| Green Striped Roof | 11742 |
| Green Striped Walls | 11743 |
| Green Striped Windows | 11744 |
| Green Tea Chair | 21409 |
| Green Tea Floor Cushion | 21421 |
| Green Toy Dinosaur | 4208 |
| Green Wrought Iron Chair | 4589 |
| Greenhouse Door | 11175 |
| Greenhouse Patio | 11176 |
| Greenhouse Roof | 11177 |
| Greenhouse Walls | 11178 |
| Greenhouse Windows | 11179 |
| Griffon Plushie | 14034 |
| Hand Carved Squirrel Statue | 21234 |
| Hand Stitched Soccer Ball | 14026 |
| Hanging Shortsword | 21229 |
| Heart Web Rug | 4353 |
| Hidden Dragon Painting | 4250 |
| Hidden Pearl Clam | 21347 |
| Historic Artifact Necklace | 2325 |
| Historic Elven Totem | 2323 |
| Historic Scrolls | 2324 |
| Hollow Lily Bloom | 14002 |
| Honeycomb Door | 11146 |
| Honeycomb Patio | 11145 |
| Honeycomb Roof | 11148 |
| Honeycomb Walls | 11149 |
| Honeycomb Window | 3961 |
| Honeycomb Windows | 11147 |
| Honorific Katana | 21230 |
| Hot Barbeque Grill | 4580 |
| House (Old) | 10100 |
| House Customization Kit | 11121 |
| Hungry Snaccoon Plushie | 4398 |
| Ice Cream Gnome | 4389 |
| Ice Door | 11180 |
| Ice Patio | 11181 |
| Ice Roof | 11182 |
| Ice Walls | 11183 |
| Ice Windows | 11184 |
| Indiglow Lamp | 3991 |
| Inflatable Bed | 4577 |
| Inflatable Pool | 4565 |
| Iris' Bed | 21539 |
| Iris' Bench | 21537 |
| Iris' Chair | 21531 |
| Iris' Dresser | 21534 |
| Iris' Lamp | 21533 |
| Iris' Painting | 21532 |
| Iris' Plushie | 21530 |
| Iris' Rug | 21536 |
| Iris' Table | 21538 |
| Iris' Topiary | 21535 |
| Iris' Wardrobe | 21540 |
| Jack in the Box | 14031 |
| Jacob Ladder Lamp | 4236 |
| Jellyfish Lamp | 21348 |
| Jolly Painting | 4329 |
| Jumbo Frog Plushie | 4246 |
| Jumbo Shark Plushie | 4271 |
| Jumbo Sleepy Snaccoon Plushie | 4365 |
| Jumbo Snaccoon Teddy Bear | 4366 |
| Jun Plushie | 21551 |
| Jun's Bed | 21550 |
| Jun's Chest | 21547 |
| Jun's Couch | 21544 |
| Jun's End Table | 21549 |
| Jun's Lamp | 21548 |
| Jun's Model Boat | 21543 |
| Jun's Rocking Chair | 21541 |
| Jun's Rug | 21542 |
| Jun's Table | 21545 |
| Jun's Wardrobe | 21546 |
| Just Right Bed | 4574 |
| Kai Plushie | 21561 |
| Kai's Bed | 21556 |
| Kai's Broom | 21559 |
| Kai's Chair | 21560 |
| Kai's End Table | 21558 |
| Kai's Mapping Table | 21555 |
| Kai's Rug | 21553 |
| Kai's Storage Boxes | 21554 |
| Kai's Torch | 21557 |
| Kai's Wardrobe | 21552 |
| Karish Plushie | 21572 |
| Karish's Aquarium | 21565 |
| Karish's Bed | 21562 |
| Karish's Chair | 21566 |
| Karish's Couch | 21564 |
| Karish's End Table | 21569 |
| Karish's Fishbowl | 21563 |
| Karish's Lamp | 21567 |
| Karish's Porthole Rug | 21571 |
| Karish's Wall Lamp | 21568 |
| Karish's Writing Desk | 21570 |
| Kids Workbench | 14018 |
| Kingdom of Qh'aab Bed | 4578 |
| Kingdom of Qh'aab Lamp | 4631 |
| Kitty Plushie | 21587 |
| Kitty's Banquet Table | 21577 |
| Kitty's Bed | 21581 |
| Kitty's Birthday Dress | 21216 |
| Kitty's Cat Head Rug | 21586 |
| Kitty's Chair | 21575 |
| Kitty's Comfy Chair | 21574 |
| Kitty's End Table | 21582 |
| Kitty's Lamp | 21583 |
| Kitty's Napping Chair | 21578 |
| Kitty's Napping Couch | 21579 |
| Kitty's Paw Print Rug | 21585 |
| Kitty's Pet Bed | 21576 |
| Kitty's Table | 21584 |
| Kitty's Vanity | 21580 |
| Kitty's Wardrobe | 21573 |
| Koi Pond Rug | 21402 |
| Lacquered Wood Bed | 21408 |
| Ladybug Painting | 4253 |
| Large Brinestone Deeps Chest | 4568 |
| Large Cute Chest | 4570 |
| Large Dragon Chest | 4566 |
| Large Leopard Gecko Plushie | 4032 |
| Large Moon Globe | 21356 |
| Large Nel'Vari Chest | 4569 |
| Large Panda Plushie | 3946 |
| Large Thin Winter Window | 4320 |
| Large Tiki Mask Totem | 4036 |
| Large Withergate Chest | 4567 |
| Large Wooden Chest | 3789 |
| Large Wooden Winter Window | 4323 |
| Lavender Field Window | 3952 |
| Liam Plushie | 21602 |
| Liam's Apron | 21601 |
| Liam's Bed | 21595 |
| Liam's Blue Stool | 21597 |
| Liam's Chair | 21588 |
| Liam's Couch | 21592 |
| Liam's End Table | 21594 |
| Liam's Family Toy Chest | 21590 |
| Liam's Fern | 21598 |
| Liam's Lamp | 21599 |
| Liam's Poster | 21600 |
| Liam's Purple Stool | 21596 |
| Liam's Rug | 21593 |
| Liam's Table | 21589 |
| Liam's Wardrobe | 21591 |
| Lightning Lamp | 3992 |
| Linen Cabinet | 21466 |
| Log Cabin Door | 11730 |
| Log Cabin Patio | 11731 |
| Log Cabin Roof | 11732 |
| Log Cabin Walls | 11733 |
| Log Cabin Windows | 11734 |
| Long Steel Window | 4138 |
| Lucia Plushie | 21613 |
| Lucia's Banquet Table | 21607 |
| Lucia's Bed | 21612 |
| Lucia's Bookcase | 21603 |
| Lucia's Chair | 21606 |
| Lucia's Couch | 21611 |
| Lucia's End Table | 21609 |
| Lucia's Firefly Bottle | 21610 |
| Lucia's Grandfather Clock | 21605 |
| Lucia's Rug | 21604 |
| Lucia's Vase | 21608 |
| Lucius' Bed | 21614 |
| Lucius' Bonsai | 21623 |
| Lucius' Chair | 21615 |
| Lucius' Couch | 21619 |
| Lucius' End Table | 21618 |
| Lucius' Incense Fountain | 21622 |
| Lucius' Lamp | 21617 |
| Lucius' Plushie | 21624 |
| Lucius' Rug | 21616 |
| Lucius' Table | 21620 |
| Lucius' Wardrobe | 21621 |
| Luminesent Pumpkin | 21210 |
| Lumpy Sandcastle | 4553 |
| Lynn Anvil | 9357 |
| Lynn Plushie | 21635 |
| Lynn's Bed | 21625 |
| Lynn's Bookshelf | 21630 |
| Lynn's Candlestick | 21628 |
| Lynn's Chair | 21633 |
| Lynn's Chest | 21629 |
| Lynn's Couch | 21634 |
| Lynn's Decorative Shield | 21627 |
| Lynn's Home Town Banner | 21632 |
| Lynn's Rug | 21626 |
| Lynn's Table | 21631 |
| Mage District Bed | 14052 |
| Mage District Chair | 14046 |
| Mage District Couch | 14045 |
| Mage District End Table | 14047 |
| Mage District Lamp | 14044 |
| Mage District Potion Set | 14049 |
| Mage District Rug | 14051 |
| Mage District Table | 14048 |
| Mage District Throne | 14050 |
| Mage District Wall Shelf | 14053 |
| Magenta Chaise Couch | 50001 |
| Magic Globe | 31106 |
| Magmastone Bed | 21442 |
| Magmastone Couch | 21444 |
| Magmastone End Table | 21451 |
| Magmastone Table | 21450 |
| Magmastone Wardrobe | 21453 |
| Magnifying Glass Collection | 31105 |
| Mailbox Demolition Kit | 11122 |
| Mailbox Lamp | 21381 |
| Mana Bloom Vase | 14013 |
| Mana Tome Forageable | 16404 |
| Marble Chessboard | 31206 |
| Medical Chair | 4467 |
| Medical Degree | 4465 |
| Medical Figure | 4466 |
| Medical Grade Microscope | 21239 |
| Medium Thin Winter Window | 4321 |
| Medium Wooden Winter Window | 4324 |
| Melting Ice Pop Fridge | 4624 |
| Microfiber Towel | 21463 |
| Microphone | 4224 |
| Miner Snaccoon Plush | 3778 |
| Mini Blue Polka Dot Door | 11810 |
| Mini Blue Polka Dot Patio | 11811 |
| Mini Blue Polka Dot Roof | 11812 |
| Mini Blue Polka Dot Walls | 11813 |
| Mini Blue Polka Dot Windows | 11814 |
| Mini Duke Statue | 21201 |
| Mini Green Polka Dot Door | 11815 |
| Mini Green Polka Dot Patio | 11816 |
| Mini Green Polka Dot Roof | 11817 |
| Mini Green Polka Dot Walls | 11818 |
| Mini Green Polka Dot Windows | 11819 |
| Mini Lattice Planter | 14012 |
| Mini Moon Chair | 4617 |
| Mini Purple Polka Dot Door | 11820 |
| Mini Purple Polka Dot Patio | 11821 |
| Mini Purple Polka Dot Roof | 11822 |
| Mini Purple Polka Dot Walls | 11823 |
| Mini Purple Polka Dot Windows | 11824 |
| Mini Red Polka Dot Door | 11825 |
| Mini Red Polka Dot Patio | 11826 |
| Mini Red Polka Dot Roof | 11827 |
| Mini Red Polka Dot Walls | 11828 |
| Mini Red Polka Dot Windows | 11829 |
| Mini Tea Yellow Floor Cushion | 21422 |
| Mini Yellow Polka Dot Door | 11830 |
| Mini Yellow Polka Dot Patio | 11831 |
| Mini Yellow Polka Dot Roof | 11832 |
| Mini Yellow Polka Dot Walls | 11833 |
| Mini Yellow Polka Dot Windows | 11834 |
| Mirror Pool Rug | 4606 |
| Mitzy Doll | 14023 |

</details>

<details>
<summary>Miyeon Plushie – Red Striped Walls (300 items)</summary>

| Item name | ID |
| --- | ---: |
| Miyeon Plushie | 21647 |
| Miyeon's Bed | 21644 |
| Miyeon's Bookshelf | 21636 |
| Miyeon's Chair | 21641 |
| Miyeon's Couch | 21646 |
| Miyeon's Dresser | 21638 |
| Miyeon's End Table | 21639 |
| Miyeon's Floral Arrangement | 21643 |
| Miyeon's Kotatsu | 21645 |
| Miyeon's Lamp | 21637 |
| Miyeon's Rug | 21640 |
| Miyeon's Turtle Plushie | 21642 |
| Model Train Set | 21224 |
| Mona-Vara | 31107 |
| Money Bag Forageable | 16401 |
| Monster Mouth Chair | 50007 |
| Monster Mouth Couch | 50009 |
| Monster Mouth Door | 11185 |
| Monster Mouth Patio | 11186 |
| Monster Mouth Roof | 11187 |
| Monster Mouth Table | 50008 |
| Monster Mouth Walls | 11188 |
| Monster Mouth Wardrobe | 50010 |
| Monster Mouth Windows | 11189 |
| Monster Moutn Window | 4132 |
| Monster Pool Table | 4186 |
| Monster Under the Rug | 4604 |
| Moon and Stars Bed | 4620 |
| Moon and Stars Couch | 4616 |
| Moon Elf Rug | 4609 |
| Moon Risen Portrait | 4438 |
| Moon Risen Potted Plant | 4440 |
| Moon Risen Wall Art | 4439 |
| Moon Window | 3957 |
| Moontouched Fountain | 21222 |
| Moontouched Mirror | 21223 |
| Mushroom Festival Bed | 4293 |
| Mushroom Festival Candle Table | 4292 |
| Mushroom Festival Couch | 4287 |
| Mushroom Festival Dining Table | 4289 |
| Mushroom Festival Harvest Rug | 4294 |
| Mushroom Festival Lamp | 4286 |
| Mushroom Festival Leaf Rug | 4291 |
| Mushroom Festival Maple Leaf Rug | 4290 |
| Mushroom Festival Plushie | 4394 |
| Mushroom Festival Rocking Chair | 4288 |
| Mushroom Festival Snaccoon Plushie | 4297 |
| Mushroom Festival Tea Set | 4395 |
| Mushroom Lamp | 3989 |
| Mushroom Window | 4298 |
| Myths and Muses Bed | 4497 |
| Myths and Muses Candelabra | 13010 |
| Myths and Muses Chair | 13011 |
| Myths and Muses Chaise | 13012 |
| Myths and Muses End Table | 4498 |
| Myths and Muses Painting | 4500 |
| Myths and Muses Rug | 4495 |
| Myths and Muses Statue | 13009 |
| Myths and Muses Table | 4499 |
| Myths and Muses Vase | 13008 |
| Myths and Muses Wardrobe | 4496 |
| Nathaniel Plushie | 21658 |
| Nathaniel's Bed | 21656 |
| Nathaniel's Chair | 21657 |
| Nathaniel's Chest | 21648 |
| Nathaniel's Couch | 21652 |
| Nathaniel's Desk | 21653 |
| Nathaniel's End Table | 21651 |
| Nathaniel's Lantern | 21649 |
| Nathaniel's Rug | 21650 |
| Nathaniel's Wall Lantern | 21654 |
| Nathaniel's Wardrobe | 21655 |
| Nature Chair | 21235 |
| Nature Door | 11190 |
| Nature Patio | 11191 |
| Nature Roof | 11192 |
| Nature Sign Post | 3990 |
| Nature Walls | 11193 |
| Nature Windows | 11194 |
| Nel'Vari Bookshelf | 4601 |
| Nel'Vari Snaccoon Plush | 3773 |
| Nel'Varian Translation Texts | 21236 |
| Neon Door | 11725 |
| Neon Patio | 11726 |
| Neon Roof | 11727 |
| Neon Sign | 21241 |
| Neon Walls | 11728 |
| Neon Window | 4137 |
| Neon Windows | 11729 |
| New Lovers Lantern | 21418 |
| New Tatami Mat Rug | 21404 |
| Nice Double Bed | 9001 |
| Nice Sofa | 9101 |
| Nice Wooden Lamp | 9400 |
| Nice Wooden Night Stand | 9306 |
| Nightclub Bed | 4164 |
| Nightclub Curved Couch | 4165 |
| Nightclub Curved Counter | 4170 |
| Nightclub End Table | 4167 |
| Nightclub Lamp | 4169 |
| Nightclub Stool | 4168 |
| Nightclub Wardrobe | 4166 |
| Nightmares Bed | 4572 |
| Nivara Bed | 3972 |
| Nivara Chair | 3979 |
| Nivara Couch | 3973 |
| Nivara End Table | 3975 |
| Nivara Lamp | 3977 |
| Nivara Rug | 3978 |
| Nivara Table | 3974 |
| Nivara Wall Jersey | 3811 |
| Nivara Wardrobe | 3976 |
| Nostalgic Couch | 4597 |
| Nutty Banner | 4458 |
| Nutty Basket | 4457 |
| Nutty Frog Display | 4459 |
| Office Chair | 4591 |
| Old Argyle Rug | 3807 |
| Old Stone Door | 11195 |
| Old Stone Patio | 11196 |
| Old Stone Roof | 11197 |
| Old Stone Walls | 11198 |
| Old Stone Windows | 11199 |
| Old Sun Haven Painting | 4255 |
| Olive Tall Lamp | 3808 |
| Once Upon a Time Bed | 13000 |
| Once Upon a Time Couch | 13005 |
| Once Upon a Time Dark Couch | 13002 |
| Once Upon a Time Dark Wardrobe | 13004 |
| Once Upon a Time Ever Rose | 13003 |
| Once Upon a Time Rug | 13006 |
| Once Upon a Time Wardrobe | 13001 |
| Oozing Creepy Window | 4133 |
| Open Beach Cooler | 4552 |
| Orange Flower Couch | 4595 |
| Orange Lava Lamp | 31232 |
| Orange Tiled Door | 11400 |
| Orange Tiled Patio | 11401 |
| Orange Tiled Roof | 11402 |
| Orange Tiled Walls | 11403 |
| Orange Tiled Windows | 11404 |
| Organized Study Desk | 21394 |
| Ornate Black Tea Pot | 21428 |
| Ornate Square Window | 3955 |
| Overcast Lamp | 4613 |
| Overgrown Arched Window | 3950 |
| Overgrown Bookshelf | 4598 |
| Overgrown Square Window | 3951 |
| Paddleball Rug | 21324 |
| Pajama Snaccoon Plush | 3783 |
| Panda Bed | 3815 |
| Panda Couch | 3947 |
| Panda End Table | 3818 |
| Panda Lamp | 3819 |
| Panda Rug | 3816 |
| Panda Table | 3945 |
| Panda Wardrobe | 3817 |
| Paper Lantern End Table | 21400 |
| Patched Pumpkin Plushie | 4295 |
| Personal Med Kit | 21238 |
| Pet Bed | 21375 |
| Pet Chair | 21376 |
| Pet Couch | 21385 |
| Pet Egg | 31234 |
| Pet End Table | 21377 |
| Pet Festival Armchair | 4263 |
| Pet Festival Bed | 4260 |
| Pet Festival Chair | 4262 |
| Pet Festival Couch | 4261 |
| Pet Festival Rug | 4264 |
| Pet Festival Snaccoon Plushie | 4270 |
| Pet Table | 21386 |
| Pet Wardrobe | 21387 |
| Phoenix Lamp | 21751 |
| Phoenixmancer Bed | 21747 |
| Phoenixmancer Chair | 21746 |
| Phoenixmancer Couch | 21750 |
| Phoenixmancer Lamp | 21749 |
| Phoenixmancer Rug | 21753 |
| Phoenixmancer Stained Glass Chest | 21748 |
| Phoenixmancer Table | 21745 |
| Phoenixmancer Wardrobe | 21752 |
| Pilot Targeting Window | 4135 |
| Pinata (Blue) | 50478 |
| Pinata (Carrot) | 50477 |
| Pinata (Orange) | 50475 |
| Pinata (Striped) | 50474 |
| Pinata (Teal) | 50473 |
| Pinata (Watermelon) | 50476 |
| Pinball Table | 31202 |
| Pink Bucket of Sand | 4558 |
| Pink Daisy Lamp | 4237 |
| Pink Gummy Bear Plushie | 4336 |
| Pink Hearts Rug | 4611 |
| Pink Snow Globe Lamp | 21478 |
| Pink Snow Yeti Bean Bag Chair | 21475 |
| Pink Snow Yeti Chair | 21473 |
| Pink Snow Yeti Couch | 21476 |
| Pink Snow Yeti Lamp | 21474 |
| Pink Snow Yeti Lounge Chair | 21480 |
| Pink Tea Floor Cushion | 21420 |
| Pink Yeti Snow Globe | 21477 |
| Pirate Life Anchor Rug | 4159 |
| Pirate Life Bed | 4155 |
| Pirate Life Chair | 4157 |
| Pirate Life Chest | 4163 |
| Pirate Life Couch | 4156 |
| Pirate Life Flag Rug | 4160 |
| Pirate Life Lamp | 4161 |
| Pirate Life Table | 4162 |
| Pirate Life Wardrobe | 4158 |
| Pirated Candelabra | 4471 |
| Pirated Jellyfish Lamp | 4472 |
| Pirated Thick Coral Display | 4473 |
| Plastic Tea Set | 14029 |
| Poinsettia Painting | 4326 |
| Polished Bathroom Mirror | 21458 |
| Poolside Table | 4034 |
| Pop Sensation Acoustic Foam | 21290 |
| Pop Sensation Basic Speaker | 21295 |
| Pop Sensation Bed | 21287 |
| Pop Sensation Cast Chair | 21293 |
| Pop Sensation Costume Cart | 21291 |
| Pop Sensation Dressing Room Table | 21302 |
| Pop Sensation Keyboard | 21298 |
| Pop Sensation L Couch | 21289 |
| Pop Sensation Large Speaker | 21296 |
| Pop Sensation Microphone | 21299 |
| Pop Sensation Neon Lights | 21301 |
| Pop Sensation Rug | 21297 |
| Pop Sensation Small Speaker | 21294 |
| Pop Sensation Stage Light | 21300 |
| Pop Sensation Star Chair | 21292 |
| Pop Sensation Table | 21288 |
| Pot of Chrysanthemums | 14000 |
| Powerful Coat Rack | 4448 |
| Powerful Shield Rug | 4450 |
| Powerful Sun Display | 4449 |
| Princely Chair | 4412 |
| Princely Fireplace | 4413 |
| Princely Portrait | 4414 |
| Princely Sword | 4464 |
| Pumpkin Couch | 50018 |
| Pumpkin Forest Painting | 4343 |
| Pumpkin Lamp | 50017 |
| Pumpkin Painting | 4301 |
| Pumpkin Pie Painting | 4303 |
| Pumpkin Table | 50020 |
| Pumpkin Wardrobe | 50021 |
| Puppy Rug | 4387 |
| Purple Lava Lamp | 31233 |
| Purple Polka Dot Door | 11795 |
| Purple Polka Dot Patio | 11796 |
| Purple Polka Dot Roof | 11797 |
| Purple Polka Dot Walls | 11798 |
| Purple Polka Dot Windows | 11799 |
| Purple Round Symbol Window | 3953 |
| Purple Ruffled Door | 11405 |
| Purple Ruffled Patio | 11406 |
| Purple Ruffled Roof | 11407 |
| Purple Ruffled Walls | 11408 |
| Purple Ruffled Windows | 11409 |
| Purple Striped Door | 11745 |
| Purple Striped Patio | 11746 |
| Purple Striped Roof | 11747 |
| Purple Striped Walls | 11748 |
| Purple Striped Windows | 11749 |
| Purple Stump | 50026 |
| Purple Wooden Chair | 50025 |
| Purple Wooden Square Desk | 50024 |
| Puzzle Piece Rug | 21322 |
| Radiant Royalty Bed | 13027 |
| Radiant Royalty Chair | 13032 |
| Radiant Royalty End Table | 13030 |
| Radiant Royalty Rug | 13031 |
| Radiant Royalty Window | 13026 |
| Radiant Stained Glass End Table | 13033 |
| Rainbow Beach Ball | 4014 |
| Rainbow Bookshelf | 4602 |
| Red Butterfly Couch | 50000 |
| Red Door | 11141 |
| Red Lava Lamp | 31231 |
| Red Patio | 11140 |
| Red Polka Dot Door | 11800 |
| Red Polka Dot Patio | 11801 |
| Red Polka Dot Roof | 11802 |
| Red Polka Dot Walls | 11803 |
| Red Polka Dot Windows | 11804 |
| Red Prism Door | 11410 |
| Red Prism Patio | 11411 |
| Red Prism Roof | 11412 |
| Red Prism Walls | 11413 |
| Red Prism Windows | 11414 |
| Red Rider Wagon | 14025 |
| Red Roof | 11143 |
| Red Round Ornate Window | 3948 |
| Red Striped Door | 11750 |
| Red Striped Patio | 11751 |
| Red Striped Roof | 11752 |
| Red Striped Walls | 11753 |

</details>

<details>
<summary>Red Striped Windows – Teal Inflatable Chair (300 items)</summary>

| Item name | ID |
| --- | ---: |
| Red Striped Windows | 11754 |
| Red Tea Chair | 21410 |
| Red Toy Dinosaur | 4206 |
| Red Walls | 11144 |
| Red Windows | 11142 |
| Refreshing Summer Fruit Display | 4265 |
| Refreshing Summer Juice Stand | 4267 |
| Refreshing Summer Watermelon Display | 4266 |
| Reindeer Decoration | 21345 |
| Renaissance Snaccoon Painting | 4369 |
| Retro Rainbow Rug | 4608 |
| Retro Synth Rug | 4607 |
| Rickity Door | 11415 |
| Rickity Patio | 11416 |
| Rickity Roof | 11417 |
| Rickity Walls | 11418 |
| Rickity Windows | 11419 |
| Robo-Hero Action Figure | 14024 |
| Robotic Door | 11420 |
| Robotic Patio | 11421 |
| Robotic Roof | 11422 |
| Robotic Walls | 11423 |
| Robotic Windows | 11424 |
| Rock 'n' Roll Amp | 21261 |
| Rock 'n' Roll Bed | 21267 |
| Rock 'n' Roll Black Guitar | 21262 |
| Rock 'n' Roll Black Rug | 21270 |
| Rock 'n' Roll Couch | 21260 |
| Rock 'n' Roll End Table | 21269 |
| Rock 'n' Roll Gold Record Award | 21266 |
| Rock 'n' Roll Lamp | 21265 |
| Rock 'n' Roll Red Guitar | 21263 |
| Rock 'n' Roll Red Rug | 21271 |
| Rock 'n' Roll Table | 21268 |
| Rock 'n' Roll Wardrobe | 21264 |
| Rombopoly | 31205 |
| Rough Elven Wood Dresser | 3799 |
| Rough Elven Wood Low Chair | 3797 |
| Rough Elven Wood Shelf | 3800 |
| Rough Elven Wood Table | 3798 |
| Royal Snail Plushie | 3809 |
| Rug of Luxury | 4488 |
| Sakura Floral End Table | 21398 |
| Sakura Print Bed | 21407 |
| Sakura Screen Divider | 21405 |
| Sakura Tea Pot | 21426 |
| Salmon Curtain Window | 4029 |
| Sand Dollar Rug | 21350 |
| Sandy Anchor | 4424 |
| Sandy Fish Basket | 4425 |
| Sandy World Map | 4426 |
| Scarf Snaccoon Plush | 3785 |
| Sea of the Sewer Rug | 4354 |
| Seahorse Plushie | 4269 |
| Seasons Story Rug | 4268 |
| Sepia Globe Rug | 4612 |
| Shang Plushie | 21667 |
| Shang's Bed | 21661 |
| Shang's Chair | 21662 |
| Shang's Charting Table | 21666 |
| Shang's Couch | 21663 |
| Shang's Lamp | 21660 |
| Shang's Rug | 21665 |
| Shang's Tiger Painting | 21765 |
| Shang's Time Table | 21664 |
| Shang's Wardrobe | 21659 |
| Shelf | 10009 |
| Shell Painting | 4278 |
| Shiny Toilet Paper Holder | 21464 |
| Shrew in Shrubs Painting | 4254 |
| Sickle Branch Lamp | 4630 |
| Silent Night Painting | 4328 |
| Simple Arched Window | 4092 |
| Simple Black Tea Pot | 21427 |
| Simple Blue Door | 11760 |
| Simple Blue Patio | 11761 |
| Simple Blue Roof | 11762 |
| Simple Blue Walls | 11763 |
| Simple Blue Windows | 11764 |
| Simple Boat Painting | 4277 |
| Simple Brick Well | 4051 |
| Simple Chrysanthemum Pot | 14003 |
| Simple Circle Window | 4093 |
| Simple Green Door | 11765 |
| Simple Green Patio | 11766 |
| Simple Green Roof | 11767 |
| Simple Green Walls | 11768 |
| Simple Green Windows | 11769 |
| Simple Kotatsu | 21423 |
| Simple Long Window | 4096 |
| Simple Purple Door | 11770 |
| Simple Purple Patio | 11771 |
| Simple Purple Roof | 11772 |
| Simple Purple Walls | 11773 |
| Simple Purple Windows | 11774 |
| Simple Red Door | 11775 |
| Simple Red Patio | 11776 |
| Simple Red Roof | 11777 |
| Simple Red Walls | 11778 |
| Simple Red Windows | 11779 |
| Simple White Tea Pot | 21425 |
| Simple Yellow Door | 11780 |
| Simple Yellow Patio | 11781 |
| Simple Yellow Roof | 11782 |
| Simple Yellow Walls | 11783 |
| Simple Yellow Windows | 11784 |
| Skeedat | 31204 |
| Sleeping Snaccoon Painting | 4370 |
| Sleepy Moon Rug | 4614 |
| Sleepy Snaccoon Rug | 4376 |
| Slime Drop Door | 11425 |
| Slime Drop Patio | 11426 |
| Slime Drop Roof | 11427 |
| Slime Drop Walls | 11428 |
| Slime Drop Windows | 11429 |
| Slimey Door | 11430 |
| Slimey Patio | 11431 |
| Slimey Roof | 11432 |
| Slimey Walls | 11433 |
| Slimey Windows | 11434 |
| Small Daisy Flower Pot | 3795 |
| Small Green Shovel | 4554 |
| Small Mystic's Bookshelf | 50034 |
| Small Seaweed | 21353 |
| Small Soccer Ball | 4013 |
| Small Thin Winter Window | 4322 |
| Small Wooden Winter Window | 4325 |
| Smooth Wooden Chair | 3791 |
| Smooth Wooden Dresser | 3793 |
| Smooth Wooden Table | 3792 |
| Smooth Wooden Wall Shelf | 3794 |
| Smore Painting | 4300 |
| Snaccoon Festival Bed | 4378 |
| Snaccoon Festival Chair | 4380 |
| Snaccoon Festival Couch | 4379 |
| Snaccoon Festival Lamp | 4381 |
| Snaccoon Festival Rug | 4377 |
| Snaccoon Festival Wall Clock | 4382 |
| Snaccoon in a Meadow Painting | 4368 |
| Snaccoon of Love Painting | 4388 |
| Snaccoon Painting | 4367 |
| Snaccoon Paw Print Window | 4371 |
| Snaccoon Snack Time Window | 4372 |
| Snaccoon Squishy Plushie | 4363 |
| Snake Statue | 21215 |
| Snow Day Bed | 21326 |
| Snow Day Bookshelf | 21327 |
| Snow Day Chair | 21328 |
| Snow Day Couch | 21332 |
| Snow Day End Table | 21330 |
| Snow Day Lamp | 21329 |
| Snow Day Rug | 21331 |
| Snow Day Table | 21333 |
| Snow Festival Bed | 4311 |
| Snow Festival Couch | 4309 |
| Snow Festival Lamp | 4310 |
| Snow Festival Rug | 4313 |
| Snow Festival Table | 4312 |
| Snowflake Painting Trio | 4330 |
| Snowglobe Rug | 4314 |
| Snowman Fridge | 4622 |
| Snowman Plushie | 4319 |
| Snowy Observation Window | 4028 |
| Sock Kites | 3810 |
| Soggy Sandcastle | 21214 |
| Sound-o-tronic 800 | 31207 |
| Space Octopus Rug | 4610 |
| Space Window | 4136 |
| Spades Rug | 4355 |
| Spirit Orb | 21251 |
| Spirit Petal Bed | 21259 |
| Spirit Petal Chair | 21255 |
| Spirit Petal Couch | 21254 |
| Spirit Petal End Table | 21256 |
| Spirit Petal Lamp | 21252 |
| Spirit Petal Rug | 21258 |
| Spirit Petal Table | 21257 |
| Spirit Petal Wardrobe | 21253 |
| Spooky Bed | 21243 |
| Spooky Chair | 21246 |
| Spooky Couch | 21245 |
| Spooky End Table | 21247 |
| Spooky Pumpkin Cauldron | 21249 |
| Spooky Rug | 21242 |
| Spooky Stack of Pumpkins | 21250 |
| Spooky Table | 21248 |
| Spooky Wardrobe | 21244 |
| Sporty Award | 4113 |
| Sporty Bed | 4104 |
| Sporty Cat Scratcher | 4383 |
| Sporty Chair | 4112 |
| Sporty Couch | 4110 |
| Sporty End Table | 4107 |
| Sporty Lamp | 4111 |
| Sporty Rug | 4109 |
| Sporty Statuette Award | 4114 |
| Sporty Table | 4105 |
| Sporty Wardrobe | 4106 |
| Spotless Bubble Bath | 21457 |
| Spotless Shower | 21459 |
| Spotless Sink | 21456 |
| Spotless Toilet | 21461 |
| Spotless Toilet Brush | 21462 |
| Spotless Vanity | 21460 |
| Spring Bed | 4060 |
| Spring Bouquet End Table | 4063 |
| Spring Chair | 4064 |
| Spring Couch | 4062 |
| Spring Door | 11840 |
| Spring Lamp | 4065 |
| Spring Patio | 11841 |
| Spring Roof | 11842 |
| Spring Rug | 4061 |
| Spring Table | 4066 |
| Spring Walls | 11843 |
| Spring Windows | 11844 |
| Squat Triangle Window | 3956 |
| Stacked Storage Shelves | 21414 |
| Stained Emerald Rug | 3801 |
| Stained Glass Butterfly Window | 4249 |
| Stained Glass Window | 3949 |
| Star Window | 3958 |
| Starfish Painting | 4279 |
| Starfish Rug | 21349 |
| Starlight Bed | 21312 |
| Starlight Chair | 21303 |
| Starlight Couch | 21310 |
| Starlight End Table | 21308 |
| Starlight Lamp | 21309 |
| Starlight Nightlight | 21306 |
| Starlight Rug | 21304 |
| Starlight Storage Chest | 21305 |
| Starlight Table | 21307 |
| Starlight Wardrobe | 21311 |
| Steampunk Bed | 14043 |
| Steampunk Chair | 14038 |
| Steampunk Clock Rug | 14042 |
| Steampunk Couch | 14037 |
| Steampunk End Table | 14039 |
| Steampunk Gear Rug | 14041 |
| Steampunk Lamp | 14036 |
| Steampunk Table | 14040 |
| Steel Door | 11470 |
| Steel Patio | 11471 |
| Steel Roof | 11472 |
| Steel Walls | 11473 |
| Steel Windows | 11474 |
| Stone Age Couch | 4594 |
| Stone Brick Door | 11435 |
| Stone Brick Patio | 11436 |
| Stone Brick Roof | 11437 |
| Stone Brick Walls | 11438 |
| Stone Brick Windows | 11439 |
| Stone Carved Bed (Blue) | 4588 |
| Stone Carved Bed (Purple) | 4586 |
| Stone Carved Bed (Teal) | 4587 |
| Stone Door | 11440 |
| Stone Garden Lamp | 4628 |
| Stone Patio | 11441 |
| Stone Roof | 11442 |
| Stone Walls | 11443 |
| Stone Windows | 11444 |
| Stormelon Lamp | 3993 |
| Straw Door | 11445 |
| Straw Patio | 11446 |
| Straw Roof | 11447 |
| Straw Walls | 11448 |
| Straw Windows | 11449 |
| Striped Lounge Chair | 4582 |
| Striped Pool Float | 4559 |
| Striped Umbrella | 4583 |
| Stucco Door | 11495 |
| Stucco Patio | 11496 |
| Stucco Roof | 11497 |
| Stucco Walls | 11498 |
| Stucco Windows | 11499 |
| Summer Bed | 4067 |
| Summer Cactus End Table | 4071 |
| Summer Chair | 4072 |
| Summer Couch | 4069 |
| Summer Door | 11845 |
| Summer Dragon Painting | 4274 |
| Summer Gnome | 4390 |
| Summer Lamp | 4070 |
| Summer Ocean Painting | 4276 |
| Summer Patio | 11846 |
| Summer Roof | 11847 |
| Summer Rug | 4068 |
| Summer Sun Shaped Window | 4273 |
| Summer Table | 4073 |
| Summer Walls | 11848 |
| Summer Windows | 11849 |
| Sun and Moon Plushie | 4100 |
| Sunflower Field Painting | 4275 |
| Surfing Gnome | 4391 |
| Sweet Dreams Pet House | 4385 |
| Sweetest Dreams Bed | 4584 |
| Table of Luxury | 4489 |
| Tall Candlestick Lamp | 4632 |
| Teal Inflatable Chair | 4592 |

</details>

<details>
<summary>Teal Pool Float – Zaria&#x27;s Table (255 items)</summary>

| Item name | ID |
| --- | ---: |
| Teal Pool Float | 4556 |
| Teal Sectional Couch | 50002 |
| Terracotta Door | 11450 |
| Terracotta Patio | 11451 |
| Terracotta Roof | 11452 |
| Terracotta Shackle Door | 11455 |
| Terracotta Shackle Patio | 11456 |
| Terracotta Shackle Roof | 11457 |
| Terracotta Shackle Walls | 11458 |
| Terracotta Shackle Windows | 11459 |
| Terracotta Walls | 11453 |
| Terracotta Windows | 11454 |
| Thorian Plushie | 14109 |
| Thorian's Ancient Vase | 14110 |
| Thorian's Basket of Scrolls | 14099 |
| Thorian's Bed | 14098 |
| Thorian's Chair | 14102 |
| Thorian's Chest | 14101 |
| Thorian's Couch | 14100 |
| Thorian's Desk | 14103 |
| Thorian's End Table | 14108 |
| Thorian's Lamp | 14106 |
| Thorian's Rug | 14105 |
| Thorian's Wall Lamp | 14107 |
| Thorian's Wardrobe | 14104 |
| Throne of Luxury | 4491 |
| Tidy Temple Wardrobe | 21429 |
| Tier 2 Barn Permit | 11114 |
| Tier 2 Barn Upgrade | 10061 |
| Tier 2 Elven Barn Permit | 11117 |
| Tier 2 House Permit | 11111 |
| Tier 2 House Upgrade | 10101 |
| Tier 3 Barn Permit | 11115 |
| Tier 3 Barn Upgrade | 10062 |
| Tier 3 Elven Barn Permit | 11118 |
| Tier 3 House Permit | 11112 |
| Tier 3 House Upgrade | 10102 |
| Tiered Stacked Storage Dresser | 21415 |
| Tiki Barrel | 4039 |
| Tiki Lantern Pole | 4038 |
| Tiki Mask Bed | 4035 |
| Tiki Mask Totem Pole | 4037 |
| Tiki Tropical Mug | 4010 |
| Tilted Window | 4134 |
| Timeless Cityscape Painting | 2320 |
| Timeless Reports | 2321 |
| Timeless Typewriter | 2322 |
| Tire Chair | 21209 |
| Tis the Season Bed | 21340 |
| Tis the Season Couch | 21335 |
| Tis the Season Holly End Table | 21342 |
| Tis the Season Jolly End Table | 21341 |
| Tis the Season Rug | 21334 |
| Tis the Season Wardrobe | 21336 |
| Tis the Season Wooden Chair | 21339 |
| Tis the Season Wreath Lamp | 21343 |
| Toy Bear Chair | 21314 |
| Toy Bear Couch | 21313 |
| Toy Bear Plushie | 21319 |
| Toy Bed | 21316 |
| Toy Block Chair | 21318 |
| Toy Block Table | 21317 |
| Toy Block Wardrobe | 21323 |
| Toy Cube Table | 21321 |
| Toy Duck Plushie | 21320 |
| Toy Watch Clock | 21315 |
| Traditional Crystal Display | 4463 |
| Traditional Elven Fern | 4460 |
| Traditional Honeybrew | 4461 |
| Traditional Portrait | 4462 |
| Traditional Shrine Lantern | 21416 |
| Traditional Snowy Rug | 4315 |
| Tree Stump Fridge | 4623 |
| Triple Diamond Window | 14058 |
| Trishy Doll | 14021 |
| Tropical Bench | 4011 |
| UFO Prototype | 4099 |
| Unaging Firewood | 4411 |
| Unaging Painting | 4409 |
| Unaging Statue | 4410 |
| Underwater Porthole Window | 4027 |
| Uneven Window Trio | 4095 |
| Unpacked Beach Bag | 4579 |
| Unsprung Jack in the Box | 14030 |
| Used Lovers Lantern | 21419 |
| Used Tatami Mat Rug | 21403 |
| Vaan Plushie | 21678 |
| Vaan's Barrel of Balloons | 21673 |
| Vaan's Bed | 21674 |
| Vaan's Chair | 21675 |
| Vaan's Couch | 21676 |
| Vaan's End Table | 21669 |
| Vaan's Globe | 21670 |
| Vaan's Lamp | 21668 |
| Vaan's Rug | 21671 |
| Vaan's Wardrobe | 21677 |
| Vaan's Weather Craft Desk | 21672 |
| Vampire Snaccoon Plush | 3781 |
| Vaporwave Rug | 4356 |
| Vined Shut Window | 3960 |
| Vintage City Signs | 4417 |
| Vintage Gamer Chair | 4416 |
| Vintage Sprite Poster | 4415 |
| Vivi Plushie | 21689 |
| Vivi's Bed | 21679 |
| Vivi's Books | 21680 |
| Vivi's Chair | 21684 |
| Vivi's Couch | 21686 |
| Vivi's Kibble Barrel | 21682 |
| Vivi's Rug | 21685 |
| Vivi's Table | 21687 |
| Vivi's Torch | 21681 |
| Vivi's Wardrobe | 21688 |
| Wall Hanging Necklace | 21232 |
| Wall Mounted Sword | 21207 |
| Water Droplet Rug | 4421 |
| Watercolor Tiger Wall Scroll | 21231 |
| Watermelon Gnome | 4392 |
| Weak Double Bed | 4041 |
| Weak Wooden Chair | 3803 |
| Weak Wooden Dresser | 3806 |
| Weak Wooden Table | 3804 |
| Weak Wooden Wardrobe | 3805 |
| Weedil Bed | 4139 |
| Welded Bronze Flower | 14016 |
| Well Fed Snaccoon Plushie | 4494 |
| Wesley Plushie | 21701 |
| Wesley's Bed | 21695 |
| Wesley's Bookshelf | 21692 |
| Wesley's Chair | 21690 |
| Wesley's Couch | 21699 |
| Wesley's Floral Display | 21693 |
| Wesley's Flower Lamp | 21698 |
| Wesley's Meal Table | 21691 |
| Wesley's Mushroom Display | 21694 |
| Wesley's Rug | 21696 |
| Wesley's Table Lamp | 21697 |
| Wesley's Wardrobe | 21700 |
| White and Teal Beach Umbrella | 4019 |
| White Bishop | 31220 |
| White Daisy Plushie | 4243 |
| White King | 31228 |
| White Knight | 31222 |
| White Pawn | 31224 |
| White Queen | 31226 |
| White Rook | 31218 |
| White Wooden Vanity | 4050 |
| Wildfire Chair | 21446 |
| Wilted Lily Bloom | 14001 |
| Windy Chair | 4454 |
| Windy Hanging Plant | 4456 |
| Windy-Mill Vase | 4455 |
| Winter Bed | 4084 |
| Winter Chair | 4087 |
| Winter Couch | 4090 |
| Winter Door | 11855 |
| Winter Festival Sled | 4033 |
| Winter Hearth Table | 4091 |
| Winter Lamp | 4086 |
| Winter Mini Tree End Table (Blue) | 4088 |
| Winter Mini Tree End Table (White) | 4089 |
| Winter Patio | 11856 |
| Winter Roof | 11857 |
| Winter Rug | 4085 |
| Winter Snaccoon Plushie | 4317 |
| WInter Visitor Painting | 4327 |
| Winter Walls | 11858 |
| Winter Windows | 11859 |
| Witch's Moon | 21202 |
| Witchy Bug Display | 4407 |
| Witchy Potion Book Stand | 4408 |
| Witchy Rose Rug | 4406 |
| Witherball Bed | 4357 |
| Witherball Blossom | 4361 |
| Witherball Bookshelf | 4362 |
| Witherball Candlestick | 4360 |
| Witherball Chair | 4359 |
| Witherball Couch | 4358 |
| Witherball Invitation | 4397 |
| Withergate Balloons | 50006 |
| Withergate Door | 11460 |
| Withergate King Painting | 4342 |
| Withergate Patio | 11461 |
| Withergate Roof | 11462 |
| Withergate Snaccoon Plush | 3772 |
| Withergate Vanity | 4189 |
| Withergate Walls | 11463 |
| Withergate Windows | 11464 |
| Witherknight Statue | 21206 |
| Woodblock Printed Scroll | 21213 |
| Wooden Counter | 9307 |
| Wooden Heart Window | 4097 |
| Wooden Pot of Roses | 14004 |
| Wooden Table | 10003 |
| Wooden Vanity | 4049 |
| Wooden Wardrobe | 10002 |
| Wool Pelt Rug | 3796 |
| Wornhardt Plushie | 21713 |
| Wornhardt's Bed | 21710 |
| Wornhardt's Bird Cage | 21704 |
| Wornhardt's Chair | 21703 |
| Wornhardt's Coffee Craft | 21709 |
| Wornhardt's Couch | 21711 |
| Wornhardt's End Table | 21706 |
| Wornhardt's Lamp | 21707 |
| Wornhardt's Painting | 21705 |
| Wornhardt's Rug | 21712 |
| Wornhardt's Table | 21708 |
| Wornhardt's Wardrobe | 21702 |
| Wrought Iron Bed | 4585 |
| Xyla's Bed | 21723 |
| Xyla's Cat Plushie | 21719 |
| Xyla's Chair | 21715 |
| Xyla's Chess Piece Lamp | 21722 |
| Xyla's Couch | 21716 |
| Xyla's End Table | 21721 |
| Xyla's Ottoman | 21718 |
| Xyla's Plushie | 21714 |
| Xyla's Rug | 21717 |
| Xyla's Table | 21720 |
| Xyla's Wardrobe | 21724 |
| Yellow and Pink Beach Umbrella | 4016 |
| Yellow Door | 11465 |
| Yellow Patio | 11466 |
| Yellow Polka Dot Door | 11805 |
| Yellow Polka Dot Patio | 11806 |
| Yellow Polka Dot Roof | 11807 |
| Yellow Polka Dot Walls | 11808 |
| Yellow Polka Dot Windows | 11809 |
| Yellow Roof | 11467 |
| Yellow Runner Tea Low Table | 21389 |
| Yellow Runner Tea Table | 21390 |
| Yellow Striped Door | 11755 |
| Yellow Striped Patio | 11756 |
| Yellow Striped Roof | 11757 |
| Yellow Striped Walls | 11758 |
| Yellow Striped Windows | 11759 |
| Yellow Tea Chair | 21412 |
| Yellow Walls | 11468 |
| Yellow Windows | 11469 |
| Young Bonsai | 21212 |
| Young Prince Painting | 4341 |
| Yummy Bento Box | 21392 |
| Zaria Plushie | 21735 |
| Zaria's Bed | 21726 |
| Zaria's Bookshelf | 21725 |
| Zaria's Chair | 21732 |
| Zaria's Couch | 21734 |
| Zaria's Empty Bucket | 21150 |
| Zaria's End Table | 21730 |
| Zaria's Lamp | 21727 |
| Zaria's Message in a Bottle | 21728 |
| Zaria's Rug | 21733 |
| Zaria's Starfish | 21729 |
| Zaria's Table | 21731 |

</details>

### Jewels from game data

**12 items**

| Item name | ID |
| --- | ---: |
| Amethyst | 1002 |
| Beryl | 10618 |
| Black Diamond | 1005 |
| Citrine | 10617 |
| Diamond | 1003 |
| Dizzite | 10860 |
| Emerald | 10620 |
| Havenite | 1004 |
| Lapis | 10619 |
| Ruby | 1001 |
| Sapphire | 1000 |
| Tanzanite | 10621 |

### Monster Drops from game data

**79 items**

| Item name | ID |
| --- | ---: |
| Ancient Amari Totem | 20160 |
| Ancient Angel Quill | 20158 |
| Ancient Elven Headdress | 20155 |
| Ancient Magic Staff | 20151 |
| Ancient Naga Crook | 20159 |
| Ancient Nel'Varian Sword | 20101 |
| Ancient Sun Haven Sword | 20100 |
| Ancient Withergate Sword | 20102 |
| Antler | 20006 |
| Bent Traffic Cone | 20027 |
| Bronze Dragon Relic | 20152 |
| Bucket Crab Trinket | 20111 |
| Bug Shell | 20003 |
| Bushie's Branch | 20002 |
| Cardboard Box Piece | 20026 |
| Centipillar Trinket | 20105 |
| Chimchuck Trinket | 20113 |
| Croc Scale | 20031 |
| Dandelion | 20022 |
| Dragon Fang | 20207 |
| Dragonfly | 20010 |
| Drill Bit | 20011 |
| Elios Blanket | 4564 |
| Elite Leafie Trinket | 20104 |
| Elite Scorpepper Trinket | 20108 |
| Empty Husk | 20038 |
| Fairy Wings | 20202 |
| Floaty Crab Trinket | 20110 |
| Fly | 20024 |
| Fur Tuft | 20009 |
| Green Pepper Flakes | 20012 |
| Griffon Egg | 20203 |
| Handmade Bobber | 20150 |
| Hat Crab Trinket | 20109 |
| Haunted Log | 20013 |
| Hollow Tube | 20039 |
| Hot Sauce | 20014 |
| Ice Cube | 20015 |
| Keelhaul Fin | 20034 |
| Knitted Socks | 4561 |
| Lava Honey | 20020 |
| Leafie Trinket | 20103 |
| Leafie's Leaf | 20000 |
| Lightning in a Bottle | 20005 |
| Mana Sap | 20204 |
| Mangler Bulb | 20035 |
| Metal Pipe | 20036 |
| Monster Candy | 20208 |
| Mysterious Antler | 20206 |
| Nel'Varian Runestone | 20154 |
| Old Mayoral Painting | 20156 |
| Old Sword Hilt | 20153 |
| Orange Pepper Flakes | 20016 |
| Peppinch - Green Trinket | 20106 |
| Petrified Log | 20200 |
| Phoenix Feather | 20201 |
| Pricklepop Pear | 20021 |
| Prickletot Pear | 20004 |
| Pumice Stone | 20205 |
| Sand | 20030 |
| Scarf | 4562 |
| Scorpepper Trinket | 20107 |
| Slime Goop | 20032 |
| Sludge | 20025 |
| Snow Ball | 20019 |
| Soot | 20017 |
| Spectre Slime | 20008 |
| Squashed Banana | 20001 |
| Sticky Sap | 20018 |
| Sun Haven Quilt | 4560 |
| Tentacle Monster Emblem | 20157 |
| Tentacrush Ink | 20033 |
| Throw Blanket | 4563 |
| Torn Page | 20007 |
| Tough Tin Can | 20028 |
| Tough Trash Bag | 20029 |
| Umbrella Crab Trinket | 20112 |
| Unicorn Hair Tuft | 20209 |
| Wind-Up Key | 20037 |

### Seeds from game data

**92 items**

| Item name | ID |
| --- | ---: |
| Acorn Seeds | 12031 |
| Armoranth Seeds | 12053 |
| Balloon Fruit Seeds | 12063 |
| Barley Seeds | 12045 |
| Beet Seeds | 13080 |
| Blizzard Berry Seeds | 12068 |
| Blue Moon Fruit Seeds | 12064 |
| Blue Rose Seeds | 12108 |
| Brr-Nana Seeds | 13082 |
| Butternut Seeds | 12044 |
| Candy Cane Seeds | 12077 |
| Carrot Seeds | 12006 |
| Cat Tail Seeds | 12032 |
| Chocoberry Seeds | 12054 |
| Cinnaberry Seeds | 12012 |
| Clover Seeds | 12055 |
| Coffee Bean Seeds | 12059 |
| Corn Seeds | 12001 |
| Cotton Seeds | 12075 |
| Cranberry Seeds | 12070 |
| Daisy Seeds | 12111 |
| Darkness Essence Seeds | 12034 |
| Demon Seeds | 12004 |
| Dragon Fruit Seeds | 12027 |
| Durian Seeds | 12062 |
| Eggplant Seeds | 12015 |
| Fire Fruit Seeds | 12024 |
| Fizzy Fruit Seeds | 12039 |
| Garlic Seeds | 12060 |
| Ghost Pepper Seeds | 12049 |
| Grape Seeds | 12022 |
| Green Bean Seeds | 12072 |
| Greenroot Seeds | 12010 |
| Guava Berry Seeds | 12035 |
| Heart Berry Seeds | 12058 |
| Heat Fruit Seeds | 12041 |
| Hexagon Berry Seeds | 12065 |
| Hibiscus Seeds | 12103 |
| Honey Flower Seeds | 12101 |
| Honeysuckle Seeds | 12076 |
| Hops Seeds | 12037 |
| Indiglow Seeds | 12030 |
| Kale Seeds | 12050 |
| Kiwi Berry Seeds | 12071 |
| Kraken Kale Seeds | 12016 |
| Lavender Seeds | 12102 |
| Lemon Seeds | 12052 |
| Lettuce Seeds | 12013 |
| Lily Seeds | 12104 |
| Lotus Seeds | 12110 |
| Mana Gem Seeds | 12033 |
| Mango Seeds | 12061 |
| Marshmallow Bean Seeds | 12042 |
| Melon Seeds | 12057 |
| Moonplant Seeds | 12017 |
| Onion Seeds | 12009 |
| Orchid Seeds | 12105 |
| Pea Seeds | 12073 |
| Pepper Seeds | 12008 |
| Pineapple Seeds | 12056 |
| Potato Seeds | 12002 |
| Pumpkin Seeds | 12036 |
| Purple Eggplant Seeds | 13081 |
| Pythagorean Berry Seeds | 12069 |
| Razorstalk Seeds | 12020 |
| Red Rose Seeds | 12107 |
| Rice Seeds | 12014 |
| Rock Fruit Seeds | 12025 |
| Shiiwalki Mushroom Seeds | 12029 |
| Shimmeroot Seeds | 12007 |
| Snappy Seeds | 12005 |
| Snow Ball Seeds | 12067 |
| Snow Pea Seeds | 12078 |
| Soda Pop Crop Seeds | 12038 |
| Soul Orb Seeds | 12021 |
| Star Fruit Seeds | 12066 |
| Stormelon Seeds | 12051 |
| Suckerstem Seeds | 12018 |
| Sugar Cane Seeds | 13079 |
| Sun Orb Seeds | 12083 |
| Sunflower Seeds | 12106 |
| Tea Leaf Seeds | 12048 |
| Tomato Seeds | 12003 |
| Tombmelon Seeds | 12019 |
| Tulip Seeds | 12109 |
| Turnip Seeds | 12040 |
| Walk Choy Seeds | 12028 |
| Water Fruit Seeds | 12023 |
| Watermelon Vine Seeds | 12074 |
| Wheat Seeds | 12000 |
| Wind Chime Seeds | 12026 |
| Yam Seeds | 12047 |

### Tools from game data

Zero matches in this build. Sun Haven’s native `Tool` class inherits from `Weapon`, and the mod checks Weapons first. Find pickaxes, axes, hoes, watering cans, and fishing rods under [Weapons](#weapons-from-game-data).

### Weapons from game data

**135 items**

| Item name | ID |
| --- | ---: |
| Adamant Axe | 3303 |
| Adamant Hoe | 3203 |
| Adamant Pickaxe | 3103 |
| Adamant Sword | 4002 |
| Adamant Watering Can | 3503 |
| Aegis | 307 |
| Algae Staff | 3210 |
| Basic Fishing Rod | 3400 |
| Branch Fishing Rod | 3403 |
| Brinestone Teleportation Spell | 361 |
| Bubble Net | 309 |
| Bubble Staff | 3211 |
| Carrot Sword | 4006 |
| Cataclysm | 310 |
| Chain Lightning | 304 |
| Copper Axe | 3301 |
| Copper Hoe | 3201 |
| Copper Pickaxe | 3101 |
| Copper Sword | 4000 |
| Copper Watering Can | 3501 |
| Coral Staff | 3214 |
| Corn Sword | 4007 |
| Crossbow | 201 |
| Dev Axe | 30005 |
| Dev Pickaxe | 30006 |
| Dev Scythe | 30007 |
| Dev Sword | 30008 |
| Dev Watering Can | 30004 |
| DevHoe | 30003 |
| Earthquake | 306 |
| Egg Crossbow | 206 |
| Elemental Tap | 352 |
| Elven Crossbow | 203 |
| Enchanted Adamant Axe | 3315 |
| Enchanted Adamant Pickaxe | 3117 |
| Enchanted Copper Axe | 3313 |
| Enchanted Copper Pickaxe | 3115 |
| Enchanted Fishing Rod | 3406 |
| Enchanted Glorite Axe | 3318 |
| Enchanted Glorite Pickaxe | 3119 |
| Enchanted Iron Axe | 3314 |
| Enchanted Iron Pickaxe | 3116 |
| Enchanted Mithril Axe | 3316 |
| Enchanted Mithril Pickaxe | 3118 |
| Enchanted Sunite Axe | 3317 |
| Enchanted Sunite Pickaxe | 3120 |
| Enhanced Adamant Axe | 3309 |
| Enhanced Adamant Pickaxe | 3111 |
| Enhanced Copper Axe | 3307 |
| Enhanced Copper Pickaxe | 3109 |
| Enhanced Glorite Axe | 3312 |
| Enhanced Glorite Pickaxe | 3114 |
| Enhanced Iron Axe | 3308 |
| Enhanced Iron Pickaxe | 3110 |
| Enhanced Mithril Axe | 3310 |
| Enhanced Mithril Pickaxe | 3112 |
| Enhanced Sunite Axe | 3311 |
| Enhanced Sunite Pickaxe | 3113 |
| Ethereal Axe | 308 |
| Fire Beam | 301 |
| Fireball | 305 |
| Ghostly Great Sword | 5912 |
| Glorite Axe | 3306 |
| Glorite Hoe | 3206 |
| Glorite Pickaxe | 3106 |
| Glorite Sword | 4005 |
| Glorite Watering Can | 3506 |
| Golden Fishing Rod | 3404 |
| Great City Teleportation Spell | 362 |
| Heavy Crossbow | 202 |
| Iron Axe | 3302 |
| Iron Hoe | 3202 |
| Iron Pickaxe | 3102 |
| Iron Sword | 4001 |
| Iron Watering Can | 3502 |
| Legendary Great Sword | 5913 |
| Legendary Hammer | 5910 |
| Lightning Hammer | 5909 |
| Miracle | 351 |
| Mithril Axe | 3304 |
| Mithril Crossbow | 204 |
| Mithril Hoe | 3204 |
| Mithril Pickaxe | 3104 |
| Mithril Sword | 4003 |
| Mithril Watering Can | 3504 |
| Nel'Vari Fishing Rod | 3402 |
| Nel'Vari Teleportation Spell | 359 |
| Nel'Varian Pickaxe | 3107 |
| Pepper Great Sword | 5911 |
| Perfect Adamant Axe | 3321 |
| Perfect Adamant Pickaxe | 3123 |
| Perfect Copper Axe | 3319 |
| Perfect Copper Pickaxe | 3121 |
| Perfect Glorite Axe | 3324 |
| Perfect Glorite Pickaxe | 3126 |
| Perfect Iron Axe | 3320 |
| Perfect Iron Pickaxe | 3122 |
| Perfect Mithril Axe | 3322 |
| Perfect Mithril Pickaxe | 3124 |
| Perfect Sunite Axe | 3323 |
| Perfect Sunite Pickaxe | 3125 |
| Potato Hammer | 5908 |
| Rain Cloud | 303 |
| Rel'Tar's Mark (Crossbow) | 205 |
| Rusty Axe | 3300 |
| Rusty Hoe | 3200 |
| Rusty Pickaxe | 3100 |
| Rusty Watering Can | 3500 |
| Scythe | 3000 |
| Shadow Rush | 350 |
| Shell Staff | 3212 |
| Simple Adamant Great Sword | 5900 |
| Simple Adamant Hammer | 5905 |
| Simple Copper Great Sword | 4008 |
| Simple Copper Hammer | 5903 |
| Simple Iron Great Sword | 4009 |
| Simple Iron Hammer | 5904 |
| Simple Mithril Great Sword | 5901 |
| Simple Mithril Hammer | 5906 |
| Simple Sunite Great Sword | 5902 |
| Simple Sunite Hammer | 5907 |
| Snowball Launcher | 207 |
| Squid Staff | 3213 |
| Sun Haven Teleportation Spell | 358 |
| Sunite Axe | 3305 |
| Sunite Hoe | 3205 |
| Sunite Pickaxe | 3105 |
| Sunite Sword | 4004 |
| Sunite Watering Can | 3505 |
| Teleportation Spell | 357 |
| Vacuumulus | 302 |
| Very Good Fishing Rod | 3401 |
| Withergate Fishing Rod | 3405 |
| Withergate Pickaxe | 3108 |
| Withergate Teleportation Spell | 360 |

## Explicit item lists

These are the entries stored in the release DLL. Categories that also check native item properties describe those checks [above](#affinity-dropdown-and-matching-rules). Item names come from the installed Sun Haven item data.

### Breads

| Item name | Game key | ID |
| --- | --- | ---: |
| Bread | `Bread` | 3032 |
| Tomato Bread | `TomatoBread` | 3097 |
| Banana Bread | `BananaBread` | 3830 |
| Mushroom Festival Pumpkin Bread | `MushroomFestivalPumpkinBread` | 30084 |
| Mushroom Toast | `MushroomToast` | 11572 |
| Avocado Toast | `AvocadoToast` | 30155 |
| Plain Pretzel | `PlainPretzel` | 3603 |
| Berry Glazed Pretzel | `BerryGlazedPretzel` | 3605 |
| Salted Pretzel | `SaltedPretzel` | 3607 |
| Chocolate Pretzel | `ChocolatePretzel` | 3608 |
| Clef Note Pretzel | `ClefNotePretzel` | 3930 |
| Algae Dipped Pretzel | `AlgaeDippedPretzel` | 30014 |
| Kelp Bun | `KelpBun` | 30013 |
| Garden Festival Buttered Bun | `GardenFestivalButteredBun` | 30074 |
| Almond Croissant | `AlmondCroissant` | 30124 |

### Crystals

| Item name | Game key | ID |
| --- | --- | ---: |
| Earth Crystal | `EarthCrystal` | 1111 |
| Fire Crystal | `FireCrystal` | 1110 |
| Water Crystal | `WaterCrystal` | 1112 |
| Crystal Cluster | `CrystalCluster` | 2056 |

### Currency

| Item name | Game key | ID |
| --- | --- | ---: |
| Red Carnival Ticket | `RedCarnivalTicket` | 18012 |
| Community Token | `CommunityToken` | 18013 |
| Darkness Essence | `DarknessEssence` | 18014 |
| Mana Shard | `ManaShard` | 18015 |
| Candy Corn Pieces | `CandyCornPieces` | 18016 |
| Kingly Ticket | `KinglyTicket` | 18017 |
| First Class Ticket | `FirstClassTicket` | 18018 |
| Economy Ticket | `EconomyTicket` | 18019 |
| Spring Token | `SpringToken` | 18020 |
| Summer Token | `SummerToken` | 18021 |
| Winter Token | `WinterToken` | 18022 |
| Fall Token | `FallToken` | 18023 |
| Black Bottle Cap | `BlackBottleCap` | 60013 |
| Doubloons | `Doubloons` | 60014 |
| Bag of Doubloons | `BagofDoubloons` | 60015 |
| Ticket | `Ticket` | 18011 |
| Coins | `Coins` | 60000 |
| Mana Orbs | `ManaOrbs` | 60001 |
| Tickets | `Tickets` | 60002 |

### Elixirs

| Item name | Game key | ID |
| --- | --- | ---: |
| Elixir of Fortitude | `ElixirofFortitude` | 3090 |
| Elixir of Mind | `ElixirofMind` | 3091 |
| Elixir of Speed | `ElixirofSpeed` | 3092 |
| Elixir of Arcane Might | `ElixirofArcaneMight` | 3093 |
| Elixir of Ferocity | `ElixirofFerocity` | 3094 |
| Elixir of Iron Will | `ElixirofIronWill` | 3095 |
| Amazing Elixir of Farming | `AmazingElixirofFarming` | 30140 |
| Amazing Elixir of Mining | `AmazingElixirofMining` | 30141 |
| Amazing Elixir of Fishing | `AmazingElixirofFishing` | 30142 |
| Elixir of Farming | `ElixirofFarming` | 18105 |
| Elixir of Exploration | `ElixirofExploration` | 18106 |
| Elixir of Mining | `ElixirofMining` | 18107 |
| Elixir of Combat | `ElixirofCombat` | 18108 |
| Elixir of Fishing | `ElixirofFishing` | 18109 |

### Fertilizers

| Item name | Game key | ID |
| --- | --- | ---: |
| Simple Earth Fertilizer | `SimpleEarthFertilizer` | 4501 |
| Advanced Earth Fertilizer | `AdvancedEarthFertilizer` | 4502 |
| Simple Fire Fertilizer | `SimpleFireFertilizer` | 4503 |
| Advanced Fire Fertilizer | `AdvancedFireFertilizer` | 4504 |
| Simple Water Fertilizer | `SimpleWaterFertilizer` | 4505 |
| Advanced Water Fertilizer | `AdvancedWaterFertilizer` | 4506 |
| Mana Fertilizer | `ManaFertilizer` | 4519 |
| Simple Magic Fertilizer | `SimpleMagicFertilizer` | 4543 |
| Advanced Magic Fertilizer | `AdvancedMagicFertilizer` | 4544 |
| Simple Sand Fertilizer | `SimpleSandFertilizer` | 4575 |
| Slime Fertilizer | `SlimeFertilizer` | 4576 |
| Compost | `Compost` | 4507 |
| Advanced Compost | `AdvancedCompost` | 4508 |
| Elven Compost | `ElvenCompost` | 4518 |
| Monster Compost | `MonsterCompost` | 4540 |
| Advanced Monster Compost | `AdvancedMonsterCompost` | 4541 |

### Fishing Bait

| Item name | Game key | ID |
| --- | --- | ---: |
| Basic Fish Bait | `BasicFishBait` | 4509 |
| Advanced Fish Bait | `AdvancedFishBait` | 4510 |
| Legendary Fish Bait | `LegendaryFishBait` | 4511 |
| Chilly Fishing Bait | `ChillyFishingBait` | 4512 |
| Spicy Fishing Bait | `SpicyFishingBait` | 4513 |
| Really Spicy Fishing Bait | `ReallySpicyFishingBait` | 4514 |
| Sweet Fish Bait | `SweetFishBait` | 4515 |
| Lucky Fish Bait | `LuckyFishBait` | 4516 |

### Flowers

| Item name | Game key | ID |
| --- | --- | ---: |
| Honey Flower | `HoneyFlower` | 11101 |
| Lavender | `Lavender` | 11102 |
| Hibiscus | `Hibiscus` | 11103 |
| Lily | `Lily` | 11104 |
| Orchid | `Orchid` | 11105 |
| Sunflower | `Sunflower` | 11106 |
| Red Rose | `RedRose` | 11107 |
| Blue Rose | `BlueRose` | 11108 |
| Tulip | `Tulip` | 11109 |
| Lotus | `Lotus` | 11110 |
| Daisy | `Daisy` | 11130 |
| Honeysuckle | `Honeysuckle` | 11076 |

### Jewels

| Item name | Game key | ID |
| --- | --- | ---: |
| Sapphire | `Sapphire` | 1000 |
| Ruby | `Ruby` | 1001 |
| Amethyst | `Amethyst` | 1002 |
| Diamond | `Diamond` | 1003 |
| Havenite | `Havenite` | 1004 |
| Black Diamond | `BlackDiamond` | 1005 |

### Ore Bars

| Item name | Game key | ID |
| --- | --- | ---: |
| Copper Bar | `CopperBar` | 1200 |
| Iron Bar | `IronBar` | 1201 |
| Adamant Bar | `AdamantBar` | 1202 |
| Mithril Bar | `MithrilBar` | 1203 |
| Sunite Bar | `SuniteBar` | 1204 |
| Gold Bar | `GoldBar` | 1205 |
| Glorite Bar | `GloriteBar` | 1206 |
| Elven Steel Bar | `ElvenSteelBar` | 1207 |
| Refined Metal | `RefinedMetal` | 2052 |
| Enhanced Copper Bar | `EnhancedCopperBar` | 1117 |
| Enhanced Iron Bar | `EnhancedIronBar` | 1118 |
| Enhanced Adamant Bar | `EnhancedAdamantBar` | 1119 |
| Enhanced Mithril Bar | `EnhancedMithrilBar` | 1120 |
| Enhanced Sunite Bar | `EnhancedSuniteBar` | 1121 |
| Enhanced Glorite Bar | `EnhancedGloriteBar` | 1122 |
| Enchanted Copper Bar | `EnchantedCopperBar` | 1123 |
| Enchanted Iron Bar | `EnchantedIronBar` | 1124 |
| Enchanted Adamant Bar | `EnchantedAdamantBar` | 1125 |
| Enchanted Mithril Bar | `EnchantedMithrilBar` | 1126 |
| Enchanted Sunite Bar | `EnchantedSuniteBar` | 1127 |
| Enchanted Glorite Bar | `EnchantedGloriteBar` | 1128 |

### Ores

| Item name | Game key | ID |
| --- | --- | ---: |
| Copper Ore | `CopperOre` | 1100 |
| Iron Ore | `IronOre` | 1101 |
| Adamant Ore | `AdamantOre` | 1102 |
| Mithril Ore | `MithrilOre` | 1103 |
| Sunite Ore | `SuniteOre` | 1104 |
| Gold Ore | `GoldOre` | 1105 |
| Glorite Ore | `GloriteOre` | 1107 |
| Elven Steel Ore | `ElvenSteelOre` | 1108 |
| Sandstone Ore | `SandstoneOre` | 2117 |
| Coal | `Coal` | 1106 |
| Stone | `Stone` | 2001 |
| Heavystone | `Heavystone` | 2119 |
| Dead Stone | `DeadStone` | 2015 |
| Dead Heavystone | `DeadHeavystone` | 2016 |
| Elven Stone | `ElvenStone` | 2021 |
| Elven Heavystone | `ElvenHeavystone` | 2022 |
| Unrefined Metal | `UnrefinedMetal` | 2122 |

### Woods

| Item name | Game key | ID |
| --- | --- | ---: |
| Log | `Log` | 2002 |
| Wood Plank | `WoodPlank` | 2003 |
| Hardwood | `Hardwood` | 2007 |
| Hardwood Plank | `HardwoodPlank` | 2008 |
| Hardwood Beam | `HardwoodBeam` | 2009 |
| Wood Beam | `WoodBeam` | 2010 |
| Dead Log | `DeadLog` | 2011 |
| Dead Hardwood | `DeadHardwood` | 2012 |
| Dead Plank | `DeadPlank` | 2013 |
| Dead Hardwood Plank | `DeadHardwoodPlank` | 2014 |
| Elven Log | `ElvenLog` | 2017 |
| Elven Hardwood | `ElvenHardwood` | 2018 |
| Elven Plank | `ElvenPlank` | 2019 |
| Elven Hardwood Plank | `ElvenHardwoodPlank` | 2020 |
| Driftwood | `Driftwood` | 2101 |
| Fallen Log | `FallenLog` | 2106 |
| Golden Log | `GoldenLog` | 2114 |
| Golden Hardwood | `GoldenHardwood` | 60259 |

## Museum items by bundle

The release stores a single list of 288 distinct IDs. They are grouped here by the 28 active Sun Haven bundles for easier lookup. Items accepted by two bundles appear in both.

### Alchemy Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Advanced Attack Potion | `AdvancedAttackPotion` | 3085 |
| Advanced Defense Potion | `AdvancedDefensePotion` | 3086 |
| Advanced Spell Damage Potion | `AdvancedSpellDamagePotion` | 3087 |
| Attack Potion | `AttackPotion` | 3082 |
| Defense Potion | `DefensePotion` | 3084 |
| Health Potion | `HealthPotion` | 3081 |
| Incredible Attack Potion | `IncredibleAttackPotion` | 3767 |
| Incredible Defense Potion | `IncredibleDefensePotion` | 3768 |
| Incredible Spell Damage Potion | `IncredibleSpellDamagePotion` | 3766 |
| Mana Potion | `ManaPotion` | 3080 |
| Speed Potion | `SpeedPotion` | 3083 |

### Aquarium — Big Tank

| Item name | Game key | ID |
| --- | --- | ---: |
| Angel Fish | `AngelFish` | 15005 |
| Black Bass | `BlackBass` | 15084 |
| Blunted Swordfish | `BluntedSwordfish` | 15017 |
| Carp | `Carp` | 15010 |
| Catfish | `Catfish` | 15018 |
| Clown Fish | `ClownFish` | 15083 |
| Cuddlefish | `Cuddlefish` | 15022 |
| Eel | `Eel` | 15002 |
| Gold Fish | `GoldFish` | 15008 |
| Ironhead Sturgeon | `IronheadSturgeon` | 15024 |
| Koi Fish | `KoiFish` | 15090 |
| Lobster | `Lobster` | 15088 |
| Popeye Goldfish | `PopeyeGoldfish` | 15082 |
| Pufferfish | `Pufferfish` | 15007 |
| Pygmy Tuna | `PygmyTuna` | 15023 |
| Rainbow Trout | `RainbowTrout` | 15004 |
| Red Snapper | `RedSnapper` | 15011 |
| Redeye Piranha | `RedeyePiranha` | 15016 |
| Ribbon Eel | `RibbonEel` | 15089 |
| Salmon | `Salmon` | 15085 |
| Sandstone Fish | `SandstoneFish` | 2118 |
| Silver Carp | `SilverCarp` | 15012 |
| Streamline Cod | `StreamlineCod` | 15014 |
| Tiger Trout | `TigerTrout` | 15086 |
| Tuna | `Tuna` | 15087 |
| Whitebelly Shark | `WhitebellyShark` | 15013 |

### Aquarium — Fall

| Item name | Game key | ID |
| --- | --- | ---: |
| Acorn Anchovy | `AcornAnchovy` | 15128 |
| Autumn Leaf Sole | `AutumnLeafSole` | 15135 |
| Coducopia | `Coducopia` | 15125 |
| Ghostfish | `Ghostfish` | 15132 |
| Hayfish | `Hayfish` | 15127 |
| King Salmon | `KingSalmon` | 15126 |
| Pirate Perch | `PiratePerch` | 15134 |
| Pumpkin Jelly | `PumpkinJelly` | 15133 |
| Vampire Piranha | `VampirePiranha` | 15131 |

### Aquarium — Nelvari

| Item name | Game key | ID |
| --- | --- | ---: |
| Angelfin | `Angelfin` | 15059 |
| Axolotl | `Axolotl` | 15055 |
| Bubblefish | `Bubblefish` | 15060 |
| Crystal Tetra | `CrystalTetra` | 15044 |
| Dragon Gulper | `DragonGulper` | 15040 |
| Flamefish | `Flamefish` | 15036 |
| Frilled Betta | `FrilledBetta` | 15054 |
| Horsefish | `Horsefish` | 15053 |
| Kelp Eel | `KelpEel` | 15045 |
| Neapolitan Fish | `NeapolitanFish` | 15056 |
| Princely Frog | `PrincelyFrog` | 15058 |
| Robed Parrotfish | `RobedParrotfish` | 15041 |
| Sky Ray | `SkyRay` | 15046 |
| Snobfish | `Snobfish` | 15042 |

### Aquarium — Spring

| Item name | Game key | ID |
| --- | --- | ---: |
| Butterflyfish | `Butterflyfish` | 15117 |
| Floral Trout | `FloralTrout` | 15119 |
| Flower Flounder | `FlowerFlounder` | 15114 |
| Neon Tetra | `NeonTetra` | 15121 |
| Painted Egg | `PaintedEgg` | 15123 |
| Raincloud Ray | `RaincloudRay` | 15118 |
| Seahorse | `Seahorse` | 15122 |
| Sunfish | `Sunfish` | 15116 |
| Tadpole | `Tadpole` | 15124 |

### Aquarium — Summer

| Item name | Game key | ID |
| --- | --- | ---: |
| Blazeel | `Blazeel` | 15104 |
| Flame Ray | `FlameRay` | 15111 |
| Hearth Angler | `HearthAngler` | 15106 |
| Magma Star | `MagmaStar` | 15108 |
| Molten Slug | `MoltenSlug` | 15112 |
| Pyrelus | `Pyrelus` | 15110 |
| Scorching Squid | `ScorchingSquid` | 15107 |
| Searback | `Searback` | 15113 |
| Tinder Turtle | `TinderTurtle` | 15109 |

### Aquarium — Winter

| Item name | Game key | ID |
| --- | --- | ---: |
| Blazing Herring | `BlazingHerring` | 15102 |
| Christmas Lightfish | `ChristmasLightfish` | 15095 |
| Frostfin | `Frostfin` | 15094 |
| Frozen Tuna | `FrozenTuna` | 15098 |
| Heatfin | `Heatfin` | 15100 |
| Holly Carp | `HollyCarp` | 15096 |
| Icicle Carp | `IcicleCarp` | 15101 |
| Jingle Bass | `JingleBass` | 15097 |
| Scarffish | `Scarffish` | 15099 |

### Aquarium — Withergate

| Item name | Game key | ID |
| --- | --- | ---: |
| Albino Squid | `AlbinoSquid` | 15079 |
| Bonemouth Bass | `BonemouthBass` | 15028 |
| Brain Jelly | `BrainJelly` | 15068 |
| Deadeye Shrimp | `DeadeyeShrimp` | 15033 |
| Devilfin | `Devilfin` | 15080 |
| Electric Eel | `ElectricEel` | 15066 |
| Ghosthead Tuna | `GhostheadTuna` | 15073 |
| Globfish | `Globfish` | 15072 |
| Goblin Shark | `GoblinShark` | 15074 |
| Kraken | `Kraken` | 15070 |
| Living Jelly | `LivingJelly` | 15031 |
| Moonfish | `Moonfish` | 15076 |
| Mummy Trout | `MummyTrout` | 15069 |
| Purrmaid | `Purrmaid` | 15037 |
| Redfinned Pincher | `RedfinnedPincher` | 15067 |
| Sea Bat | `SeaBat` | 15071 |
| Shadow Tuna | `ShadowTuna` | 15029 |
| Slime Leech | `SlimeLeech` | 15035 |
| Toothy Angler | `ToothyAngler` | 15030 |
| Vampire Squid | `VampireSquid` | 15075 |
| Viperfish | `Viperfish` | 15077 |
| Water Bear | `WaterBear` | 15065 |

### Archeology Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Balloon Fruit | `BalloonFruit` | 11063 |
| Blizzard Berry | `BlizzardBerry` | 11068 |
| Blue Moon Fruit | `BlueMoonFruit` | 11064 |
| Brr-Nana | `BrrNana` | 12082 |
| Candy Cane | `CandyCane` | 11077 |
| Heat Fruit | `HeatFruit` | 11041 |
| Hexagon Berry | `HexagonBerry` | 11065 |
| Marshmallow Bean | `MarshmallowBean` | 11042 |
| Purple Eggplant | `PurpleEggplant` | 12081 |
| Pythagorean Berry | `PythagoreanBerry` | 11069 |
| Snow Ball | `SnowBall` | 20019 |
| Snow Pea | `SnowPea` | 11078 |
| Star Fruit | `StarFruit` | 11066 |
| Tea Leaves | `TeaLeaves` | 11048 |
| Turnip | `Turnip` | 11040 |

### Bars Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Adamant Bar | `AdamantBar` | 1202 |
| Copper Bar | `CopperBar` | 1200 |
| Elven Steel Bar | `ElvenSteelBar` | 1207 |
| Glorite Bar | `GloriteBar` | 1206 |
| Gold Bar | `GoldBar` | 1205 |
| Iron Bar | `IronBar` | 1201 |
| Mithril Bar | `MithrilBar` | 1203 |
| Sunite Bar | `SuniteBar` | 1204 |

### Combat Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Ancient Nel'Varian Sword | `AncientNelVarianSword` | 20101 |
| Ancient Sun Haven Sword | `AncientSunHavenSword` | 20100 |
| Ancient Withergate Sword | `AncientWithergateSword` | 20102 |
| Bucket Crab Trinket | `BucketCrabTrinket` | 20111 |
| Centipillar Trinket | `CentipillarTrinket` | 20105 |
| Chimchuck Trinket | `ChimchuckTrinket` | 20113 |
| Elite Leafie Trinket | `EliteLeafieTrinket` | 20104 |
| Elite Scorpepper Trinket | `EliteScorpepperTrinket` | 20108 |
| Floaty Crab Trinket | `FloatyCrabTrinket` | 20110 |
| Hat Crab Trinket | `HatCrabTrinket` | 20109 |
| Leafie Trinket | `LeafieTrinket` | 20103 |
| Peppinch - Green Trinket | `PeppinchGreenTrinket` | 20106 |
| Scorpepper Trinket | `ScorpepperTrinket` | 20107 |
| Umbrella Crab Trinket | `UmbrellaCrabTrinket` | 20112 |

### Exploration Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Dragon Fang | `DragonFang` | 20207 |
| Fairy Wings | `FairyWings` | 20202 |
| Griffon Egg | `GriffonEgg` | 20203 |
| Mana Sap | `ManaSap` | 20204 |
| Monster Candy | `MonsterCandy` | 20208 |
| Mysterious Antler | `MysteriousAntler` | 20206 |
| Petrified Log | `PetrifiedLog` | 20200 |
| Phoenix Feather | `PhoenixFeather` | 20201 |
| Pumice Stone | `PumiceStone` | 20205 |
| Unicorn Hair Tuft | `UnicornHairTuft` | 20209 |

### Fall Crops Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Barley | `Barley` | 11045 |
| Butternut | `Butternut` | 11044 |
| Cranberry | `Cranberry` | 11070 |
| Fizzy Fruit | `FizzyFruit` | 11039 |
| Garlic | `Garlic` | 11060 |
| Ghost Pepper | `GhostPepper` | 11049 |
| Pumpkin | `Pumpkin` | 11036 |
| Soda Pop Crop | `SodaPopCrop` | 11038 |
| Yam | `Yam` | 11047 |

### Fishing Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Ancient Amari Totem | `AncientAmariTotem` | 20160 |
| Ancient Angel Quill | `AncientAngelQuill` | 20158 |
| Ancient Elven Headdress | `AncientElvenHeaddress` | 20155 |
| Ancient Magic Staff | `AncientMagicStaff` | 20151 |
| Ancient Naga Crook | `AncientNagaCrook` | 20159 |
| Bronze Dragon Relic | `BronzeDragonRelic` | 20152 |
| Handmade Bobber | `HandmadeBobber` | 20150 |
| Nel'Varian Runestone | `NelVarianRunestone` | 20154 |
| Old Mayoral Painting | `OldMayoralPainting` | 20156 |
| Old Sword Hilt | `OldSwordHilt` | 20153 |
| Tentacle Monster Emblem | `TentacleMonsterEmblem` | 20157 |

### Flowers Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Blue Rose | `BlueRose` | 11108 |
| Daisy | `Daisy` | 11130 |
| Hibiscus | `Hibiscus` | 11103 |
| Honey Flower | `HoneyFlower` | 11101 |
| Lavender | `Lavender` | 11102 |
| Lily | `Lily` | 11104 |
| Lotus | `Lotus` | 11110 |
| Orchid | `Orchid` | 11105 |
| Red Rose | `RedRose` | 11107 |
| Sunflower | `Sunflower` | 11106 |
| Tulip | `Tulip` | 11109 |

### Foraging Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Apple | `Apple` | 3044 |
| Berry | `Berry` | 16500 |
| Blueberry | `Blueberry` | 3046 |
| Log | `Log` | 2002 |
| Mushroom | `Mushroom` | 3001 |
| Orange | `Orange` | 3045 |
| Peach | `Peach` | 3048 |
| Raspberry | `Raspberry` | 3049 |
| Sand Dollar | `SandDollar` | 2102 |
| Seaweed | `Seaweed` | 3002 |
| Starfish | `Starfish` | 2103 |
| Strawberry | `Strawberry` | 3047 |

### Gem Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Amethyst | `Amethyst` | 1002 |
| Black Diamond | `BlackDiamond` | 1005 |
| Diamond | `Diamond` | 1003 |
| Dizzite | `Dizzite` | 10860 |
| Havenite | `Havenite` | 1004 |
| Ruby | `Ruby` | 1001 |
| Sapphire | `Sapphire` | 1000 |

### Golden Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Golden Apple | `GoldenApple` | 3054 |
| Golden Blueberry | `GoldenBlueberry` | 3056 |
| Golden Egg | `GoldenEgg` | 3052 |
| Golden Feather | `GoldenFeather` | 2115 |
| Golden Log | `GoldenLog` | 2114 |
| Golden Milk | `GoldenMilk` | 2920 |
| Golden Orange | `GoldenOrange` | 3055 |
| Golden Peach | `GoldenPeach` | 3058 |
| Golden Pomegranate | `GoldenPomegranate` | 3053 |
| Golden Raspberry | `GoldenRaspberry` | 3059 |
| Golden Silk | `GoldenSilk` | 2116 |
| Golden Strawberry | `GoldenStrawberry` | 3057 |
| Golden Wool | `GoldenWool` | 2113 |

### Mana Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Mana Drop | `ManaDrop` | 60234 |

### Money Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Coins | `Coins` | 60000 |
| Mana Orbs | `ManaOrbs` | 60001 |
| Tickets | `Tickets` | 60002 |

### Nelvari Farming Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Acorn | `Acorn` | 11031 |
| Cat Tail | `CatTail` | 11032 |
| Dragon Fruit | `DragonFruit` | 11027 |
| Fire Fruit | `FireFruit` | 11024 |
| Indiglow | `Indiglow` | 11030 |
| Mana Gem | `ManaGem` | 11033 |
| Rock Fruit | `RockFruit` | 11025 |
| Shiiwalki Mushroom | `ShiiwalkiMushroom` | 11029 |
| Walk Choy | `WalkChoy` | 11028 |
| Water Fruit | `WaterFruit` | 11023 |
| Wind Chime | `WindChime` | 11026 |

### Nelvari Mines Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Mana Shard | `ManaShard` | 18015 |
| Sharp Dragon Scale | `SharpDragonScale` | 1116 |
| Sparkling Dragon Scale | `SparklingDragonScale` | 1115 |
| Tough Dragon Scale | `ToughDragonScale` | 1114 |

### Nelvari Temple Books Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Origins of Dynus and Shadows, Book I | `OriginsofDynusandShadowsBookI` | 6510 |
| Origins of Dynus and Shadows, Book II | `OriginsofDynusandShadowsBookII` | 6511 |
| Origins of Dynus and Shadows, Book III | `OriginsofDynusandShadowsBookIII` | 6512 |
| Origins of Dynus and Shadows, Book IV | `OriginsofDynusandShadowsBookIV` | 6513 |
| Origins of Dynus and Shadows, Book V | `OriginsofDynusandShadowsBookV` | 6514 |
| Origins of Sun Haven and Elios, Book I | `OriginsofSunHavenandEliosBookI` | 6505 |
| Origins of Sun Haven and Elios, Book II | `OriginsofSunHavenandEliosBookII` | 6506 |
| Origins of Sun Haven and Elios, Book III | `OriginsofSunHavenandEliosBookIII` | 6507 |
| Origins of Sun Haven and Elios, Book IV | `OriginsofSunHavenandEliosBookIV` | 6508 |
| Origins of Sun Haven and Elios, Book V | `OriginsofSunHavenandEliosBookV` | 6509 |
| Origins of the Grand Tree and Nivara, Book I | `OriginsoftheGrandTreeandNivaraBookI` | 6500 |
| Origins of the Grand Tree and Nivara, Book II | `OriginsoftheGrandTreeandNivaraBookII` | 6501 |
| Origins of the Grand Tree and Nivara, Book III | `OriginsoftheGrandTreeandNivaraBookIII` | 6502 |
| Origins of the Grand Tree and Nivara, Book IV | `OriginsoftheGrandTreeandNivaraBookIV` | 6503 |
| Origins of the Grand Tree and Nivara, Book V | `OriginsoftheGrandTreeandNivaraBookV` | 6504 |

### Spring Crops Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Carrot | `Carrot` | 11006 |
| Cinnaberry | `Cinnaberry` | 11012 |
| Corn | `Corn` | 11001 |
| Grapes | `Grapes` | 11022 |
| Greenroot | `Greenroot` | 11010 |
| Kale | `Kale` | 11050 |
| Lettuce | `Lettuce` | 11013 |
| Onion | `Onion` | 11009 |
| Pepper | `Pepper` | 11008 |
| Potato | `Potato` | 11002 |
| Shimmeroot | `Shimmeroot` | 11007 |
| Tomato | `Tomato` | 11003 |
| Wheat | `Wheat` | 11000 |

### Summer Crops Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Armoranth | `Armoranth` | 11053 |
| Beet | `Beet` | 12080 |
| Chocoberry | `Chocoberry` | 11054 |
| Durian | `Durian` | 11062 |
| Guava Berry | `GuavaBerry` | 11035 |
| Lemon | `Lemon` | 11052 |
| Melon | `Melon` | 11057 |
| Pepper | `Pepper` | 11008 |
| Pineapple | `Pineapple` | 11056 |
| Stormelon | `Stormelon` | 11051 |

### Winter Crops Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Balloon Fruit | `BalloonFruit` | 11063 |
| Blizzard Berry | `BlizzardBerry` | 11068 |
| Blue Moon Fruit | `BlueMoonFruit` | 11064 |
| Brr-Nana | `BrrNana` | 12082 |
| Candy Cane | `CandyCane` | 11077 |
| Heat Fruit | `HeatFruit` | 11041 |
| Hexagon Berry | `HexagonBerry` | 11065 |
| Marshmallow Bean | `MarshmallowBean` | 11042 |
| Purple Eggplant | `PurpleEggplant` | 12081 |
| Pythagorean Berry | `PythagoreanBerry` | 11069 |
| Snow Ball Crop | `SnowBallCrop` | 11067 |
| Snow Pea | `SnowPea` | 11078 |
| Star Fruit | `StarFruit` | 11066 |
| Tea Leaves | `TeaLeaves` | 11048 |
| Turnip | `Turnip` | 11040 |

### Withergate Farming Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Demon Orb | `DemonOrb` | 11004 |
| Eggplant | `Eggplant` | 11015 |
| Kraken Kale | `KrakenKale` | 11016 |
| Moonplant | `Moonplant` | 11017 |
| Razorstalk | `Razorstalk` | 11020 |
| Snappy Plant | `SnappyPlant` | 11005 |
| Suckerstem | `Suckerstem` | 11018 |
| Tombmelon | `Tombmelon` | 11019 |

### Withergate Mines Bundle

| Item name | Game key | ID |
| --- | --- | ---: |
| Candy Corn Pieces | `CandyCornPieces` | 18016 |
| Hard Butterscotch Gem | `HardButterscotchGem` | 3760 |
| Jawbreaker Gem | `JawbreakerGem` | 3761 |
| Rock Candy Gem | `RockCandyGem` | 3759 |
