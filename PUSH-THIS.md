# Important: GitHub is showing an OLD page

If the live site still shows **Connect GitHub / Export / buttons under the card**, GitHub Pages is **not** using the latest `index.html`.

Your **local** file is already correct (admin only behind 🗝️). You must **replace** the file on GitHub.

## Push the latest file

1. Open your repo on GitHub  
2. Open `index.html`  
3. Click the pencil **Edit** (or upload a new file)  
4. Delete everything in that file  
5. Copy **all** of `Desktop\BingoCard\index.html` from your PC and paste it  
6. Commit: `Update bingo board UI and sync`  
7. Also add/update **`board.json`** in the repo root if it’s missing  

Or from Git (if you use git locally):

```bash
git add index.html board.json
git commit -m "Hide admin tools; fix multi-user GitHub sync"
git push
```

## After push

1. Wait 1–2 minutes for GitHub Pages  
2. Hard refresh the live site: **Ctrl+F5** (or open in a private window)  
3. You should **only** see the bingo card + progress + small 🗝️  
4. No Connect GitHub bar at the bottom  

## Same board local + GitHub

1. 🗝️ → `salem1692` → **Connect GitHub** (token once)  
2. After that, **local file** and **Pages URL** both use the same `board.json`  
3. Optional: hardcode owner/repo in `index.html` under `GITHUB_DEFAULTS` so detection always works  

```javascript
const GITHUB_DEFAULTS = {
  owner: "YourUser",
  repo: "YourRepo",
  path: "board.json",
  branch: "main",
  pollMs: 3000,
};
```

Then push that file again.
