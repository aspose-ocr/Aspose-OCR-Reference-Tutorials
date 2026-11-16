---
category: general
date: 2026-03-26
description: Crea un poligono ROI per eseguire l'OCR sull'area selezionata. Scopri
  come definire più regioni, registrarle ed estrarre il testo con un motore OCR Python.
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: it
og_description: Crea un poligono ROI ed esegui OCR sull'area selezionata con un motore
  Python. Codice completo, spiegazioni e consigli inclusi.
og_title: Crea poligono ROI – OCR rapido sull'area selezionata
tags:
- OCR
- Python
- Image Processing
title: Crea Poligono ROI – Guida passo‑passo per OCR sull'area selezionata
url: /it/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea Poligono ROI – Tutorial Completo per OCR su Area Selezionata

Hai mai avuto bisogno di **creare un poligono ROI** così da poter eseguire OCR solo sulla parte dell'immagine che interessa? Forse stai scansionando ricevute e ti interessano solo i totali, o hai un modulo in cui è necessario leggere solo il campo della firma. In questi casi, **ocr su area selezionata** fa risparmiare tempo e aumenta la precisione.  

In questa guida percorreremo tutto ciò di cui hai bisogno: dalla definizione di due poligoni, alla registrazione con un motore OCR, fino a estrarre il testo riconosciuto in una singola chiamata pulita. Alla fine avrai uno script pronto all'uso e una solida comprensione del perché concentrarsi sulle regioni di interesse è importante.

## Cosa Imparerai

- Come **creare oggetti poligono ROI** usando una tipica libreria OCR.
- La differenza tra definire una singola regione e più regioni.
- Come registrare quelle regioni con il motore affinché venga eseguito `ocr on selected area`.
- Output previsto e come risolvere le difficoltà comuni (ad esempio, ROI sovrapposti, risultati vuoti).

### Prerequisiti

- Python 3.8+ installato.
- Una libreria OCR che espone i metodi `Polygon`, `Point` e `add_region_of_interest` (l'esempio utilizza un modulo `ocr` fittizio; sostituiscilo con il tuo SDK reale, come i wrapper Tesseract‑Python o EasyOCR).
- Un file immagine di esempio (`sample.png`) che contiene testo all'interno delle coordinate mostrate di seguito.

> **Consiglio professionale:** Se stai usando una libreria reale, assicurati che l'immagine sia caricata nello stesso spazio di coordinate (origine in alto‑sinistra, X che aumenta verso destra, Y che aumenta verso il basso).  

---  

## Passo 1: Importa il Modulo OCR e Carica la Tua Immagine  

Per prima cosa, porta il pacchetto OCR nello scope e leggi l'immagine che vuoi elaborare.  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Perché è importante:* Il motore ha bisogno dei dati dell'immagine prima di poter allegare qualsiasi **poligono ROI**. Alcune librerie consentono anche di passare l'immagine più tardi, ma l'inizializzazione precoce mantiene il flusso di lavoro ordinato.

## Passo 2: Definisci il Primo Poligono ROI  

Ora creiamo la prima regione di interesse. Pensala come disegnare un rettangolo attorno all'intestazione di una tabella.  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Spiegazione:*  
- `ocr.Point(x, y)` utilizza coordinate in pixel.  
- L'elenco dei punti è ordinato in senso orario, come si aspetta la maggior parte dei motori.  
- Puoi aggiungere quanti punti desideri per creare forme irregolari; un rettangolo è solo un caso speciale.

## Passo 3: Definisci Poligoni ROI Aggiuntivi (Opzionale)  

Non devi fermarti a uno solo. Ecco un secondo poligono che cattura un campo firma più in basso nella pagina.  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*Perché aggiungerne altri?* Eseguire **ocr su area selezionata** per più zone ti consente di estrarre dati disparati in un unico passaggio, il che è molto più veloce rispetto al ritaglio e all'elaborazione di ogni sezione separatamente.

## Passo 4: Registra i ROI con il Motore OCR  

Con i poligoni pronti, indica al motore quali aree ispezionare.  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Nota importante:* Alcuni SDK richiedono di chiamare il metodo `clear_regions()` prima di aggiungerne di nuovi se riutilizzi il motore per un'altra immagine.

## Passo 5: Esegui OCR e Recupera il Testo  

Infine, avvia il riconoscimento. Il motore guarderà solo all'interno dei poligoni appena aggiunti.  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Output previsto** (supponendo che `sample.png` contenga le parole “Invoice Total: $123.45” nel primo ROI e “Signature: John Doe” nel secondo):

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

Se l'output è vuoto, verifica che le coordinate intersechino effettivamente del testo e che la risoluzione dell'immagine corrisponda al sistema di coordinate.

## Casi Limite & Problemi Comuni  

| Situazione                               | Cosa Controllare                               | Correzione / Soluzione Alternativa                              |
|------------------------------------------|------------------------------------------------|-----------------------------------------------------------------|
| **ROI sovrapposti**                      | Il testo potrebbe essere restituito due volte. | Mantieni i poligoni disgiunti o deduplica l'output.            |
| **ROI fuori dai limiti dell'immagine**   | Il motore potrebbe sollevare un errore o non restituire nulla. | Limita le coordinate a `0 ≤ x < width`, `0 ≤ y < height`. |
| **ROI molto piccolo**                    | La precisione OCR diminuisce a causa di pixel insufficienti. | Espandi il poligono di qualche pixel o ingrandisci prima l'immagine. |
| **Forma non rettangolare**               | Alcuni motori supportano solo poligoni convessi. | Dividi forme complesse in più ROI convessi. |
| **Cambio della dimensione dell'immagine**| Le coordinate hard‑coded diventano non valide. | Calcola le coordinate ROI relative alle dimensioni dell'immagine (ad esempio, percentuali). |

## Esempio Completo Funzionante  

Di seguito trovi lo script completo che puoi copiare‑incollare ed eseguire (sostituisci `ocr` con la tua libreria reale).  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

Eseguilo con `python ocr_roi_example.py` e dovresti vedere le stringhe estratte dalle due zone definite.

## Prossimi Passi  

- **Generazione dinamica di ROI:** Invece di codificare le coordinate, usa l'elaborazione delle immagini (ad esempio, rilevamento contorni con OpenCV) per individuare automaticamente tabelle o campi.  
- **Post‑elaborazione:** Rimuovi spazi bianchi, applica regex o converti i numeri nei tipi di dato appropriati.  
- **Elaborazione batch:** Cicla su una cartella di immagini, riutilizzando le stesse definizioni ROI se il layout è coerente.  

Se sei curioso di sapere come **ocr su area selezionata** funzioni per documenti più complessi—pensa a PDF multi‑pagina o moduli scansionati—esplora le librerie che supportano la registrazione di ROI per pagina.  

---  

### Panoramica Visiva  

![Diagramma che mostra due poligoni ROI su un'immagine di esempio](roi_diagram.png){alt="esempio di creazione di poligono ROI che mostra due aree selezionate"}

Il diagramma illustra come i due rettangoli (blu e verde) si mappano sull'immagine sottostante, evidenziando esattamente ciò che il motore OCR leggerà.

---  

## Conclusione  

Abbiamo appena **creato oggetti poligono ROI**, li abbiamo registrati con un motore OCR e abbiamo eseguito `ocr on selected area` in uno script pulito e riproducibile. Limitando il motore alle zone di tuo interesse, riduci i tempi di elaborazione, migliori la precisione e semplifichi notevolmente la gestione dei dati a valle.  

Provalo con le tue immagini—modifica le coordinate, aggiungi altri poligoni o collega l'output a un database. Il cielo è il limite una volta che padroneggi l'OCR basato su regioni.  

Hai domande o vuoi condividere un caso d'uso interessante? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}