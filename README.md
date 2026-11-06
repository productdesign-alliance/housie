# Housie

A mobile-friendly Housie (Tambola) game for office teams. It's a single `index.html` with no build step, and it can sync phones live through Firebase.

## How to play

1. **Host:** open the page, tap **Host the game** and read out the 4-letter game code.
2. **Players:** open the same link on their phones, tap **Join as player** and enter their name and the code to get a unique ticket.
3. The host taps **Draw number**. Every player's phone shows the number live, with voice calling and auto-draw as options.
4. Players tap numbers to mark them, or turn on **Auto-mark**. When a pattern is done, they tap **Claim**.
5. The claim pops up on the host's screen. Tap **Verify** to see whether it's valid or a bogey, then **Award** it. The player's phone shows the result.

**Prizes:** Early Five, Top Line, Middle Line, Bottom Line, Four Corners, Full House.

## One-time setup: live sync with Firebase (about 5 minutes, free)

1. Go to <https://console.firebase.google.com>, click **Add project**, name it `housie` and turn Analytics off.
2. In the left menu, open **Build → Realtime Database → Create database**. Pick the **Singapore** location and choose **Start in test mode**.
3. Open the **Rules** tab, paste the rules below and click **Publish**:
   ```json
   {
     "rules": {
       "games": {
         ".read": true,
         ".indexOn": ["state/updated"],
         "$code": { ".read": true, ".write": true }
       }
     }
   }
   ```
4. Click the ⚙️ **Project settings** gear. Under **Your apps**, click the **Web `</>`** icon, register an app called `housie` (no hosting needed) and copy the `firebaseConfig` object.
5. Paste it into `firebase-config.js`:
   ```js
   window.HOUSIE_FIREBASE = {
     apiKey: "…",
     authDomain: "…",
     databaseURL: "https://….firebasedatabase.app",
     projectId: "…",
     // …the rest of the config
   };
   ```
   `databaseURL` is required. If it's missing from the config, copy it from the top of the Realtime Database page.

The free Spark plan allows 100 phones connected at once, which is plenty for office games. A Firebase web config isn't a secret, so it's fine to commit it.

## Hosting on GitHub Pages

In **Settings → Pages**, set the source to the `main` branch, root folder. The game will be live at `https://productdesign-alliance.github.io/housie/`.

## Notes

- Tickets come from **game code + player name**. The same spelling always gives the same ticket, so the host can rebuild any ticket to check a claim.
- Without Firebase config, the game still works without live sync: players listen to the host and mark their tickets by hand.
- Progress and marks are also saved on each phone, so refreshing the page doesn't lose anything.
- **Auto-cleanup:** a game is deleted from Firebase 30 minutes after the host's last activity. The host screen keeps its game alive while it's open, and the cleanup runs whenever anyone opens the page (Realtime Database has no built-in expiry on the free plan).
