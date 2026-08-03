# KOSHIRA — Sito e-commerce

Sito single-page statico. **Tutti i file su un solo livello, nessuna sottocartella.**
`index.html` + tutte le immagini (`img-*.jpg` / `img-*.png`) nella stessa cartella.

## Deploy su GitHub

1. Crea un repository su github.com.
2. Carica **tutti** i file di questa cartella nella root del repo
   (index.html + tutti gli img-*.*). Essendo tutti allo stesso livello,
   l'uploader web di GitHub li accetta trascinandoli insieme.
3. Settings → Pages → Source: Deploy from a branch → main → / (root).
4. Il sito sarà su https://<utente>.github.io/<repo>/

Il file `.nojekyll` evita il processing Jekyll di Pages.

## Naming immagini
- `img-<n>-1..3.jpg` — foto prodotto (n = cartella originale)
- `img-models-<id>.jpg` — ritratti campagna
- `img-edit-1..9.jpg`   — editoriali (9 = stella)
- `img-brand-*.png`     — logo / wordmark / simbolo

## ⚠ Prima della produzione
- Pubblicare su Pages rende il sito **visibile a chiunque**.
- Checkout dimostrativo (alert), prezzi a "— €".
- Mancano link social e pagine legali.
