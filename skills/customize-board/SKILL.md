# Customize the board

When the owner asks to change how the board looks or works, follow this skill. Do not rewrite the UI code. Change the `CONFIG` block at the top of `board.html` (and the matching Page, if one exists), then rebuild. Keep card ids stable.

## Visual vs structural

**Gear / Settings panel** (the owner can do these themselves; you can also set them in CONFIG as the new baseline): theme (Auto, Light, Dark, Custom), accent color, card color, background, font, density (comfortable or compact), card fields (age, deadline, group, sources), the $ badge, swimlanes, default filter, header logo, title, refresh (the top-right timer; `00:00:00` is off), and the default snooze length. These stick in the browser when `CONFIG.persistPrefs` is true (the default). Settings has **Reset to defaults**, which clears those tweaks and leaves snoozed or dismissed cards alone.

**CONFIG, which you edit on request:** columns (rename, reorder, hide, add, colors), urgency rules, custom badge definitions, group colors, snooze defaults, and any visual keys they want baked in so a later rebuild does not lose them.

## How to edit

Change only `CONFIG`. Afterward, update the Page if there is one and the HTML file only at a path they named. If a setting also lives in the gear panel, tell them they can change it there too. If they have not asked to change a value, leave it. Shipped defaults match the original board: five columns, gold accent, comfortable density, urgency of 48 hours / 3 days, snooze until midnight, $ badge on, swimlanes off.

## Common requests

- **Rename Blocked to Stuck:** set that column's `label`. Keys stay the same so existing cards still land there.
- **Add a Someday column:** append `{ key: "someday", label: "Someday", color: "#7B4FC9", ink: "#ffffff" }` to `CONFIG.columns`. Use a unique `key`. New cards use `col: "someday"`.
- **Hide Done:** set `hidden: true` on that column. Do not delete it if cards still use the key.
- **Reorder or recolor columns:** reorder the `columns` array, or set each column's `color` and optional `ink`.
- **Make urgent 24h:** `CONFIG.urgency.dueWithinHours = 24`. Waiting-more-than is `waitingMoreThanDays` (default 3). Set `enabled: false` to turn both rules off.
- **Add a badge for legal items:** push `{ key: "legal", label: "LEGAL", color: "#7B4FC9", keyword: "legal" }` onto `CONFIG.badges.custom`. The badge shows when the keyword appears in the card text or `card.badges` includes the key. `CONFIG.badges.money = false` hides the $ badge.
- **Compact mode:** `CONFIG.density = "compact"`. Comfortable is the default.
- **Change accent to green:** set `CONFIG.theme.accent` (for example `#2e8b57`) and `CONFIG.theme.preset` to `"custom"` if this should be the baseline. Dark and Light presets stay available in the theme control and in Settings.
- **Hide age or deadlines:** `CONFIG.fields.age` or `CONFIG.fields.deadline` (also `group`, `sources`) set to `false`.
- **Swimlanes by group:** `CONFIG.swimlanes = true` (off by default).
- **Default filter Work:** `CONFIG.defaultFilter = "work"` (or `"all"` or `"today"`).
- **Title or header logo:** `CONFIG.title`, and `CONFIG.showHeaderLogo = true` to show `CONFIG.logo` beside the title (off by default).
- **Snooze length:** `CONFIG.snooze.default` is `"midnight"` (current), `"1h"`, `"4h"`, `"morning"`, or `"custom"` with `customHours`. The drawer always offers a menu of those lengths. `morningHour` is 9 by default.
- **Refresh:** `CONFIG.refresh.enabled` and `intervalSec` (default 900). The timer in the top-right can still override this in the browser.

## Safety

Do not put secrets in CONFIG. The board still never sends, pays, or books.
