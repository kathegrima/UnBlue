# ⚡ UnBlue

> Trasforma il blu in energia.

**UnBlue** è un sito motivazionale gratuito pensato per combattere il **Blue Monday** — il lunedì più pesante dell'anno — e ogni giornata no. L'utente descrive cosa lo blocca o lo pesa, e riceve un messaggio motivazionale personalizzato, scritto con tono umano e empatico.

🌐 **Live:** [tuonome.github.io/unblue](https://tuonome.github.io/unblue)

---

## Come funziona

1. L'utente sceglie una categoria (Lavoro, Studio, Energia…) e scrive cosa sta affrontando
2. Il frontend invia il messaggio a un **Cloudflare Worker**
3. Il Worker chiama l'**API Google Gemini** con un prompt ottimizzato
4. La risposta viene mostrata in una bubble nella pagina

```
Browser (GitHub Pages) → Cloudflare Worker → Google Gemini API
```

La chiave API non è mai esposta al browser — vive nelle variabili d'ambiente del Worker.

---

## Stack

| Layer | Tecnologia |
|---|---|
| Hosting | GitHub Pages |
| Frontend | HTML + CSS + JS vanilla (zero dipendenze) |
| Backend/Proxy | Cloudflare Workers (free tier) |
| AI | Google Gemini 2.5 Flash-Lite |

---

## Struttura del repo

```
/
├── index.html       # Tutto il frontend (singolo file)
└── unblue.jpg       # Logo
```

---

## Deploy

### 1. Fork e GitHub Pages
1. Fai fork di questo repo
2. Vai su **Settings → Pages** → Source: `main` / `root`
3. Il sito è live su `https://tuonome.github.io/unblue`

### 2. Cloudflare Worker
1. Crea un account su [cloudflare.com](https://cloudflare.com)
2. Vai su **Workers & Pages → Create → Start with Hello World**
3. Incolla il contenuto di `worker.js` nell'editor
4. Clicca **Save and deploy**
5. In **Settings → Variables and Secrets** aggiungi:
   - Nome: `GEMINI_API_KEY`
   - Tipo: **Secret**
   - Valore: la tua chiave da [aistudio.google.com/apikey](https://aistudio.google.com/apikey)

### 3. Collega il Worker al frontend
In `index.html` cerca questa riga e sostituisci con l'URL del tuo Worker:

```javascript
const WORKER_URL = 'https://tuo-worker.tuo-account.workers.dev/';
```

---

## Limiti gratuiti

| Servizio | Limite gratuito |
|---|---|
| GitHub Pages | Illimitato |
| Cloudflare Workers | 100.000 req/giorno |
| Gemini 2.5 Flash-Lite | 1.000 req/giorno |

---

## Privacy

I messaggi degli utenti vengono elaborati da Google Gemini tramite API. Con il **free tier** di Google AI Studio, i dati potrebbero essere usati per il miglioramento dei modelli. Nessun dato viene salvato da UnBlue. Per disabilitare il data training, attiva la fatturazione su Google AI Studio.

---

## Cos'è il Blue Monday?

Il **Blue Monday** cade il terzo lunedì di gennaio ed è considerato il giorno più depressivo dell'anno, secondo una (discussa) formula che combina meteo, debiti post-natalizi, fallimento dei buoni propositi e ore di luce ridotte. UnBlue esiste per ricordare che ogni lunedì può diventare un punto di partenza.

---

## Licenza

MIT — libero di usare, modificare e condividere.
