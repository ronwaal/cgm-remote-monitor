# Nieuwe Nightscout setup met MongoDB Atlas en Render

Deze handleiding is bedoeld voor een nieuwe, schone Nightscout-site voor read-only glucoseweergave op Garmin Edge 840 en Garmin Enduro 3.

## Veiligheidsprincipe

Deze setup is uitsluitend bedoeld als extra displaylaag. De Garmin-weergave vervangt nooit de Medtronic MiniMed 780G, MiniMed Mobile, CareLink, SmartGuard/Auto Mode of je eigen diabetesprotocol.

Gebruik deze setup nooit voor:

- pompbesturing
- insulinedosering
- bolusadvies
- automatische behandeling
- wijzigingen aan SmartGuard/Auto Mode

## Doelarchitectuur

```text
Medtronic 780G + Guardian 4 / Simplera
→ MiniMed Mobile / CareLink
→ Nightscout uploader/bridge, later te bepalen
→ Nightscout op Render
→ Garmin Connect IQ
→ Garmin Edge 840 + Garmin Enduro 3
```

## Stap 1 — MongoDB Atlas database maken

1. Maak een MongoDB Atlas-account aan.
2. Maak een nieuw cluster aan.
3. Maak een database user aan, bijvoorbeeld `nightscout`.
4. Gebruik een lang uniek databasewachtwoord.
5. Gebruik dit wachtwoord niet voor Medtronic, CareLink, Garmin, Gmail, GitHub of API_SECRET.
6. Zet network access veilig. Voor Render kan tijdelijk brede toegang nodig zijn, maar beperk dit later waar mogelijk.
7. Kopieer de connection string.

De string lijkt op:

```text
mongodb+srv://nightscout:<DATABASE_PASSWORD>@<CLUSTER_HOST>/nightscout?retryWrites=true&w=majority
```

Bewaar deze string alleen in Render Environment Variables. Commit hem nooit naar GitHub.

## Stap 2 — Render web service maken

Maak in Render een nieuwe web service aan via Docker image of blueprint.

Image:

```text
nightscout/cgm-remote-monitor:latest
```

Gebruik environment variables uit `.env.example`.

Verplicht handmatig in Render invullen:

```text
MONGODB_URI=<jouw MongoDB Atlas connection string>
API_SECRET=<lang uniek Nightscout secret van minimaal 12 tekens>
```

Gebruik geen echte secrets in `render.yaml`, `.env.example`, README, screenshots of commits.

## Stap 3 — Nightscout openen

Na succesvolle deployment geeft Render een URL zoals:

```text
https://jouw-nightscout.onrender.com
```

Open deze URL en maak het profiel aan.

Aanbevolen profiel:

```text
Timezone: Europe/Amsterdam
Units: mmol/L
Low warning: 4.5 mmol/L
High warning: 13 mmol/L
```

## Stap 4 — Eerste validatie

Controleer:

- De site opent via HTTPS.
- Units staan op mmol/L.
- De site is niet publiek schrijfbaar.
- `AUTH_DEFAULT_ROLES=denied` staat actief.
- Er staan geen echte secrets in GitHub.
- De Nightscout URL is bekend.

## Stap 5 — Uploader/bridge later kiezen

Voor Medtronic 780G + Guardian 4/Simplera moet de uploader/bridge apart worden gekozen en getest. De oude `minimed-connect-to-nightscout` route is waarschijnlijk legacy en moet niet automatisch als geschikt voor 780G/Simplera worden beschouwd.

Te verifiëren routes:

- CareLink follower via xDrip+ op Android bridge
- actuele community bridge voor 780G/Guardian 4/Simplera
- iOS-only route indien bewezen betrouwbaar

## Wat je niet moet delen

Deel nooit in chat, GitHub of screenshots:

- `API_SECRET`
- `MONGODB_URI`
- MongoDB password
- CareLink gebruikersnaam/wachtwoord
- Medtronic credentials
- Garmin credentials
- tokens

## Definitie van gereed voor Garmin

Nightscout is pas gereed voor Garmin als:

1. De URL werkt via HTTPS.
2. De site mmol/L gebruikt.
3. Er actuele glucosewaarden binnenkomen.
4. Laatste meting zichtbaar jonger is dan 10 minuten.
5. Oude data herkenbaar is als stale/no data.
6. De gekozen Garmin Connect IQ datafield getest is op Edge 840 en Enduro 3.
