# Rail Dash: standing rules for Claude

These are the owner's standing rules for this project. Follow them on every change without being asked.

1. **Push every change.** Commit it on `main` and run `git push origin main`. The remote URL pins the Doctram user on purpose, so leave it as it is.
2. **Add a debug scene.** Whenever it makes sense (bosses, dragons, power-ups, attacks, animations), add an entry to `DEBUG_TRIGGERS` in `index.html` so the change can be watched on the practice stage. Number keys 0-9 are all used, so new scenes need letter keys.
3. **Keep the debug version current.** The "Rail Dash (Debug)" desktop shortcut opens this same `index.html` with `?debug`, so it updates by itself. Check that the debug scene for the change works.
4. **Explain simply.** The owner uses this project to learn, so explain each change like a short lesson.
5. **Don't break saves.** Internal ids such as `switchman` (shown to players as The Conductor) are stored in save data. Rename display text only.

## Project facts
- The whole game is one file, `index.html`: three.js loaded from cdnjs, one script inside an IIFE.
- Bosses: Molgrath, Scyrus and The Conductor. They take turns through `BOSS_ORDER`.
- Debug mode: `?debug`, Ctrl+Shift+D, or the debug desktop shortcut. Debug keys open a practice stage where nothing can hurt you.
