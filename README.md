# Music Relationship Graph

An interactive, read-only graph for exploring relationships between musicians, bands, albums, labels, and more. Hosted on GitHub Pages; data lives in `relationships.csv` — edit the CSV and push to update the graph.

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

Upload both files to the repo root:
- `index.html` — the app
- `relationships.csv` — your data

You can drag and drop them via the GitHub web UI, or use git:

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

After a minute or two, your app will be live at the URL shown. After that, every push to `main` automatically updates the live site within ~30 seconds.

---

## Editing data

All editing is done directly in `relationships.csv`. Open it in any text editor, Numbers, or Excel, make your changes, and push to GitHub.

### CSV format

```
from,from_type,relationship,to,to_type,notes
Dean Wareham,person,was a member of,Galaxie 500,band,1987–1991
Galaxie 500,band,released,On Fire,album,1989
Rough Trade,label,released,On Fire,album,
Mark Kramer,producer,produced,On Fire,album,
```

| Column | Description |
|---|---|
| `from` | Name of the source node |
| `from_type` | Type of the source node (see below) |
| `relationship` | Label shown on the connecting edge |
| `to` | Name of the target node |
| `to_type` | Type of the target node |
| `notes` | Optional extra info shown in brackets |

### Node types

The following types have predefined colours and shapes. You can use any other word as a type — it will be auto-assigned a colour.

| Type | Shape | Colour | Use for |
|---|---|---|---|
| `person` | circle (small) | red | Musicians, individuals |
| `band` | circle (large) | yellow | Bands, groups, duos |
| `album` | diamond | purple | Releases, EPs, singles |
| `label` | square | blue | Record labels |
| `producer` | triangle | orange | Producers |
| `engineer` | triangle | green | Recording/mixing engineers |

To add a new type (e.g. `venue`, `manager`, `festival`), just use it in the CSV — it will appear automatically with an auto-assigned colour.

### Tips

- **The same node can appear many times** as a source or target — it's always treated as the same node as long as the name matches exactly (case-insensitive).
- **Commas in names**: wrap the value in double quotes, e.g. `"Crosby, Stills & Nash"`
- **Reload button**: the app has a `↺ reload` button in the header — useful after pushing changes if you have the page open.
- **Running locally**: open with a simple server (`python3 -m http.server` then visit `localhost:8000`) rather than opening `index.html` directly, as browsers block local file fetches.

### Adding new node type styles

To customise the colour or shape of a new type, edit the `NODE_TYPES` object near the top of `index.html`:

```javascript
const NODE_TYPES = {
  venue:   { color: '#ff6b9d', shape: 'hexagon', size: 11, label: 'Venue' },
  manager: { color: '#a8e6cf', shape: 'square',  size: 10, label: 'Manager' },
  // ... existing types
};
```

Available shapes: `circle`, `diamond`, `square`, `triangle`, `hexagon`
