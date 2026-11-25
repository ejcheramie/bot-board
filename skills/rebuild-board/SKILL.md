# Rebuild the board

Use this whenever you update Bot Board: after a scheduled rebuild, after the owner asks for a refresh, or after a teammate push that should change a card.

## Fresh copy of the UI

The source of the board UI is this exact URL, not a packaged file:

https://raw.githubusercontent.com/ejcheramie/bot-board/main/board.html

Download it when you are doing first-time setup, when the local or Page copy is missing, or when the owner asks you to pull a UI update. The request must return HTTP 200. If it fails, retry once, then tell the owner and stop rather than inventing a substitute UI. After a download, re-apply the owner's existing CONFIG so customization is not wiped (columns, urgency, theme, badges, snooze, density, fields, groups, bots, and cards). For an ordinary card refresh, do not re-download; only rewrite CONFIG in the copy you already maintain.

## What you may change

Rewrite only the `CONFIG` block at the top of `board.html` (and the matching data if you also maintain a Page). When refreshing cards, keep the owner's customization already in CONFIG. Update the bot list, the timestamp, and the cards. Leave the UI code alone.

Urgency follows `CONFIG.urgency` (default: on, due within 48 hours, waiting more than 3 days). Card `col` values must match a key in `CONFIG.columns` (including any columns they added). Optional `card.badges` lists custom badge keys.

## Card shape

Each card needs a stable `id` (keep it the same across rebuilds so snooze and dismiss still work), `bot`, `botId` (for the chat link), `col` (`reminders` | `waiting` | `progress` | `blocked` | `done`), `title`, `summary`, `context` (array of short lines), and `next`. Optional: `group`, `money`, `schedule`, `since` (ISO with offset), `sinceBefore` (YYYY-MM-DD when only an upper bound is known), `due` (ISO with offset), `dueNote`, `links` (`title`, `site`, `href`).

Do not put secrets, passwords, card numbers, dates of birth, private keys, or raw mail / event / account identifiers in a card or link. Prefer a human title and, if needed, a link the owner already has in a bot chat.

## How to fill cards

Use teammate pushes, this bot's own notes, and what the owner told you. Do not invent a status. If a teammate did not report, leave their last honest card or drop it if the owner closed it.

Reminders are recurring until the owner removes them. Done is "done this week," not a permanent archive. Money items get `money: true` so the $ badge shows. Set `CONFIG.updated` to now in the owner's timezone.

## Delivery

- Update the Grok Bot Page in place when one exists. Remember the Page width limit: it may stay in a centered frame and not fill the window.
- If the owner chose a local HTML file, write the updated `board.html` to the path they named, and only that path. The file's refresh timer only reloads the tab; it does not wake you. Your rebuild routine is what refreshes the card data.
- Stay quiet after a scheduled rebuild unless something urgent is in Waiting on me, or the owner asked to be pinged.

## Safety

The board never sends, pays, books, posts, or files. If a card's next step is an outgoing action, the next step is "approve it in that bot's chat," not an action you take from the board.
