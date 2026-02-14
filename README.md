# atem

**interface for thinking**

a 3D spatial thought-mapping tool. thoughts are spheres in space. tap to create, drag to move, hold to connect.

---

## features

- **zero friction capture** — persistent + button for instant thought entry
- **spatial organization** — 3D canvas with full pan/rotate/zoom via OrbitControls
- **folders** — lightweight categorization with tab-based filtering
- **connections** — hold-drag between thoughts to link them, tap lines to delete
- **lasso select** — hold-drag on empty space to select and batch-assign to folders
- **color control** — 8-color palette per thought
- **PWA** — offline-first, installable on iOS/Android
- **dev tools** — built-in export/import, state dump, orphan finder, fps counter

---

## architecture

- **single-file PWA** — `index.html` is the entire app (no build step, no modules)
- **Three.js** — loaded via CDN importmap for 3D rendering
- **localStorage** — state persists under key `'atem-state'`
- **service worker** — caches assets for offline use

---

## local development

just open `index.html` in a browser. no dependencies, no server needed.

for live reload during dev, use any static server:
```bash
python3 -m http.server 8000
# or
npx serve
```

---

## deployment

deploy to Vercel, Netlify, GitHub Pages, or any static host. the entire app is in `index.html` + two icon PNGs + manifest/service worker.

**important:** the app must be served over HTTPS for PWA features (service worker, install prompt) to work.

---

## state structure

```js
{
  thoughts: [
    { id, text, position: [x,y,z], color, folder, created, touched }
  ],
  connections: [
    { id, from, to, created }
  ],
  folders: ["work", "personal", ...],
  activeFolder: null,  // null = show all
  camera: { px, py, pz, tx, ty, tz },
  openToCapture: false
}
```

---

## controls

**tap** empty space → create thought  
**tap** thought → edit  
**drag** thought → move  
**hold** thought → start connection, drag to target  
**tap** connection line → delete  
**hold** empty space → lasso select (batch folder assign)  

**zero button** (bottom center) → quick capture overlay  
**tray button** (bottom left) → menu  

---

## constraints

- do not split into modules
- do not add a build step
- do not add npm dependencies
- keep single-file architecture
- Three.js via CDN importmap only
- state must remain in localStorage under `'atem-state'`

---

## known issues / todo

- [ ] search/filter thoughts by text
- [ ] undo/redo
- [ ] connection labels/notes
- [ ] keyboard shortcuts
- [ ] mobile: 3-dot menu still broken on some iOS browsers (known event race)

---

## license

MIT
