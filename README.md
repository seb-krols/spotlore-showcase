# Spotlore

> Your photos already tell a story. Put them on the map.

<div align="center">
  <video src="https://github.com/user-attachments/assets/6728c599-b579-45e9-b057-73b8e29c7a65" autoplay loop muted playsinline width="80%"></video>
</div>

<div align="center">

[![Live App](https://img.shields.io/badge/Live%20App-spotlore.app-4F46E5?style=flat&logo=vercel&logoColor=white)](https://YOUR_VERCEL_URL_HERE)
[![Status](https://img.shields.io/badge/Status-Live-brightgreen)](https://YOUR_VERCEL_URL_HERE)

</div>

---

## What Is Spotlore?

Spotlore turns a folder of photos and a set of meaningful locations into a cinematic, interactive map tour — like a short film made from memories. Pin your places, upload your photos, pick a theme, and share a password-protected link. The recipient opens it and watches the map fly between each location with photos sliding in at every stop.

Built for the moments that matter: Valentine's Day gifts, anniversary compilations, travel diaries, exchange student adventures, proposals, family reunion memories, memorial tributes.

---

## How It Works

**Drop your pins** — Search for places by name, address, or postcode. Fine-tune coordinates with a draggable mini-map pin. Write captions, add dates, upload photos and videos.

**Make it yours** — Choose from 6 themes (Valentine, Anniversary, Travel, Backpacker, Road Trip, Nightlife) each with dark and light variants. Override accent colours until it feels exactly right.

**Send the link** — Set a password and share. They type it in, and the map flies through every memory — cinematic and sequential, or free exploration at their own pace.

<div align="center">
  <img src="https://github.com/user-attachments/assets/2bd0f3c0-5ed6-4ac0-9bdc-3f22c6a6bdee" width="80%" alt="Spotlore Tour Editor" />
</div>

---

## Two Viewer Modes

**Cinematic Mode** — Auto-plays a Mapbox flyTo sequence through every location. Distance-aware zoom logic means short hops stay close while cross-country jumps pull back for context. A photo panel slides in at each pin with the caption, date, and media slideshow. Keyboard shortcuts, touch/swipe navigation, progress bar, and a full-screen replay at the end.

**Interactive Mode** — All pins visible on the map at once. Click any pin to open a popup with the full photo set and location details. Next/prev navigation between stops. Explore in any order.

Tours set to "both" show a mode selector — the recipient chooses how they want to experience it.

<div align="center">
  <img src="https://github.com/user-attachments/assets/e2388f76-a3d6-4638-84b7-654db1c8b287" width="80%" alt="Spotlore Cinematic Viewer" />
</div>
---

## Architecture

41 source files across 8 route pages, 14 components, 4 custom hooks, and supporting libraries.

**Frontend** — Next.js 14 App Router with TypeScript. Eight routes: landing, login, signup, dashboard, editor, preview (presentation mode for screen recording), public viewer (`/t/[shareId]`), and an API verify endpoint. Error boundaries at app-wide and editor level.

**Backend** — Supabase handles everything: PostgreSQL with full Row Level Security, Storage for media files (MIME + extension whitelist enforced server-side), and Auth with email/password and Google OAuth. A single API route handles public viewer password verification via service role key, with rate limiting at 5 attempts per 15 minutes.

**Deployment** — Vercel for zero-config Next.js. Supabase free tier for DB and storage.

```
src/
├── app/
│   ├── page.tsx                   — Landing page
│   ├── dashboard/                 — Tour management
│   ├── editor/[tourId]/           — Tour builder
│   ├── preview/[tourId]/          — Presentation mode
│   ├── t/[shareId]/               — Public viewer (password gated)
│   └── api/tours/[shareId]/verify — Password check + tour data fetch
├── components/
│   ├── editor/                    — TourSettings, LocationEditor, MediaUploader, AutoSave
│   ├── viewer/                    — CinematicViewer, InteractiveViewer, PhotoPanel, Controls
│   └── shared/                    — PasswordGate, ThemeProvider
├── hooks/                         — useAutoSave, useTour, useMediaUpload
└── lib/                           — Supabase client/server, Mapbox config, theme system, types
```

---

## Tech Stack

| Layer | Tools |
|---|---|
| Framework | Next.js 14, TypeScript, App Router |
| Styling | Tailwind CSS |
| Maps | Mapbox GL JS v3 |
| Database + Auth | Supabase (PostgreSQL, RLS, Auth, Storage) |
| Deployment | Vercel |

---

## Editor Features

- Inline title editing (Canva-style, directly in the header)
- 6 themes × 2 variants (dark/light) with custom accent colour overrides
- Mapbox Geocoding place search — POIs, restaurants, addresses, postcodes
- Mini-map with draggable pin for coordinate fine-tuning
- Drag-and-drop location reordering with visual drop indicator
- Media upload with MIME whitelist, size validation, and progress tracking
- Auto-save with 2s debounce and live status indicator
- Undo for location delete (5s toast with one-click restore)
- Share dropdown with link copy, password toggle, click-outside-to-close
- `beforeunload` warning for unsaved changes

## Viewer Features

- Distance-aware flyTo zoom logic (short hops stay tight, long distances pull back)
- Photo panel slideshow with smooth slide-in transitions
- Autoplay with configurable stop durations per location
- Progress bar and step counter
- Keyboard shortcuts (Space, arrows, Esc) with on-screen hints
- Touch/swipe navigation for mobile
- Full-screen map on tour end with replay button
- Back-to-editor button on preview (creator only)
- View count tracking

## Security

- Rate limiting on password endpoint (5 attempts / 15 min)
- Input validation and maxLength on all fields
- File upload MIME + extension whitelist (jpg, png, webp, mp4, webm)
- RLS on all tables — users can only access their own data
- Error boundaries at app and editor level
- Middleware auth with graceful Supabase-down handling

---

## Free vs Pro

| Feature | Free | Pro |
|---|---|---|
| Tours | 3 | Unlimited |
| Locations per tour | 15 | Unlimited |
| Photos per location | 3 | Unlimited |
| Viewer modes | Interactive only | Cinematic + Interactive |
| Password protection | — | ✅ |
| Custom accent colours | — | ✅ |
| Presentation mode | — | ✅ |

---

## Origin

Spotlore started as a Valentine's Day gift — a single HTML file with a hand-coded cinematic map tour of 51 meaningful locations, delivered with flowers. The response made it obvious this should exist as a product anyone could build and send. This is that product.

---

## Status

Deployed to Vercel and live. Stripe integration and Pro tier in progress.

---

## This is a Showcase

This is a public showcase of a private repository. Source code is kept private — Spotlore is intended for commercial launch.

Interested in the project, want to collaborate, or just want to try it? Reach out.

---

## Contact

**Sebastian Krols**
[github.com/seb-krols](https://github.com/seb-krols) · [LinkedIn](https://www.linkedin.com/in/sebastians-krols/)

---

*© 2026 Sebastian Krols. All rights reserved.*
