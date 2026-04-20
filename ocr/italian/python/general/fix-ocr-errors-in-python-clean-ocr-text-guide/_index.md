---
category: general
date: 2026-03-18
description: Correggi rapidamente gli errori OCR in Python. Scopri come pulire l'OCR,
  come pulire il testo OCR, sostituire lo zero con O e applicare il post‑processing
  OCR in Python.
draft: false
keywords:
- fix OCR errors
- how to clean OCR
- clean OCR text python
- replace zero with O
- python OCR post processing
language: it
og_description: Correggi rapidamente gli errori OCR in Python. Scopri come pulire
  l'OCR, sostituire lo zero con la O e utilizzare il post‑processing OCR in Python
  in un unico tutorial.
og_title: Correggi gli errori OCR in Python – Guida alla pulizia del testo OCR
tags:
- OCR
- Python
- Text Cleaning
title: Correggi gli errori OCR in Python – Guida per pulire il testo OCR
url: /it/python/general/fix-ocr-errors-in-python-clean-ocr-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Correggere gli Errori OCR in Python – Guida alla Pulizia del Testo OCR

Ti è mai capitato di guardare una fattura scansionata e pensare, *“Come faccio a correggere gli errori OCR prima di inserirla nel mio database?”* Non sei l’unico. Nel mondo dell’automazione dei documenti, un singolo carattere letto male può interrompere un’intera pipeline, quindi imparare **come pulire l’output OCR** è fondamentale.  

In questo tutorial vedrai un modo pratico, end‑to‑end, per **correggere gli errori OCR** usando un piccolo post‑processore che sostituisce la cifra “0” con la lettera “O” — un inconveniente comune nei codici prodotto. Alla fine, potrai integrare la soluzione in qualsiasi workflow OCR Python e ottenere testo più pulito e affidabile.

> **Cosa otterrai:** uno script Python completo e eseguibile, spiegazioni sul perché ogni riga è importante, consigli per estendere la logica e un rapido sanity‑check dell’output previsto.

## Prerequisiti — Cosa Serve Prima di Iniziare

- Python 3.8 o superiore (la sintassi funziona su tutte le versioni recenti).  
- Una libreria OCR di base (ad es., Tesseract via `pytesseract`) che restituisce stringhe grezze.  
- Familiarità minima con funzioni e oggetti in Python.  

Se hai già un passaggio OCR che restituisce una stringa, sei pronto a partire — non servono installazioni aggiuntive per la parte di post‑processing.

## Passo 1: Configurare un Wrapper Minimal‑Tipo‑AI (Perché Ce Ne Serve)

In molti progetti il motore OCR vive all’interno di una classe più ampia “AI” che gestisce preprocessing, inference e post‑processing. Per mantenere l’esempio autonomo creeremo una piccola classe `AIProcessor` che imita questo pattern. Questo rende semplice inserire il codice in un code‑base esistente senza riscrivere nulla.

```python
# ai_wrapper.py
class AIProcessor:
    """
    Simple wrapper that stores a post‑processing callable.
    In real projects this could be a full‑fledged model class.
    """
    def __init__(self):
        self._post_processor = None

    def set_post_processor(self, func):
        """Register a function that will clean OCR output."""
        if not callable(func):
            raise TypeError("Post‑processor must be callable")
        self._post_processor = func

    def run_postprocessor(self, text):
        """Apply the registered post‑processor to raw OCR text."""
        if self._post_processor is None:
            raise RuntimeError("No post‑processor has been set")
        return self._post_processor(text)
```

**Perché è importante:** tenere il post‑processore separato dal motore OCR rispetta il principio della singola responsabilità e ti permette di scambiare la logica di pulizia senza toccare il codice OCR.

## Passo 2: Scrivere la Funzione che **Corregge gli Errori OCR**

Ora creiamo il cuore del tutorial: una funzione che **corregge gli errori OCR** scambiando il numero “0” con la lettera “O”. Questo schema copre codici prodotto, numeri di serie e qualsiasi identificatore alfanumerico in cui l’OCR confonde spesso i due caratteri.

```python
# post_processors.py
def correct_ocr_errors(text: str) -> str:
    """
    Replace common OCR mis‑reads.
    Example: change digit "0" to letter "O" in product codes.
    """
    # You could add more rules here, e.g.:
    # text = text.replace('1', 'I')
    # text = text.replace('5', 'S')
    return text.replace("0", "O")
```

**Perché sostituiamo 0 con O:** in molti font lo zero e la O maiuscola sono identici, quindi l’OCR spesso indovina quello sbagliato. Correggendolo subito, le convalide a valle (come i controlli regex) funzionano come previsto.

## Passo 3: Collegare il Post‑Processor all’Istanze AI

Con il wrapper e la funzione di pulizia pronti, li colleghiamo insieme. Questo rispecchia come registreresti un post‑processore personalizzato in una pipeline di produzione.

```python
# main.py
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Create the AI‑like object
ai = AIProcessor()

# Register our OCR‑fixing function
ai.set_post_processor(correct_ocr_errors)
```

Se dovessi **pulire l’output OCR** per un’altra lingua o formato di dati, basta scrivere un’altra funzione e chiamare nuovamente `set_post_processor` — non è necessario toccare il resto della pipeline.

## Passo 4: Fornire il Testo OCR Grezzo e Ottenere il Risultato Pulito

Simuliamo una stringa OCR grezza che contiene il temuto “0” in un codice prodotto. In uno scenario reale sostituirai il segnaposto con `pytesseract.image_to_string(image)` o una chiamata simile.

```python
# Simulated OCR output (replace with your own OCR call)
raw_text = "Product code: 10A0B"

# Run the post‑processor to obtain cleaned text
cleaned_text = ai.run_postprocessor(raw_text)

print("Before cleaning :", raw_text)
print("After cleaning  :", cleaned_text)
```

**Output previsto**

```
Before cleaning : Product code: 10A0B
After cleaning  : Product code: 1OAOB
```

Nota come gli zero sono diventati O maiuscole, fornendoci una stringa che corrisponde al formato atteso dalla maggior parte dei sistemi di inventario.

## Passo 5: Ampliare la Logica – Varianti del Mondo Reale

La semplice sostituzione sopra risolve un caso ristretto, ma in produzione incontrerai altre stranezze:

| Errore comune | Esempio OCR | Correzione desiderata | Come aggiungere |
|----------------|------------|-----------------------|-----------------|
| “1” letto come “I” | `I23` | `123` | `text = text.replace('I', '1')` |
| “5” letto come “S” | `S9` | `59` | `text = text.replace('S', '5')` |
| Spazi bianchi extra | `  ABC  ` | `ABC` | `text = text.strip()` |
| Confusione maiuscole/minuscole | `oRder` | `Order` | `text = text.title()` |

Puoi estendere `correct_ocr_errors` con una qualsiasi di queste regole. Mantieni ogni trasformazione **idempotente** (eseguirla due volte non deve cambiare il risultato) per evitare corruzioni accidentali dei dati.

```python
def correct_ocr_errors(text: str) -> str:
    text = text.replace("0", "O")
    text = text.replace("I", "1")
    text = text.replace("S", "5")
    return text.strip()
```

**Consiglio professionale:** se disponi di un catalogo noto di codici validi, considera di validare la stringa pulita con una regex o una tabella di lookup. Questo passaggio aggiuntivo cattura eventuali errori OCR residui che semplici sostituzioni di caratteri non rilevano.

## Passo 6: Integrare con un Motore OCR Reale (Opzionale)

Di seguito trovi una rapida illustrazione di come collegare il post‑processore a un flusso OCR reale usando `pytesseract`. Questa parte è opzionale ma mostra la pipeline end‑to‑end.

```python
import pytesseract
from PIL import Image
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Initialize AI wrapper and register the cleaner
ai = AIProcessor()
ai.set_post_processor(correct_ocr_errors)

# Load an image containing a product label
image = Image.open("sample_label.png")

# Perform OCR (this returns raw text)
raw_ocr = pytesseract.image_to_string(image)

# Clean the OCR output
cleaned = ai.run_postprocessor(raw_ocr)

print("Raw OCR   :", raw_ocr)
print("Cleaned   :", cleaned)
```

> **Nota:** `pytesseract` richiede che Tesseract OCR sia installato sul tuo sistema. Lo snippet sopra funziona su Windows, macOS e Linux purché il binario sia nel tuo PATH.

## Passo 7: Verificare i Risultati Programmaticamente

Quando automatizzi grandi lotti, è utile asserire che il passaggio di pulizia si sia comportato come previsto. Un test unitario rapido può far risparmiare ore di debug in seguito.

```python
def test_correct_ocr_errors():
    assert correct_ocr_errors("0O0") == "OOO"
    assert correct_ocr_errors(" 10A0B ") == "1OAOB"
    print("All tests passed!")

test_correct_ocr_errors()
```

Eseguire questo test conferma che la funzione **corregge gli errori OCR** in modo coerente, anche quando si infilano spazi extra.

## Illustrazione Immagine

Di seguito trovi uno schizzo visivo della pipeline (la keyword principale appare nel testo alt per SEO).

![Diagramma del flusso di correzione degli errori OCR – mostra l'OCR grezzo che alimenta un post‑processore che sostituisce lo zero con O]()

## Conclusione – Cosa Abbiamo Realizzato

Abbiamo percorso un esempio completo e eseguibile che mostra **come pulire l’output OCR** in Python, in particolare **come sostituire zero con O** e **correggere gli errori OCR** usando un post‑processore modulare. Separando la logica di pulizia dal motore OCR, ottieni flessibilità, testabilità e un punto chiaro dove aggiungere future regole, come *come pulire OCR* per altre confusioni di caratteri.

Pronto per il passo successivo? Prova ad aggiungere un validatore regex per i codici prodotto, sperimenta il fuzzy matching per testo rumoroso, o esplora una libreria completa come `ocrmypdf` che già include hook di post‑processing. Il pattern che abbiamo coperto scala bene, sia che tu gestisca una manciata di fatture sia milioni di documenti scansionati.

---

*Buon coding, e che le tue pipeline OCR rimangano prive di errori!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}