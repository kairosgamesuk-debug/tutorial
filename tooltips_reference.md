# Kairos — Tooltip Reference

Complete list of UI elements that should have tooltips.
Edit the tooltip text below, then implement via `addTooltipHtml()` in Game.js.

## How BGA Tooltips Work

```javascript
// Simple text tooltip
this.addTooltip('elementId', 'Help text here', '');

// Rich HTML tooltip (preferred for Kairos)
this.addTooltipHtml('elementId', '<div><strong>Title</strong><br>Description</div>');

// Apply to all elements with a CSS class (each must have unique id)
this.addTooltipHtmlToClass('css-class', '<div>Help text</div>');

// Remove a tooltip
this.removeTooltip('elementId');
```

Call tooltips in `setup()` after DOM is built. Delay of 500-1000ms prevents flash on quick mouse movement.

---

## AGENT ACTION BUTTONS (Detail Panel)

Action buttons are created dynamically in `showDetailActions()` inside `#detail-panel-actions`.
CSS classes distinguish button types. Tooltips should be applied after each button is created.

| CSS Class | Tooltip Title | Tooltip Text |
|---|---|---|
| `.detail-btn-travel` | **Time Travel** | Enter travel mode. Click a destination tile on the hex grid, then roll Travel Dice to reach it. Costs the agent's turn on success. Cancel anytime before rolling. |
| `.detail-btn-recover` | **Recover / Guard Article** | Roll Recovery Dice to recover a crystal or guard an artifact at this location. Requires matching specialist factors (A, S, C, P, M, H). Costs the agent's turn. |
| `.detail-btn-pickup` | **Pick Up Item** | Pick up an item at this location. Items are free to pick up (no dice roll needed). Carry items back to HQ and restore them for Kairos/Blot/Paradox benefits. Does NOT end the agent's turn. |
| `.detail-btn-recall` | **Recall to HQ** | Recall this agent directly back to their home HQ. Free action (no dice roll), but ends the agent's turn. |
| `.detail-btn-skip` | **Skip Agent** | Skip this agent's action for the round. The agent does nothing and their turn is marked complete. |
| `.detail-btn-forced` | **Bribe Xanadu** | Pay Kairos and gain Blots to bribe your way out of Jail. Forced on the 3rd Jail turn. |
| `.detail-btn-cancel` | **Cancel Travel** | Exit travel mode without selecting a destination. Returns to normal action selection. |

## AGENT SPECIAL ACTIONS

| Context | Tooltip Title | Tooltip Text |
|---|---|---|
| Empower Crystal (`.detail-btn-recover` at HQ) | **Empower Crystal** | Activate an unempowered crystal at HQ. Empowered crystals get +1 bonus to their Crystal Light dice roll each round. TimeLords can also nerf paired Kronos artifacts when empowering. |
| Vortex Switch-Off (`.detail-btn-recover` at VORTEX) | **Attempt Vortex Switch-Off** | TimeLord-only action. Roll 2d6 — need 9 or higher to switch off the Vortex. Primary player receives +8 Kairos and −3 Blots. Other players with TimeLords at the Vortex who contributed to the dice modifier receive an assist bonus of +4 Kairos and −1 Blot each. |
| Rescue from LIT (`.detail-btn-recover` at HQ) | **Rescue Agent** | TimeLord at HQ rescues an allied agent who is Lost in Time. The rescued agent returns to HQ. Costs the TimeLord's turn. |
| Jail Escape Roll (`.detail-btn-recover` at JAIL) | **Attempt Escape — Roll Doubles** | Roll two dice — if they match (doubles), you escape Jail. Costs Kairos. If you fail, you stay locked up another turn. |
| Jail Escape Card (`.detail-btn-pickup` at JAIL) | **Use Escape Card** | Play a Jail Escape or Wild KEEP card to leave Jail immediately without rolling or paying a bribe. |
| Drop Article (`.detail-btn-pickup` at field TL) | **Drop Article** | Drop a carried article at the current location. Free action — does not end the agent's turn. |
| TimeLord Bonus (label) | **TimeLord Bonus Action** | After a TimeLord's main action, they get a bonus action: empower a crystal at HQ, rescue an LIT agent, or attempt recovery at a field location. |

---

## PERSISTENT GAME BUTTONS (Action Panel)

Located in `#game-action-panel` (right column).

| Element ID | Tooltip Title | Tooltip Text |
|---|---|---|
| `btn-debug-toggle` | **Debug Panel** | Toggle the debug panel for testing and development tools. Only visible in debug mode. |
| `btn-anim-toggle` | **Toggle Animations** | Turn board animations on or off. Disabling animations speeds up gameplay, especially during Automa and Kronos turns. |
| `btn-portals` | **Portal Status** | View all active portals, their protection status, and this round's portal rotation changes. Portals add a Blue die to Travel rolls from that location. |
| `btn-articles` | **Article Status** | View all articles in the game: Items, Crystals, and Artifacts. See their locations, holders, recovery requirements, and current status (guarded, restored, empowered, nerfed). |
| `btn-notif-log` | **Game Log** | View the notification log showing all game events: dice rolls, agent moves, article recoveries, Kronos actions, and score changes. |
| `gs-btn-end-turn` | **End Turn** | End your turn. All remaining agents that haven't acted will be skipped. Glows green when all agents have completed their actions. |
| `gs-btn-quit` | **Quit Game** | Leave the game immediately. |

---

## PLAYER RESOURCES (Player Panel)

Inserted into each player's BGA panel via `bga.playerPanels`.

| Element ID Pattern | Tooltip Title | Tooltip Text |
|---|---|---|
| `kairos-counter-{playerId}` | **Kairos** | Temporal energy resource. Earned by restoring Items at HQ, guarding Artifacts, empowering Crystals, and switching off the Vortex. Spent on Jail escapes. Must accumulate as much as possible to win. |
| `blots-counter-{playerId}` | **Blots** | Karma penalties. Gained from negative events, Jail bribes, and Kronos damage. Reduced by restoring certain Items at HQ. Must reach zero Blots to win. |
| `.kairos-display` | **Kairos** | Your current Kairos count. Kairos is the primary scoring resource — earn it through successful missions. |
| `.blots-display` | **Blots** | Your current Blots count. Blots are penalties — you must reduce them to zero to meet the win condition. |

---

## GAME STATE BAR (Top Bar)

Located in `#game-state-bar`.

| Element ID | Tooltip Title | Tooltip Text |
|---|---|---|
| `gs-timeline` | **Main Line Timeline (MLT)** | The health of the timeline, ranging from -20 to +20. Empowered crystals boost MLT each round; Kronos damages it. MLT must be positive at game end to win. Colour-coded: green = positive, gold = zero, red = negative. |
| `gs-paradoxes` | **Paradox Counter** | Current number of active paradoxes. Paradoxes increase the risk of Time Collapse checks. Reduced by restoring certain Items at HQ. |
| `gs-round` | **Current Round** | The current round number. Each round, all players act with their agents, then Kronos takes his turn. |
| `gs-singularity-remaining` | **Rounds to Singularity** | Countdown to the Singularity (game end). When this reaches zero, the game enters its final scoring. Players must meet all win conditions before the Singularity. |
| `gs-excess-warn` | **Timeline Overflow Warning** | Kronos has pending overflow actions: extra artifact raids and/or crystal corruptions that will trigger on the next Kronos turn. Caused by timeline dropping below threshold. |

---

## TIMELINE RULER

Visual ruler widget in `#timeline-ruler`.

| Element ID | Tooltip Title | Tooltip Text |
|---|---|---|
| `timeline-ruler` | **Timeline Ruler** | Visual representation of the Main Line Timeline from -20 to +20. The marker shows the current MLT value. Green = safe (positive), gold = neutral (zero), orange/red = danger (negative). |
| `tr-marker` | **MLT Marker** | Current position on the Main Line Timeline. Empowered crystals push it positive each round; Kronos damage pushes it negative. Must be positive at game end. |
| `tr-marker-value` | **MLT Value** | The exact numeric value of the Main Line Timeline. |

---

## SCOREBOARD

Located in `#scoreboard-panel`.

| Element ID / Class | Tooltip Title | Tooltip Text |
|---|---|---|
| `scoreboard-panel` | **Scoreboard** | Player rankings sorted by score (Kairos minus Blots). Click any player row to view their full game history. Shows Vortex status badge when switched off. |
| `.sb-row` | **Player Score** | Player's current standing. Shows Kairos, Blots, and net score. Click to view detailed history of score changes. |
| `.sb-automa-tag` | **AI Player** | This player seat is controlled by the Automa (AI opponent). |
| `.sb-vortex-badge` | **Vortex Switched Off** | The Vortex has been successfully switched off by a TimeLord. This is one of the win conditions. |
| `.sb-stats` | **Player Stats** | Current Kairos and Blots values for this player. |

---

## DICE TRAY — TRAVEL DICE

The dice tray overlay (`#dice-tray-overlay` / `#dice-tray`) appears when time travelling or recovering articles.

### Travel Dice Colours

| Die Code | Die Label | Tooltip Title | Tooltip Text |
|---|---|---|---|
| `Or` | Ring | **Orange — Ring Die** | Determines which ring of the hex grid the agent can reach. Higher values = outer rings, further in time. |
| `Bk` | Direction | **Black — Direction Die** | Sets the directional sector on the hex grid. Combined with Ring to pinpoint the destination tile. |
| `Gr` | Base | **Green — Base Die** | Base travel die included in every travel roll. Provides a foundational navigation value. |
| `Bl` | Portal | **Blue — Portal Die** | Bonus die added when travelling FROM a portal location. Portals enhance your travel range. Not included in non-portal travel. |
| `Wh` | Planet | **White — Planet Die** | Navigation die keyed to planetary alignment. Part of the standard travel pool. |
| `Yl` | Adjacent | **Yellow — Adjacent Die** | Allows travel to tiles adjacent to the calculated destination. Provides flexibility in landing. |
| `TL` | Timelord | **TL — TimeLord Die** | Extra die available only to TimeLord agents. Gives TimeLords greater travel range and flexibility. |
| `Hz` | Baal | **Hazard — Baal Die** | Danger die. Can show a hazard cross (+) that triggers negative events during travel. Dark red colour. |
| `Pu` | Alpha | **Purple — Alpha Die** | Bonus die for AutoAlpha automata (3 wilds, 3 blanks). Boosts travel and recovery success rates. |

### Recovery Dice Colours

Recovery dice start black and take on the colour of their rolled face.

| Die Code | Die Label | Tooltip Title | Tooltip Text |
|---|---|---|---|
| `Rd` | Red | **Red Recovery Die** | Standard recovery die. Rolls specialist factor faces (A, S, C, P, M, H), Wilds, Skulls, or Blanks. |
| `Bl` | Blue | **Blue Recovery Die** | Standard recovery die. Same face pool as other recovery dice. |
| `Gr` | Green | **Green Recovery Die** | Standard recovery die. Same face pool as other recovery dice. |
| `Bk` | Black | **Black Recovery Die** | Standard recovery die. Same face pool as other recovery dice. |
| `Wh` | White | **White Recovery Die** | Standard recovery die. Same face pool as other recovery dice. |
| `TL` | TL | **TL — TimeLord Recovery Die** | Extra recovery die available only to TimeLord agents. Gives TimeLords better odds on recovery rolls. |
| `Hz` | Baal | **Hazard — Baal Die** | Danger die in recovery. Can trigger negative events via the hazard cross (+). |
| `Pu` | Alpha | **Purple — Alpha Die** | Bonus recovery die for AutoAlpha automata (3 wilds, 3 blanks). Boosts recovery success rates. |

### Dice Faces (Special)

| Face | Symbol | Tooltip Title | Tooltip Text |
|---|---|---|---|
| `*` | Wild | **Wild Face** | Matches any required specialist factor. Automatically locked when rolled. Shown as a star symbol. |
| `X` | Skull | **Skull Face** | Bad result. Automatically locked and cannot be re-rolled. Skulls do not count toward requirements and may trigger penalties. |
| `0` | Blank | **Blank Face** | No value. Does not match any requirement. Can be re-rolled on subsequent rolls. |
| `$` | Event | **Event Face** | Triggers a random event card. Events can be positive, negative, or neutral. Resolved when the dice session ends. |
| `+` | Hazard Cross | **Hazard Cross** | Appears on the Baal (Hazard) die only. Triggers a negative event — jail, lost in time, blots, paradox, or other penalties. |

### Recovery Specialist Factors

| Face | Name | Colour | Tooltip Title | Tooltip Text |
|---|---|---|---|---|
| `A` | Archivist | Yellow (#c8a800) | **Archivist (A)** | Archive specialist. Required by articles with Archivist factor requirements. Match this face to satisfy A requirements in recovery rolls. |
| `S` | Security | Red (#cc2222) | **Security (S)** | Security specialist. Required by articles with Security factor requirements. Match this face to satisfy S requirements. |
| `C` | Crypto | Green (#228b22) | **Cryptohacker (C)** | Cryptography specialist. Required by articles with Crypto factor requirements. Match this face to satisfy C requirements. |
| `P` | Psychic | Blue (#1a5fb4) | **Psychotronics (P)** | Psychotronic specialist. Required by articles with Psychic factor requirements. Match this face to satisfy P requirements. |
| `M` | Medic | Orange (#e8a000) | **Medical (M)** | Medical specialist. Required by articles with Medical factor requirements. Match this face to satisfy M requirements. |
| `H` | Historian | White (#cccccc) | **Historian (H)** | History specialist. Required by articles with Historian factor requirements. Match this face to satisfy H requirements. |

---

## DICE TRAY CONTROLS

| Element ID | Tooltip Title | Tooltip Text |
|---|---|---|
| `btn-roll-dice` | **Roll Dice** | Roll all unlocked dice. Locked dice (click to lock) keep their current face and are not re-rolled. Each roll after the first is a re-roll of unlocked dice only. |
| `btn-end-roll` | **End Roll** | Accept the current dice result and resolve the travel or recovery. Enabled when minimum requirements are met. Wilds fill remaining unmet requirements automatically. |
| `btn-cancel-travel` | **Cancel** | Cancel this travel or recovery attempt. The agent's turn is NOT consumed — they can try again or take a different action. |
| `dice-requirements` | **Requirements** | Shows the specialist factors needed for this recovery. Green chips = requirements met. Grey chips = still needed. Wilds auto-fill remaining gaps. |
| `dice-roll-log` | **Roll Log** | History of dice rolls in this session, showing what changed each roll. |
| `dice-event-area` | **Event Area** | Displays event card details when an Event ($) face is rolled. Events resolve at the end of the dice session. |
| `dice-result-area` | **Result** | Final outcome of the dice roll: success or failure, with details on Kairos/Blots gained and any triggered events. |

---

## ARTICLE TYPES

Articles appear as chips (`.article-chip`) on tiles and in the detail panel.

| CSS Class | Tooltip Title | Tooltip Text |
|---|---|---|
| `.article-type-item` | **Item** | Portable article (icon: box). Pick up for free (no dice roll). Carry to HQ and restore for Kairos, Blot reduction, or Paradox reduction. Items can be carried by any agent (limit based on agent type). |
| `.article-type-crystal` | **Crystal** | Recoverable article (icon: gem). Requires a Recovery Dice roll with matching specialist factors. Crystal Light is 3-tier: HQ crystals give flat +1 to MLT (+2 if empowered); field crystals at correct TL roll 2d6 vs 9 for +1; carried crystals contribute nothing. |
| `.article-type-artifact` | **Artifact** | Guardable article (icon: vase). Requires a Recovery Dice roll to guard in place. Guarded artifacts protect portal locations from Kronos raids. Artifacts stay at their location — they are NOT carried to HQ. |

### Article States

| CSS Class | Tooltip Title | Tooltip Text |
|---|---|---|
| `.article-guarded` | **Guarded** | This artifact has been successfully guarded. It protects its location from Kronos artifact theft. Shown with a shield badge. |
| `.article-restored` | **Restored** | This item has been restored at HQ. Its Kairos/Blot/Paradox benefits have been applied. Shown with a checkmark badge. |
| `.article-nerfed` | **Corrupted/Nerfed** | This article has been corrupted by Kronos. Corrupted crystals cannot be empowered. Shown with a dimmed visual. |
| Crystal (empowered) | **Empowered Crystal** | This crystal is active and boosting the MLT each round. Shown with a lightning bolt badge. Empowered by a TimeLord or any agent at HQ. |

---

## SPECIAL TILES (Right Column)

Located in `#special-grid`. Each tile has class `.special-tile-wrapper`.

| Element ID | Tooltip Title | Tooltip Text |
|---|---|---|
| `special-hex-JAIL` | **Xanadu Jail** | Agents sent here by events are trapped. Escape options: Roll doubles (costs Kairos), Bribe Xanadu (costs Kairos + gains Blots), or play a KEEP escape card. Forced bribe on the 3rd consecutive Jail turn. |
| `special-hex-LIT` | **Lost in Time** | Agents sent here by events are stranded outside the timeline. Escape: roll d6 and get 5+ (automatic each round), or be rescued by a TimeLord at HQ. |
| `special-hex-KRONOS` | **Kronos HQ** | Kronos's base of operations. Shows stolen artifacts and empowered crystal count. Kronos steals unguarded artifacts and damages the MLT each round. Articles held by Kronos are shown here. |
| `special-hex-DEAD` | **Wiped** | Agents that have been wiped out are placed here. Wiped agents cannot act and are removed from play for the remainder of the game. |

---

## KRONOS PANEL

Kronos information is displayed on the KRONOS special tile and in the detail panel when clicked.

| Element ID / Class | Tooltip Title | Tooltip Text |
|---|---|---|
| `kronos-articles` | **Kronos Artifacts** | Articles stolen by Kronos. Stolen artifacts damage the MLT and cannot be recovered. Empowering the paired crystal at HQ can nerf a stolen artifact, reducing Kronos's power. |
| `detail-kronos-history-btn` | **Kronos History** | View the full history of Kronos end-of-round actions: artifact raids, crystal corruptions, MLT damage, and timeline overflow events. |

---

## TIME FIELD (Hex Grid)

The hex grid is in `#hex-grid-container` / `#tile-display-area`.

| Element Class / ID | Tooltip Title | Tooltip Text |
|---|---|---|
| `.hex-tile` | **Time Location** | A location in the time field. Click to inspect — view agents, articles, and available actions. Each tile has a name and time period. Travel here by selecting an agent and entering travel mode. |
| `.tile-name` | **Location Name** | The name of this time location. |
| `.tile-time` | **Time Period** | The historical era or time period of this location. |
| `.tile-agent-area` | **Agents Here** | Agents currently at this time location. Shown as coloured tokens matching their player's colour. |
| `.hex-tile.portal-active` | **Portal Location** | This tile is an active portal. Agents travelling FROM a portal location gain a bonus Blue (Portal) die in their travel roll. Portals rotate each round. Shown with a blue border. |
| `.hex-tile.travel-target` | **Travel Destination** | Available destination for time travel. Click to select this tile as your travel target. Shown with a green glow during travel mode. |
| `.hex-tile.highlighted` | **Selected Tile** | This tile has been selected or highlighted for an action. |
| `.hex-tile.inspected` | **Inspected Tile** | This tile is currently being viewed in the detail panel. |

---

## HQ TILES (Left Column)

Located in `#hq-grid`. Each HQ tile has class `.hq-grid-tile`.

| Element ID Pattern | Tooltip Title | Tooltip Text |
|---|---|---|
| `hq-tile-{HQn}` | **Headquarters** | Player's home base. Agents start here and return when recalled. Restore Items here for Kairos/Blot/Paradox benefits. Empower Crystals here for Crystal Light bonuses. Click to view agents, articles, and available actions. |
| `hq-agent-panel-{HQn}` | **HQ Agent Icons** | Quick-view of all agents assigned to this HQ. Green = available, red = spent this turn, X = wiped. Star indicates TimeLord. Click an agent icon to jump to their location and select them. |
| `.hq-agent-icon` | **Agent** | One of your agents. Shows their status: green (available), red (acted this turn), or dead (wiped). TimeLords show a star. Click to inspect the agent's current location. |
| `.agent-icon-available` | **Available** | This agent has not yet acted this round. Select them to perform a time travel, recovery, or other action. |
| `.agent-icon-spent` | **Acted** | This agent has already completed their action this round. They cannot act again until the next round. |
| `.agent-icon-dead` | **Wiped** | This agent has been wiped out and is removed from play. |

---

## DETAIL PANEL (Left Column)

Located in `#detail-panel`.

| Element ID | Tooltip Title | Tooltip Text |
|---|---|---|
| `detail-panel` | **Inspection Panel** | Detailed view of the selected tile. Shows the location image, name, time period, agents present, articles available, and context-sensitive action buttons for your agents. |
| `detail-panel-image` | **Location Image** | The visual representation of this time location. |
| `detail-panel-name` | **Location Name** | Name of the currently inspected location. |
| `detail-panel-time` | **Time Period** | The era or time period of this location. |
| `detail-panel-agents` | **Agents at Location** | All agents currently at this location. Click your own agents to select them and see available actions. |
| `detail-panel-articles` | **Articles at Location** | Items, Crystals, and Artifacts present at this location. Shows type, name, requirements, and status. Hover for detailed article information. |
| `detail-panel-article-image` | **Article Preview** | Enlarged image of the hovered article, showing its artwork and details. |
| `detail-panel-kept-cards` | **KEEP Cards** | Special cards held by the player at this HQ. KEEP cards can be played for free effects: Jail Escape, LIT Escape, or Wild (use as either). |
| `detail-panel-actions` | **Actions** | Context-sensitive action buttons for the selected agent. Available actions depend on the agent's location and status. |
| `detail-panel-inventory` | **Inventory** | Articles being carried by agents at this location. |
| `detail-history-btn` | **Player History** | View this player's complete scoring history: Kairos gained, Blots incurred, and the events that caused each change. Click for round-by-round breakdown. |

---

## AGENT TOKENS

| Element ID Pattern / Class | Tooltip Title | Tooltip Text |
|---|---|---|
| `agent-token-{agentId}` | **Agent Token** | Visual token representing an agent on the board. Colour matches the owning player. Positioned at the agent's current location (HQ, field tile, Jail, LIT, or Wiped). |
| `.agent-token` | **Agent** | A player's agent in the time field. Agents perform actions each round: time travel to locations, recover articles, and carry items back to HQ. |

---

## AUTOMA (AI Player)

Automa players appear in the scoreboard and have their own HQ tiles.

| Class / Context | Tooltip Title | Tooltip Text |
|---|---|---|
| `.sb-automa-tag` | **Automa (AI)** | This player seat is controlled by the Automa — an automated AI opponent. The Automa takes its turn automatically, travelling agents and recovering articles based on priority rules. |
| Automa HQ tile | **Automa Headquarters** | Home base for the AI-controlled player. The Automa's agents operate from here, travelling to time locations and recovering articles automatically. |
| Status bar (Automa turn) | **Automata's Turn** | The Automa is resolving its turn. Click the Automata button to trigger its actions. All Automa decisions are resolved server-side. |

---

## POPUPS & OVERLAYS

| Element ID | Tooltip Title | Tooltip Text |
|---|---|---|
| `portal-info-overlay` | **Portal Status Popup** | Full portal information: active portals with protection status, artifacts present, and this round's portal rotation (added/removed portals). Portals reset every 5 rounds. |
| `article-list-overlay` | **Article List Popup** | Complete article inventory showing all Items, Crystals, and Artifacts in the game. Displays location, holder, requirements, and current status for each article. |
| `dice-tray-overlay` | **Dice Tray** | Modal overlay for rolling Travel or Recovery dice. Shows the dice pool, required faces, roll history, and result. Lock dice by clicking them before re-rolling. |

---

## PLAYER HISTORY POPUP

| Element ID / Class | Tooltip Title | Tooltip Text |
|---|---|---|
| `ph-close-btn` | **Close** | Close the player history popup. |
| `ph-round-details-btn` | **Round Details** | View detailed round-by-round breakdown of this player's actions, including individual agent moves, recoveries, and events. |
| `.ph-event-row` | **Score Event** | A single scoring event showing what happened, the Kairos/Blots change, and the running total. |

---

## Implementation Example

```javascript
// In Game.js setup(), after DOM is built:
_setupTooltips() {
    // Game state bar
    this.addTooltipHtml('gs-timeline', `
        <div style="max-width:280px">
            <strong>Main Line Timeline (MLT)</strong><br>
            Health of the timeline (-20 to +20).<br>
            Empowered crystals boost it; Kronos damages it.<br>
            <em>Must be positive at game end to win.</em>
        </div>
    `, 500);

    this.addTooltipHtml('gs-paradoxes', `
        <div style="max-width:280px">
            <strong>Paradox Counter</strong><br>
            Active paradoxes increase Time Collapse risk.<br>
            Reduce by restoring certain Items at HQ.
        </div>
    `, 500);

    // Action panel buttons
    this.addTooltipHtml('btn-portals', `
        <div style="max-width:280px">
            <strong>Portal Status</strong><br>
            View active portals and their protection status.<br>
            Portals add a Blue die to travel rolls from that tile.
        </div>
    `, 500);

    this.addTooltipHtml('btn-articles', `
        <div style="max-width:280px">
            <strong>Article Status</strong><br>
            View all Items, Crystals, and Artifacts in the game.<br>
            See locations, holders, and recovery requirements.
        </div>
    `, 500);

    // Detail panel action buttons (apply after creation in showDetailActions)
    // Use addTooltipHtmlToClass for dynamic buttons:
    this.addTooltipHtmlToClass('detail-btn-travel', `
        <div style="max-width:280px">
            <strong>Time Travel</strong><br>
            Enter travel mode — click a destination tile, then roll Travel Dice.<br>
            <em>Costs the agent's turn on success.</em>
        </div>
    `);

    // ... repeat for each element above
}
```
