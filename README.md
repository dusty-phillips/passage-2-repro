# Repro of passage 2 refresh token bug in svelte

My svelte app worked fine with passage-elements 1.21.6. However, after I
updated to passage-elements 2.0.2 and passage-js 4.0.1, refresh tokens stopped
working.

## Repro

- Create a passage app with refresh tokens enabled
- set the access token to expire every 30 seconds
- Change the app-id in [src/routes/+page.svelte](src/routes/+page.svelte) (in two places)
- `bun install && bun dev` (npm, yarn should work too)
- visit http://localhost:5173/
- log in
- wait 30 seconds
- refresh page
- see that you've been logged out

Watching the network tab, I don't see that passage-js ever tries to send the
refresh token to passage servers. According to the docs, it is supposed to do
this whenever you call `passage.session.refresh()` and should do it
automatically when you call `passage.currentUser.userInfo()`.

This behaviour worked in Passage 1.21.6.
