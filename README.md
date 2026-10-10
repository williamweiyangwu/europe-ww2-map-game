# Europe WWII Map Game

A single-file, dependency-free strategy game covering the 1939 European theatre.
Open `index.html` in any modern browser — there is nothing to install or build.

## Play

1. Pick a nation.
2. **Select a territory** you own on the map.
3. **Shop** → buy units. Each nation has its own historical arsenal, split into
   **Army** (10 weapons) and **Air Force** (5 aircraft).
4. **Battle** → tick the units you want to attack with, then pick a target border.
5. Mines are your only income, so buy mine cars early.

### Play online

1. On the start screen press **Play online multiplayer**.
2. One player presses **Host a room** and starts the war once others join.
3. Everyone else types the 4-letter room code into **Join** (or picks it from the
   open-rooms list).
4. Every nation is a seat — pick yours. Unpicked nations fight for the AI.
   Players who stop responding are released back to the AI after ~12 seconds.
5. The host runs the simulation on their machine; guests send orders (recruit,
   move) which the host applies. Guests should keep the host's tab open.

Uses the free public MQTT relay `broker.emqx.io:8084` (secure WebSocket). Rooms
are ephemeral — there is no account, no stored game, and nothing leaves your
browser except the topics above.

### Controls

| Key | Action |
| --- | --- |
| `S` | Open the Shop |
| `B` | Open the Battle page |
| `N` | Jump to the newspaper (right sidebar) |
| `M` | Jump to the diplomatic pouch (right sidebar) |
| `Esc` | Return to the map |
| `Space` | Pause / resume |

The **right sidebar** holds **The Continental** — a newspaper written from what
actually happened on the map: who occupied what, with which machines (a German
*Panzer VIII Maus* leading the way into Poland), and who was wiped off the map.
Captures, collapsed treasuries, vanished nations, and the unveiling of legendary
weapons all reach the front page. A fresh edition arrives every ten days,
replacing the last.

The sidebar also holds the **diplomatic pouch**. Other nations write to you, and
every letter offers between two and four replies — accept a pact, make peace, or
answer a threat with force. You can also post your own notes under five subjects:
offer an alliance, a trade deal, congratulations, a warning, or an ultimatum.
Opening a letter or composing a note pauses the war until you close it.

## Rules worth knowing

- Income is `mines x 4 gold/day`, minus unit upkeep. There is no passive territory income.
- Gold under `-40` is bankruptcy.
- Garrison capacity scales with a nation's size: about **6** units for the smallest states up to **17** for the Soviet Union.
- Air units fly: they strike any enemy border province and return home.
- Enemy garrisons are only visible in provinces bordering your territory.
- Annexed regions (Iceland, Austria) belong to another nation and cannot be played.

## Technical notes

- One HTML file, ~128 KB, no build step, no external assets (the game itself).
- Map is inline SVG; all rules live in one inline `<script>`.
- Works from `file://` as well as over HTTP.
- Multiplayer is host-authoritative: the host's `tick()` drives the war and
  broadcasts a compact JSON state; guests render it and send `move`/`recruit`/
  `mail` orders over MQTT (WSS, topic namespace `ow/<ROOM>/…`).