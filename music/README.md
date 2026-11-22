# Recorded music

The first asset files BONEBOX ships. Everything else in the game is drawn or
synthesised in code; these are real recordings, so they live in `public/` and
vite copies them to the bundle root untouched.

**Each file is named after the song id it replaces** (`src/audio/songs.ts`), so
`swamp.mp3` is what plays wherever the written `swamp` song used to. The map
is in `src/audio/musicTracks.ts`; `src/audio/Music.ts` prefers a recording when
one exists for the id it is asked for, and falls back to the written song when
one does not.

A dungeon's five level arrangements (`swamp-L1` ... `swamp-L5`) all resolve to
the dungeon's own file: there is one recording per dungeon, not five.

| file | song id | where it plays | from |
| --- | --- | --- | --- |
| `title.mp3` | `title` | title screen, character select, gacha | `bonebox menu (demo)` |
| `hallway.mp3` | `hallway` | the corridor between dungeons, and the chalice room | `hallway challace room (demo)` |
| `swamp.mp3` | `swamp` | Bog of Bones | **`percussive track`** |
| `kitchen.mp3` | `kitchen` | Gorging Kitchen | `kitchen theme (demo)` |
| `observatory.mp3` | `observatory` | Starlit Observatory | `starlit observatory (demo)` |
| `cathedral.mp3` | `cathedral` | Hollow Cathedral | `hollow catherdal (demo)` |
| `citadel.mp3` | `citadel` | Cloud Citadel | `cloud citadel (demo)` |
| `arcade.mp3` | `arcade` | Haunted Arcade | `haunted arcade` |
| `rift.mp3` | `rift` | Nightmare Rift | `Nightmare rift (demo)` |
| `studio.mp3` | `studio` | Mugdot's Studio | `mugdot's studio (demo)` |

Two things about that table are deliberate and easy to "fix" by mistake:

- **Bog of Bones plays the percussive track.** The `bog of bones (demo)` file
  from the same drop is NOT used; the percussive one takes its place. If you
  ever add `bog of bones` back, it is not the Bog of Bones theme.
- **`hallway` is a new song id.** There was no written song for the corridor or
  the chalice room: the corridor used to play the next dungeon's theme and the
  chalice room played whatever was already going.

The other 13 dungeons and every boss still use their written songs. Adding a
recording for one is a two-line change: drop `<songid>.mp3` in here and add the
id to `musicTracks.ts`.

All ten are 192 kbps CBR, 44.1 kHz joint stereo, 27 s to 1:45, 14 MB in total.
Nothing is downloaded until a track is first asked for.
