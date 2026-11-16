# Archive Old Dev Logs

The early development history of **Shima QoL**, from its tooltip prototypes through **v0.0.144** and the move to public GitHub releases.

This is a retrospective, version-by-version account assembled from the retained development notes. Many versions were internal development builds rather than public releases. Entries describe changes at that point in time: experiments were sometimes replaced, and an earlier fix does not mean every related issue was resolved permanently.

For current features, see the [README](README.md). For downloads and current release notes, visit [Releases](https://github.com/Shimaryu4k/Shima-QoL/releases).

## Contents

- [Prototype history and the version reset](#prototype-history)
- [0.0.1-0.0.19: tooltips, settings, and inventory](#versions-1-19-tooltips-settings-and-inventory)
- [0.0.20-0.0.39: farming tools and automation](#versions-20-39-farming-tools-and-automation)
- [0.0.40-0.0.59: storage, shared beds, and properties](#versions-40-59-storage-shared-beds-and-properties)
- [0.0.60-0.0.79: player interactions and shared events](#versions-60-79-player-interactions-and-shared-events)
- [0.0.80-0.0.99: sitting, couches, and spouse sleep](#versions-80-99-sitting-couches-and-spouse-sleep)
- [0.0.100-0.0.119: spouse movement and home activities](#versions-100-119-spouse-movement-and-home-activities)
- [0.0.120-0.0.144: polish, storage movement, and releases](#versions-120-144-polish-storage-movement-and-releases)

## Prototype history

### About 0.0.0

The retained notes do **not** document a release numbered **0.0.0**. The current version sequence starts at **0.0.1**. Earlier tooltip work used the separate legacy numbers below; those numbers have been preserved rather than reassigned to imaginary 0.0.x releases.

### Legacy 0.2.0 — Grok Haven and broader tooltips

- Adopted the working name **Grok Haven** for the early tooltip project.
- Expanded beyond crops to broader world-object information while retaining existing configuration compatibility.

### Legacy 0.2.1 — Tree and mining names

- Corrected cases where trees displayed seed/item labels and mining objects showed internal node names.
- Improved recognizable world names while preserving meaningful object labels.

### Legacy 0.2.2 — Reducing recurring stutters

- Investigated a noticeable one-second stutter during gameplay.
- Replaced repeated global object searches with more limited discovery work and reuse of existing information.

### Legacy 0.3.0 — Fruit counts and world coverage

- Added fruit-tree stock counts, including compatibility with the fruit-storage-cap mod used during development.
- Expanded world-artwork coverage and refined how nearby objects and scenery were identified.

### Legacy 0.4.0 — Settings and category controls

- Added a draggable settings panel with collapsible sections, configurable hotkeys, and category switches.
- Introduced Save settings and Revert controls for preferences.

### Legacy 0.4.1 — Consistent building identities

- Improved building names across exterior artwork, attached details, and entrances.
- Added more consistent residential names, including Pod's and Lynn's homes.

### Legacy 0.4.2 — Reference UI and Environment category

- Refined the settings appearance using the supplied visual reference.
- Added a separate Environment category for scenery that should not clutter ordinary object tooltips.

### Legacy 0.4.3 — Scenery filtering and barrels

- Broadened scenery filtering to recognize map layers, decals, and naming variations.
- Improved the separation of decorative scenery from interactive/destructible objects such as barrels.

### Legacy 0.4.4 — Town House and capitalization

- Corrected a town building's displayed identity to **Town House**.
- Refined capitalization and naming for plant-related objects.

### Legacy 0.4.5 — Terrain, chest keys, and the smithery

- Expanded terrain/scenery recognition, including cliffs, quarry artwork, light rays, and tile layers.
- Improved Solon's Smithery naming and treasure-chest key information.

## Versions 1-19: tooltips, settings, and inventory

### 0.0.1 — First Early Access version

- Started the new **0.0.x Early Access** sequence while retaining existing settings.
- Improved numbered terrain names, cart-part labels, Sun Haven Mines naming, and Bulletin Board recognition.

### 0.0.2 — Object categories and town assets

- Separated **Interactable Objects** from **Decorative Objects**.
- Migrated existing category preferences and kept optional scenery categories from appearing unexpectedly.

### 0.0.3 — Interior flooring recognition

- Improved tooltip recognition of actual indoor flooring surfaces.
- Distinguished flooring from similarly named shop/display objects.

### 0.0.4 — Interior category

- Added a dedicated **Interior** category for indoor walls, floors, and furniture.
- Kept interior information separately configurable from outdoor/world categories.

### 0.0.5 — Tooltip background fade

- Added a darker tooltip background with a fading edge, based on the supplied in-game visual reference.
- Improved the separation of tooltip text from the world behind it.

### 0.0.6 — Rounded tooltips and Grass naming

- Added rounded corners and an angled fade to the tooltip background.
- Improved generic grass/scenery naming.

### 0.0.7 — Nested settings and crop choices

- Organized settings into expandable Hotkeys, General, Interior, and crop sections.
- Added individual crop switches while keeping the main menu compact when sections were collapsed.

### 0.0.8 — Dear ImGui settings

- Rebuilt the settings window around Dear ImGui, with a dedicated renderer for Sun Haven.
- Retained the mod's controls and preferences within the new settings interface.

### 0.0.9 — Single-DLL installation

- Embedded the native settings dependency and its license notices into the mod DLL.
- Simplified installation and retained default-off behavior for optional scenery information.

### 0.0.10 — Shima QoL and merged Quick Actions

- Adopted the official name **Shima QoL** and combined the tooltip mod with Quick Actions.
- Brought both features into one settings window with shared configuration and Save/Revert controls.

### 0.0.11 — Custom chest-name tooltips

- Displayed storage chests' player-assigned names instead of only generic item names.
- Reflected renaming changes without requiring a scene reload.

### 0.0.12 — Mount shortcut

- Added a configurable Mount quick action.
- Allowed a tap to cycle through distinct carried mount whistles, with no repeated cycling while the key was held.

### 0.0.13 — Configuration and accessible startup

- Added a Configuration section, Show on startup, transparency, and font scaling.
- Opened settings at startup by default so players could rebind the menu without relying on an Insert key.

### 0.0.14 — Bee Box identity

- Corrected Bee Boxes being identified as Geode Munchers.
- Placed Bee Box information under Interactable Objects.

### 0.0.15 — Stack Splitter

- Added percentage-based inventory splitting with **Alt + right-click**.
- Introduced a configurable percentage and convenient presets.

### 0.0.16 — Fixed-amount splitting

- Added a **Fixed items** mode alongside percentage splitting.
- Remembered each mode's amount and handled stacks smaller than the requested fixed quantity.

### 0.0.17 — Repeated split clicks

- Fixed subsequent split clicks falling back to the game's one-item transfer.
- Allowed repeated configured transfers to accumulate on a compatible cursor stack, respecting its capacity.

### 0.0.18 — Hold-to-repeat splitting

- Added repeated splitting while **Alt + right mouse** stayed held.
- Used an initial delay followed by accelerating repeats while retaining ordinary single-click use.

### 0.0.19 — Splitting in paused inventory

- Fixed held splitting stopping after its first transfer when the single-player inventory paused the world.
- Retained input, focus, capacity, and inventory-window restrictions.

## Versions 20-39: farming tools and automation

### 0.0.20 — Hovered plot borders

- Added an optional native-style border around hovered crops and prepared plots.
- Kept the added border available after watering, independently of the ordinary tool-selection indicator.

### 0.0.21 — Separate markers and border controls

- Separated the mouse-hover marker from the equipped tool's nearby target marker.
- Added independent border colors and corrected settings/input behavior associated with the new controls.

### 0.0.22 — In-game border colors

- Corrected the rendering behavior that prevented chosen border colors from appearing in-game.
- Preserved the separate hovered-plot and tool-target markers.

### 0.0.23 — Move toward the mouse

- Added optional movement toward the cursor while using supported tools and attacks.
- Provided individual action choices for mining, chopping, hoeing, watering, scything, and attacking.

### 0.0.24 — Secondary-action movement

- Extended mouse-directed movement to supported native secondary actions.
- Addressed cases such as removing farming plots with the hoe's alternate action.

### 0.0.25 — Straighter farming targets

- Reduced sideways target jumps when hoeing or watering along an aimed row or column.
- Kept tool targets within normal reach and allowed deliberate changes of direction.

### 0.0.26 — Plot Planner

- Added custom farm outlines using multiple points, including L-shaped layouts.
- Displayed tile counts with configurable planning shortcuts and independent border appearance.

### 0.0.27 — Clearer planning previews

- Reduced overlap between neighboring plan markers.
- Added point accents and separate transparency for previews and confirmed plans.

### 0.0.28 — Confirm the latest planning point

- Allowed another press on the most recent point to finish a plan.
- Removed the need to return to the starting point when confirming supported open/custom layouts.

### 0.0.29 — Splitting across inventory windows

- Extended Stack Splitter beyond the character inventory to chests and supported crafting/item windows.
- Retained ordinary item ownership, stack limits, and cursor behavior.

### 0.0.30 — Totem and scarecrow ranges

- Added an optional range display when hovering over placed totems and scarecrows.
- Based the display on the object's native placement/effect range.

### 0.0.31 — Totem effect descriptions

- Added the game's localized effect descriptions to supported totem/scarecrow tooltips.
- Paired effect information with the existing optional range display.

### 0.0.32 — Automation Chest

- Introduced links between supported crafting/cooking stations and storage such as chests, wardrobes, and fridges.
- Added an initial multiplayer-aware collection workflow; subsequent versions addressed startup, transfer, and recovery issues.

### 0.0.33 — Automation startup and feedback

- Fixed automation initialization problems affecting the first implementation.
- Added native notifications for station/storage linking feedback.

### 0.0.34 — Current storage contents and retries

- Corrected transfers using stale storage information instead of current contents.
- Added retryable waits for storage that was busy, full, or otherwise temporarily unavailable.

### 0.0.35 — Furnace-transfer freeze correction

- Changed automatic collection to respect the game's normal pauses between completed entries.
- Addressed the reported furnace-to-storage hang caused by processing collection too aggressively in one frame.

### 0.0.36 — Station-first linking

- Changed setup to select a station first and its storage second.
- Added a settings list of saved links with individual unlink controls and clearer setup instructions.

### 0.0.37 — Outline Hover

- Added an opt-in accessibility outline for supported hovered interactables.
- Used native-style outlines for objects such as stations and chests, independently of tooltip-category visibility.

### 0.0.38 — Storage icons and reverse links

- Used the destination chest's color/icon in automation feedback.
- Added connection information when hovering over linked storage, as well as linked stations.

### 0.0.39 — Accumulating transfer notices

- Added pickup-style notifications after successful automatic delivery.
- Accumulated repeated deliveries to the same destination rather than creating a separate notice each time.

## Versions 40-59: storage, shared beds, and properties

### 0.0.40 — Auto/Manual modes and recovery

- Added shared station **Auto / Manual** controls and filtering for placeable outputs.
- Introduced recovery handling for an earlier collection problem involving escaped floor pickups.

### 0.0.41 — Mixed crafting-output corrections

- Fixed problems when a station contained a mixture of ordinary items and placeable outputs.
- Improved output filtering and isolated unsupported cases so they did not stop unrelated automation work.

### 0.0.42 — Background transfers and personal notices

- Extended supported delivery while the link owner was elsewhere, subject to online/availability requirements.
- Added optional transfer notices attributed to the player who queued the crafting work.

### 0.0.43 — Shared beds

- Added the Miscellaneous settings category and shared sleeping in compatible wide beds.
- Assigned separate pillow positions to participating players.

### 0.0.44 — Anytime AFK rest

- Added resting at a bed during the day without immediately skipping the day.
- Kept ordinary sleeping separate from the new AFK-rest action.

### 0.0.45 — Co-op automation permissions

- Fixed a joining-player readiness problem that blocked storage linking.
- Added host-controlled **Everyone / Host Only** link permissions and clearer permission feedback.

### 0.0.46 — Goodnight visual prototype

- Introduced an actual-player Goodnight/kiss prototype with explicit partner and role selection.
- This was an exploratory visual step; later versions replaced its room-level presentation with bed-based interactions.

### 0.0.47 — Goodnight at the player's bed

- Moved the interaction to the player's own compatible double bed and followed the native-style bedtime sequence more closely.
- Improved shared-bed visibility during the overnight transition.

### 0.0.48 — Saved partnerships, Goodnight, and Cuddle

- Added accepted player partnerships and saved role choices in the then-named **Shima Life** settings page.
- Connected Goodnight to actual sleeping and added a separate requested Cuddle interaction.

### 0.0.49 — Native Partners interface

- Refined the renamed **Partners** page using the game's normal dropdowns, rows, and separators.
- Improved control sizing and added the native Relationships icon.

### 0.0.50 — Consistent settings and saving

- Matched custom field labels more closely to the game's settings.
- Synchronized bed options between settings screens and added an explicit Save settings action inside Partners.

### 0.0.51 — Joining-player automation areas

- Corrected area information used when a guest linked a station to storage.
- Improved Host Only feedback and removed redundant prototype controls from the settings.

### 0.0.52 — AFK rest through co-op nights

- Allowed AFK-resting players to participate when the rest of the group went to sleep.
- Kept those players resting the following morning while preserving separate homes and private couple scenes.

### 0.0.53 — Property ownership and privacy

- Added a host-enabled Privacy and Ownership Mode for supported houses and sheds.
- Introduced claiming, property names, visitor access, knocking, and a native Properties settings tab.

### 0.0.54 — Restored settings tabs

- Fixed Partners and Properties not appearing in the game's settings.
- Retained the native settings-tab design rather than moving the features into a separate inventory page.

### 0.0.55 — Usable property renaming

- Added a clearer Rename action and corrected the text-entry field.
- Prevented gameplay/mod shortcuts from interfering while entering a property name.

### 0.0.56 — Accurate button hit areas

- Corrected custom buttons reacting to the cursor above or below their visible artwork.
- Improved click and hover boundaries in Partners and Properties.

### 0.0.57 — Property names in tooltips

- Displayed custom property names and ownership information when hovering over supported buildings.
- Used **Claim Property** consistently for both houses and sheds.

### 0.0.58 — Properties house icon

- Added the game's native house icon to the Properties tab.
- Kept the tab's appearance consistent with neighboring native settings tabs.

### 0.0.59 — Birthday invitation prototype

- Added a Join / Decline invitation prototype for attending another player's birthday event.
- Established shared-event observation that was expanded in later versions.

## Versions 60-79: player interactions and shared events

### 0.0.60 — Shared birthday events and host controls

- Added host-controlled event options and synchronized birthday dialogue/cinematics.
- Kept response choices with the celebrant while attending players observed the shared event.

### 0.0.61 — Player interaction and gifting

- Added nearby player interaction, gifting, and partner selection as a foundation for further social features.
- Used ordinary in-game item transfers while handling inventory limits and delivery outcomes.

### 0.0.62 — Player Interaction master switch

- Added **Allow Player Interaction** above the individual social-feature options.
- Made disabling the master switch stop new interaction prompts and related actions.

### 0.0.63 — Player proposals and gift experience

- Added accepted player proposals using an Engagement Ring and partner consent.
- Improved gift experience handling for the player giving the gift.

### 0.0.64 — Player weddings and guests

- Added a next-day player-wedding flow involving Bernard and the actual player characters.
- Extended Online Events Sync to let invited players attend the ceremony.

### 0.0.65 — Composter, gifts, and repeat weddings

- Improved Composter output collection and gift HUD/experience behavior.
- Allowed repeat player weddings through the normal proposal/setup flow with another ring.

### 0.0.66 — Retaining the selected station

- Preserved an in-progress station selection through temporary native input/menu restrictions.
- Addressed linking interruptions reported while setting up Composter automation.

### 0.0.67 — Midnight rest and spouse homes

- Improved forced-midnight handling for AFK-resting co-op players.
- Added owner-selected Tier 3 homes for native NPC spouses while property ownership/privacy was enabled.

### 0.0.68 — Spouse housing availability

- Fixed a native-method lookup problem that made spouse housing unavailable.
- Improved single-player housing status and removed stale native tooltip information from the custom UI.

### 0.0.69 — Knocks, Bernard, and wedding setup

- Queued property-knock offers behind active inventory/modal screens.
- Corrected Bernard's native ceremony location and refined repeat player ceremonies and wedding-task handling.

### 0.0.70 — NPC wedding ceremonies and outlines

- Added supported repeat ceremonies with the player's actual NPC spouse and shared audience invitations.
- Introduced full-character hover outlines, which received further visual corrections in following versions.

### 0.0.71 — One character silhouette

- Combined clothing/body parts into a single outer character outline.
- Removed internal clothing seams from the outline presentation.

### 0.0.72 — Initial wedding invitations and audience positions

- Added invitations to the initial ceremony flow as well as repeat ceremonies.
- Improved guest standing positions and kept ceremony vows tied to the correct spouse.

### 0.0.73 — Upright outlines and smoother ceremonies

- Corrected inverted character outlines and reduced unnecessary work during wedding scenes.
- Refined couple spacing and synchronized Cuddle kiss movement.

### 0.0.74 — Wedding kiss presentation

- Gave the kiss more time on screen and restored a neutral pose afterward.
- Centered the heart effect and slowed the close-up camera framing.

### 0.0.75 — Wedding exit confirmation

- Added native-style, role-appropriate confirmation when leaving a wedding scene with Escape.
- Suppressed unrelated hover names and tooltips during the ceremony.

### 0.0.76 — Larger crafting-queue metadata

- Corrected ordinary crafting queues being rejected as containing too much item metadata.
- Improved bounded transfers for stations such as the Baker's Station linked to a fridge.

### 0.0.77 — Draining finished backlogs

- Allowed larger completed crafting backlogs to drain through repeated small collection runs.
- Preserved unfinished recipes and filtered items instead of requiring the whole queue to be collected manually.

### 0.0.78 — More flexible settings overlay

- Made the mod window less restrictive to ordinary gameplay clicks.
- Expanded manual menu access and remembered the settings window's position.

### 0.0.79 — Birthday invitation parity

- Applied the newer invitation checks and reliability work to birthday events.
- Reduced repeated work during shared-event playback.

## Versions 80-99: sitting, couches, and spouse sleep

### 0.0.80 — Allow Sitting prototype

- Added an opt-in sitting prototype for supported chairs and benches, including public locations.
- Kept the player's own appearance and provided native-style Sit / Stand up interaction.

### 0.0.81 — Missing furniture profiles

- Added or corrected profiles for previously unrecognized chairs and a wide public bench.
- Expanded the furniture review against available item/reference information.

### 0.0.82 — Clearer sitting prompts and shared benches

- Improved furniture identity and Sit-prompt behavior around supported chairs.
- Added quieter prompts and four shared positions on the supported public bench.

### 0.0.83 — Direct placed-chair detection

- Fixed compatible placed chairs being missed by the existing world-object discovery.
- Restored sitting prompts for cases such as Basic Wooden and Green Wrought Iron chairs.

### 0.0.84 — Broader chair coverage

- Expanded the supported chair catalog using native furniture information.
- Kept discovery work limited while adding more seating targets.

### 0.0.85 — Side-facing chair pilot

- Added left/right sitting support for Basic Wooden, Green Wrought Iron, and Beach chairs.
- Tuned individual seat positions while retaining the player's appearance.

### 0.0.86 — North-facing chair pilot

- Added north-facing sitting for the three pilot chair types.
- Used direction-specific seating positions and furniture artwork.

### 0.0.87 — Basic Wooden Chair alignment

- Corrected the north-facing Basic Wooden Chair pose, which appeared too low in the furniture.
- Preserved the other pilot chair profiles.

### 0.0.88 — Eating and fishing while seated

- Enabled ordinary food use and fishing while sitting on supported furniture.
- Retained normal movement restrictions for the seated pose.

### 0.0.89 — More chair directions

- Expanded left/right/north support across compatible chairs.
- Preserved the player's clothing and appearance while adapting to the supported native furniture directions.

### 0.0.90 — Espresso Cushioned Couch pilot

- Added sitting on compatible rotations of the Espresso Cushioned Couch.
- Used that couch as a pilot for broader multi-seat furniture support.

### 0.0.91 — Couch catalog and capacities

- Expanded seating across the couch/armchair catalog with furniture-specific capacities.
- Added four positions to the Espresso couch and assigned suitable one-, two-, three-, or four-seat layouts elsewhere.

### 0.0.92 — Side-couch visibility

- Corrected side-facing couch cushions hiding too much of the seated player's body.
- Retained furniture depth while improving the visible seated pose.

### 0.0.93 — Seated Quick Action fishing

- Allowed the Quick Actions fishing shortcut to work while seated.
- Kept ordinary seated fishing and existing couch visibility behavior.

### 0.0.94 — Beach Hammock and sleep options

- Added supported Beach Hammock sitting with the player's own appearance.
- Refined Sleep Options for compatible beds, keeping ordinary sleeping and AFK rest distinct.

### 0.0.95 — NPC spouse sleep and bed coverage

- Added native-spouse sleep interactions at a supported chosen double bed and refined which partner actions were shown.
- Expanded the bed catalog and corrected Animal Food acceptance in supported fridge automation.

### 0.0.96 — Unsupported cases and quiet rest

- Added safer unsupported-case feedback and improved automation behavior around unavailable/unsupported output entries.
- Reduced persistent AFK-rest prompts and formalized tracking of reported issues.

### 0.0.97 — Native spouse spacing

- Adjusted the NPC-spouse cutscene positions to match the native couple's spacing more closely.
- Addressed the reported gap between the player and spouse during the bedtime scene.

### 0.0.98 — Spouse overnight presence

- Preserved spouse presence through the bedtime scene and into the morning.
- Introduced the following return-home behavior, which was refined by later movement updates.

### 0.0.99 — Bedside conversation and return attempts

- Improved bedside conversation and delayed departure while the player remained nearby.
- Introduced collision-aware return attempts; live pathfinding problems led to the next series of navigation updates.

## Versions 100-119: spouse movement and home activities

### 0.0.100 — Native walking prototype

- Reworked the spouse-return prototype to use native walking and animation behavior.
- Further testing exposed furnished-house route problems, so this was a foundation rather than a finished navigation fix.

### 0.0.101 — Spouse-return diagnostics

- Added a temporary route/obstacle view to investigate blocked spouse returns.
- Provided controls to show/hide the view and capture a diagnostic report.

### 0.0.102 — Correct NPC movement footprint

- Corrected obstacle checks using an unsuitable NPC collision footprint.
- Reduced false route rejection around furniture and narrow spaces.

### 0.0.103 — Doorway turns and upstairs coverage

- Improved turning around blocked diagonal segments near doorways.
- Expanded route-map coverage for upstairs destinations; subsequent testing confirmed the reported upstairs return in the tested house.

### 0.0.104 — Conversation during the return

- Allowed the player to accompany and talk to the returning spouse, then resume the journey.
- Reduced player-body interference and made diagnostic collection more automatic, with the overlay hidden by default.

### 0.0.105 — Tomorrow's spouse plan

- Added **Spend time off / Work tomorrow** choices alongside ordinary native conversation.
- Applied choices the next morning and retained them until changed, using the assigned spouse home.

### 0.0.106 — Arrival rendering

- Addressed a pale rectangular frame appearing when the spouse arrived.
- Improved the handoff between the ordinary NPC artwork and the mod's home presentation.

### 0.0.107 — Recovering from repeated obstructions

- Refined corner recovery and retry behavior during spouse returns.
- Kept genuinely blocked routes waiting rather than treating every obstruction as a completed journey.

### 0.0.108 — Movement checks and clearer timing reports

- Added a guard around actual physics movement during route following.
- Separated route work from diagnostic/reporting work to investigate pauses more accurately.

### 0.0.109 — House exit and re-entry continuity

- Preserved the active spouse-return journey when the initiating player left and re-entered the house.
- Refined stair/corner recovery; the recorded live confirmation applied to the tested route, not every possible house layout.

### 0.0.110 — Smoother house transitions

- Improved spouse visibility during fade/unload/load transitions.
- Retained journey progress and remaining route information across re-entry rather than restarting the route unnecessarily.

### 0.0.111 — NPC Settings and shared returns

- Added the main **NPC Settings** category and a shared spouse-return foundation designed for up to eight players.
- Coordinated journey control, waiting, arrivals, and reconnects so observers did not run independent competing routes.

### 0.0.112 — Additional Lynn dialogue

- Integrated additional Lynn morning and bedtime conversations alongside native dialogue, including time-off-aware selection.
- Added visitor conversation about the married player and retained native-style gift opportunity/frequency handling.

### 0.0.113 — Lynn indoor activity prototype

- Added short indoor walks, pauses, and looking around during an active day off.
- Preserved normal conversation/resume behavior and shared activity observation.

### 0.0.114 — Whole-house indoor activity

- Expanded Lynn's activity coverage across the assigned house, including upstairs.
- Refined activity timing, departures, and movement between destinations.

### 0.0.115 — Arrival jitter correction

- Corrected the small forward/backward movement reported when an indoor walk reached its destination.
- Improved the transition between the completed walk and the stable idle pose.

### 0.0.116 — Independent spouse activity

- Addressed the player's own sitting or UI state unnecessarily stopping the spouse's indoor routine.
- Restored native overhead notifications during walking and interaction.

### 0.0.117 — Lynn furniture company

- Added shared use of supported couches/chairs and AFK-bed company for Lynn.
- Adjusted the walking/presentation handoff while investigating the reported doorway flash; later versions continued the follow-up work.

### 0.0.118 — Recovery after overnight events

- Retained the chosen bedside intent through overnight or morning events that temporarily moved the spouse elsewhere.
- Improved recovery once normal scene control and the original house became available again.

### 0.0.119 — Couch company and rest stages

- Fixed solo couch use not attracting Lynn's company and added clearer settling/resting/waking stages.
- Refined far-left upstairs route coverage and companion departure behavior.

## Versions 120-144: polish, storage movement, and releases

### 0.0.120 — Quiet seated interaction

- Reduced persistent labels after the player had settled into a seat.
- Gave the nearby companion's conversation prompt priority over the competing Stand up prompt.

### 0.0.121 — On-demand performance capture

- Added a short, manually triggered performance capture to investigate outdoor slowdowns.
- Kept it off by default and stopped recording automatically rather than leaving continuous logging active.

### 0.0.122 — Performance capture startup

- Fixed the new capture feature failing before it could begin.
- Corrected the shortcut-conflict handling involved in startup.

### 0.0.123 — Targeted outdoor optimization

- Reduced repeated naming/discovery work and passive automation-hover work.
- The user's captured outdoor session showed an improvement; this was not a promise of a fixed frame rate across all worlds or PCs.

### 0.0.124 — Seasonal sitting experiment

- Attempted to match seated Lynn's appearance to seasonal outfits.
- Later feedback exposed unwanted pose distortion; this approach was replaced by the native-sitting restoration in 0.0.125.

### 0.0.125 — Native sitting restored

- Held and then discarded the unsuitable seasonal-pose/deformation approach, restoring supported native Lynn sitting.
- Parked custom seasonal artwork as reviewed references rather than integrating it into gameplay.
- Retained separate gift-interaction, visible-outline, and bedside-approach improvements prepared during this iteration.

### 0.0.126 — More married-NPC indoor routines

- Expanded day-off indoor walking, pausing, and looking around to all 25 supported married NPCs.
- Kept sitting/resting support dependent on each NPC's available native animations rather than assuming every activity worked for every spouse.

### 0.0.127 — Simpler NPC settings

- Shortened main settings descriptions and moved additional setup details into expandable sections.
- Added a host-controlled **Enable NPC Settings** master switch while retaining saved plans when disabled.

### 0.0.128 — Menu memory and version notice

- Remembered the settings window's open/closed state and position between launches.
- Added a persistent co-op version notice and reorganized shared-event controls under Player Interaction.

### 0.0.129 — Storage pickup with contents

- Added supported storage pickup and placement while retaining contained item data.
- Established the save/reload and co-op handling that subsequent storage-movement versions refined.

### 0.0.130 — Current-inventory pickup correction

- Addressed storage pickup being blocked by a stale comparison with saved contents.
- Used the currently loaded inventory for validation while retaining item-integrity checks.

### 0.0.131 — More responsive storage rearrangement

- Introduced right-click storage rearrangement and corrected delayed hotbar/placement-preview updates.
- The interaction was refined into the direct in-world movement flow in 0.0.132.

### 0.0.132 — Direct in-world storage movement

- Made right-click move supported storage within the current area without requiring a hotbar item or free inventory slot.
- Added confirmation/cancellation behavior while preserving the storage contents.

### 0.0.133 — Chest preview and movement distance

- Corrected missing storage-preview artwork and retained the appropriate chest appearance.
- Removed the distance restriction for valid in-world moves within the same area.

### 0.0.134 — Ending a player partnership

- Added **End partnership**, with confirmation, in the native Partners tab.
- Retained the ending for later reconciliation with an offline former partner; native NPC marriage remained a separate system.

### 0.0.135 — Dismissible version notice

- Added a close action for the top version notice, hiding it for the current connection until reconnecting.
- Corrected totem/scarecrow hover-range behavior while preserving native effects.

### 0.0.136 — Styled version card

- Applied the approved brown-and-gold notice design with an information badge and **Got it** button.
- Added a reconnect hint and layouts suitable for narrower windows and larger player rosters.

### 0.0.137 — Hardware Store search

- Added an optional name filter for the Hardware Store's Customization Shop catalog.
- Later follow-up versions corrected the search bar's attachment and text visibility.

### 0.0.138 — Search bar attachment

- Fixed the enabled Hardware Store search bar not appearing in the opened shop.
- Attached the controls to the shop's active interface after it moved into the main UI.

### 0.0.139 — Search captions and input text

- Corrected blank placeholder, Clear, and result-count captions in the shop search bar.
- Refined font/text bounds while keeping ordinary buying behavior intact.

### 0.0.140 — Map fast travel

- Added optional travel from supported map destinations for **500 gold per trip**.
- Used the normal wallet and retained native region/story restrictions; the option started disabled.

### 0.0.141 — Travel layout and repair requirements

- Improved map-button layout and required completed repairs before travel to the affected shops.
- Gave Storage Movement, Sitting, Shared Beds, and AFK Bed Rest their own collapsible settings sections.

### 0.0.142 — Fertilizer in crop tooltips

- Added the active fertilizer name beneath crop growth information.
- Kept unfertilized crops' display unchanged and used available native/localized item names.

### 0.0.143 — Sun Haven barn flooring

- Added optional flooring changes for ordinary Sun Haven barns at levels 1-3.
- Stored each barn's choice separately through upgrades and saves, with an option to restore the original floor.
- Kept the original appearance for unmodded viewers; regional barns were outside this feature's scope.

### 0.0.144 — Flooring alignment and release packaging

- Improved repeating barn-floor patterns, including Modern Marble seams and diagonal repeats, while preserving existing floor choices.
- Added the main **Universal** ZIP and a separate **Manual Install** ZIP using the same compiled mod DLL.
- Added the package manifest, 256-pixel package icon, BepInEx dependency declaration, and player-facing package README. Local checks and the Markdown preview passed; Thunderstore's signed-in team validation was still pending in the retained release record.

## Where this archive ends

This archive stops at **v0.0.144**, the first public GitHub Early Access release. Continue with the [GitHub release notes](https://github.com/Shimaryu4k/Shima-QoL/releases) for later published versions.

At that point, reports involving Save & Exit after AFK rest and lingering crop/object grids after watering were still under investigation. New visual and multiplayer changes also required further in-game confirmation. Historical entries should not be read as a claim that those open issues were resolved.

AI tools were used throughout this development journey as part of learning coding and mod development. Ideas, testing, and feedback from players helped guide the iterations.

[Back to the showcase](README.md) · [Join the community](https://discord.gg/hWFdr9ayFB)
