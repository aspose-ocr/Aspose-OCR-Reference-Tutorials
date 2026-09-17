---
date: 2026-05-19
description: Scopri come estrarre testo dalle immagini usando Aspose.OCR per .NET,
  convertire l'immagine in documento e migliorare la precisione OCR nelle tue applicazioni.
keywords:
- extract text from images
- convert image to document
- improve ocr accuracy
- ocr image to txt
- save ocr as pdf
linktitle: Impostazioni OCR
second_title: Aspose.OCR .NET API
title: Estrai testo dalle immagini – Impostazioni OCR con Aspose.OCR
url: /it/net/ocr-settings/
weight: 26
---

{{< blocks/products/pf/main-wrap-class >}}  
{{< blocks/products/pf/main-container >}}  
{{< blocks/products/pf/tutorial-page-section >}}  

# Estrai testo dalle immagini – Impostazioni OCR con Aspose.OCR  

## Introduzione  

Nell'odierno mondo digitale in rapida evoluzione, **extract text from images** è una capacità critica per tutto, dalla gestione delle fatture agli archivi ricercabili. Aspose.OCR per .NET ti offre un motore potente e pronto all'uso che può trasformare qualsiasi immagine in testo modificabile, PDF, DOCX o file di testo semplice. In questa guida esamineremo le impostazioni OCR più comuni, spiegheremo *perché* ciascuna è importante e ti mostreremo come applicarle in scenari reali così da aumentare precisione, velocità e flessibilità nelle tue applicazioni.  

## Risposte rapide  
- **Che cosa significa “extract text from images”?** È il processo di riconoscimento dei caratteri all'interno dei file immagine e della loro conversione in testo modificabile.  
- **Quale libreria gestisce al meglio questo in .NET?** Aspose.OCR per .NET offre precisione leader nel settore e supporto multilingua.  
- **Posso convertire il risultato OCR in PDF o DOCX?** Sì – il tutorial “Save Result as Document” mostra come esportare in PDF, DOCX o TXT con una singola chiamata.  
- **Come posso velocizzare l'OCR per grandi batch?** Aumenta il conteggio dei thread (vedi “Set Threads Count”) per eseguire il riconoscimento in parallelo.  
- **È possibile effettuare il fine‑tuning?** Assolutamente – è possibile impostare valori di soglia, creare una whitelist dei caratteri consentiti, una blacklist dei caratteri ignorati e caricare i language pack per risultati ottimali.  

## Che cos'è “extract text from images”?  

Converte la rappresentazione visiva dei caratteri in testo Unicode modificabile analizzando i pattern dei pixel, applicando pre‑elaborazioni come binarizzazione e riduzione del rumore, e poi usando modelli linguistici addestrati per riconoscere ogni glifo. Le stringhe risultanti possono essere archiviate, ricercate, indicizzate o ulteriormente elaborate nelle tue applicazioni.  

## Perché usare Aspose.OCR per .NET?  

Carica la libreria Aspose.OCR e ottieni immediatamente il supporto per **oltre 50 formati di input e output** — inclusi JPEG, PNG, BMP, TIFF, conversione PDF‑in‑immagine e molto altro – e la possibilità di elaborare file fino a **500 MB** senza esaurire la memoria. Il motore offre **fino al 98 % di precisione** su scansioni pulite e fornisce una pre‑elaborazione integrata che migliora immagini a basso contrasto o rumorose a risultati quasi perfetti.  

## Salva risultato come documento nel riconoscimento OCR di immagini  

`SaveResultAsDocument` salva l'output OCR direttamente in un file documento.  

Quando chiami `ocrEngine.SaveResultAsDocument(outputPath, SaveFormat.Pdf)`, Aspose.OCR scrive il testo in un PDF con livelli di testo selezionabili, consentendo la ricerca e la funzionalità copia‑incolla senza alcuna post‑elaborazione aggiuntiva.  

## Imposta il conteggio dei thread nel riconoscimento OCR di immagini  

Regolare il pool di thread controlla quante pagine immagine vengono elaborate simultaneamente.  

**Definizione:** La proprietà `ThreadsCount` determina il numero massimo di thread lavoratori OCR in parallelo che il motore avvierà.  

Aumentare questo valore dal valore predefinito **1** a **4** (o più su server multi‑core) può ridurre il tempo di elaborazione del **30‑70 %** per grandi batch, rispettando comunque il limite di memoria impostato nella configurazione dell'applicazione.  

## Imposta valore di soglia nel riconoscimento OCR di immagini  

La sogliatura converte un'immagine in scala di grigi in una bitmap in bianco‑nero, fondamentale per fonti a basso contrasto.  

**Definizione:** La proprietà `Threshold` imposta il valore di soglia di luminanza (0‑255) usato durante la binarizzazione.  

Per una scansione sbiadita, una soglia di **180** spesso produce bordi dei caratteri più puliti, riducendo i falsi positivi fino al **15 %** rispetto all'impostazione automatica predefinita.  

## Specifica i caratteri consentiti nel riconoscimento OCR di immagini  

A volte è necessario solo un sottoinsieme di caratteri, come le cifre per i numeri di serie.  

**Definizione:** La collezione `AllowedCharacters` funge da whitelist, limitando il riconoscimento ai caratteri specificati.  

Limitando il motore a `"0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"` è possibile eliminare il rumore della punteggiatura e migliorare la precisione per i codici alfanumerici del **20 %**.  

## Specifica i caratteri ignorati nel riconoscimento OCR di immagini  

Al contrario, potresti voler ignorare i caratteri che appaiono frequentemente come rumore.  

**Definizione:** La collezione `IgnoredCharacters` è una blacklist che indica al motore OCR di scartare i simboli corrispondenti durante il riconoscimento.  

Rimuovere artefatti comuni come “#” o “$” quando non fanno parte dei dati target riduce drasticamente i tassi di riconoscimento errato, specialmente nei moduli scansionati.  

## Lavorare con lingue diverse nel riconoscimento OCR di immagini  

Aspose.OCR include language pack per **oltre 30 script**, dal latino al cirillico, arabo e caratteri asiatici.  

**Definizione:** La proprietà `Language` seleziona il modello linguistico che guida l'analisi della forma dei caratteri.  

Caricare il pack appropriato (ad esempio, `ocrEngine.Language = Language.French`) aumenta la precisione sui documenti multilingue del **10‑25 %**, poiché il motore applica euristiche specifiche per lo script.  

## Tutorial impostazioni OCR  

### [Salva risultato come documento nel riconoscimento OCR di immagini](./save-result-as-document/)  
Sblocca il potenziale di Aspose.OCR per .NET. Riconosci facilmente il testo nelle immagini e salva i risultati in vari formati documento.  

### [Imposta il conteggio dei thread nel riconoscimento OCR di immagini](./set-threads-count/)  
Sblocca l'efficienza OCR in .NET. Imposta il conteggio dei thread senza sforzo con Aspose.OCR. Aumenta precisione e velocità.  

### [Imposta valore di soglia nel riconoscimento OCR di immagini](./set-threshold-value/)  
Esplora Aspose.OCR per .NET, una soluzione OCR robusta. Imposta valori di soglia personalizzati senza sforzo. Migliora il riconoscimento del testo nelle tue applicazioni.  

### [Specifica i caratteri consentiti nel riconoscimento OCR di immagini](./specify-allowed-characters/)  
Sblocca OCR preciso in .NET con Aspose.OCR. Riconosci il testo dalle immagini senza sforzo. Scarica ora per un'esperienza di sviluppo trasformativa.  

### [Specifica i caratteri ignorati nel riconoscimento OCR di immagini](./specify-ignored-characters/)  
Esplora le capacità OCR avanzate con Aspose.OCR per .NET. Efficiente, preciso e orientato allo sviluppatore.  

### [Lavorare con lingue diverse nel riconoscimento OCR di immagini](./working-with-different-languages/)  
Sblocca la magia dell'OCR multilingue con Aspose.OCR per .NET. Estrai testo senza sforzo in varie lingue.  

## Come estrarre testo dalle immagini usando Aspose.OCR – Panoramica impostazioni comuni  

Carica il tuo motore OCR, configura le impostazioni desiderate e chiama `Recognize` – questo è il flusso di lavoro principale in **meno di 10 righe di codice**. Padroneggiando le impostazioni comuni di seguito, puoi personalizzare il motore per velocità, precisione o supporto multilingue, a seconda delle esigenze del tuo progetto.  

| Impostazione | Scopo | Quando usarla |
|--------------|-------|---------------|
| **Save Result as Document** | Esporta l'output OCR in PDF/DOCX/TXT | Quando ti serve un documento riutilizzabile e ricercabile |
| **Threads Count** | Controlla l'elaborazione parallela | Grandi batch o app critiche per le prestazioni |
| **Threshold Value** | Regola la binarizzazione dell'immagine | Immagini a basso contrasto o rumorose |
| **Allowed Characters** | Whitelist di simboli specifici | Dati specifici del dominio (ad es., numeri di serie) |
| **Ignored Characters** | Blacklist di simboli indesiderati | Rimuovere rumore come la punteggiatura |
| **Language Packs** | Abilita il riconoscimento multilingue | Documenti contenenti script non latini |

## Domande frequenti  

**Q:** Posso usare Aspose.OCR in un progetto .NET Core?  
**A:** Sì, Aspose.OCR per .NET supporta pienamente .NET Core, .NET 5+ e .NET 6+ con la stessa interfaccia API.  

**Q:** Come posso migliorare la precisione OCR su immagini a bassa risoluzione?  
**A:** Aumenta il valore di `Threshold`, abilita il language pack `Language` appropriato e considera di specificare `AllowedCharacters` per limitare il set di caratteri.  

**Q:** È possibile estrarre testo direttamente dai PDF?  
**A:** Sebbene Aspose.OCR si concentri sui file immagine, è possibile prima convertire le pagine PDF in immagini usando Aspose.PDF, quindi eseguire l'OCR sulle immagini risultanti.  

**Q:** Quali licenze sono necessarie per l'uso in produzione?  
**A:** È necessaria una licenza commerciale Aspose.OCR per il deployment; è disponibile una prova gratuita di 30 giorni per la valutazione.  

**Q:** Ci sono limiti di dimensione per le immagini che posso elaborare?  
**A:** La libreria gestisce comodamente immagini fino a **500 MB**; per file più grandi, aumenta `ThreadsCount` e regola le impostazioni di memoria di conseguenza.  

---  

**Ultimo aggiornamento:** 2026-05-19  
**Testato con:** Aspose.OCR 24.11 for .NET  
**Autore:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutorial correlati

- [Estrai testo da immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/net/ocr-optimization/)
- [Imposta il conteggio dei thread per migliorare la precisione OCR in .NET](/ocr/net/ocr-settings/set-threads-count/)
- [Riconosci testo da immagine con Aspose OCR per più lingue](/ocr/net/ocr-settings/working-with-different-languages/)


{{< /blocks/products/pf/tutorial-page-section >}}  
{{< /blocks/products/pf/main-container >}}  
{{< /blocks/products/pf/main-wrap-class >}}