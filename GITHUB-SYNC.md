# GitHub live sync + mobile

## Deploy (important)

Replace **`index.html`** on GitHub with the latest from `Desktop\BingoCard\index.html`.  
Also keep **`board.json`** in the repo root.

Hard-refresh on phone: Safari → close tab → reopen, or Chrome → wipe cache for the site.

## Public page vs admin

| Public | Admin (🗝️ password `salem1692`) |
|--------|-----------------------------------|
| Bingo card, complete tasks | Add / reset tasks |
| Live status line | **Connect GitHub**, Pull, Export/Import |

## Connect token (mobile)

1. Create fine-grained PAT: Contents **Read and write**, only this repo  
2. Copy token **immediately**  
3. Open site → 🗝️ → password → **Connect GitHub**  
4. Owner / repo / `board.json` / branch  
5. **Paste** token (field is plain text so mobile paste works)  
6. Save & Connect  

Token is cleaned of spaces/zero-width chars and validated before use.

## Multi-user sync behavior

- Completions are sticky (won’t undo if two people work at once)  
- New tasks from everyone are kept  
- Reset bumps `boardGeneration` so old tasks don’t return  
- Pushes merge remote first, then write (retries on conflict)  
- Debounced + serialized saves (better on mobile double-taps)  
- Pulls when tab becomes visible again / back online  

## Optional hardcode (same board local + Pages)

In `index.html`:

```javascript
const GITHUB_DEFAULTS = {
  owner: "YourUser",
  repo: "YourRepo",
  path: "board.json",
  branch: "main",
  pollMs: 3500,
};
```

## Never put a token in the HTML file
