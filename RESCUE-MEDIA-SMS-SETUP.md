# Rescue Media + Country-Wise SMS Setup

## Media
Rescue reports accept a photo or short video, with a live camera preview on supported HTTPS/mobile browsers. Photos are compressed in-browser. Camera video recording is limited to 15 seconds, and large clips are rejected before upload.

## Country routing
The backend reverse-geocodes the rescue coordinates to an ISO 3166-1 alpha-2 country code and then loads active operators from `server/rescue-operators.json` or the path supplied by `RESCUE_OPERATOR_FILE`.

The current configured project contact for Bangladesh is the Purrfect Pantry Rescue Desk at `+8801755800203`. Other countries intentionally have empty operator lists until verified animal-care/rescue contacts are added.

## SMS
The backend supports either:
- a generic SMS gateway using `SMS_API_URL`, `SMS_API_KEY`, `SMS_SENDER_ID`
- optional Twilio Messaging API using `TWILIO_ACCOUNT_SID`, `TWILIO_API_KEY`, `TWILIO_API_SECRET`, plus `TWILIO_FROM` or `TWILIO_MESSAGING_SERVICE_SID`

Credentials stay on the backend. The frontend contains no SMS secrets.

## Production routing behavior
When a rescue is submitted through the API, the server detects the country, matches active operators in that country, stores attached media, and sends an alert to each matched operator when an SMS provider is configured. The response reports how many operators matched and how many alerts were successfully sent.

If no SMS provider is configured, the rescue request is still stored, but the system explicitly reports that no SMS was sent.

## Geocoding
The default detector uses Nominatim with a one-request-per-second throttle for uncached reverse lookups and an identifying User-Agent. For larger or commercial deployments, use a dedicated or self-hosted geocoder rather than depending on the public Nominatim service.

## Deployment
For GitHub Pages, publish the storefront files as the static site and deploy the `server/` backend separately. In production, keep `.env` and the operator registry outside the public webroot when possible, and set `RESCUE_OPERATOR_FILE` to that private path.
