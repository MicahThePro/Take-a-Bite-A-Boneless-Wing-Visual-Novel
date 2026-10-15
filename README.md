# 🍗 Take a Bite: A Boneless Wing Visual Novel

**One bite of a boneless wing can end the world.**

*Take a Bite* is a short, silly, DDLC-inspired visual novel that runs entirely in your browser. It's a single HTML file with no installs, no build step, no dependencies, and no image or audio files. Every texture is generated in code, and the soundtrack is synthesized live.

<!-- Add a screenshot here: ![Screenshot](screenshot.png) -->

**▶ Play it:** `<add your GitHub Pages link here>`

---

## The premise

It's 11:47 PM on a Friday at **Wingstead 24/7**, a diner that smells like fryer oil and bad decisions. You've just been served the Boneless Wings in the Sauce of the Week. Then a nervous chemistry student bursts in and tells you not to eat it, because the sauce contains something called **Compound Omega**, and the wing seems to be... watching you.

You have about ten minutes to decide whether to take the bite.

## Features

- **20 endings**, some where the Earth explodes and some where it survives, plus a few that are neither
- **Branching story** with investigation routes, hidden choices that unlock from clues you find, and a true ending you have to earn
- **A small cast:** Mika the server, Noor the chemist, Chef Gus, Agent Kell of the Department of Condiments, and Wingy, the wing
- **Procedural art:** backgrounds are painted on a canvas with wood grain, checkered floors, neon, film grain and vignettes. Characters are SVG sprites with grainy fabric and hair textures and several expressions.
- **Synthesized soundtrack:** a Web Audio loop that shifts mood with the story (jazzy diner, tense, calm, and a low rumble for the apocalypse)
- **Ren'Py-style menus:** Save, Load, Preferences, Auto, Skip, and an Endings tab
- **12 save slots** across two pages, with scene thumbnails and timestamps
- **Mobile-friendly:** works in both portrait and landscape
- **Glitchy meta moments** in the spirit of the games that inspired it (they can be turned off in Preferences)

## How to play

Open the game and press **New Game**.

| Action | Desktop | Mobile |
|---|---|---|
| Advance text | Click, Space, or Enter | Tap |
| Open the menu | Esc | Tap **Prefs** |
| Auto-advance | **Auto** in the bottom bar | Same |
| Fast-forward | **Skip** in the bottom bar (stops at choices) | Same |
| Save / Load | **Save** / **Load** in the bottom bar or main menu | Same |

Tapping the screen cancels Auto and Skip.

### Preferences

- Text speed
- Auto-forward time
- Music volume
- Glitch effects on/off
- Fullscreen
- Erase all saves and endings

Saves, settings, and your list of found endings are stored in your browser's `localStorage`. They are tied to the browser and site you play on, and they will be lost if you clear site data.

## Running it

**Locally:** download `index.html` and open it in a browser. Audio starts after you press New Game, because browsers require a user interaction first.

**On GitHub Pages:**
1. Put `index.html` in the root of your repo.
2. Go to **Settings → Pages**, choose your branch and the `/ (root)` folder, and save.
3. Your game will be live at `https://<username>.github.io/<repo>/`.

### Browser support

Any modern browser. The layout uses CSS container query units, so you'll want Chrome 105+, Safari 16+, or Firefox 110+. Fullscreen may not be available on iPhone.

## Endings

<details>
<summary><b>⚠️ Spoilers: show the ending list</b></summary>

1. Flavor Country
2. Employee Discount
3. Split the Check
4. Ranch Saves All
5. Classified Flavor
6. Deep Fried
7. Going Viral
8. Peer Reviewed
9. Controlled Experiment
10. Wing Whisperer
11. Betrayal
12. Pigeon Problem
13. Ordinary Night
14. Wing Wedding
15. Mika's Heart
16. Nobel Flavor
17. Iron Stomach
18. Just Wingy
19. Groundhog Wing
20. Good Taste

**Hints**
- Some options only appear after you've talked to the right people, so explore before you decide.
- Noor and Mika both know something about dairy.
- The true ending needs everyone's help. Talk to every character and the wing itself.

</details>

## How it's built

The whole game lives in one file and uses only browser built-ins:

- **Canvas 2D** for backgrounds, textures, and the Earth explosion
- **SVG filters** (`feTurbulence`) for grain on the character sprites and the crispy look of the wing
- **Web Audio API** for the music: oscillators, simple chord and melody patterns, and a scheduler, with no audio files
- **Vanilla JavaScript** for the engine (typewriter text, choices, flags, save/load, menus)
- **CSS container query units** so the whole UI scales with the game window in both orientations

### Editing the story

The script is a plain-text block inside the HTML file, one scene per line:

```
id|speaker|text|next|characters|effects|choices
```

| Field | Meaning |
|---|---|
| `id` | Unique scene name |
| `speaker` | `M` Mika, `N` Noor, `G` Gus, `K` Kell, `W` Wingy, `Y` You, or empty for narration |
| `text` | The line shown in the dialogue box |
| `next` | The scene that follows (leave empty if the scene has choices or is an ending) |
| `characters` | Space-separated sprites like `N.s.l M.h.r`: **character . expression . position** (see below). Use `-` to clear the stage. |
| `effects` | Semicolon-separated settings (see below) |
| `choices` | `Label>target>condition`, separated by `~` |

**Expressions:** `h` happy, `s` sad, `x` shocked, `m` smirk, `b` blank  
**Positions:** `l` left, `c` center, `r` right

**Effects:**

| Key | What it does |
|---|---|
| `bg=diner` / `back` / `space` | Changes the background |
| `fx=glitch` / `none` | Turns the glitch effect on or off |
| `mu=jazz` / `tense` / `calm` / `doom` | Changes the music mood |
| `set=flag` | Sets one or more flags, comma-separated |
| `boom` / `calm` | Plays the Earth explosion or the Earth-survives finale |
| `end=N:Title` | Registers ending number `N` with its title |
| `msg=TEXT` | The line shown on the finale screen |

**Conditions** on a choice are flags joined with `&`, and `!flag` means "flag not set yet". For example, `Dunk it in ranch first>r1>aN&aM` only appears after both `aN` and `aM` are set.

Keep the characters `| ; ~ >` out of dialogue text and choice labels, since the parser uses them as separators.

**Adding a character** takes one entry in the `C` table (hair color, outfit color, skin tone, and a hair style) and a letter in the speaker list.

## Content note

Cartoonish world-ending, food-related silliness, and some glitchy meta horror played for laughs. There's no gore.

## Inspiration

Inspired by the format and menus of *Doki Doki Literature Club!* and Ren'Py visual novels. This is an independent fan-style parody project. It contains no assets from either and isn't affiliated with them.
