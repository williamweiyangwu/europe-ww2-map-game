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

### Controls

| Key | Action |
| --- | --- |
| `S` | Open the Shop |
| `B` | Open the Battle page |
| `Esc` | Return to the map |
| `Space` | Pause / resume |

## Rules worth knowing

- Income is `mines x 4 gold/day`, minus unit upkeep. There is no passive territory income.
- Gold under `-40` is bankruptcy.
- A province holds at most **10** units.
- Air units fly: they strike any enemy border province and return home.
- Enemy garrisons are only visible in provinces bordering your territory.
- Annexed regions (Iceland, Austria) belong to another nation and cannot be played.

## Technical notes

- One HTML file, ~92 KB, no network requests, no build step, no external assets.
- Map is inline SVG; all rules live in one inline `<script>`.
- Works from `file://` as well as over HTTP.