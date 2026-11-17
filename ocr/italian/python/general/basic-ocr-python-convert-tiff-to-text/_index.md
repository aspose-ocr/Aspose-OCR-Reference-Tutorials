---
category: general
date: 2026-03-18
description: Il tutorial base di OCR in Python mostra come convertire TIFF in testo,
  caricare l'OCR dell'immagine, impostare i layer GPU e correggere gli zeri iniziali
  con Aspose AI.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: it
og_description: Il tutorial base di OCR in Python ti guida nella conversione di file
  TIFF in testo pulito, nel caricamento delle immagini, nella configurazione dei layer
  GPU e nella correzione degli zero iniziali.
og_title: OCR di base in Python – converti TIFF in testo
tags:
- OCR
- Python
- AI
- Aspose
title: OCR di base in Python – converti TIFF in testo
url: /it/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – Converti TIFF in Testo con AI Post‑Processing

Cerchi un modo per fare **basic ocr python** sui tuoi documenti scansionati? In questa guida ti mostreremo come convertire un file TIFF in testo pulito e ricercabile usando Aspose OCR e un post‑processor AI.  

Se hai mai avuto difficoltà a **convert TIFF to text** perché l'output grezzo è pieno di errori di battitura o simboli strani, non sei solo. Ti mostreremo anche come **load image OCR**, regolare il motore per **set GPU layers**, e persino **fix leading zeroes** che compaiono spesso nei numeri di fattura.

## What You’ll Learn

- Come inizializzare il motore Aspose OCR per documenti stampati.  
- I passaggi esatti per **load image OCR** da un file TIFF e ottenere il testo grezzo.  
- Configurare un modello AI, scaricarlo automaticamente e **set GPU layers** per un'inferenza più veloce.  
- Aggiungere il controllo ortografico integrato più una funzione personalizzata che **fix leading zeroes**.  
- Pulire il risultato OCR e rilasciare correttamente le risorse.  

Al termine di questo tutorial avrai uno script Python unico e riutilizzabile che trasforma qualsiasi TIFF in testo rifinito e ricercabile—senza necessità di copia‑incolla manuale.  

### Prerequisiti

- Python 3.8+ installato sulla tua macchina.  
- Pacchetto `aspose-ocr` (`pip install aspose-ocr`).  
- Opzionale: una GPU con almeno 4 GB VRAM se desideri **set GPU layers**; altrimenti il codice ricade automaticamente sulla CPU.  

---

## basic ocr python – carica immagine e riconosci testo

La prima cosa da fare è **load image OCR** così il motore può leggere i pixel. L’`OcrEngine` di Aspose gestisce molti formati, ma qui ci concentriamo su TIFF perché è il più comune per le fatture scansionate.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Pro tip:** Se lavori con TIFF multi‑pagina, Aspose elabora automaticamente ogni pagina in sequenza, quindi non servono loop aggiuntivi.

Ora che l’immagine è caricata, eseguiamo un passaggio di riconoscimento di base.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

Vedrai qualcosa di simile:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Nota gli *zero* prima delle lettere? È un classico artefatto OCR che puliremo più tardi.

![flusso di lavoro basic ocr python](/images/ocr-workflow.png "diagramma del flusso di lavoro basic ocr python")

---

## Step 2: Converti TIFF in testo – prepara il post‑processor AI

L’OCR grezzo è utile, ma la maggior parte delle pipeline di produzione richiede una versione rifinita. Aspose fornisce un wrapper `AsposeAI` che può scaricare un modello da Hugging Face, eseguirlo sulla GPU e applicare automaticamente il controllo ortografico.

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### Perché `set GPU layers` è importante

Il parametro `gpu_layers` indica al modello GGUF sottostante quante layer del transformer mantenere sulla GPU. Più layer = inferenza più veloce ma maggiore utilizzo di VRAM. Se usi un laptop modesto, riduci il valore a `10` o ometti del tutto per rimanere sulla CPU.

---

## Step 3: Applica il controllo ortografico e **fix leading zeroes**

Aspose AI include un correttore ortografico integrato, che cattura la maggior parte degli errori di battitura in inglese. Tuttavia, correzioni specifiche del dominio—come trasformare uno `0` iniziale in una `O` per i codici di fattura—richiedono un post‑processor personalizzato.

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **Why this works:** L’espressione regolare cerca un confine di parola (`\b`), uno zero, poi esattamente tre lettere maiuscole. Sostituisce quindi lo zero con la lettera “O”. Puoi estendere il pattern per altre stranezze (es., `0[0-9]{2}` per numeri letti erroneamente).

---

## Step 4: Pulisci il risultato OCR con il post‑processor AI

Ora combiniamo tutto: la stringa grezza da **basic ocr python**, il controllo ortografico e la nostra correzione dei zero. Il metodo `run_postprocessor` restituisce una versione pulita pronta per i sistemi a valle.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

Output tipico dopo il post‑processor:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Puoi vedere che lo zero iniziale è stato trasformato in una `O`, e gli errori di battitura più comuni sono corretti. Il testo è ora adatto per l’indicizzazione in un motore di ricerca o per l’alimentazione a una pipeline di estrazione dati.

---

## Step 5: Rilascia le risorse AI – mantieni felice la tua GPU

Se esegui più lavori OCR in un servizio a lungo termine, è buona pratica liberare la memoria GPU del modello quando hai finito.

```python
ocr_ai.free_resources()
```

Saltare questo passaggio può causare errori “out‑of‑memory” nelle chiamate successive, specialmente quando **set GPU layers** è impostato a un valore alto.

---

## Varianti opzionali e casi limite

| Situazione | Cosa cambiare |
|------------|---------------|
| **Documenti scritti a mano** | Usa `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` invece di `PRINTED`. |
| **Nessuna GPU disponibile** | Imposta `gpu_layers=0` o ometti l'argomento; il modello verrà eseguito sulla CPU (più lento ma sicuro). |
| **Lingua diversa** | Sostituisci l'ID del repository Hugging Face con un modello specifico per la lingua, ad es., `microsoft/Florence-2-base`. |
| **Elaborazione batch** | Racchiudi i passaggi in un ciclo `for file in glob("*.tif"):` e accumula i risultati in una lista o CSV. |
| **Modelli di zero più complessi** | Estendi `invoice_fix` con regex aggiuntive, come `r"\b0+([A-Z]{2,})\b"` per più zero iniziali. |

---

## Conclusione

Abbiamo appena completato una pipeline **basic ocr python** che carica un TIFF, estrae testo grezzo e lo pulisce usando un modello AI mentre **set GPU layers** per le prestazioni. Il post‑processor personalizzato dimostra come **fix leading zeroes**, un dettaglio piccolo ma spesso trascurato che può compromettere le analisi a valle.

Sentiti libero di sperimentare: prova una quantizzazione diversa (`float16` per maggiore accuratezza), sostituisci il controllo ortografico con un dizionario specifico per il dominio, o concatena più correzioni personalizzate. Il modello rimane lo stesso—carica, riconosci, configura AI, post‑processa e pulisci.

**Prossimi passi** che potresti esplorare includono:

- Integrare l'output pulito con un database o un indice Elasticsearch.  
- Usare lo stesso approccio per **convert TIFF to text** per PDF multilingua.  
- Aggiungere un’interfaccia UI con Flask o FastAPI così gli utenti non tecnici possono caricare file e ricevere testo pulito istantaneamente.  

Buon coding, e che i tuoi risultati OCR siano sempre nitidi e privi di zero!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}