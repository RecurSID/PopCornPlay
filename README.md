# PopcornPlay

PopcornPlay is a lightweight, open-source movie and TV browser for personal use. It uses [TMDB](https://www.themoviedb.org/) for catalog data and [VidFast](https://vidfast.vc/) for embedded playback. The frontend has no framework or build step; a small Vercel function keeps the TMDB key out of the browser.

## Features

- Trending, popular, now-playing, and top-rated titles
- Movie and TV search
- Responsive VidFast movie and episode playback
- Season and episode selection
- PostMessage play, pause, mute, and status controls
- Local continue-watching history with automatic resume
- Responsive interface with no frontend dependencies

## Run locally

You need Node.js 18+ and a free [TMDB API key](https://developer.themoviedb.org/docs/getting-started).

```bash
npm install
```

Create `.env.local` in the project root:

```env
TMDB_API_KEY=your_tmdb_api_key
```

Then start the Vercel development server:

```bash
npm run dev
```

Open the local URL printed in the terminal.

## Deploy to Vercel

Import the repository into Vercel, add `TMDB_API_KEY` in **Project Settings → Environment Variables**, and deploy. `vercel.json` already routes `/api/tmdb/*` through the serverless proxy.

## VidFast integration

PopcornPlay uses the current endpoints:

```text
https://vidfast.vc/movie/{id}?autoPlay=true
https://vidfast.vc/tv/{id}/{season}/{episode}?autoPlay=true
```

The ID may be from TMDB or IMDb. Player settings are in `PARAMS` near the top of the script in `public/index.html`. VidFast also supports `startAt`, `server`, `hideServer`, `fullscreenButton`, `chromecast`, and `sub`; PopcornPlay adds `startAt` automatically when saved progress exists.

Incoming PostMessage events are accepted only from documented VidFast origins. `MEDIA_DATA` events are stored under `vidFastProgress` in browser localStorage, so PopcornPlay watch history stays on the device. Use **Clear history** or clear site data to remove it.

## Structure

```text
public/index.html  Frontend, styles, and player integration
api/tmdb.js        Allowlisted TMDB API proxy
vercel.json        Vercel route configuration
```

## Notes

- This project does not host, upload, or index video files.
- TMDB data is used under TMDB's terms. This project is not endorsed or certified by TMDB.
- Playback availability and content are controlled by the configured embed provider.
- You are responsible for complying with applicable laws and service terms.

## Contributing

Issues and pull requests are welcome. Please keep changes small, dependency-light, and suitable for personal deployments.

## License

Released under the [MIT License](LICENSE).
