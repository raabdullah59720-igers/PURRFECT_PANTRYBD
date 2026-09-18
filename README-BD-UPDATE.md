# Purrfect Pantry Bangladesh Price + OTP Update

Built as an update to the existing fixed storefront.

Features: BDT pricing for all six launch products; central price API; admin price panel; Bangladesh mobile validation; OTP before order creation; OTP expiry, resend cooldown and attempt limits; server-side order totals; rate limiting; admin token.

## Price list in this build
Daily Adult Cat Food — ৳790 (display/previous ৳850)
Kitten Growth Recipe — ৳720
Indoor Cat Balance — ৳840 (display/previous ৳900)
Daily Budgie Seed Mix — ৳320
Premium Finch Blend — ৳360 (display/previous ৳390)
Bird Daily Essentials — ৳590

These are the existing launch-build prices, centralized for updating. They are not represented as live market quotations.

## Real OTP
The frontend is static and the OTP backend is in `server/`. GitHub Pages cannot securely run Node.js or store SMS credentials. Deploy `server/` to a Node.js backend host, set `PANTRY_API_BASE` in `index.html`, then configure `SMS_API_URL`, `SMS_API_KEY` and `SMS_SENDER_ID` for your chosen Bangladesh SMS provider. Never put the SMS API key in frontend code.

## Local test
`cd server` → `npm install` → copy `.env.example` to `.env` → set `NODE_ENV=development` and `ADMIN_TOKEN` → `npm start`. Without an SMS URL, development mode prints the OTP to the server console.


## Expanded food catalogue
The storefront now includes cat, dog, bird, fish, rabbit, hamster and treats categories. Prices are configurable launch prices in BDT and are not presented as an official government market-price feed.

## Search + SMS provider readiness
- A visible catalogue search field is available in the Shop section, with clear-search support and matching across product name, pet type, food type, flavour/description, brand and pack size.
- The existing header search control remains available and stays synchronized with the main catalogue search.
- SMS OTP provider settings remain intentionally blank in `server/.env.example` (`SMS_API_URL`, `SMS_API_KEY`, `SMS_SENDER_ID`) so a real Bangladesh SMS provider can be connected later without changing the checkout UI.
- Do not publish real API keys in the frontend. Configure SMS credentials only on the backend/server environment.
- Current catalogue prices are launch/store prices configured for this build, not a claim of an official government live-price feed.


## Final stability + cart pass
- Added a compact `assets/logo-mark.png` for mobile/header favicon use so the brand remains legible at small sizes.
- Restored the OTP verification UI expected by `script.js`; provider configuration stays blank until a real SMS service is selected.
- Upgraded the visible storefront control from Bag to Cart and verified quantity, remove, clear-cart, subtotal and localStorage flows in code.
- Product cards and product details both use the same Add to cart action path; Buy now adds the item and opens checkout.
- Dog and small-pet category shortcut buttons are wired.

## Customer Voice update
- Customer Voice now contains a written comment/review form and a live browser voice-mail recorder in the same section.
- Voice messages can be recorded, previewed, deleted, and sent to `/api/voicemails` when `PANTRY_API_BASE` is configured.
- On a GitHub Pages/static-only deployment, the Save voicemail action downloads the recording locally and keeps a lightweight local outbox record instead of pretending it reached the shop server.
- Optional customer name and Bangladesh phone number fields are supported for voice messages.
- Admin endpoints are available for reading recent reviews and voicemail metadata when the backend is protected with `ADMIN_TOKEN`.


## Rescue Center update
- Added a Rescue Center for injured or vulnerable cats, dogs and birds.
- Visitors can click the map or use browser geolocation to set a rescue marker.
- Each request stores animal type, urgency, description, optional contact details, place note, and coordinates.
- Active rescue markers are shown on the map with urgency-aware pins and a recent request list.
- Static GitHub Pages mode stores rescue requests locally in the browser. When `PANTRY_API_BASE` is connected, requests sync to `/api/rescues` for shared server-side visibility.
- Map uses a pinned Leaflet 1.9.4 client and OpenStreetMap tiles. The Leaflet client loads after the storefront starts, so a blocked/slow map library does not prevent the shop from opening. If the map library is unavailable, the form remains usable with manual coordinates.
- Public rescue responses intentionally omit reporter name and phone; protected admin rescue data retains them for the connected rescue team.
- Public rescue descriptions should not contain private or unnecessary personal information.

## 18 September 2026 final merge + QA
The latest Purrfect Pantry rescue/media/SMS-ready storefront build was used as the base. The new visual layer was added without removing the existing shop, cart, OTP checkout, review, voicemail, rescue media/camera, Leaflet map and backend files.

Added visual layer:
- Italian-inspired burgundy/gold treatment around the existing Purrfect Pantry logo
- LIVE MODE bar with Bangladesh time and refresh control
- Animated cat/dog/bird floating hero accents over the existing Mediterranean hero artwork
- Mobile-safe responsive behavior for the new live layer

The live bar is a storefront UI indicator. Actual OTP/SMS delivery, shared rescue synchronization and operator dispatch still depend on the configured backend/provider documented in the project setup files.


Final QA refresh: Small-pet shortcut now filters fish, rabbit, hamster and treats instead of opening the full catalogue. Browser storage calls are guarded individually so private-mode/quota failures do not break cart or review state.
