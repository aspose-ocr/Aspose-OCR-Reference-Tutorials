---
category: general
date: 2026-07-18
description: Esegui OCR su un'immagine usando Aspose OCR in Python. Impara a estrarre
  il testo semplice dall’immagine, applicare il post‑processing AI e ottenere risultati
  puliti rapidamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract plain text from image
- Aspose OCR Python
- AI post‑processor OCR
- image text extraction
language: it
lastmod: 2026-07-18
og_description: Esegui OCR su un'immagine con Aspose OCR e Python. Questo tutorial
  mostra come estrarre testo semplice da un'immagine e aumentare la precisione usando
  un post‑processore AI.
og_image_alt: Screenshot showing run OCR on image results in Python console
og_title: Esegui OCR su immagine – Guida completa Python con Aspose AI
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Run OCR on image using Aspose OCR in Python. Learn to extract plain
    text from image, apply AI post‑processing, and get clean results fast.
  headline: Run OCR on Image with Aspose AI – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI
title: Esegui OCR su un'immagine con Aspose AI – Tutorial completo in Python
url: /it/python/general/run-ocr-on-image-with-aspose-ai-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine con Aspose AI – Tutorial Python Completo

Ti sei mai chiesto come **run OCR on image** file senza combattere con API di basso livello? Non sei l'unico. In molti progetti—elaborazione di fatture, scansione di ricevute o digitalizzazione di vecchi documenti—ottenere testo pulito e ricercabile da un'immagine è il primo, e spesso il più difficile, passo.

In questa guida percorreremo un esempio pratico che non solo **run OCR on image** ma mostra anche come **extract plain text from image** usando il motore OCR di Aspose, per poi perfezionare il risultato con un piccolo post‑processor AI. Alla fine avrai uno script pronto all'uso, una chiara comprensione di ogni componente e alcuni consigli per evitare gli errori più comuni.

![Esempio di Run OCR su Immagine](/images/run-ocr-on-image.png){: .align-center alt="Output della console Run OCR on image che mostra il testo originale e quello migliorato dall'AI"}

## Cosa Ti Serve

- Python 3.8+ installato (il codice funziona su Windows, macOS e Linux).
- Una licenza attiva di Aspose OCR per Python o una prova gratuita (il pacchetto è `aspose-ocr` su PyPI).
- Un file immagine di esempio (ad es., una fattura o una ricevuta scannerizzata) salvato localmente.
- Opzionale: una macchina con GPU abilitata se prevedi di modificare l'impostazione `gpu_layers` in seguito.

Tutto qui—nessun motore OCR pesante, nessuna chiamata a servizi cloud esterni, solo un singolo pip install e poche righe di codice.

## Passo 1: Installa il Pacchetto Aspose OCR

Apri un terminale ed esegui:

```bash
pip install aspose-ocr
```

Il pacchetto scarica il motore OCR core più lo spazio dei nomi leggero `aspose.ocr` che utilizzeremo durante tutto il tutorial.

## Passo 2: Importa le Classi Necessarie

Iniziamo importando le due classi principali: `AsposeAI` per il post‑processing potenziato dall'AI e `OcrEngine` per l'estrazione reale del testo.

```python
# Step 1: Import required classes
from aspose.ocr import AsposeAI, OcrEngine
```

*Perché è importante*: `OcrEngine` si occupa del lavoro pesante di riconoscimento dei glifi, mentre `AsposeAI` ci permette di collegare logica personalizzata—come la capitalizzazione di ogni parola—senza riscrivere il core OCR.

## Passo 3: Crea un'Istanza AsposeAI (Logger Opzionale)

Se desideri un logging dettagliato puoi passare un logger personalizzato, ma il valore predefinito funziona bene nella maggior parte dei casi.

```python
# Step 2: Create an AsposeAI instance (optional custom logger can be supplied)
ai = AsposeAI()
```

## Passo 4: Modifica il Modello Sottostante (Opzionale)

Aspose OCR viene fornito con un modello linguistico predefinito, ma puoi puntarlo a un repository HuggingFace o forzare l'esecuzione su CPU. Di seguito abilitiamo i download automatici e selezioniamo il piccolo modello `gpt2`—solo per illustrare le impostazioni disponibili.

```python
# Step 3: (Optional) Adjust the underlying model configuration
ai.config.allow_auto_download = "true"          # permit automatic model download
ai.config.hugging_face_repo_id = "openai/gpt2"   # specify the HuggingFace model
ai.config.gpu_layers = 0                        # force CPU execution
```

> **Consiglio Pro:** Se disponi di una GPU compatibile CUDA, aumenta `gpu_layers` a `1` o `2` per un notevole aumento di velocità.

## Passo 5: Registra un Post‑Processor Semplice

Il nostro obiettivo è **extract plain text from image** e poi renderlo più gradevole. Ecco una piccola funzione che capitalizza ogni parola. Potresti sostituirla con un correttore ortografico, il rilevamento della lingua o persino una chiamata a un LLM completo.

```python
# Step 4: Register a simple post‑processor that capitalizes each word
def capitalize_words(text, settings):
    """Capitalize every word in the OCR output."""
    return " ".join(word.capitalize() for word in text.split())

# Attach the processor to the AsposeAI instance
ai.set_post_processor(capitalize_words, custom_settings={})
```

Il dizionario `custom_settings` ti consente di passare parametri aggiuntivi in seguito—utile quando evolvi il processore.

## Passo 6: Carica un'Immagine ed Esegui OCR

Ora finalmente **run OCR on image**. Recupereremo due tipologie di output:

1. **Plain text** – una stringa grezza senza informazioni di layout.
2. **Structured text** – consapevole del layout, preserva colonne e tabelle.

```python
# Step 5: Load an image and obtain OCR results (plain and layout‑aware)
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()                     # raw text
structured_text = ocr_engine.recognize_structured()    # layout‑aware text
```

> **Perché entrambi?** `plain_text` è perfetto per ricerche rapide, mentre `structured_text` brilla quando devi ricostruire tabelle o mantenere l'allineamento delle colonne.

## Passo 7: Migliora gli Output OCR con il Post‑Processor AI

Con i risultati OCR a disposizione, li passiamo a `AsposeAI.run_postprocessor`. È qui che viene eseguita la funzione `capitalize_words` definita prima.

```python
# Step 6: Enhance the OCR outputs using the AI post‑processor
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)
```

Se in seguito decidi di sostituire il post‑processor con qualcosa di più sofisticato—ad esempio un correttore grammaticale—basta sostituire la funzione al passo 5 e il resto della pipeline rimane identico.

## Passo 8: Visualizza i Risultati

Stampiamo tutto affiancato così puoi confrontare l'OCR grezzo con la versione migliorata dall'AI.

```python
# Step 7: Display original and enhanced texts
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)
```

### Output Atteso

```
Original plain text: invoice #12345 date 01/02/2024 total $123.45
AI‑enhanced plain text: Invoice #12345 Date 01/02/2024 Total $123.45

Original structured text: invoice #12345
date 01/02/2024
total $123.45
AI‑enhanced structured text: Invoice #12345
Date 01/02/2024
Total $123.45
```

Nota come il post‑processor AI ha trasformato le parole tutte in minuscolo in parole capitalizzate, rendendo il testo molto più leggibile. Puoi applicare qualsiasi trasformazione tu voglia—questo è solo una prova di concetto.

## Passo 9: Pulisci le Risorse

Aspose carica file di modello pesanti in memoria. Quando hai finito, liberali per evitare perdite di memoria, specialmente in servizi a lunga esecuzione.

```python
# Step 8: Release model resources when done
ai.free_resources()
```

## Domande Frequenti & Casi Limite

| Domanda | Risposta |
|----------|--------|
| **Posso eseguire OCR su più immagini in un ciclo?** | Assolutamente. Basta istanziare `OcrEngine` una volta, chiamare `load_image` all'interno del ciclo e riutilizzare la stessa istanza `AsposeAI` per il post‑processing. |
| **E se l'immagine è a bassa risoluzione?** | Pre‑processa con OpenCV (ad esempio `cv2.resize` e `cv2.threshold`) prima di passarla a `OcrEngine`. |
| **Ho bisogno di una GPU?** | Non è necessario. La modalità CPU predefinita funziona bene per la maggior parte dei documenti. Imposta `ai.config.gpu_layers` > 0 solo se hai una GPU compatibile e necessiti di velocità. |
| **Come estrarre plain text from image in altre lingue?** | Modifica `ocr_engine.language = "fr"` (o qualsiasi codice ISO‑639‑1) prima di chiamare `recognize`. Lo stesso post‑processor verrà comunque eseguito, ma potresti aver bisogno di logica specifica per la lingua. |

## Script Completo Funzionante

Mettendo tutto insieme, ecco il programma completo, pronto all'uso:

```python
# Full script: run OCR on image, extract plain text, and apply AI post‑processing

from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Initialize AsposeAI
ai = AsposeAI()
ai.config.allow_auto_download = "true"
ai.config.hugging_face_repo_id = "openai/gpt2"
ai.config.gpu_layers = 0   # set >0 for GPU

# 2️⃣ Register post‑processor (capitalizes each word)
def capitalize_words(text, settings):
    return " ".join(word.capitalize() for word in text.split())

ai.set_post_processor(capitalize_words, custom_settings={})

# 3️⃣ Load image and run OCR
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()
structured_text = ocr_engine.recognize_structured()

# 4️⃣ Enhance outputs
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)

# 5️⃣ Print results
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)

# 6️⃣ Clean up
ai.free_resources()
```

Salva questo come `run_ocr_on_image.py`, sostituisci il percorso segnaposto con la tua immagine reale ed esegui `python run_ocr_on_image.py`. Dovresti vedere l'output prima/dopo proprio come nell'esempio sopra.

## Conclusione

Abbiamo eseguito con successo **run OCR on image** su file usando Aspose OCR, dimostrato come **extract plain text from image**, e mostrato un modo leggero per migliorare la leggibilità con un post‑processor AI. Il modello di base—OCR

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai Testo da Immagine con Aspose OCR – Guida Passo‑Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Estrai testo immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Estrai Testo da Immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}