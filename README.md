# Housie

A mobile-friendly Housie (Tambola) game for office teams. Everything is in a single `index.html` file with no build step.

## How to play

1. **Host:** open the page, tap **Host the game** and share the 4-letter game code.
2. **Players:** open the page on their phones, tap **Join as player** and enter their name and the code to get a unique ticket.
3. The host taps **Draw number**. Voice calling and auto-draw are optional.
4. Players tap numbers on their ticket to mark them. When a pattern is complete, they claim it (or shout "Housie!").
5. The host types the player's name under **Check ticket**. The same ticket is rebuilt from the name and code, and the page shows whether the claim is valid or a bogey.

**Prizes:** Early Five, Top Line, Middle Line, Bottom Line, Four Corners, Full House.

## Hosting

- **GitHub Pages:** in Settings → Pages, set the source to the `main` branch, root folder. The game will be live at `https://<user>.github.io/housie/`.
- **Locally:** open `index.html` in any browser.

## Notes

- Tickets are generated from **game code + player name**. The same spelling always gives the same ticket, so the host can verify claims without a server.
- Live sync between phones (called numbers, claims and auto-mark) only works when the page is opened as a Claude artifact. Hosted anywhere else, the game runs standalone: players listen to the host's calls and mark their tickets by hand.
- Game progress and ticket marks are saved in each browser's local storage.
