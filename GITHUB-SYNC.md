# GitHub live sync for Tonight's Tasks

Everyone opens the same GitHub Pages (or repo) URL. The board is stored in **`board.json`** in the repo. The page **polls every ~3 seconds** and **saves changes** through the GitHub API.

---

## How it works

```text
Your browser  --pull-->  board.json on GitHub  <--push--  teammates
                 (every 3s)                    (when you change tasks)
```

| Who | Needs token? |
|-----|----------------|
| **View + complete / add tasks** | Yes — so saves can write `board.json` |
| **View only** | No — can still pull latest (read-only) |

---

## Setup (once)

### 1. Put these files in your repo

- `index.html` (the app)
- `board.json` (empty starter — already included)

Enable **GitHub Pages** (Settings → Pages → Deploy from branch → `/` or `/docs`).

Your site will look like:

```text
https://YOURUSER.github.io/YOURREPO/
```

### 2. Create a Personal Access Token

1. GitHub → **Settings → Developer settings → Personal access tokens**
2. Prefer **Fine-grained token**:
   - Resource owner: you
   - Repository access: **Only select** this bingo repo
   - Permissions → Repository → **Contents: Read and write**
3. Generate and **copy** the token (`github_pat_…` or `ghp_…`)

> Do **not** commit the token into the repo or paste it into `index.html`.  
> Each person stores it only in their browser via **Connect GitHub**.

### 3. Each team member connects (once per browser)

1. Open the live Pages URL  
2. Click **Connect GitHub**  
3. Confirm:
   - Owner = your GitHub username (or org)
   - Repo = repository name  
   - Path = `board.json`  
   - Branch = `main` (or `master`)  
4. Paste the **token**  
5. **Save & Connect**

Status should show: **`Live · GitHub · [time]`**

The first save creates/updates `board.json` in the repo (you'll see commits like *Update Tonight's Tasks board*).

---

## Day-to-day use

1. Everyone uses the **same Pages URL**  
2. Leave the tab open  
3. Add / complete tasks as usual  
4. Changes save to GitHub automatically  
5. Others see them within a few seconds (poll)  
6. Click **Pull Latest** anytime to force refresh  

---

## Security notes

- Token stays in **localStorage on that browser only**
- Use a **fine-grained** token limited to **one repo**
- If the site is public, never put the token in the HTML source
- Revoke the token anytime in GitHub settings if it leaks

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| 401 / 403 on save | Token missing, expired, or lacks Contents write |
| 404 board.json | Connect with token and add a task (creates the file) |
| Owner/repo wrong | Check Connect GitHub fields; must match the Pages repo |
| Updates slow | Normal ~3s; click Pull Latest |
| Merge conflict | App retries with merge; if stuck, Pull Latest then edit again |
| Rate limit | Use a token (much higher limits than anonymous) |

---

## Admin password

Still **`salem1692`** for the 🗝️ admin chamber (add task / reset).  
GitHub token is separate — it's only for writing `board.json`.
