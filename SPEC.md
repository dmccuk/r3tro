# r3tro.io product spec

Version 1.0, October 2026

## 1. Overview

**One-liner:** r3tro.io is a free collection of simple, addictive arcade-style games, each built with AI and documented in public on TikTok, Instagram and YouTube.

**The idea in brief:** Launch with one polished game and a simple homepage. Grow an audience by sharing how each game is made, let followers vote on what gets built next, and add community features (leaderboards, accounts) and income (tips, sponsorships, subscriptions) only once people are actually playing.

**Who it's for**

- Players: anyone with two minutes to kill on a phone or computer who wants a quick, satisfying game with no downloads or sign-ups.
- Followers: people curious about building things with AI, indie game development and "build in public" stories.

**Guiding principles**

1. Playable in under five seconds. No sign-up, no ads, no loading screens to start.
2. Mobile first. Every game must work with touch as well as keyboard.
3. Original games only. Inspired by classics, never copies of them.
4. Ship small, ship often. A finished simple game beats an unfinished ambitious one.
5. The audience shapes the roadmap. Polls decide what comes next.

## 2. Brand

| Item | Decision |
|---|---|
| Name | r3tro (always lowercase, always with the 3) |
| Domain | r3tro.io |
| Voice | Friendly, plain, a little playful. Short sentences. |
| Look | Glowing vector lines on a deep navy screen, like an old arcade monitor |
| Display font | Major Mono Display (wordmark, headings, scores) |
| UI font | Chakra Petch (body text, buttons) |

**Colour palette**

| Token | Hex | Use |
|---|---|---|
| Background | `#060a1a` | Screen |
| Line | `#d9ecff` | Main vector lines and text |
| Cyan | `#7fe6ff` | Player, links, glow |
| Amber | `#ffb44a` | Scores, multipliers, primary buttons |
| Rose | `#ff5c8a` | Enemies, danger |
| Mint | `#8dffc4` | Bonuses, extra lives |
| Dim | `#6d80a6` | Secondary text |

**Spoken-name tip:** People who hear "retro dot io" may type it without the 3. Use the 3 prominently in every logo and video, and register `retro.io` too if it ever becomes available.

## 3. Site structure

| URL | Page |
|---|---|
| `/` | Homepage: wordmark, play button, game list, socials, tip link |
| `/games/shardfield/` | Shardfield |
| `/games/duskhold/` | Duskhold |
| `/games/tumblewell/` | Tumblewell |
| `/games/<slug>/` | Each future game |
| `/privacy/` | Privacy policy (needed before Phase 2) |

**Tech approach (Phase 1):** Static HTML hosted free on GitHub Pages. Each game is one self-contained `index.html` file with its own CSS and JavaScript. No frameworks, no build step, no server. This keeps the AI-to-website workflow simple: generate the file, test it, commit it.

## 4. Game requirements checklist

Every game must meet these before it goes on the homepage:

- [ ] Original name, characters and art (no trademarked names like Pac-Man, Tetris or Asteroids)
- [ ] Works on phone (touch buttons) and computer (keyboard)
- [ ] Starts within one tap or key press from the title screen
- [ ] Saves the player's best score in the browser (localStorage)
- [ ] Shows "x short of your best" or "New best" on game over
- [ ] Instant "Play again" button
- [ ] Pauses automatically when the tab is hidden or the app loses focus
- [ ] Sound with a mute button that remembers the choice
- [ ] Respects reduced-motion settings (no screen shake)
- [ ] Link back to the r3tro homepage
- [ ] Uses the r3tro colour palette and fonts
- [ ] Single file, under 1 MB

**Addictiveness ingredients** to consider for every game: a score multiplier or combo system, escalating difficulty, power-ups, near-miss rewards, a visible personal best, and audio that builds tension.

## 5. Game 1: Shardfield

A vector-style space shooter. Fly a small ship, shoot drifting rocks that split into smaller pieces, and survive as long as possible.

**Controls**

| Action | Keyboard | Touch |
|---|---|---|
| Turn | Left/Right arrows or A/D | Control stick (left thumb): the ship turns to face the stick |
| Thrust | Up arrow or W | Push the stick past halfway |
| Fire | Space (or J/K) | Large circle button |
| Pause | P or Escape | Pause button, top right |
| Mute | M | Speaker button, top right |

**Scoring**

| Event | Base points |
|---|---|
| Large rock | 20 |
| Medium rock | 50 |
| Small rock | 100 |
| Saucer | 500 |
| Close call (rock passes very near) | 25 |
| Wave clear | 250 × wave number |

All points except the wave-clear bonus are multiplied by the current combo multiplier.

**Combo multiplier:** Every hit within 2.4 seconds of the last one extends the chain. Every 4 hits in a chain adds +1 to the multiplier, up to x8. Missing the window or losing a ship resets it to x1.

**Power-ups** (dropped by roughly 1 in 8 large rocks, 1 in 14 smaller rocks, and most saucers)

| Power-up | Effect | Duration |
|---|---|---|
| Triple shot (T) | Fires three bullets in a spread | 9 s |
| Rapid fire (R) | More than doubles fire rate | 9 s |
| Shield (S) | Absorbs one hit | 14 s or until hit |
| Nova (N) | Destroys everything nearby | Instant |

**Progression:** Each wave adds one more large rock (up to 11) and speeds rocks up by 8%. From wave 2, an enemy saucer appears every 12 to 20 seconds and aims more accurately each wave. Players start with 3 ships and earn an extra ship every 10,000 points.

## 6. Game 2: Duskhold

A torch-lit castle explorer, inspired by 1980s flip-screen adventures. Walk room to room through a dark castle, search furniture for keys and clues, and find three seals to open the gate in the Sealed Crypt.

**Controls**

| Action | Keyboard | Touch |
|---|---|---|
| Move | Arrows or WASD | Drag anywhere on the left half |
| Throw dagger | Space (or J/K) | Large button, bottom right |
| Search | Walk into a chest, urn, shelf or locked door | Same |
| Pause | P or Escape | Pause button, top right |
| Mute | M | Speaker button, top right |

**The castle:** A new castle is built for every run: a 5x5 grid of rooms joined as a maze, with a few extra doorways. Three locked doors (Silver, Gold and Crimson) sit on the route to the crypt, and each key is always placed somewhere you can reach before its door, so every castle can be finished.

**Torch:** Only what the torch lights is visible, apart from a faint outline of the walls. The torch burns down over about three and a half minutes and the light shrinks with it. Lamp oil adds 40%. With no light, the dark takes a heart every 5 seconds.

**Searching:** Chests, urns and bookshelves line the walls. Chests hold gold, oil, food, keys, seals or a spider trap. Urns smash open (walk into them or hit them with a dagger). Shelves may hold an old note, which reveals where the next missing key or seal is hidden and marks that room on the minimap.

**Enemies:** Bats (fast, erratic), spiders (chase when you get close) and ghosts (slow, pass through walls, take two hits). Each room spawns new enemies when you enter it, and later parts of the castle spawn more. The player starts with 3 hearts, up to a maximum of 5.

**Scoring**

| Event | Points |
|---|---|
| New room explored | 50 |
| Gold | 25 to 150 |
| Old note | 100 |
| Key | 250 |
| Seal | 1,000 |
| Bat / spider / ghost | 50 / 75 / 150 |
| Escape bonus | 5,000 + 500 per heart + 20 per % of torch left + 10 per second under 15 minutes |

Best score and fastest escape are saved in the browser.

## 7. Game 3: Tumblewell

A falling-block puzzle where the well itself turns. Every 20 to 30 seconds the whole well rotates a quarter turn clockwise, and blocks keep falling toward its floor. After two turns you are playing upside down, with blocks falling up the screen.

**Controls** (screen-relative, so they always match what you see)

| Action | Keyboard | Touch |
|---|---|---|
| Move block | The arrow (or WASD) pointing where you want it to go on screen | Drag |
| Drop faster | The arrow pointing at the well's floor | Drag toward the floor |
| Rotate | The arrow pointing away from the floor, or X / Z | Tap |
| Drop instantly | Space | Flick toward the floor |
| Pause | P or Escape | Pause button, top right |
| Mute | M | Speaker button, top right |

**The well:** 10 wide by 18 deep. The floor is lit amber so you can always tell which way is down. The turn timer under the multiplier fills down to each turn, then flashes and ticks for the last 3 seconds. Play freezes for under a second while the well turns.

**Scoring**

| Event | Points |
|---|---|
| 1 / 2 / 3 / 4 lines | 100 / 300 / 500 / 800 × level × chain |
| Soft drop | 1 per row |
| Hard drop | 2 per row |
| Well turn survived | 250 × level |

**Chain multiplier:** Each block in a row that clears at least one line adds +1 to the chain, up to x8. A block that clears nothing resets it to x1.

**Progression:** Level goes up every 10 lines, and blocks fall faster each level.

**Keeping it original:** The name, the turning well, the vector-outline art, the colours, the 10x18 well and the corner-tick landing marker are all our own. The game does not use the name or look of any existing falling-block game.

## 8. Roadmap

### Phase 1: Launch and build an audience

Goal: a live site with 3 to 4 games and a growing social following.

- Launch r3tro.io with the homepage and Shardfield
- Post the first videos (see section 11)
- Run a poll for game 2, build it, post the process, repeat
- Add simple privacy-friendly visitor counts (see section 13)

Move to Phase 2 when: the site has steady daily players and followers are asking to compare scores.

### Phase 2: Community

Goal: give players a reason to come back every day.

- Global leaderboards per game (daily, weekly, all-time)
- Optional accounts to save scores across devices and claim a leaderboard name
- Daily challenge: one seeded run per day that everyone plays
- Extra levels or modes for existing games
- Privacy policy page (required before any accounts)

### Phase 3: Support and income

Goal: cover costs and fund new games, without spoiling the free experience.

- Tip jar link on the homepage and game-over screens
- Game sponsorships (see section 10)
- Optional supporter subscription with perks
- Merchandise only if there is clear demand

## 9. Phase 2 technical design: accounts and leaderboards

GitHub Pages only serves static files, so leaderboards need a hosted backend. The simplest option is a "backend as a service" such as **Supabase** or **Firebase**, both of which offer free tiers and work directly from browser JavaScript, so the site can stay on GitHub Pages.

**Data model (example)**

| Table | Fields |
|---|---|
| `profiles` | id, display_name, created_at |
| `scores` | id, profile_id (optional), game_slug, score, wave_or_level, created_at |

**Rules**

- Anyone can read leaderboards.
- Players can only write their own scores, enforced with the provider's security rules (for Supabase, row-level security).
- Display names are filtered for offensive words before saving.
- Guest play stays fully available. Accounts are only for saving and ranking.

**Cheating basics:** Browser games can always be cheated by determined people. Keep it reasonable: reject impossible scores (above a per-game ceiling, or too high for the time played), rate-limit submissions, and let you remove scores manually. For a free hobby site this is enough.

**Sign-in:** Email magic link or Google sign-in, both supported by Supabase and Firebase. Avoid storing passwords yourself.

## 10. Monetisation

| Stream | When | How |
|---|---|---|
| Tips | Phase 1 onward | Ko-fi or Buy Me a Coffee link. Zero setup cost. |
| Game sponsorship | Once videos get consistent views | A supporter or brand pays to have their name on a game's title screen and in its launch video. Set a simple flat price per game. |
| Supporter subscription | Phase 3 | Monthly support via Ko-fi, Patreon or similar. Perks: name in credits, early access to new games, a vote that counts double, exclusive game modes. |
| YouTube | Ongoing | Channel monetisation once eligible. Long devlogs earn more than short clips. |

**Rules for keeping it fun:** No pay-to-win. Core games stay free. No intrusive ads in the middle of play.

## 11. Content plan

**Core story:** "I'm building an arcade website using AI, one game at a time, and you choose what I make next."

**Recurring video formats**

| Format | Platform | Length |
|---|---|---|
| Prompt to playable: the prompt, the first broken version, the fixes, the final game | TikTok, Reels, Shorts | 30 to 60 s |
| Beat my score: gameplay clip with a score to beat | TikTok, Reels, Shorts | 15 s |
| Vote for the next game: show 3 or 4 options, ask in the comments or a poll | TikTok, Instagram Stories | 15 s |
| Full devlog: the whole build of one game, start to finish | YouTube | 10 to 20 min |
| Milestones: first 100 players, first sponsor, first leaderboard | All | Short |

**The weekly loop**

1. Post a poll for the next game.
2. Build it, filming as you go.
3. Post short clips during the build.
4. Launch it on r3tro.io with a "beat my score" video.
5. Post the full devlog on YouTube.
6. Start the next poll.

**Tips:** Hook in the first second (show the game, not your face). Always show the score on screen. Put "r3tro.io" in your bio and on screen in every video. Reply to comments with video responses.

## 12. Game backlog

Candidates for the first polls. All are quick to build and easy to show in a short clip.

| Idea | Inspired by | Twist to make it original | Build effort |
|---|---|---|---|
| Snake game | Classic phone snake | Speed boosts and portals | Low |
| Brick breaker | Arkanoid-style games | Combo multiplier carried over from Shardfield | Low to medium |
| Block stacker | Falling-block puzzles | Built as Tumblewell: the well turns every 20 to 30 seconds | Done |
| One-tap flyer | Flappy-style games | Vector visuals, gravity flips | Low |
| Maze chaser | Pac-style games | Original characters and maze rules | Medium |
| Lane runner | Frogger-style games | Neon traffic, daily seeds | Medium |

Each game needs its own original name. Avoid naming or styling a game after an existing one.

## 13. Analytics

Use a privacy-friendly, cookie-free analytics tool such as GoatCounter or Plausible, so no cookie banner is needed. Track: visitors per day, games started, games finished, and which game is most played. Use these numbers in your milestone videos.

## 14. Legal and policy checklist

This is a general checklist, not legal advice. Check the rules where you live.

- **Trademarks:** Never use existing game names, characters or logos.
- **Privacy policy:** Required before collecting any personal data (accounts, emails, leaderboard names).
- **Children:** Games appeal to kids. If you add accounts, look up children's privacy rules (such as COPPA in the US and GDPR rules in the UK and EU), and consider requiring users to be 13 or older to sign up.
- **Sponsorship disclosure:** Label sponsored games and videos clearly (for example "#ad" or the platform's paid partnership tag).
- **AI disclosure:** Being open that the games are AI-built is part of the brand. Keep doing it.
- **Code licence:** Decide whether the repo is public with an open-source licence (MIT is common) or public but all rights reserved. GitHub Pages works either way on a public repo.

## 15. Success metrics

| Phase | Measure |
|---|---|
| 1 | Games live, followers, video views, daily visitors |
| 2 | Returning players, leaderboard submissions, accounts created |
| 3 | Monthly tips and sponsorship income vs. costs |

## 16. Open questions

- Which game wins the first poll?
- Free tier limits on the chosen leaderboard backend once traffic grows
- Whether to add a "suggest a game" form on the site
- Pricing for sponsorships and supporter tiers
