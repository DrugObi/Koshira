# Handoff — Sito KOSHIRA

Stato del progetto al **30 settembre 2026**. Documento per chiunque prosegua il lavoro: sviluppatore, agenzia o una futura sessione.

> ⚠ **Questo documento sostituisce integralmente la versione del 20 settembre 2026.** In quella data il sito era progettato come e-commerce. Non lo è più: il 29 settembre il proprietario ha stabilito che sarà **solo una vetrina illustrativa**, con i prezzi indicati e un contatto WhatsApp per capire dove acquistare. Tutto l'impianto di vendita è stato smontato e diverse sezioni sono state rifatte. Le parti del vecchio handoff che parlano di carrello, checkout, recesso, spedizioni e pagamenti **non sono più valide**.

---

## 1. Cos'è il sito

KOSHIRA è un brand di eyewear di ispirazione giapponese. Dietro il marchio c'è la società **FRABEN S.r.l.** di Dalmine (BG).

Il sito è una **vetrina single-page statica**, pubblicata su GitHub Pages (`https://drugobi.github.io/Koshira/`, repo `drugobi/Koshira`). Presenta la collezione, mostra i prezzi consigliati al pubblico, e indirizza agli ottici rivenditori. **Non vende online**: niente carrello d'acquisto, niente pagamenti, niente spedizioni.

Il "carrello" esiste ancora ma è stato convertito in **selezione**: l'utente mette da parte i pezzi che gli interessano e con un pulsante apre WhatsApp con l'elenco già scritto.

---

## 2. File del progetto

Tutti i file stanno nella **root del repo**, senza sottocartelle — l'hosting lo richiede.

| File | Cosa contiene |
|---|---|
| `index.html` | Tutto il sito: markup, CSS e JS in un unico file (~90 KB) |
| `privacy.html` | Informativa privacy + cookie policy |
| `informazioni.html` | Dati societari, prezzi, dove acquistare, garanzia, conformità CE, marchi |
| `img-*.jpg` / `img-*.png` | Tutte le immagini, nomi appiattiti |
| `font-bodoni-moda.woff2` | Bodoni Moda ospitato in casa (42 KB, latino, pesi 400–500, licenza OFL) |
| `favicon.svg`, `favicon.ico`, `apple-touch-icon.png` | Monogramma KS bianco su nero, ricavato da `img-brand-symbol.png` |

⚠ **`condizioni.html` va cancellato dal repo** se è stato caricato: era il documento da e-commerce, sostituito da `informazioni.html`.

**Naming immagini (flat):**

- `img-<n>-1..3.jpg` — foto prodotto (n = cartella originale; 1 = frontale, 2 = tre quarti, 3 = dettaglio)
- `img-models-<id>.jpg` — 7 ritratti campagna
- `img-edit-1..9.jpg` — editoriali (1 = ruota, 5-8 filmstrip, 9 = still-life stella d'oro)
- `img-brand-*.png` — wordmark, logo-full, symbol
- `img-negozio-<slug>.jpg` — interni dei due negozi rivenditori
- `img-logo-<slug>.png` — loghi dei rivenditori, scontornati con trasparenza

⚠ Le foto prodotto e gli editoriali 5-8 non compaiono nel markup: vengono costruiti a runtime dal JS. **Devono comunque essere tutti presenti nel repo.**

⚠ `img-edit-2.jpg`, `img-edit-3.jpg`, `img-edit-4.jpg` **non sono più usati**: servivano al mosaico, che è stato rimosso. Si possono togliere dal repo.

⚠ `img-brand-symbol.png` non è più usato nella pagina, ma è la sorgente delle favicon: tenerlo.

---

## 3. Struttura della pagina

1. **Header fisso** — wordmark, nav, pulsante "Selezione" con contatore. `mix-blend-mode: difference`. Nav nascosta sotto i 720px, sostituita dal menu a pannello.
2. **Hero** — full viewport nero, logo, tagline, コシラ verticale.
3. **Marquee** — striscia scorrevole.
4. **Vetrine** (`#vetrine`) — sei pannelli verticali: cinque filtri sulle 22 combinazioni (Nero 10, Tartarugato 6, Sole 14, Vista 8, Trasparente 3 — Sole e Vista seguono la categoria della lente, vedi §5) più l'archivio. Fisarmonica in hover su desktop, nastro con snap sotto i 980px.
5. **Ruota cinetica** (`#wheel`) — la foto ruota dentro un oblò circolare.
6. **Collezione** (`#collezione`) — griglia 7 modelli + 1 tile editoriale decorativa.
7. **Trova la tua forma** (`#trova`) — quiz a 3 domande che consiglia un modello.
8. **Archivio** (`#archivio`) — scroller cinetico: le 22 combinazioni scorrono in orizzontale su un cilindro prospettico mentre si scrolla in verticale.
9. **La campagna** (`#campagna`) — **nuova**. Banda nera a tutta larghezza, i sette ritratti scorrono in loop orizzontale, nome sotto ogni volto. Si ferma in hover. Ha sostituito il mosaico.
10. **Storia** (`#storia`) — **rifatta**. Quattro movimenti separati da stanghette verticali, che si rivelano riga per riga allo scroll, più una chiusura in oro.
11. **La stella** (`#dettaglio`) — **rifatta**. Foto still-life dell'ottone su fondo carta senza cornice, testo a sinistra, kanji 星 in filigrana, colonna verticale 星・ほし sulla foto, e un riflesso che segue il cursore sul metallo.
12. **Costruisci il tuo** (`#banco`) — configuratore forma ✦ colore ✦ lente.
13. **Filmstrip** — 4 foto editoriali orizzontali.
14. **Dove trovarli** (`#dove`) — **nuova**. Due schede rivenditore: a riposo il logo su fondo carta, in hover la foto della vetrina scurita all'80% e la scheda che passa al nero.
15. **Footer** (`#contatti`) — コシラ in oro, wordmark, contatti, link legali, dati societari chiusi a soffietto.
16. **Overlay prodotto** (`#overlay`) e **drawer selezione** (`#drawer`).

---

## 4. Design token

| Token | Valore | Uso |
|---|---|---|
| `--nero` | `#0b0b0a` | Fondi scuri, testi |
| `--bianco` | `#ffffff` | Fondo pagina |
| `--carta` | `#f4f4f2` | Fondo tile e gallerie — identico al fondo delle foto prodotto |
| `--grigio` | `#6e6e6a` | Didascalie, note (5,4:1 su bianco) |
| `--linea` | `#e4e4e1` | Hairline |
| `--oro` | `#b08d3e` | Secondo accento: hairline archivio, barre, kana, etichette |
| `--serif` | Didot / Bodoni 72 / Bodoni Moda / Georgia | Solo la Storia e pochi numeri |
| `--titolo` | `var(--sans)` | **Tutti i titoli e le etichette** |
| `--sans` | system stack | Testi e UI |

**`--titolo` è una leva sola**: rimettere `--titolo: var(--serif)` riporta tutto il lettering a Didot senza toccare altro.

⚠ `--oro` su `--carta` non raggiunge il contrasto minimo (2,8:1): va usato per elementi grafici e micro-etichette, non per testo corrente.

La stella ✦ nella pagina non è più un carattere: uno script in fondo a `index.html` sostituisce ogni ✦ testuale con `<i class="st">`, una stella vettoriale disegnata in CSS (maschera SVG) che prende il colore del testo. Vale anche per i testi generati dal JS. Nei contenuti si continua a scrivere ✦ normalmente. Titolo, meta e messaggi WhatsApp restano col carattere, perché lì serve come testo.

I caratteri giapponesi (コシラ, 星, ほし) sono renderizzati dal font di sistema: Hiragino su Apple, Yu Gothic su Windows, Noto su Android. Nessun rischio di quadratini, ma la forma cambia. Per una resa identica ovunque servirebbe caricare Noto Serif JP.

---

## 5. Dati e listino

I dati vivono in `index.html` nell'array `const MODELLI`. Ordine vetrina, scelta del proprietario ("dal nero alla luce"):

Benè → Alone. → Robin → Anuar → Riri → Julian → Joel

### Prezzi

Listino consigliato al pubblico, stabilito dal proprietario il 30 settembre: **da vista € 350, da sole € 390, Robin € 450**.

```js
const LISTINO = { Vista: 350, Sole: 390 };
const lenteDi  = (m, v, fin) => fin !== 'unica' ? fin : (v.lente ?? m.lente);
const prezzoDi = (m, v, fin) => m.prezzo ?? LISTINO[lenteDi(m, v, fin)];
```

Il prezzo segue la **categoria della lente**. Le versioni `Vista`/`Sole` la dichiarano già nella chiave; le versioni `unica` la prendono dal campo `lente` — sul modello (Benè, Alone., Robin, Anuar: `Sole`) o sulla singola variante (Riri 03 Rosso trasparente e Joel 02 Cristallo: `Vista`, lente chiara). Robin scavalca il listino col proprio `prezzo: 450`.

La stessa funzione `lenteDi` alimenta le vetrine Sole/Vista, le etichette (" · Sole", " · Vista") in scheda, archivio, quiz, configuratore e selezione, e il messaggio WhatsApp ("da sole" / "da vista"). La chiave `unica` resta negli indirizzi (`#/bene/01/unica`), così i link già condivisi continuano a funzionare.

Tutti i prezzi sono dichiarati sul sito come **consigliati al pubblico**: il prezzo effettivo lo fa l'ottico. Il listino è scritto anche in `informazioni.html`, sezione Prezzi: se cambia, va aggiornato in entrambi i posti.

### Misure

Campo `misure` presente solo su **Riri** (56▫11 145) e **Anuar** (50▫22 145), dai disegni tecnici del produttore. Gli altri cinque modelli hanno il blocco nascosto. Servono: Benè, Alone., Robin, Julian, Joel.

---

## 6. Contatti e rivenditori

**WhatsApp**: `const WA = '393274436757'` in cima al blocco delle richieste. Due punti di ingresso:

- "Richiedi questo modello" nella scheda → apre WhatsApp con nome, codice, colore, finitura e link diretto alla combinazione (`#/riri/02/Sole`)
- "Chiedi dove provarli" nel drawer → manda l'elenco completo della selezione

**Rivenditori** (sezione `#dove`, dati anche in `informazioni.html`):

- **ItalianOptic** — Via Bergamo 32, 24035 Curno (BG) — 035 463950
- **Ottica Luce** — Via Abate Crippa 5/D, 24047 Treviglio (BG) — 0363 562450

Orari presi da Google e dichiarati come indicativi.

---

## 7. Impianto legale

Il sito è una vetrina, quindi **non si applicano** Codice del Consumo sulla vendita a distanza, diritto di recesso, SCIA per il commercio elettronico, né l'obbligo di accessibilità dell'European Accessibility Act (che copre i servizi che permettono di concludere un contratto online).

**Cosa c'è:**

- Dati societari in ogni footer, chiusi in un `<details>` nativo
- `privacy.html` — titolare, dati trattati, finalità e basi giuridiche, destinatari (GitHub, WhatsApp Ireland), trasferimenti USA, diritti, cookie policy. Google Fonts rimosso il 30 settembre: i font sono ospitati sul sito
- `informazioni.html` — società, prezzi consigliati, dove acquistare, garanzia legale 24 mesi, conformità DPI categoria I, marchi
- Nessun cookie di profilazione, quindi nessun banner necessario

**Cosa manca ancora:**

1. ~~REA, PEC, data di pubblicazione~~ — inseriti il 30/9: REA BG-490364, PEC frabensrl@namirialpec.it, pagine datate 30 settembre 2026. Nessun segnaposto `class="todo"` rimasto a video
2. Nome del **fabbricante** che firma la dichiarazione di conformità CE. Oggi il sito dice che la dichiarazione è disponibile su richiesta, che è sufficiente; la categoria del filtro è rimandata all'astina e alla nota informativa (prima diceva, falsamente, "nella scheda")
3. **Liberatoria** per le due foto dei negozi: non sono di Fraben. La foto ItalianOptic viene da un articolo, quindi il diritto potrebbe essere anche del fotografo o della testata
4. ⚠ Il **logo ItalianOptic** fornito porta la dicitura "**Trescore**", ma il negozio citato è quello di **Curno**: va chiesto il marchio senza città o quello della sede giusta

---

## 8. Mobile

Ottimizzato e verificato a 390 / 768 / 1500px: nessuno sforamento orizzontale, nessun errore a runtime.

- **Archivio**: sotto i 760px il rapporto di scorrimento scende da `0.68` a `0.40`, così la corsa obbligata passa da 5,1 a 3,4 schermate. Funzione `ratio()`, una riga.
- **Storia**: sotto i 720px le andate a capo forzate spariscono e il testo si impagina da solo. ⚠ I `<br>` hanno uno spazio dopo, indispensabile: senza, nascondendoli le parole si incollano.
- **Rivenditori**: su touch resta il logo e il nome resta nascosto, per non scriverlo due volte. Link telefono e mappe con area toccabile.
- **Campagna**: volti a 44vw, due per schermata.
- **Stella**: il kanji in filigrana si sposta a sinistra e si rimpicciolisce.

La pagina resta lunga — circa 18 schermate su telefono. È una vetrina da scorrere: la lunghezza fa parte del progetto. Se servisse accorciarla, il taglio sensato è il configuratore "Costruisci il tuo" (1,6 schermate), che è la quarta strada verso la stessa scheda prodotto.

---

## 9. Cosa è cambiato il 29 settembre 2026

**Correzione di sostanza.** Il sito diceva ovunque che la stella è "incisa sul frontale". È falso: è un **pezzo di ottone montato sulla cerniera**. Corretto in dodici punti — meta description, og e twitter, JSON-LD, descrizioni prodotto, sezione dettaglio, nota delle Vetrine, noscript. Su un sito che espone prezzi, una descrizione di prodotto non vera è una pratica commerciale scorretta, non solo un errore di copy.

**Da e-commerce a vetrina.** Rimossi checkout, flag di accettazione delle condizioni, riferimenti a spedizioni e recesso. Il carrello è diventato "Selezione", il totale "indicativo", il pulsante "Chiedi dove provarli". Aggiunta la nota "prezzo consigliato al pubblico" in scheda, drawer e pagina informazioni.

**Sezioni rifatte o nuove.** Storia riscritta e ricostruita (prima era testo provvisorio dichiarato tale a video). Sezione stella rifatta: prima diceva il falso e usava una lente col cursore poco riuscita. Mosaico **rimosso** e sostituito dalla Campagna. Sezione Dove trovarli **nuova**.

**Cose provate e scartate**, per non rifarle: una tavola tecnica quotata della stella disegnata a mano, e poi un profilo tracciato automaticamente dallo scatto e sovrapposto alla foto. Entrambe bocciate dal proprietario — la linea tracciata gli sembrava fatta male. La strada buona è risultata **foto e basta**.

**Altro.** Ricarica che riparte dall'alto (`scrollRestoration = 'manual'`, con eccezione se c'è un hash, per non rompere i link diretti). WhatsApp collegato. Loghi rivenditori scontornati. TikTok e capitale sociale rimossi dal footer. Dati societari a soffietto. Kana e kanji introdotti in footer e sezione stella. Prezzi a listino.

---

## 10. Cose rimaste aperte

**Da chiedere al proprietario:**

1. ~~REA, PEC, data~~ — fatto
2. ~~Prezzi~~ — fatto: listino per categoria
3. Misure di Benè, Alone., Robin, Julian, Joel
4. Logo ItalianOptic senza "Trescore"
5. Liberatoria per le foto dei negozi
6. **Origine del nome Koshira** — la Storia oggi si apre con il solo marchio, perché l'etimologia che era stata ipotizzata (こしらえる, "fare con le mani") non è confermata. Se una ragione esiste, è la materia migliore per quella sezione
7. Quale delle tre occorrenze di `img-edit-9.jpg` liberare: tile della collezione, pannello Archivio delle Vetrine, sezione stella

**Tecnico, in ordine di rapporto sforzo/risultato:**

8. **WebP/AVIF + `srcset`** — declassato: verificato il 30/9 che le foto prodotto pesano già 15–45 KB l'una, il guadagno non vale il raddoppio dei file. `width`/`height` aggiunti alle immagini statiche; quelle generate dal JS stanno già in contenitori con proporzioni fisse. Unico file pesante rimasto: `img-logo-italianoptic.png` (272 KB), da rifare comunque col logo senza "Trescore"
9. ~~Font self-hosted~~ — fatto il 30/9
10. ~~Stella come SVG~~ — fatto il 30/9
11. **Dominio / nuovo hosting** — 30 indirizzi assoluti puntano a `https://drugobi.github.io/Koshira/` (28 in `index.html`: canonical, og, twitter, JSON-LD; 1 canonical in ciascuna pagina legale). Col nuovo dominio: un solo trova-e-sostituisci su questa stringa nei tre file. Poi aggiungere `robots.txt` e `sitemap.xml`
12. **Analytics** — nessuno installato. Nota: le richieste WhatsApp arrivano col codice del modello dentro, quindi dopo qualche settimana si sa già quali pezzi interessano davvero, senza installare niente
13. ~~Favicon~~ — mancavano davvero nel repo (tre 404 a ogni visita): create il 30/9
14. ~~Twitter card~~ — passata a `summary`, adatta all'immagine quadrata

**Contenuti e asset:**

15. Testi definitivi delle descrizioni modello (sono bozze scritte guardando le foto)
16. Foto Riri "lente sabbia" — mai ricevute
17. Foto dedicate per le sei Vetrine: oggi usano i ritratti campagna, e il pannello "Tartarugato" mostra un modello che nella sua foto porta il nero
18. Passaggio a **WhatsApp Business**: messaggio di benvenuto, orari, etichette, e soprattutto il profilo col nome del brand

---

## 11. Cosa è cambiato il 30 settembre 2026

Solo interventi tecnici, nessun cambiamento visibile al disegno:

- **Font in casa**: via i tre collegamenti a Google Fonts, Bodoni Moda servito dal sito con `@font-face` e `preload`. Il sito non contatta più nessun server terzo al caricamento. Aggiornata di conseguenza `privacy.html` (tolto Google dai destinatari, dai trasferimenti e dalla cookie policy; "carrello" → "selezione").
- **Stella vettoriale** ovunque (vedi §4). Verificato: 68 stelle convertite, zero rimaste come carattere, anche dopo aggiunte alla selezione.
- **Favicon** create.
- **Twitter card** → `summary`.
- `width`/`height` su logo hero, wordmark footer, loghi rivenditori, più `height:auto` nella regola base `img`. Misurato: dimensioni a video identiche a prima, a 390 e 1500px.

---

### Secondo giro, stesso giorno

- **Listino per categoria** (vedi §5), REA, PEC e data inseriti in footer, privacy e informazioni.
- **Bug corretto**: il configuratore "Costruisci il tuo" metteva in selezione i pezzi **senza prezzo** (usava il campo `prezzo` del modello, vuoto per tutti tranne Robin), quindi drawer e totale mostravano "— €".
- **Vetrine Sole/Vista**: prima contavano solo le versioni con doppia lente, quindi la vetrina Sole escludeva Benè, Alone., Robin e Anuar, che sono tutti da sole. Ora Sole 14, Vista 8.
- **JSON-LD**: Benè, Robin e Anuar erano classificati "da vista", corretti in "da sole"; Riri, Julian e Joel "da vista e da sole".
- **Selezione salvata**: chiave passata da `koshira-cart-v1` a `koshira-cart-v2`, così nessun visitatore si ritrova in selezione pezzi salvati coi prezzi vecchi. Aggiornata anche la cookie policy.
- **Verifica completa** a 390, 768 e 1500px: zero errori JS, zero risorse mancanti, zero chiamate a server esterni al caricamento, zero ID duplicati, zero ancore rotte, nessuno sforamento orizzontale. Testati i link diretti di tutte le combinazioni, prezzi in scheda, aggiunta dalla scheda e dal configuratore, messaggi WhatsApp singolo e da selezione. Il sito funziona anche senza `img-edit-2/3/4.jpg`.

---

## 12. Nota di metodo

Il proprietario preferisce scambi essenziali: poche iterazioni, materiale in blocco, e decisioni prese invece che domande di conferma. Se una sezione non gli piace, la strada giusta è **rifarla o toglierla**, non chiedere quale delle due.

Gusto preciso: anteprime sempre frontali, ordine cromatico della vetrina, casting internazionale, foto editoriali usate come decorazione. Rifiuta le soluzioni "morte" — griglie regolari senza gerarchia, immagini forti trattate come foto prodotto. Chiede che ogni sezione abbia **una idea forte ma ordinata**: l'asimmetria sì, lo sfalsamento no. Le direzioni cinetiche e interattive sono benvenute, l'esecuzione dev'essere pulita.

Un'indicazione emersa lavorando: quando una soluzione grafica generata automaticamente sembra approssimativa, va buttata subito. Meglio una foto sola ben messa che un disegno che non regge.
