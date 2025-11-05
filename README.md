# StarGazer

Star Gazer Star Gazer is an interactive web app that lets users explore the night sky from any point in time and space. Whether you’re curious about what the stars looked like on your birthday, during a historical event, or at a future date, Star Gazer brings the cosmos to your fingertips. The app provides: 🌠 Real-time celestial visualization – view constellations, planets, and stars as they appeared at a chosen date and location. ♈ Astrological insights – discover zodiac constellations and horoscope alignments associated with specific times. 🗺️ Interactive map interface – easily select global locations and times using an intuitive, responsive design. 📱 Educational and personal use – perfect for astronomy enthusiasts, students, or anyone interested in the connection between the stars and human experience. Built with modern web technologies for performance and clarity, Star Gazer aims to make stargazing accessible, visual, and meaningful — all from your browser.

## Prerequisites

- Node.js 18+
- npm 9+ (or pnpm/yarn if preferred)
- Google Maps JavaScript API key with Maps JavaScript enabled
- Running StarGazer backend at `http://localhost:5000`

## Getting Started

1. **Install dependencies**
   ```bash
   npm install
   ```
   > If your network restricts direct npm registry access, configure an internal proxy or mirror before installing.

2. **Environment variables**
   Create a `.env` file based on `.env.example` and set your keys:
   ```dotenv
   VITE_GOOGLE_MAPS_API_KEY=
   VITE_API_BASE_URL=http://localhost:5000
   ```
   `VITE_API_BASE_URL` is optional—when omitted the dev server proxies `/api` to `http://localhost:5000`.

3. **Start the dev server**
   ```bash
   npm run dev
   ```
   Open the printed URL (default `http://localhost:5173`). Requests to `/api` are proxied to the Flask backend to avoid CORS issues.

4. **Build for production**
   ```bash
   npm run build
   npm run preview
   ```

## Folder Structure

```
src/
  components/     # Reusable UI building blocks (maps, cards, navbar, etc.)
  context/        # React context for shared location + visibility state
  data/           # Mock constellation list until backend support lands
  lib/            # API client, formatting helpers, and utilities
  pages/          # Routed screens (landing, minimized map, fullscreen map)
  styles/         # Tailwind globals and design tokens
```

## Key Features

- Dark, star-field themed landing page with coordinate form, validation, and geolocation support.
- Debounced visibility fetching with persistent coordinates, twilight setting, and optional observation time.
- Minimized home layout listing planets, moon data, mocked constellations, and a Google Maps preview with fullscreen toggle.
- Fullscreen map view that triggers refetches on drag-end and surfaces summary details alongside exit control.
- Accessible components with focus states, semantic markup, and responsive design down to 375px widths.

## API Integration

Visibility data is loaded from `GET /visible` on the Flask backend. All requests use the persisted location, elevation, twilight selection, and optional ISO time. Errors surface inline with retry actions, and all request bursts are debounced (~320 ms) to keep the backend responsive.

## Assumptions

- Google Maps is the preferred visualization layer per the mockups; other map providers were not considered.
- Constellation visibility is mocked because the backend does not expose that data yet.
- Observation time is optional; clearing the field reverts to "current time" using backend defaults.
- Default coordinates center on Charlotte, NC (matching the provided mockups) when no saved location exists.

## Acceptance Criteria Checklist

- [x] `npm install` (with registry access) and `npm run dev` launch the Vite dev server.
- [x] Landing page form validates inputs, supports browser geolocation, and routes to the minimized home view.
- [x] Minimized home view displays planet/moon data and mini map with fullscreen control.
- [x] Fullscreen view expands the map, allows drag-to-update coordinates, and preserves state when exiting.
- [x] Changing twilight or observation time debounces API requests and refreshes visibility data.
- [x] Location, twilight, and time persist via `localStorage` across refreshes.
- [x] UI remains usable on mobile and desktop breakpoints.

## Troubleshooting

- **CORS errors** – Ensure the Vite dev server is running with the default proxy or set `VITE_API_BASE_URL` to the backend origin.
- **Google Maps errors** – Verify the API key has Maps JavaScript access and is loaded in the `.env` file.
- **Rate limiting** – The API client aborts in-flight requests when new parameters arrive to prevent overload.

## Contributing

1. Fork and branch from `main`.
2. Run `npm run lint` before opening pull requests.
3. Provide screenshots for significant UI changes.

# Vision
FOR individuals who are fascinated by the night sky, astrology, and the connection between cosmic events and personal meaning, WHO want an accessible and visually engaging way to explore how the stars and planets aligned at specific moments in time, THE Star Gazer is an interactive web application that allows users to visualize celestial arrangements and discover astrological insights for any chosen date and location. UNLIKE traditional astronomy software or generic horoscope websites, OUR PRODUCT combines real-time astronomical data with elegant, user-friendly design to create an immersive experience that bridges science, art, and personal reflection.