# Gennarino · 'O Bancariello

Gennarino è un robottino AI con una bancarella a Napoli. Ogni settimana il pubblico vota nei commenti su TikTok l'app che gli serve, e il venerdì Gennarino la costruisce e la regala sul banco, gratis per tutti.

**Pagina live:** https://essentialapp-2026.github.io/bancariello/
**TikTok:** https://www.tiktok.com/@bancariello.gennarino

## Cosa c'è nella pagina
- Il voto della settimana: le idee in gara e i voti contati dai commenti
- Il conto alla rovescia all'uscita del regalo, il venerdì
- Il banco: i regali usciti finora, gratis per tutti
- Il diario degli episodi

## Come si aggiorna
Tutto sta in un unico file, `index.html`, senza dipendenze. I dati sono nel blocco `DATI` in fondo alla pagina: il voto della settimana, i regali sul banco e il diario.

### La settimana
- **Lunedì**: tre idee nuove in `voto.opzioni` (voti a zero), con `voto.chiude` (mercoledì sera) e `voto.uscita` (venerdì alle 19). `conteggio` e `vince` tornano vuoti.
- **Le sere di voto**: i voti contati dai commenti (dal conta-voti di Spinta, «Copia per Claude») vanno in `voti`, con l'ora in `voto.conteggio`.
- **Giovedì**: a voto chiuso, `voto.vince` prende la lettera vincente e il regalo entra nella cartella `regali/` e in `prodotti`, con `esce` uguale a `voto.uscita`.
  Se nei commenti non ha votato nessuno, `voto.vince` diventa `"nessuno"`: quella settimana non esce nessuna app e la pagina lo dice al posto del conto alla rovescia.
- **Venerdì alle 19**: il regalo si apre da solo. Fino a quell'ora sul banco si vede «In arrivo» con l'orario; dopo, il bottone «Apri» e, in alto, «Apri il regalo».
- Ogni puntata importante va nel `diario`.

### La settimana dopo, in anticipo
`DATI.prossimo` = `{ dal, voto, diario }`: da `dal` (il lunedì a mezzanotte) la pagina usa quel voto e aggiunge quelle righe al diario, da sola. Il lunedì poi si sposta tutto in `voto` e `diario` e si svuota `prossimo`.

### I regali
Ogni regalo è una cartella `regali/<nome>/` con `index.html` (tutta l'app in un file), `manifest.webmanifest`, `sw.js` e le icone: si apre dal telefono, si può aggiungere alla schermata Home e dopo la prima apertura funziona anche senza rete. Niente registrazione, niente pubblicità, i dati restano sul telefono.

In `prodotti` un regalo è così:
```js
{ nome: "Timer p' 'a moka", emoji: "☕", descrizione: "…", link: "regali/timer-moka/", esce: "2026-10-09T19:00:00+02:00", lettera: "B", voti: 58 }
```

Un progetto [EssentialApp](https://essentialapp-2026.github.io/). Gennarino è un personaggio animato da un'AI.
