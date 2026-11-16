# Someday Binder

A read-later memo keeper. Say or type what you found and what you'd use it for, file it under a tab, and mark what you're waiting on (time, money, or the right setup). Installs to an Android home screen from Chrome, works offline, and shows up in the share sheet.

The app is a handful of static files with no build step. Memos save on the device and, once connected, sync to a file called `memos.json` in a private GitHub repo you own.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole app |
| `manifest.webmanifest` | Makes it installable and adds it to the Android share sheet |
| `sw.js` | Keeps the app available offline |
| `icon-*.png` | Home screen icons |
| `memos-starter.json` | Optional first memo. Goes in the private repo, not this one |

## Setup

### 1. Publish the app (public repo)

Free GitHub Pages needs a public repo. This repo holds only the app code. No memos and no token ever go in it.

1. Create a new **public** repo, for example `someday-binder`.
2. Add `index.html`, `manifest.webmanifest`, `sw.js`, and the three `icon-*.png` files to the top level. Leave `memos-starter.json` out.
3. In the repo, open **Settings > Pages**, set the source to **Deploy from a branch**, pick `main` and `/ (root)`, and save. (That is GitHub's label for the setting.)
4. After a minute or two the app is live at `https://YOUR-USERNAME.github.io/someday-binder/`.

### 2. Create the memo store (private repo)

1. Create a new **private** repo, for example `someday-binder-memos`. Tick "Add a README" so it has a first commit.
2. Optional: upload `memos-starter.json` and rename it to `memos.json` to begin with the IPv6 memo. If you skip this, the app creates `memos.json` on the first sync.

### 3. Create an access token for that one repo

1. On GitHub, open **Settings > Developer settings > Personal access tokens > Fine-grained tokens** and choose **Generate new token**.
2. Under **Repository access**, choose **Only select repositories** and pick the private memo repo.
3. Under **Permissions > Repository permissions**, set **Contents** to **Read and write**. Leave everything else alone.
4. Pick an expiry you can live with. When it runs out, the app says so, and you paste in a new one.
5. Copy the token. GitHub shows it once.

### 4. Connect each device

1. Open the app's address in Chrome.
2. Scroll to **Sync and backup**, enter your GitHub username, the private repo name, and the token, then tap **Connect**.
3. On Android, open Chrome's menu and choose **Add to Home screen > Install**. After that, Someday Binder appears when you tap **Share** on an article in Chrome, Gmail, or a feed reader.
4. Repeat steps 1 and 2 on your desktop browser.

## Good to know

- **The token lives in each browser's storage on that device.** It can only touch the one private repo. If a device is lost, delete the token on GitHub and make a new one.
- **Sync happens** when you open the app, when you change something, when you come back online, and when you tap **Sync now**. If two devices edit the same memo, the most recent edit wins.
- **Offline is fine.** Memos save on the device first and go up on the next sync.
- **Backups:** `memos.json` is a plain file with full history in the private repo. **Save a backup file** in the app also downloads a copy.
- **Voice:** the **Talk it in** button uses Chrome's speech recognition. Where a browser doesn't offer it, use the microphone on the keyboard.
- **Updating the app:** replace the files in the public repo. If you change `sw.js` or the icons, bump `someday-binder-v1` in `sw.js` to `v2` so devices pick up the new files.
