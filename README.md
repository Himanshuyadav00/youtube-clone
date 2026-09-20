# Pulse YouTube Clone

Pulse is a responsive YouTube-style discovery website. It uses the official YouTube Data API v3 for live search, thumbnails, channel names, view counts, durations, dates, category browsing, and pagination. Playback uses the official YouTube embed player.

## Included

- Responsive desktop and mobile layout
- Live YouTube search
- Music, live, travel, technology, documentary, podcast, and design discovery tabs
- Video metadata loaded from the YouTube API
- Official YouTube player modal
- Load-more pagination
- Keyboard-friendly buttons and Escape-to-close playback
- A small real-YouTube fallback feed when the API key is not available, so the site never displays a missing-API error
- GitHub Actions deployment to GitHub Pages

## Local setup

Requirements: Node.js 20 or newer and npm.

```bash
npm install
cp .env.example .env.local
npm run dev
```

Open `http://localhost:5173/` in a browser.

## Enable the live API

1. Open [Google Cloud Console](https://console.cloud.google.com/).
2. Create or select a project.
3. Enable **YouTube Data API v3** under **APIs & Services**.
4. Create an API key under **Credentials**.
5. Put the key in `.env.local`:

```env
VITE_YOUTUBE_API_KEY=your_api_key_here
```

6. Restart the Vite server.

Restrict the key by HTTP referrer in Google Cloud. For local development, allow `http://localhost:5173/*`. For GitHub Pages, allow `https://himanshuyadav00.github.io/youtube-clone/*`.

The key is used by browser requests, so it must be restricted. Never commit `.env.local` or place an unrestricted key in the repository.

## Deploy to GitHub Pages

The workflow at `.github/workflows/deploy.yml` deploys automatically whenever `main` receives a push.

1. In the repository on GitHub, open **Settings > Secrets and variables > Actions**.
2. Create a repository secret named `VITE_YOUTUBE_API_KEY`.
3. Paste the restricted Google API key as its value.
4. Open **Settings > Pages** and set the source to **GitHub Actions**.
5. Push to `main` or run **Deploy to GitHub Pages** from the Actions tab.

The deployed URL is:

`https://himanshuyadav00.github.io/youtube-clone/`

## Commands

| Command | Purpose |
| --- | --- |
| `npm run dev` | Start the local development server |
| `npm run build` | Create the production bundle in `dist/` |
| `npm run preview` | Preview the production bundle locally |

## Project structure

| Path | Purpose |
| --- | --- |
| `src/main.js` | YouTube API client, state, rendering, search, filters, and player |
| `src/style.css` | Responsive visual design |
| `index.html` | Browser entry document |
| `vite.config.js` | Vite and GitHub Pages base path |
| `.github/workflows/deploy.yml` | Automated GitHub Pages deployment |
| `.env.example` | Required environment variable template |

## API and account scope

This project intentionally uses public YouTube Data API requests and the official embed player. Subscriptions, likes, comments, personalized recommendations, watch history, and channel management require a Google OAuth flow and additional server-side security. They cannot be safely implemented with a public API key alone.