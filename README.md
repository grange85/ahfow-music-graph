# Music Relationship Graph

An interactive graph for mapping relationships between musicians, bands, and artists. Data is stored as a CSV file in this repository and loaded/saved directly via the GitHub API.

## Live app

Once GitHub Pages is enabled, your app will be at:
```
https://grange85.github.io/ahfow-music-graph/
```

---

## Setup

### 1. Create the repository

- Go to [github.com/new](https://github.com/new)
- Name it something like `music-graph`
- Set it to **Public** (required for the free GitHub Pages tier)
- Click **Create repository**

### 2. Upload the files

Upload both files from this folder to the repo root:
- `index.html` — the app
- `relationships.csv` — your data

You can drag and drop them into the GitHub web UI, or use git:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main
```

### 3. Enable GitHub Pages

- Go to your repo → **Settings** → **Pages**
- Under *Source*, select **Deploy from a branch**
- Choose **main** branch, **/ (root)** folder
- Click **Save**

After a minute or two, your app will be live at the URL shown.

### 4. Generate a Personal Access Token

The app needs a token to read and write `relationships.csv` on your behalf.

- Go to [github.com/settings/tokens/new](https://github.com/settings/tokens/new)
- Give it a description like `MusicGraph`
- Select the **`public_repo`** scope (or `repo` if your repo is private)
- Click **Generate token** and copy it — you won't see it again

> **Fine-grained tokens** also work: grant *Read and write* access to *Contents* for your specific repo.

### 5. Connect the app

- Open your app in the browser
- Click **⚙ GitHub** in the top-right
- Fill in your username, repo name, branch (`main`), and paste your token
- Click **Save & Connect**

The app will immediately load your `relationships.csv` and show a **↑ Save to GitHub** button. Every time you click save, it commits the updated CSV to your repo.

---

## Data format

`relationships.csv` is a plain CSV file you can also edit directly in GitHub or any spreadsheet app:

```
from,from_type,relationship,to,to_type,notes
Dean Wareham,artist,was a member of,Galaxie 500,band,1987–1991 co-founder
Naomi Yang,artist,was a member of,Galaxie 500,band,1987–1991
Dean Wareham,artist,founded,Luna,band,1991 after Galaxie 500 broke up
```

**Columns:**

| Column | Values | Notes |
|---|---|---|
| `from` | any name | Person or band |
| `from_type` | `artist` or `band` | Controls node colour |
| `relationship` | any text | Label shown on the edge |
| `to` | any name | Person or band |
| `to_type` | `artist` or `band` | Controls node colour |
| `notes` | any text | Optional — shown in brackets on the edge and in the inspector |

---

## Tips

- **Bulk editing**: Export CSV from the app, edit in a text editor or Numbers/Excel, paste back and Import, then Save to GitHub.
- **Direct GitHub edits**: Edit `relationships.csv` directly on GitHub, then reload the app and click ⚙ GitHub → Save & Connect to pull the latest version.
- **Version history**: Every save creates a git commit, so you have a full history of changes you can roll back to from the GitHub Commits view.
- **Token security**: Your token is stored in your browser's `localStorage` and is never sent anywhere except the GitHub API. It is **not** included in the repository.

---

## Privacy note

If your repo is **public**, anyone can read `relationships.csv` — but only someone with your token can modify it. If you want the data to be private, create a **private** repo and use a token with the full `repo` scope instead of `public_repo`.
