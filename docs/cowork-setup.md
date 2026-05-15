# Cowork Automation — Intelligence Briefing

## Panoramica

Workflow automatizzato che produce ogni mattina il briefing di intelligence
su 5 dossier energetici e geopolitici, partendo dalla rassegna stampa ricevuta via Gmail.

## Flusso tecnico

```
[06:30] Gmail — Arrivo rassegna stampa (Michele Cozzolino)
    ↓
[07:00] Cowork — Trigger automatico "Intelligence Briefing"
    ↓
[07:01] Lettura email + estrazione testo rassegna
    ↓
[07:02] Chiamata Claude API con:
         - system prompt (prompts/system-prompt-briefing.md)
         - rassegna stampa come input
         - dossier attivi come contesto
    ↓
[07:05] Strutturazione output in 5 sezioni emoji-coded
    ↓
[07:06] Creazione bozza Gmail
    ↓
[07:07] Invio via Chrome → inbox Massimo
    ↓
[07:30] Lettura e uso nel workflow mattutino
```

## Configurazione Cowork

### Workflow: "Intelligence Briefing"
```yaml
nome: Intelligence Briefing
trigger: scheduled
orario: 07:00
giorni: lun-ven

passi:
  1. gmail_read:
       mittente: michele.cozzolino@opengateitalia.com
       oggetto_contiene: "rassegna"
       ultimi_n_giorni: 1
  
  2. claude_api:
       model: claude-sonnet-4-20250514
       system: [vedi prompts/system-prompt-briefing.md]
       input: {testo_email}
  
  3. gmail_draft:
       destinatario: m.micucci@opengateitalia.com
       oggetto: "Intelligence Briefing — {data_oggi}"
       corpo: {output_claude}
  
  4. chrome_send:
       azione: invia_bozza
```

### Workflow parallelo: "Rassegna Stampa"
```yaml
nome: Rassegna Stampa
trigger: scheduled
orario: 08:00
giorni: lun-ven

note: >
  Versione semplificata — legge email Michele Cozzolino,
  include calendario del giorno, segnala eventi 10ª Commissione
  e keyword A.S. 1836 / EUMR / SGI.
```

## Fallback manuale

Se Cowork non è disponibile:

1. Aprire Gmail → trovare rassegna stampa di Michele
2. Copiare il testo
3. Aprire Claude (claude.ai)
4. Incollare il prompt da `prompts/system-prompt-briefing.md`
5. Aggiungere il testo della rassegna
6. Copiare output → inviare a se stessi via Gmail

## Troubleshooting

| Problema | Causa probabile | Soluzione |
|----------|----------------|-----------|
| Briefing non arriva | Rassegna non pervenuta | Verificare Gmail Michele |
| Output malformato | Prompt cambiato | Ripristinare da questo file |
| Errore Chrome send | Sessione scaduta | Riaprire Chrome e ripetere |
| API timeout | Rassegna troppo lunga | Dividere in 2 chiamate |

