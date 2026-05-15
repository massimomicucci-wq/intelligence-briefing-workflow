# 📰 Intelligence Briefing Workflow

Sistema di **briefing quotidiano** su dossier energetici e geopolitici,
progettato per consulenti PA e analisti policy.
Basato su automazione AI (Claude/Anthropic) con delivery via Gmail.

---

## Struttura del briefing

Il briefing si articola in **5 sezioni emoji-coded**, in registro analyst:

```
⚡ ENERGIA & REGOLAZIONE
   EU Methane Regulation, MRV/OGMP 2.0, recepimento normativo IT

🌍 GEOPOLITICA & GAS
   Piano Mattei, corridoi TAP/SOCAR/Transmed, dinamiche LNG

🏛️ PARLAMENTO & ISTITUZIONI
   Commissioni, DDL tracking, nomine enti pubblici

📊 MERCATI & DATI
   Prezzi TTF, flussi gas, posizioni futures

📌 AGENDA & FOLLOW-UP
   Scadenze, incontri, azioni in sospeso
```

---

## Workflow tecnico

```
Gmail (rassegna stampa Michele Cozzolino)
    ↓
Claude API (elaborazione + sintesi)
    ↓
Struttura 5 sezioni
    ↓
Gmail Draft → Send via Chrome
```

---

## Template prompt

### Sistema
```
Sei un analista senior specializzato in energia, geopolitica e politica italiana.
Produci un briefing quotidiano sintetico in italiano, registro analyst,
senza filler, strutturato in 5 sezioni emoji-coded.
```

### Dossier attivi
- `EUMR` — EU Methane Regulation 2024/1787
- `PianoMattei` — Cooperazione energetica Italia-Africa
- `TAP_SOCAR` — Corridoio Sud del Gas, Azerbaijan
- `Hormuz_LNG` — Dinamiche stretto di Hormuz e mercato LNG
- `Parlamento_IT` — Monitoraggio 10ª Commissione Senato

---

## Configurazione Cowork

Il workflow è automatizzato tramite **Cowork** (desktop agent):

1. Legge email da mittente autorizzato (rassegna stampa)
2. Chiama Claude API con prompt strutturato
3. Genera bozza Gmail
4. Invia via Chrome

---

## Output di esempio

```
⚡ ENERGIA & REGOLAZIONE
Il Senato ha calendarizzato per giovedì 22 la discussione del DDL S.1836
(recepimento EUMR). La 10ª Commissione dovrebbe esprimere parere entro fine mese.

🌍 GEOPOLITICA & GAS
Tensioni nel Golfo: Qatar ha dichiarato force majeure su due contratti LNG spot.
TTF ha reagito con +4.2% nelle ultime 24h. Roma ancora priva di risposta strutturale.
[...]
```

---

## Licenza

MIT — libero utilizzo con attribuzione.
