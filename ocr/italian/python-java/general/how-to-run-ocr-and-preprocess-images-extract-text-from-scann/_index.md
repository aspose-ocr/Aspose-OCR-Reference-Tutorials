---
category: general
date: 2026-04-26
description: Come eseguire l'OCR su un modulo scansionato, imparare a pre‑processare
  l'immagine per ridurre il rumore e estrarre rapidamente il testo dall'immagine.
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: it
og_description: Come eseguire l'OCR su documenti scansionati, preelaborare le immagini,
  ridurre il rumore ed estrarre il testo in modo efficiente.
og_title: Come eseguire OCR e pre‑elaborare le immagini – Guida rapida
tags:
- OCR
- image processing
- Python
title: Come eseguire OCR e pre‑elaborare le immagini – Estrarre il testo da moduli
  scansionati
url: /it/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR – Guida completa per estrarre testo dalle immagini

Ti sei mai chiesto **come eseguire OCR** su un modulo scansionato disordinato e ottenere testo pulito e ricercabile? Non sei l'unico. In molti progetti reali l'immagine grezza è piena di macchie, illuminazione non uniforme e altre stranezze che fanno inciampare l'OCR pronto all'uso.  

La buona notizia? Con poche righe di Python e una pipeline di pre‑elaborazione intelligente, puoi aumentare drasticamente la precisione del riconoscimento, **ridurre il rumore** e estrarre le parole esatte di cui hai bisogno. In questo tutorial percorreremo ogni passaggio—dal caricamento dell'immagine alla stampa della stringa finale—così avrai a disposizione uno snippet pronto da adattare a fatture, ricevute o qualsiasi documento scansionato.

## Cosa costruirai

- Un'istanza `OcrEngine` che comunica con la libreria OCR sottostante.  
- Una catena di pre‑elaborazione che **binarizza** l'immagine e applica un **median blur** per levigare le macchie.  
- Una semplice chiamata a `process()` che restituisce un oggetto con l'attributo `text`, la stringa estratta.  

Alla fine avrai uno script autonomo che potrai eseguire su qualsiasi file immagine e vedere immediatamente il testo estratto nella console.

## Prerequisiti

- Python 3.9+ (la sintassi usata qui corrisponde all'ultima versione stabile).  
- Il pacchetto fittizio `aocr` – pensalo come un leggero wrapper attorno a Tesseract o a qualsiasi motore OCR moderno. Installalo con `pip install aocr`.  
- Un'immagine scansionata (`scanned_form.jpg`) collocata in una cartella a cui puoi fare riferimento.  

Se usi una libreria OCR reale come `pytesseract`, puoi sostituire `OcrEngine` con la classe appropriata—tutto il resto rimane invariato.

![](how-to-run-ocr-example.png "esempio di come eseguire OCR che mostra un modulo scansionato e il testo estratto")

*Alt text: come eseguire OCR su un documento scansionato e visualizzare il testo estratto.*

---

## Passo 1: Come eseguire OCR – Inizializzare il motore

Prima che il motore possa leggere qualcosa, dobbiamo creare un'istanza. Pensa a `OcrEngine` come al cervello che interpreterà in seguito i dati visivi.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **Perché è importante:** L'istanziazione del motore configura i modelli interni, carica i pacchetti linguistici e prepara l'ambiente di esecuzione. Saltare questo passaggio di solito porta a un errore `NoneType` quando successivamente chiami `process()`.

---

## Passo 2: Come pre‑elaborare l'immagine – Carica il tuo modulo scansionato

Ora che il cervello è pronto, gli forniamo un'immagine. L'immagine può essere in qualsiasi formato supportato da `aocr.Image`.

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **Suggerimento:** Usa percorsi assoluti durante lo sviluppo per evitare sorprese “file non trovato” quando lo script viene eseguito da una directory di lavoro diversa.

---

## Passo 3: Come ridurre il rumore – Applica binarizzazione e median blur

Le scansioni grezze contengono spesso punti sparsi, sfondi non uniformi o ombre leggere. Due trucchi classici—**binarizzazione** e **median blur**—puliscono tutto senza sacrificare i bordi che definiscono i caratteri.

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### Approfondimento

- **Binarizzazione**: Il valore `threshold=180` indica all'algoritmo: “Tutto ciò che è più luminoso di 180 diventa bianco; tutto il resto diventa nero.” Regola questo numero se la tua scansione è troppo scura o troppo chiara.  
- **Median Blur**: Un raggio di `2` significa che il filtro osserva una finestra di 5×5 pixel e sostituisce il pixel centrale con il valore mediano. Questo elimina le macchie isolate mantenendo intatti i tratti delle lettere.

> **Caso limite:** Se il tuo documento contiene evidenziazioni colorate, una semplice soglia binaria potrebbe cancellarle. In tal caso, considera l'uso di `aocr.ImageFilters.adaptive_threshold()`—adatta il cutoff localmente sull'intera immagine.

---

## Passo 4: Come estrarre il testo – Esegui il processo OCR

Con un'immagine pulita in mano, lasciamo finalmente che il motore faccia la sua magia.

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **Cosa succede dietro le quinte?** Il motore esegue una rete neurale (o un matcher di pattern legacy) sulla matrice di pixel, traduce ogni glifo riconosciuto in caratteri Unicode e li assembla in linee e paragrafi.

---

## Passo 5: Come estrarre il testo – Stampa il risultato

L'oggetto `ocr_result` espone un comodo attributo `text`. Vediamo cosa otteniamo.

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### Output previsto

Se il modulo scansionato contiene:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Dovresti vedere qualcosa di simile a:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Nota come il passaggio di pre‑elaborazione ha eliminato i punti sparsi che prima trasformavano “Amount” in “Am0unt”. Questa è la potenza di **come ridurre il rumore** prima dell'OCR.

---

## Problemi comuni e come risolverli

| Sintomo | Causa probabile | Soluzione rapida |
|---------|-----------------|------------------|
| Caratteri confusi (es. “@#%”) | Immagine troppo scura o troppo chiara | Regola il `threshold` in `binarize()`; prova `adaptive_threshold`. |
| Parole mancanti | Rumore ancora presente | Aumenta il `radius` per `median_blur` o aggiungi un filtro `gaussian_blur`. |
| Lingua errata (es. lettere inglesi diventano cinesi) | Pacchetto linguistico sbagliato caricato | Passa `language="eng"` quando crei `OcrEngine()` se la libreria lo supporta. |
| Elaborazione lenta su file grandi | Alta risoluzione | Ridimensiona l'immagine prima: `aocr.ImageFilters.resize(width=1200)` prima della binarizzazione. |

---

## Approfondimenti – Prossimi passi e argomenti correlati

- **Elaborazione batch**: Avvolgi la logica sopra in un ciclo per gestire decine di file automaticamente.  
- **Output strutturato**: Usa espressioni regolari su `ocr_result.text` per estrarre campi come date o importi.  
- **Librerie alternative**: Sostituisci `aocr` con `pytesseract`—il codice cambia solo al passo di inizializzazione del motore.  
- **Come pre‑elaborare immagini per PDF**: Converti ogni pagina PDF in immagine, poi applica la stessa pipeline.  

Queste estensioni ti permettono di scalare la soluzione da un singolo modulo a una pipeline di ingestione documenti di livello aziendale.

---

## Conclusione

Abbiamo coperto **come eseguire OCR** dall'inizio alla fine, mostrato **come pre‑elaborare l'immagine** per **ridurre il rumore**, e dimostrato **come estrarre testo dall'immagine** con uno script pulito e riproducibile. Il punto chiave? Alcuni filtri semplici—binarizzazione e median blur—possono trasformare una scansione rumorosa in una fonte affidabile di dati, risparmiandoti ore di pulizia manuale.

Prova lo script con i tuoi documenti, regola le soglie e osserva la precisione migliorare. Quando sei pronto, esplora l'elaborazione batch o integra l'output in un database per archivi ricercabili. Buona programmazione, e che il tuo OCR sia sempre impeccabile!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}