# Rail Dash: rules for Claude

Read this at the start of every session. These are the owner's standing rules for this project. Follow them every time, without being asked.

## Every change
1. **Save it to GitHub.** Commit every change, to the game and to the debug stage, on `main` and run `git push origin main`. The remote URL pins the Doctram user on purpose, so leave it as it is.
2. **Change the debug stage to match.** Every change to the main game must also show up on the debug stage. If a boss, attack or animation changes (for example Scyrus), update its debug scene too, so the debug version always plays exactly like the real game. The stage runs the same game code, so most changes carry over by themselves. Scenes that set up a moment by hand, such as "Molgrath with 1 core left", must be updated whenever the thing they set up changes. Then open the scene and check that it still works. This is for finished changes only. Experiments follow rule 6.
3. **Add a debug scene for anything new.** New bosses, attacks and animations get their own entry in `DEBUG_TRIGGERS` in `index.html`. Number keys 0-9 are all used, so new scenes need letter keys (not W, A, S, D or P). C, F, G, H, I, J, K, L, N and R are taken. So are -, +, [ and ] (tuning keys), ` (folds the panel) and Esc (stops the scene). The "Rail Dash (Debug)" desktop shortcut opens this same `index.html` with `?debug`, so it updates by itself.
   Every new debug command follows the pattern of "Demon smash from the arm raise" (key 2): one entry in `DEBUG_TRIGGERS` with a key, a label and a `play()` that starts the attack, partway through if that helps. Commands that change a tuning value use the same entry shape, add `again()`, and work like key 3: press the key once to watch, and press it again to step to the next value. The label shows the current value.
4. **Explain it simply.** The owner uses this project to learn. After each change, explain what changed and how it works, like a short lesson.
5. **Remember new rules.** When the owner says "remember this" or gives a lasting rule, add it to this file and push it.
6. **Experiments stay in debug until the owner says so.** The owner uses the debug version to try out ideas and polish them before they go in the game. A change made for the debug stage, or one the owner is still tuning, must not reach the real game until the owner says to put it there (for example "put it in the game"). Since debug and the real game run the same code, gate the experiment behind debug mode with a named flag, such as `EXP.scyCharge` that is on only when `DEBUG.on`, so a normal run keeps the old version. Still commit and push the experiment. When the owner approves it, remove the gate. If you are unsure whether a change is an experiment or meant for the game, ask. Never merge a branch or push work into the real game that the owner has not approved. (Rule added 2026-11-27, after an unfinished Scyrus charge reached the real game.)

## Every time you write code
1. **Keep it one file.** The whole game is `index.html`: one classic script inside an IIFE, with three.js r128 loaded from cdnjs. Don't split it into modules or add build tools.
2. **Follow the existing patterns.** Bosses share one system: `bossDur`, `bossPhase`, `updateBoss` and `animateBoss` branch on `BOSS.kind`. Extend that instead of building a parallel system. Do the same for other features: find how similar things are already done and copy that shape.
3. **Name your numbers.** Put timings, speeds and sizes in named constants near the related code, such as `MOL_DUR` or `SOLO`, not as bare numbers inside logic.
4. **Comment in plain English.** Write short comments that say what the code does in the game, such as "he keeps running and can't be hurt", so a learner can follow them.
5. **Don't break saves.** Saved progress lives in localStorage (`rd-save2`). Never rename stored ids, such as `switchman` (shown to players as The Conductor). Change display text only. Any new saved field needs a safe default for old saves.
6. **Never let the game freeze or crash.** Guard against missing data the way `bossDur` does: log an error and fall back to a safe value.
7. **Keep it fair.** Every hazard needs a warning the player can react to. Fire rings must stay more than 0.64 s apart, the jump's airtime. The guitar solo must stay under 1.3 s. The Conductor's Shunt Charge shows its yellow stripe for 0.4 to 0.5 s before it turns red, and it charges three times in a row (`SW_SHUNT`).
8. **Check before you push.** After editing, parse the script to catch syntax errors. Then test the change in Chrome when you can.
9. **Change only what was asked.** If you notice another problem, mention it instead of fixing it quietly.

## Project facts
- There are no powers and no coins. The track power-ups, the shop powers and coins were all removed on 2026-11-23. Every outfit is free. Don't add any of these back unless the owner asks.
- Bosses: Molgrath, Scyrus and The Conductor. They take turns through `BOSS_ORDER`.
- Debug mode: `?debug`, Ctrl+Shift+D, or the debug desktop shortcut. Debug keys open a practice stage where nothing can hurt you.
- Testing in Chrome: the extension can't open file:// pages, so serve the folder with a small local node server. The game clamps each frame to 50 ms (`frame()`), and it pauses when the tab loses focus.
