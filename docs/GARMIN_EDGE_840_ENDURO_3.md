# Garmin Edge 840 en Garmin Enduro 3 setup

Deze handleiding beschrijft de gewenste Garmin-weergave voor Nightscout-glucosedata.

## Veiligheidsstatus

Garmin is een extra display. Gebruik Garmin niet als enige bron voor behandelbeslissingen. Bij twijfel, symptomen, alarmen of oude data controleer je altijd de Medtronic pomp en/of MiniMed Mobile.

## Vereisten

- Werkende Nightscout URL via HTTPS
- Glucosewaarden in mmol/L
- Actuele data jonger dan 10 minuten
- Garmin Connect app
- Garmin Connect IQ
- Garmin Edge 840
- Garmin Enduro 3

## Connect IQ datafields om te beoordelen

Beoordeel en test minimaal:

1. Nightscout DataField
2. CGM Datafield 2
3. CGM+ Datafield

Selectiecriteria:

- ondersteunt Nightscout URL
- werkt op Edge 840
- werkt op Enduro 3
- toont mmol/L
- toont trendpijl
- toont leeftijd van de meting
- toont duidelijke no-data of stale-status
- werkt tijdens activiteit
- heeft zo weinig mogelijk afleiding tijdens sport

## Edge 840 — hoofdscherm

Doel: glucose zichtbaar houden naast normale prestatievelden.

Aanbevolen velden:

```text
Glucose + trend
3s power of lap power
Hartslag
Snelheid
Afstand
Timer
```

## Edge 840 — Diabetes Safety scherm

Doel: één groot veiligheidsscherm dat je tijdens fietsen kort kunt checken.

Aanbevolen velden:

```text
Glucose groot
Trendpijl
Updateleeftijd / minuten sinds laatste meting
Delta indien beschikbaar
Hartslag
Vermogen
Timer
```

## Enduro 3 — hardloopscherm

Doel: beperkt, leesbaar en niet afleidend.

Aanbevolen velden:

```text
Glucose mmol/L
Trendpijl
Updateleeftijd
Hartslag
Pace of running power
Timer
```

## Waarschuwingsregels

Persoonlijke drempels:

```text
Laag: 4.5 mmol/L
Hoog: 13 mmol/L
Stale: ouder dan 10 minuten
```

Interpretatie:

- `LIVE`: laatste meting jonger dan 10 minuten
- `STALE`: laatste meting ouder dan 10 minuten
- `GEEN DATA`: geen actuele Nightscout-data beschikbaar

## Sportprotocol

Tijdens fietsen:

- kijk elke 10 tot 15 minuten kort naar Garmin
- bij dalende trend eerder handelen
- bij snel dalende trend intensiteit verlagen
- bij 4.5 mmol/L of lager: pomp/telefoon controleren en eigen diabetesprotocol volgen
- bij STALE of GEEN DATA: Garmin niet gebruiken voor beslissingen

Tijdens hardlopen:

- vaker checken bij tempo of intervallen
- dalende trend extra serieus nemen
- bij twijfel wandelen of stoppen en pomp/telefoon controleren

## Testprocedure

1. Controleer glucose op pomp.
2. Controleer glucose in MiniMed Mobile.
3. Controleer glucose in Nightscout.
4. Controleer glucose op Edge 840.
5. Controleer glucose op Enduro 3.
6. Vergelijk waarden en timestamps.
7. Noteer vertraging tussen systemen.
8. Test wat gebeurt bij geen internet of oude data.

## Niet gebruiken als

Gebruik Garmin niet als primaire bron als:

- de waarde ouder is dan 10 minuten
- er geen trendpijl is bij snel veranderende glucose
- je hypo-symptomen voelt
- pomp/telefoon een alarm geeft
- Nightscout offline is
- telefoonverbinding ontbreekt
