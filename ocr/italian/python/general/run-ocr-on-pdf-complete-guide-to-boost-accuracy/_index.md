---
category: general
date: 2026-07-05
description: Impara a eseguire OCR su PDF e a migliorare l'accuratezza dell'OCR usando
  un modello Hugging Face. Configurazione passo‑passo, carica PDF per l'OCR e configura
  il modello Hugging Face.
draft: false
keywords:
- run OCR on PDF
- improve OCR accuracy
- load PDF for OCR
- configure Hugging Face model
language: it
og_description: Esegui OCR su PDF con un modello Hugging Face e migliora la precisione
  dell'OCR. Segui questa guida per caricare il PDF per l'OCR e configurare il modello.
og_title: Esegui OCR su PDF – Tutorial completo per una maggiore precisione
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Learn how to run OCR on PDF and improve OCR accuracy using a Hugging
    Face model. Step‑by‑step setup, load PDF for OCR, and configure Hugging Face model.
  headline: run OCR on PDF – Complete Guide to Boost Accuracy
  type: TechArticle
- description: Learn how to run OCR on PDF and improve OCR accuracy using a Hugging
    Face model. Step‑by‑step setup, load PDF for OCR, and configure Hugging Face model.
  name: run OCR on PDF – Complete Guide to Boost Accuracy
  steps:
  - name: What if the PDF is multi‑page?
    text: The `Image.from_file` call automatically creates a multi‑frame image object.
      Loop over `input_image.frames` and call `ocr_engine.recognize` for each frame,
      then concatenate the results before running the post‑processor.
  - name: How to handle languages other than English?
    text: 'Set the OCR engine’s language property before recognition:'
  - name: Can I run this on CPU only?
    text: Yes—just omit `model_cfg.gpu_layers` or set it to `0`. The model will run
      entirely on CPU, though inference will be slower (roughly 5‑10 seconds per page
      on a modern i7).
  type: HowTo
tags:
- OCR
- Python
- AI post‑processor
title: Esegui OCR su PDF – Guida completa per aumentare la precisione
url: /it/python/general/run-ocr-on-pdf-complete-guide-to-boost-accuracy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# eseguire OCR su PDF – Guida completa per aumentare l'accuratezza

Ti sei mai chiesto come **eseguire OCR su PDF** senza spendere una fortuna in SDK commerciali? Non sei il solo. Che tu stia digitalizzando fatture, estraendo dati da report scansionati, o semplicemente sia curioso dell'estrazione di testo potenziata dall'AI, la capacità di **eseguire OCR su PDF** in modo efficiente è una competenza indispensabile per qualsiasi sviluppatore moderno.

In questo tutorial percorreremo un esempio pratico, end‑to‑end, che non solo ti mostra come **eseguire OCR su PDF**, ma dimostra anche come **migliorare l'accuratezza OCR** collegando un post‑processore AI. Copriremo anche i dettagli di **caricare PDF per OCR** e **configurare il modello Hugging Face** in modo da ottenere le migliori prestazioni su una workstation modesta.

Al termine di questa guida avrai uno script completamente funzionante che:

* Carica un PDF (o immagine) per OCR  
* Configura un modello Hugging Face con quantizzazione personalizzata e layer GPU  
* Esegue OCR semplice e poi migliora il risultato con un post‑processore AI  
* Stampa sia il testo grezzo sia quello migliorato dall'AI per un facile confronto  

Nessun servizio esterno, nessuna tariffa nascosta—solo librerie open‑source e poche righe di Python.

## Cosa ti servirà

Prima di immergerci, assicurati di avere i seguenti prerequisiti:

* Python 3.9 o successivo installato (il modulo `venv` è comodo)  
* Pacchetto `aocr` (Aspose OCR) – installa con `pip install aocr`  
* Accesso a Internet per il download una tantum del modello da Hugging Face  
* Un file PDF che desideri elaborare (useremo `invoice_2026.pdf` come esempio)  

Tutto qui. Se qualcosa ti è poco familiare, non preoccuparti—ogni passaggio qui sotto spiega il perché e il come, così sarai operativo in pochi minuti.

---

## Passo 1: Configurare il modello Hugging Face

La prima cosa da fare è **configurare il modello Hugging Face** con parametri adatti al tuo hardware. Nel nostro caso scaricheremo il nuovissimo modello `Qwen/Qwen2.5-3B-Instruct-GGUF`, lo quantizzeremo a `int8` per un'impronta di memoria minima, e sposteremo i primi 20 layer sulla GPU per velocità.

```python
import aocr

# Create the AI engine that will later post‑process OCR results
ai_engine = aocr.AsposeAI()

# Build the model configuration – this is where we "configure Hugging Face model"
model_cfg = aocr.AsposeAIModelConfig()
model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"   # released early‑2026
model_cfg.hugging_face_quantization = "int8"                     # small memory footprint
model_cfg.gpu_layers = 20                                        # use first 20 layers on GPU
model_cfg.allow_auto_download = "true"

# Initialize the engine – it will download the model if it's not already cached
ai_engine.initialize(model_cfg)
```

**Perché è importante:** Quantizzare a `int8` riduce il modello da diversi gigabyte a meno di un gigabyte, rendendolo fattibile su laptop. Limitare i layer GPU bilancia velocità e utilizzo della VRAM—perfetto per una scheda da 6 GB.

> **Consiglio pro:** Se incontri errori di out‑of‑memory, riduci `gpu_layers` a `10` o passa `quantization` a `"float16"` per un modello leggermente più grande che comunque entra nella maggior parte delle GPU consumer.

---

## Passo 2: Caricare PDF per OCR

Ora che il motore AI è pronto, dobbiamo **caricare PDF per OCR**. La libreria Aspose OCR tratta PDF e immagini in modo uniforme, così puoi puntare a un percorso file o a uno stream.

```python
# Create the OCR engine that will perform the initial text extraction
ocr_engine = aocr.OcrEngine()

# Attach the AI post‑processor – we’ll use the default run_postprocessor method
ocr_engine.set_post_processor(ai_engine.run_postprocessor, None)  # no custom settings required

# Load the PDF document – this is the step where we "load PDF for OCR"
input_image = aocr.Image.from_file("YOUR_DIRECTORY/invoice_2026.pdf")
```

**Perché è importante:** Caricando il PDF direttamente in un oggetto `Image`, il motore OCR può gestire PDF multi‑pagina pagina‑per‑pagina in background. Non è necessario suddividere manualmente il PDF in immagini.

> **Attenzione:** Se il tuo PDF contiene pagine criptate, dovrai fornire la password tramite `Image.from_file(..., password="secret")`.

---

## Passo 3: Eseguire OCR su PDF

Con il documento in memoria, è il momento di **eseguire OCR su PDF**. Il primo passaggio ci fornisce il testo grezzo, spesso pieno di errori di spaziatura, caratteri riconosciuti in modo errato o punteggiatura mancante—soprattutto nelle fatture scansionate.

```python
# Perform the plain OCR pass – this is the core "run OCR on PDF" operation
raw_result = ocr_engine.recognize(input_image)  # raw OCR output
```

A questo punto `raw_result.text` contiene l'output OCR non modificato. Puoi ispezionarlo, registrarlo, o anche alimentarlo a pipeline successive. 

> **Nota a margine:** Il metodo `recognize` rileva automaticamente l'orientamento della pagina e tenta di correggere lo skew, ma non risolve le stranezze specifiche della lingua—ecco dove brilla il post‑processore AI.

---

## Passo 4: Migliorare l'accuratezza OCR con il post‑processore AI

Ora la parte divertente: **migliorare l'accuratezza OCR**. Inviando il risultato grezzo al motore AI configurato in precedenza, lasciamo che un grande modello linguistico pulisca il testo, corregga gli errori di battitura e persino inferisca valori mancanti.

```python
# Enhance the raw OCR output using the AI post‑processor
enhanced_result = ocr_engine.run_postprocessor(raw_result)
```

Il post‑processore esegue il LLM su ogni riga (o blocco) di testo, applicando un prompt che gli chiede di “pulire gli errori OCR mantenendo il significato originale”. Il risultato è una versione levigata, notevolmente più leggibile.

**Perché funziona:** I moderni LLM hanno una forte comprensione dei pattern linguistici e possono inferire la parola desiderata quando l'OCR fornisce un token confuso. Accoppiato al modello quantizzato `int8`, il miglioramento avviene in meno di un secondo per una tipica fattura di una pagina.

---

## Passo 5: Revisionare i risultati

Infine, stampiamo sia l'output grezzo sia quello migliorato dall'AI affiancati, così puoi vedere la differenza con i tuoi occhi.

```python
print("=== Raw OCR ===")
print(raw_result.text)

print("\n=== AI‑enhanced ===")
print(enhanced_result.text)
```

**Output atteso (troncato):**

```
=== Raw OCR ===
Inv0ice N0: 2026-00123
Date: 01/02/2026
Tot@l Am0unt: $1,234.56
...

=== AI‑enhanced ===
Invoice No: 2026-00123
Date: 01/02/2026
Total Amount: $1,234.56
...
```

Nota come la versione migliorata dall'AI abbia corretto le confusioni di zero‑lettera (`Inv0ice` → `Invoice`) e rimosso il simbolo `@` errato. Per la maggior parte dei documenti vedrai una riduzione degli errori OCR del 30‑80 %.

> **Consiglio pro:** Se ti serve il testo migliorato in un formato strutturato (ad es., JSON), puoi post‑processare ulteriormente `enhanced_result` con regex o una piccola funzione di parsing.

---

## Opzionale: Visualizzare il processo

Di seguito trovi un semplice diagramma che illustra il flusso. Il testo alternativo contiene la keyword principale per soddisfare la SEO.

![Diagram showing steps to run OCR on PDF and improve OCR accuracy with an AI post‑processor](run-ocr-on-pdf-diagram.png)

---

## Domande frequenti & casi limite

### E se il PDF è multi‑pagina?

La chiamata `Image.from_file` crea automaticamente un oggetto immagine multi‑frame. Itera su `input_image.frames` e chiama `ocr_engine.recognize` per ogni frame, poi concatena i risultati prima di eseguire il post‑processore.

```python
pages_text = []
for frame in input_image.frames:
    raw = ocr_engine.recognize(frame)
    enhanced = ocr_engine.run_postprocessor(raw)
    pages_text.append(enhanced.text)

full_text = "\n".join(pages_text)
```

### Come gestire lingue diverse dall'inglese?

Imposta la proprietà `language` del motore OCR prima del riconoscimento:

```python
ocr_engine.language = aocr.Language.French  # or aocr.Language.Spanish, etc.
```

Il LLM migliorerà comunque l'accuratezza finché il modello che **configuri Hugging Face model** supporta la lingua target (la maggior parte lo fa).

### Posso eseguire tutto solo su CPU?

Sì—basta omettere `model_cfg.gpu_layers` o impostarlo a `0`. Il modello verrà eseguito interamente su CPU, anche se l'inferenza sarà più lenta (circa 5‑10 secondi per pagina su un i7 moderno).

---

## Riepilogo

Abbiamo coperto tutto ciò che ti serve per **eseguire OCR su PDF** e **migliorare l'accuratezza OCR**:

1. **Configura il modello Hugging Face** con quantizzazione e layer GPU.  
2. **Carica PDF per OCR** usando `Image.from_file` di Aspose OCR.  
3. **Esegui OCR su PDF** per ottenere il testo grezzo.  
4. **Migliora l'accuratezza OCR** passando il risultato a un post‑processore AI.  
5. **Revisiona** entrambi gli output, grezzo e migliorato.

Sentiti libero di sperimentare—sostituisci l'ID del repository del modello con un LLM più recente, modifica il prompt dentro `ai_engine.run_postprocessor` (se esplori il suo codice), o aggiungi passaggi di pre‑processing personalizzati come il deskew. La pipeline è modulare, quindi puoi sostituire qualsiasi componente senza rompere il resto.

---

## Prossimi passi

* **Esplora altri modelli di post‑processing** – prova una variante `distilbert` più piccola se lavori su una macchina a bassa potenza.  
* **Integra con un database** – archivia il testo migliorato in SQLite o Elasticsearch per archivi ricercabili.  
* **Aggiungi generazione PDF** – usa `reportlab` o `pypdf` per annotare il PDF originale con il testo pulito.  

Se hai seguito la guida, ora possiedi una solida base per costruire documenti robusti e potenziati dall'AI.

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci alternativi nei tuoi progetti.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [如何在 .NET 中使用 Aspose.OCR 進行 PDF OCR](/ocr/hongkong/net/text-recognition/recognize-pdf/)
- [.NET에서 Aspose.OCR을 사용하여 PDF OCR하는 방법](/ocr/korean/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}