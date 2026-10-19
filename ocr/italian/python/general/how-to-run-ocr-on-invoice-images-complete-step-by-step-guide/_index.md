---
category: general
date: 2026-01-12
description: Come eseguire l'OCR e estrarre il testo dalle immagini di fatture usando
  Aspose OCR e un modello leggero di Hugging Face. Impara a scaricare il modello,
  correggere gli errori OCR e eseguire l'OCR sull'immagine.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: it
og_description: Come eseguire l'OCR su immagini di fatture, estrarre il testo e correggere
  gli errori con un LLM di Hugging Face. Segui questa guida completa per risultati
  impeccabili.
og_title: Come eseguire l'OCR su immagini di fatture – Tutorial completo
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: Come eseguire l'OCR su immagini di fatture – Guida completa passo passo
url: /it/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR su immagini di fatture – Guida completa passo‑passo

Ti sei mai chiesto **come eseguire OCR** su una fattura scannerizzata e ottenere testo pulito e ricercabile senza passare ore a pulirlo? Non sei il solo. In molti progetti reali l'output grezzo dell'OCR è pieno di errori di riconoscimento — pensa a “O” al posto di “0”, “l” al posto di “1”, o addirittura intere parole distorte. La buona notizia? Con poche righe di Python puoi non solo **perform OCR on image** files ma anche correggere automaticamente **correct OCR errors** usando un modello leggero da Hugging Face.

In questo tutorial ti guideremo passo passo su tutto ciò che devi sapere: dal caricamento di un'immagine di fattura, all'estrazione del testo grezzo, al download di un modello quantizzato, fino alla rifinitura del risultato in modo da ottenere una trascrizione perfetta pronta per l'elaborazione successiva. Alla fine sarai in grado di **extract text from invoice** PDF o PNG in un unico script ripetibile.

## Prerequisiti e configurazione

Prima di immergerti, assicurati di avere:

| Requisito | Perché è importante |
|-------------|----------------|
| Python 3.9+ | Sintassi moderna e type hints |
| `aspose-ocr` package | Fornisce il `ocr.OcrEngine` usato nell'esempio |
| `aspose-ai` package | Fornisce il post‑processor `AsposeAI` |
| Access to a GPU (optional) | Accelera i layer LLM; altrimenti la CPU funziona bene |
| Internet connection (first run) | Necessario per **download Hugging Face model** automaticamente |

Puoi installare le librerie richieste con:

```bash
pip install aspose-ocr aspose-ai
```

> **Pro tip:** Se prevedi di eseguire il LLM su GPU, installa `torch` con supporto CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

Ora che l'ambiente è pronto, entriamo nel codice.

---

## Passo 1 – Inizializzare il motore OCR e caricare l'immagine della fattura

La prima cosa da fare è creare un'istanza del motore OCR di Aspose e puntarlo al file che vuoi elaborare. Questo passo è la base di **how to run OCR** su qualsiasi immagine.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Perché è importante:** `load_image` accetta PNG, JPEG, TIFF e anche pagine PDF, permettendoti di **perform OCR on image** dati indipendentemente dal formato.

---

## Passo 2 – Eseguire OCR di base per catturare il testo grezzo

Una volta caricata l'immagine, il motore può produrre una trascrizione grezza. Questo output è spesso rumoroso, motivo per cui più tardi eseguiremo un passo di correzione.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

Typical raw output might look like:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

Nota gli zero (`0`) dove dovrebbe esserci la lettera “O”? È esattamente il tipo di errore che correggeremo più tardi.

---

## Passo 3 – Configurare il post‑processor AI con un LLM leggero

Ora introduciamo un **download Hugging Face model** abbastanza piccolo da funzionare su hardware modesto ma sufficientemente potente da comprendere il linguaggio delle fatture. L'esempio utilizza il modello Qwen 2.5 3B‑Instruct GGUF, quantizzato a `int8` per un'impronta di memoria minima.

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **Perché questo modello?** La quantizzazione `int8` riduce il file a ~1,2 GB, rendendolo fattibile sulla maggior parte dei laptop. I layer GPU accelerano l'inferenza, ma il codice ricade elegantemente sulla CPU quando non viene trovata una GPU.

---

## Passo 4 – Eseguire la correzione basata su LLM sul risultato OCR grezzo

Con il modello pronto, alimentiamo il testo grezzo nel post‑processor. L'LLM riscriverà la trascrizione, correggendo i comuni errori OCR e normalizzando i numeri.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

Expected cleaned output:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

Puoi vedere che gli zero sono tornati alla lettera “O”, e “Am0unt” è ora “Amount”. Questo è il fulcro di **correct OCR errors** automaticamente.

---

## Passo 5 – Rilasciare le risorse e pulire

I grandi modelli di linguaggio possono occupare memoria GPU, quindi è buona pratica liberare le risorse quando hai finito.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

Se prevedi di elaborare molte fatture in batch, potresti mantenere il modello caricato e liberarlo solo alla fine dello script.

---

## Esempio completo funzionante

Mettendo tutto insieme, ecco un unico script che puoi inserire in un file `.py` e eseguire:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

Eseguire lo script dovrebbe produrre un output simile al blocco “AI‑corrected” mostrato prima. Sentiti libero di sostituire il percorso dell'immagine con qualsiasi altra fattura o ricevuta per **extract text from invoice** file in blocco.

---

## Domande frequenti e casi particolari

### E se non ho una GPU?

Il parametro `gpu_layers` è opzionale. Impostalo a `0` o omettilo, e il modello verrà eseguito interamente su CPU. Aspettati un'inferenza più lenta — circa 2–3 secondi per pagina su un laptop moderno.

### Le mie fatture sono PDF multi‑pagina. Come le gestisco?

Converti ogni pagina in un'immagine separata (ad es., usando `pdf2image`) e itera sulle pagine con lo stesso script. Il motore OCR può elaborare ogni immagine indipendentemente, e l'LLM correggerà ogni blocco di testo.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### Il download del modello fallisce dietro un firewall?

Scarica il modello manualmente dal hub dei modelli Hugging Face, decomprimilo in una cartella locale e imposta `hugging_face_repo_id` sul percorso locale:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### Quanto è accurata la correzione?

Per le tipiche fatture in lingua inglese, l'LLM corregge >95 % degli errori OCR comuni. Note scritte a mano complesse potrebbero comunque richiedere una revisione manuale.

---

## Consigli e trucchi per l'uso in produzione

- **Batch processing:** Raggruppare i passi 2‑4 in una funzione e fornire una lista di percorsi file. Riutilizzare la stessa istanza `AsposeAI` per evitare di ricaricare il modello.  
- **Logging:** Sostituire `print` con il modulo `logging` di Python per catturare sia gli output grezzi che corretti per le tracce di audit.  
- **Error handling:** Avvolgere la chiamata OCR con blocchi `try/except`. Se un'immagine fallisce, registrare il nome file e continuare.  
- **Performance tuning:** Sperimentare con `gpu_layers`. Più layer su GPU accelerano l'inferenza ma aumentano l'uso di VRAM.  

---

## Conclusione

Abbiamo coperto **how to run OCR** su immagini di fatture dall'inizio alla fine, mostrandoti come **perform OCR on image**, **download Hugging Face model**, e **correct OCR errors** automaticamente. Lo script completo dimostra un flusso di lavoro pratico che puoi inserire in qualsiasi pipeline di automazione basata su Python.

Prossimi passi? Prova ad estendere il pipeline per **extract key fields** (numero fattura, data, totale) usando espressioni regolari sul testo corretto, o inserisci l'output pulito in un database per record ricercabili. Potresti anche sperimentare altri LLM leggeri da Hugging Face se ti serve una lingua diversa o conoscenza specifica di dominio.

Buon coding, e che i tuoi risultati OCR siano sempre cristallini! 

![come eseguire OCR su un'immagine di fattura](ocr_invoice_example.png "come eseguire OCR su fattura")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}