---
layout: page
title: Make your own database
game: Managed Football
---
Managed Football comes with its own invented world. If you would rather play with other clubs and players — a league you made up, your Sunday league, a world a friend built — you can write them into a **database file** and start a career from it.

The easiest way is to make the file on a computer and then move it to your phone. Your file is only ever read on your phone; the game never uploads it. What you put in it is your own responsibility.

<p><a href="example-ardeland.json" download>Download the example template (example-ardeland.json)</a></p>

The template is a complete, working database: two seasons of an invented league, each with four divisions of sixteen clubs, and some clubs written out in full so you can see the fields in use.

## 1. Make the file on your computer

1. Download the template above.
2. Open it in a plain text editor. Notepad works; an editor that checks JSON as you type (such as Visual Studio Code or Notepad++) makes mistakes much easier to spot. Don't use a word processor: it changes the quotation marks and the file stops working.
3. Change the names and details to your own. Only the club names are required. Anything you leave out — squads, grounds, colours, money, staff — is generated for you.
4. Save it as a `.json` file in UTF-8 (the usual default), with a name you will recognise, such as `My League.json`. You can also zip it: a `.zip` holding one `.json` works too.

## 2. Move it to your phone

Use whichever is easiest:

- **Send it to yourself.** Email it, or put it in a cloud drive or messaging app, and save it to your phone's Downloads.
- **USB cable.** Connect the phone, choose "File transfer" on the phone, and copy the file into its `Download` folder.

## 3. Import it in the game

1. Open **New career ▸ World: Custom database ▸ Choose a database**.
2. Tap **Choose a file on this phone** and pick your file. The game copies it into its own folder.
3. The file appears in the list marked "Ready", or with a number of warnings or problems. Tap it for the details.
4. If there are problems, each one gives the line in the file and what is wrong. Fix it on your computer, move the file across again and import it again.
5. Tap **Choose a starting season**, pick your club, and play.

If you prefer, you can copy files straight into the folder the game reads, `Android/data/com.iterumgames.managedfootball/files/Databases/`, over USB and then tap **Check folder**. Many newer Android versions hide that folder from file manager apps on the phone, so USB is the reliable way to reach it.

Uninstalling the game deletes the copies it holds, so keep your original on your computer.

## In short

- One JSON text file, UTF-8, ending in `.json` (or a `.zip` with one `.json` inside).
- It holds one or more **editions**: the world as it stands at the start of one season. A file with several editions lets you choose the starting year.
- Each edition has **1 to 6 divisions of 8 to 24 clubs** (an even number each; divisions may differ in size).
- A file with nothing but club names is valid; a file with every player, attribute and stand is used exactly as written.

## The smallest valid file

```json
{
  "name": "My League",
  "editions": [
    {
      "startYear": 2026,
      "divisions": [
        { "name": "First Division",  "clubs": ["Club 1", "Club 2", "... 16 names ..."] },
        { "name": "Second Division", "clubs": ["... 16 names ..."] },
        { "name": "Third Division",  "clubs": ["... 16 names ..."] },
        { "name": "Fourth Division", "clubs": ["... 16 names ..."] }
      ]
    }
  ]
}
```

Every club gets a generated squad, ground, colours, money and staff that fit its division. Within a
division, the first club listed is treated as the biggest (highest reputation) and the last as the
smallest, unless you give a `reputation`.

## A fuller example

```json
{
  "format": "managedfootball-database",
  "formatVersion": 1,
  "name": "Ardeland Example League",
  "author": "You",
  "version": "1.0",
  "description": "Anything you like, shown on the database screen.",
  "editions": [
    {
      "label": "2026–27",
      "startYear": 2026,
      "nations": [
        { "name": "Ardeland", "adjective": "Ardelish", "code": "ARD" },
        { "name": "Valdoria", "adjective": "Valdorian", "code": "VAL" }
      ],
      "cupName": "Ardeland Lantern Cup",
      "divisions": [
        {
          "name": "Ardeland Premier Circle", "shortName": "Premier Circle", "tier": 1,
          "clubs": [
            {
              "name": "Halvermoor Athletic", "shortName": "Halvermoor", "code": "HAL",
              "reputation": 86, "colours": ["#1C5D99", "#FFFFFF"],
              "fanBase": 52000, "balance": 34000000,
              "stadium": {
                "name": "Moorside Lane", "capacity": 48000,
                "stands": [
                  { "side": "west", "name": "The Founders Stand", "seats": 15000, "standing": 0, "roof": true },
                  { "side": "north", "name": "Kilnyard End", "seats": 9000, "standing": 2000, "roof": true }
                ]
              },
              "staff": [
                { "firstName": "Aurelia", "lastName": "Thackwray", "role": "AssistantManager", "quality": 68 }
              ],
              "players": [
                { "firstName": "Tobin", "lastName": "Ambrell", "dateOfBirth": "1998-03-14", "nationality": "Ardeland",
                  "positions": ["GK"], "foot": "right", "shirtNumber": 1, "wage": 9500, "contractEnd": "2029-06-30",
                  "attributes": { "goalkeeping": 79, "agility": 74, "awareness": 72, "pace": 51 } },
                { "firstName": "Arlo", "lastName": "Pellow", "age": 19, "positions": ["AM", "CM"], "overall": 66, "potential": 81 },
                { "lastName": "Varnell", "positions": ["ST"] }
              ]
            },
            "Quenby Wanderers",
            "... 14 more clubs ..."
          ]
        },
        "... three more divisions ..."
      ],
      "freeAgents": [
        { "firstName": "Kit", "lastName": "Rendle", "age": 27, "positions": ["CB"], "overall": 49 }
      ]
    }
  ]
}
```

Comments (`// ...`) are allowed and ignored. Field names are case-sensitive; an unknown field is
reported as a warning so a typo does not go unnoticed.

## Fields

### The file

| Field | Required | Meaning |
|---|---|---|
| `name` | recommended | Shown in the list and on saves. Default "Custom database". Up to 40 characters. |
| `author`, `version` | no | Shown on the database screen. |
| `description` | no | Up to 400 characters. |
| `format`, `formatVersion` | no | `"managedfootball-database"`, `1`. A newer version number is read as far as this game understands. |
| `editions` | **yes** | 1 to 30 editions. |

### Edition

| Field | Required | Meaning |
|---|---|---|
| `startYear` | recommended | The year the first season starts (1 July). 1900–2200. Default 2026. |
| `label` | no | Name in the season picker, e.g. "2026–27". Default made from the year. |
| `nations` | no | Up to 60. A name (`"Ardeland"`) or `{ "name", "adjective", "code" }`. The **first** nation is the league's home. A player's `nationality` that is not listed is added automatically. Default: one invented nation. |
| `divisions` | **yes** | 1 to 6, see below and "Shapes". |
| `cupName` | no | The knockout cup every club enters. Default "<nation> Cup". |
| `freeAgents` | no | Players without a club, up to 1000 (same fields as players). |
| `generateFreeAgents` | no | `true` (default) tops the free-agent pool up to 120 with generated players. |

### Division

| Field | Required | Meaning |
|---|---|---|
| `name` | recommended | Full name. Default "Division 1"... |
| `shortName` | no | For tabs and tables. |
| `tier` | no | 1 = top to the number of divisions = bottom; each once. Default: the order in the file. |
| `relegationPlaces` | no | Clubs relegated from this division to the one below, and promoted from below in exchange. 1 to a third of the smaller of the two divisions. Default: about a sixth of the smaller division (see "Shapes"). Ignored, with a warning, on the bottom division. |
| `clubs` | **yes** | 8 to 24, an even number. Each is either a name (text) or a club object. |

### Club

| Field | Default when left out | Notes |
|---|---|---|
| `name` | — (required) | Up to 40 characters. A repeated name gets " 2" added (warning). |
| `shortName` | the name without "FC"/"AFC", cut to 18 characters | |
| `code` | made from the name | 3 letters/digits, starting with a letter, unique. |
| `reputation` | from the division and the order in the list | 1–99. |
| `colours` (or `colors`) | generated | `["#RRGGBB", "#RRGGBB"]`, home colour first. |
| `stadium` | generated for the division | `{ "name", "capacity", "stands" }`. `capacity` (1,000–150,000) scales a generated ground. `stands` override single sides: `side` (north/east/south/west, required), `name`, `seats`, `standing`, `roof` (true/false). |
| `fanBase` | about the ground's capacity | Committed supporters. |
| `balance` | by division and reputation | Starting money, whole units. |
| `staff` | five generated staff (assistant, fitness, goalkeeping coach, physio, scout) | Up to 20: `firstName`, `lastName` (required), `role` (required: AssistantManager, FitnessCoach, TechniqueCoach, GoalkeepingCoach, DefenceCoach, AttackCoach, YouthCoach, Physio, Doctor, ChiefScout, Scout, Groundskeeper, StadiumManager, CommercialManager), `quality` 1–99, `dateOfBirth`. Roles you do not list among the five are still generated. |
| `players` | a full generated squad of 24 | Up to 30. See "Squads". |

### Player

| Field | Default when left out | Notes |
|---|---|---|
| `lastName` | — (required) | |
| `firstName` | empty | |
| `dateOfBirth` | from `age`, else generated (17–35) | `YYYY-MM-DD`. The player must be 15–45 in the start year. |
| `age` | generated | Used only when there is no `dateOfBirth`. |
| `nationality` | the first nation | A nation name or code. |
| `positions` | generated | 1–3 of GK, CB, LB, RB, LWB, RWB, DM, CM, LM, RM, AM, LW, RW, ST. The first is his main position. |
| `foot` | generated | right, left or both. |
| `shirtNumber` | a free number | 1–99, unique in the club. |
| `wage` | a fair wage for the club's division | Weekly, whole units. |
| `contractEnd` | 1–5 seasons (a 30 June) | `YYYY-MM-DD`, after the start date. |
| `overall` | from the club's level and his age | 1–99. Attributes are generated to match it for his position. |
| `potential` | generated from age and overall | 1–99; never below his overall. |
| `attributes` | generated | Any of: pace, strength, stamina, determination, passing, shooting, tackling, heading, control, agility, awareness, setPieces, leadership, goalkeeping (1–99). Given ones are used exactly; missing ones are generated (around `overall` if you give it). |

So for each player you can give everything, or just `overall` + `potential`, or only a name.

## Squads

- A club with no `players` gets a generated squad of 24.
- A club with fewer than 18 players is topped up to 22 with generated players in the positions it
  is missing, and with goalkeepers to make at least 2 (shown as a warning).
- Up to 30 players per club; more is a problem to fix.

## Editions and years

Each edition is complete on its own: its own divisions, clubs and players. Use several editions for
several seasons of the same world (clubs promoted and relegated, players older, new signings). When
you start a career the game asks which edition to start from; the season then starts on 1 July of
its `startYear` and the world moves on from there as usual.

## Shapes the game supports

One nation's league pyramid: **1 to 6 divisions**, each of **8 to 24 clubs** (an even number).
Divisions may differ in size (for example 24, 22 and 20). Everything else follows from the sizes:

- **League season.** Every club plays every other twice (home and away); divisions of 10 clubs or
  fewer play each other four times so the season is not too short (8 clubs: 28 matches). Matches
  are on Saturdays from the second weekend of August to mid-May with a two-week winter break. A
  division with more matchdays than there are Saturdays (22 or 24 clubs) also plays some midweek
  (Wednesday) rounds, spread through the season and never in a cup week; the winter break is kept.
- **Promotion and relegation.** The same number of clubs goes down and comes up across each
  boundary, so division sizes never change. Default: about a sixth of the smaller division, 1 to 4
  (8 clubs: 1, 12: 2, 16 or 20: 3, 22 or 24: 4). Set `relegationPlaces` on a division to choose.
- **Cup.** Every club enters. When the number of clubs is not a power of two (64, 32, ...), the
  lowest-ranked clubs (bottom divisions first) play a preliminary round and the rest go straight
  into round 2 (20 clubs: 8 play 4 preliminary ties, 12 have byes, then a 16-club knockout).
  Up to 144 clubs: at most 8 rounds, the final in late April.
- **Money and stature.** Prize money, broadcasting, sponsorship, advertising, ticket prices, wages,
  reputation, fan bases, grounds and starting money are set by tier: tiers 1 to 4 are exactly the
  generated world's divisions, and a 5th or 6th tier continues the scale downward (smaller grounds,
  crowds and wages, weaker squads). A single-division file plays at top-tier level.

Not supported: more than one nation's pyramid in a file (extra `nations` are only used for players'
nationalities), divisions of odd size or outside 8–24, more than 6 divisions, regional splits
within a tier, play-offs, and cups for only part of the pyramid. The game says which division has
the wrong count.

## Problems and warnings

- **Problems** stop the file from being used: not valid JSON (with the line), missing `editions`,
  `divisions` or club names, wrong numbers of divisions or clubs, a player without a `lastName`, an
  unknown position, a date not written `YYYY-MM-DD`, numbers that are not numbers or far out of
  range, too many players, stands without a side, staff without a role.
- **Warnings** are fixed for you: unknown fields ignored, values outside 1–99 brought into range, bad
  codes or colours regenerated, duplicate club names or shirt numbers renamed, squads topped up.

The database screen shows the first problems and how many there are in all; each says the line
number and the place in the file (e.g. `editions[0].divisions[2].clubs[5].players[3].dateOfBirth`).

## Limits

File up to 16 MB · 30 editions · 60 nations · 30 players and 20 staff per club · 1000 free agents ·
names up to 40 characters.
