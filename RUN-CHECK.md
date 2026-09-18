# Local Run Check

## Storefront only
From this folder, run:

`python3 -m http.server 8080`

Then open:

`http://127.0.0.1:8080/`

The storefront is designed to remain usable without an API. Cart, search, reviews and local rescue markers use browser storage in this mode. Voicemail can be saved locally.

## API-enabled mode
From `server/`:

`npm install`
`npm start`

Then set `window.PANTRY_API_BASE` in `index.html` to the deployed API base URL. Configure SMS provider settings in `.env` for real OTP delivery.
