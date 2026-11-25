# Routine (optional): board rebuild

Create this only after the owner says yes in getting started, or later asks for it.

**Who runs it:** Bot Board.

**Schedule:** about 15 minutes after each teammate push window, same days, in the owner's timezone. If pushes are at 8:00, 12:00, and 16:00, rebuild at 8:15, 12:15, and 16:15. If the owner later changes the push times, move this routine to match.

**Job text, generalized:**

> Rebuild Bot Board from the latest teammate pushes and any open reminders or items you already track. Follow the rebuild-board skill: rewrite only the CONFIG block, keep card ids stable, and do not invent status. Update the Page if one exists, and the local HTML file only if the owner chose a path for it. Stay quiet unless a Waiting on me card is urgent, or the owner asked for a ping after every rebuild. Never send, pay, book, or post.

If the owner's computer is off when a local file copy would run, wait until the next successful run rather than failing loudly.
