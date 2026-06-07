---
category: general
date: 2026-06-06
description: Estrai testo da un'immagine con OCR in Python in pochi minuti. Scopri
  l'OCR multilingue per immagini, il rilevamento automatico della lingua e come estrarre
  il testo OCR con precisione.
draft: false
keywords:
- extract text from image
- how to extract OCR text
- multilingual image OCR
- detect language OCR
- auto detect language OCR
language: it
og_description: Estrai testo da immagini con OCR in Python rapidamente. Scopri l'OCR
  multilingue per immagini, il rilevamento automatico della lingua e come estrarre
  il testo OCR passo dopo passo.
og_title: Estrai il testo da un'immagine usando OCR Python – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  headline: Extract Text from Image Using Python OCR – Complete Guide
  type: TechArticle
- description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  name: Extract Text from Image Using Python OCR – Complete Guide
  steps:
  - name: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
    text: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
  - name: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
    text: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
  - name: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
    text: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Multilingual
title: Estrai il testo da un'immagine usando OCR Python – Guida completa
url: /it/python-java/general/extract-text-from-image-using-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine usando Python OCR – Guida completa

Ti è mai capitato di dover **estrarre testo da un'immagine** ma non eri sicuro quale libreria potesse gestire più lingue automaticamente? Non sei solo: gli sviluppatori chiedono continuamente *come estrarre testo OCR* quando si tratta di documenti internazionali, ricevute o volantini scansionati. In questo tutorial percorreremo un esempio pratico in Python che non solo estrae testo da un'immagine ma **rileva anche la lingua** al volo, rendendo l'OCR multilingue un gioco da ragazzi.

Copriamo tutto, dall'installazione del pacchetto OCR all'abilitazione del **rilevamento automatico della lingua OCR**, all'esecuzione del motore su un'immagine di esempio e, infine, alla stampa sia della lingua rilevata sia della stringa estratta. Alla fine avrai uno snippet riutilizzabile da inserire in qualsiasi progetto, sia che tu stia costruendo una pipeline di traduzione o un servizio di ingestione dati.

## Estrarre testo da immagine – Configurare l'ambiente

Prima di immergerci nel codice, assicurati che la tua postazione soddisfi questi requisiti minimi:

- Python 3.8 o successivo (la libreria utilizza type hints che le versioni più vecchie ignorano)
- `pip` per la gestione dei pacchetti
- Un file immagine che contenga testo in almeno due lingue diverse (ad es., inglese + spagnolo)

Avrai inoltre bisogno della libreria OCR che alimenta questa demo. Per il presente tutorial useremo il pacchetto fittizio `ocr`, che rispecchia strumenti reali popolari come Tesseract o EasyOCR ma offre un'API Python pulita.

```bash
# Install the OCR package and its optional image dependencies
pip install ocr[image]
```

> **Suggerimento:** Se incontri errori di permessi, anteponi il comando con `python -m` o usa un ambiente virtuale—mantiene ordinati i tuoi site‑packages globali.

## Crea un'istanza del motore OCR

Ora che la libreria è pronta, il primo passo logico è **creare un'istanza del motore OCR**. Pensa al motore come a uno scanner intelligente che puoi configurare prima di alimentarlo con le immagini.

```python
import ocr

# Step 1: Initialize the OCR engine
engine = ocr.OcrEngine()
```

Perché istanziamo il motore separatamente invece di chiamare un metodo statico? L'oggetto motore conserva lo stato di configurazione (come le preferenze di lingua) che potresti voler riutilizzare su molte immagini, risparmiandoti il sovraccarico di reinizializzarlo ogni volta.

## Abilita il rilevamento automatico della lingua OCR

La maggior parte degli strumenti OCR richiede di specificare un codice lingua—`eng` per l'inglese, `spa` per lo spagnolo, ecc. Indovinare manualmente la lingua vanifica lo scopo di un flusso di lavoro **OCR multilingue per immagini**. Fortunatamente, il pacchetto `ocr` offre una modalità *auto detect language OCR* che analizza l'immagine e seleziona il modello linguistico più adatto in background.

```python
# Step 2: Turn on automatic language detection
engine.set_recognition_language(ocr.Language.AUTO_DETECT)
```

Abilitare **detect language OCR** in questo modo significa che non dovrai mantenere una lunga lista di codici lingua. Il motore cercherà di corrispondere allo script rilevato—Latino, Cirillico, Han, ecc.—e caricherà automaticamente il modello appropriato.

## Esegui OCR multilingue su immagine

Con il motore pronto, è il momento di **estrarre testo da un'immagine**. Il metodo `recognize_image` accetta un percorso file e restituisce un oggetto risultato contenente sia il testo grezzo sia la lingua rilevata.

```python
# Step 3: Run OCR on a multilingual image
image_path = "YOUR_DIRECTORY/multilang_page.png"
result = engine.recognize_image(image_path)
```

Se ti chiedi *come estrarre testo OCR* da un PDF invece che da un PNG, lo stesso motore offre `recognize_pdf`—basta cambiare il nome del metodo. La logica di rilevamento sottostante rimane identica, così benefici della stessa funzionalità **auto detect language OCR**.

## Visualizza lingua rilevata e testo estratto

Infine, mostriamo ciò che il motore ha scoperto. L'oggetto risultato espone `detected_language` (un tag BCP‑47 come `en` o `es`) e `text`, che contiene l'output OCR grezzo.

```python
# Step 4: Show the language and the extracted string
print(f"Detected language: {result.detected_language}")
print("Extracted text:")
print(result.text)
```

Eseguendo lo script sulla nostra immagine di esempio dovrebbe produrre qualcosa di simile a:

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

Nota come il motore abbia identificato correttamente l'inglese come lingua principale, ma abbia comunque catturato la riga in spagnolo—esattamente ciò che ti aspetti da una soluzione **OCR multilingue per immagini** robusta.

### Cosa succede se il rilevamento fallisce?

A volte il motore OCR può ricadere su una lingua predefinita (di solito l'inglese) se l'immagine è sfocata o lo script è troppo esotico. In questi casi puoi forzare una lista di lingue:

```python
engine.set_recognition_language([ocr.Language.ENGLISH, ocr.Language.SPANISH])
```

Ma ricorda, forzare le lingue vanifica la comodità del **auto detect language OCR**, quindi usalo solo quando hai un sottoinsieme di lingue noto.

## Problemi comuni e come estrarre testo OCR in modo affidabile

Anche con l'auto‑rilevamento, alcuni intoppi possono ostacolarti:

1. **Immagini a bassa risoluzione** – L'accuratezza OCR diminuisce drasticamente sotto i 150 dpi. Upscale o richiedi una scansione a risoluzione più alta.
2. **Rumore e artefatti di compressione** – Applica un semplice filtro di soglia (`opencv` o `Pillow`) prima di fornire l'immagine al motore.
3. **Script misti in una pagina** – Alcuni motori hanno difficoltà con caratteri latini e CJK simultanei. Dividi la pagina in regioni ed esegui riconoscimenti separati se necessario.

Affrontare questi problemi migliora notevolmente la qualità del processo di **estrazione di testo da immagine**, specialmente quando si trattano documenti reali e multilingue.

## Esempio completo funzionante

Di seguito trovi lo script completo, pronto da eseguire, che combina tutti i passaggi discussi. Salvalo come `multilingual_ocr.py` ed eseguilo dalla riga di comando.

```python
import ocr

def main():
    # Initialize engine with auto language detection
    engine = ocr.OcrEngine()
    engine.set_recognition_language(ocr.Language.AUTO_DETECT)

    # Path to your multilingual image
    image_path = "YOUR_DIRECTORY/multilang_page.png"

    # Perform OCR
    result = engine.recognize_image(image_path)

    # Output results
    print(f"Detected language: {result.detected_language}")
    print("Extracted text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Output previsto** (supponendo che l'immagine di esempio contenga testo in inglese e spagnolo):

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

Sentiti libero di sostituire `multilang_page.png` con qualsiasi immagine che contenga testo in altre lingue—grazie al **auto detect language OCR**, lo script ti fornirà comunque un tag lingua sensato e il testo corrispondente.

![Esempio di estrazione di testo da immagine](https://example.com/ocr-sample.png "Estrai testo da immagine")

## Conclusione

Ora sai esattamente **come estrarre testo OCR** da un'immagine, come abilitare **auto detect language OCR** e come gestire scenari **OCR multilingue per immagini** con un codice minimo. Creando un'istanza del motore OCR, attivando il rilevamento automatico della lingua e chiamando `recognize_image`, puoi estrarre in modo affidabile sia l'identificatore della lingua sia il testo grezzo.

Cosa fare dopo? Prova a inviare le stringhe estratte a un'API di traduzione, archiviarle in un database ricercabile o combinare più pagine in un unico report PDF. Puoi anche sperimentare con diversi back‑end OCR (Tesseract, EasyOCR, Google Vision) mantenendo lo stesso flusso di lavoro ad alto livello—grazie all'interfaccia coerente **detect language OCR**.

Se incontri qualche stranezza, rivedi la sezione “Problemi comuni” o modifica i passaggi di pre‑elaborazione dell'immagine. Buon coding, e che il tuo prossimo progetto sia pieno di testo correttamente rilevato e perfettamente estratto!

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}