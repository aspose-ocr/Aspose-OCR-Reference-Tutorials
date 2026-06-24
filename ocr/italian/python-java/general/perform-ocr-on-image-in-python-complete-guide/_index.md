---
category: general
date: 2026-06-22
description: Esegui OCR su un'immagine usando Python in poche righe. Scopri come caricare
  l'immagine per l'OCR, riconoscere il testo da un PNG e utilizzare il motore OCR
  in modo efficiente.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: it
og_description: Esegui OCR su un'immagine rapidamente con Python. Questo tutorial
  mostra come caricare l'immagine per l'OCR, riconoscere il testo da un PNG e utilizzare
  il motore OCR con fiducia.
og_title: Esegui OCR su un'immagine in Python – Guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Esegui OCR su immagine in Python – Guida completa
url: /it/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine in Python – Guida Completa

Hai mai dovuto **eseguire OCR su file immagine** ma ti sei bloccato alla prima riga di codice? Non sei solo. In questo tutorial ti mostreremo esattamente come **caricare l'immagine per OCR**, configurare un motore OCR leggero e infine **riconoscere il testo da PNG** con pochi comandi.

Copriamo tutto, dall'installazione della libreria alla personalizzazione della whitelist in modo che solo cifre e lettere maiuscole vengano riconosciute. Alla fine avrai uno script pronto all'uso da inserire in qualsiasi progetto—senza misteri, senza superflui.

## Cosa Imparerai

- Come **usare il motore OCR** programmaticamente in Python.  
- I passaggi esatti per **caricare l'immagine per OCR** da una cartella locale.  
- Perché e come limitare il riconoscimento a un set di caratteri personalizzato.  
- Come **riconoscere il testo da PNG** e gestire il risultato in modo sicuro.  

**Prerequisiti:** Python 3.7+ installato, un terminale con cui ti trovi a tuo agio e un'immagine (ad es. `serial-number.png`) che vuoi leggere. Nessuna esperienza pregressa con OCR è necessaria.

---

## Esegui OCR su Immagine – Inizializza il Motore OCR

La prima cosa da fare è creare un'istanza del motore OCR. Pensa al motore come al cervello che analizzerà i pixel e li trasformerà in caratteri.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Perché è importante:* Senza un motore non c'è nulla che possa elaborare l'immagine. La classe `OcrEngine` raggruppa tutto il lavoro pesante—pre‑processing, segmentazione e classificazione dei caratteri—in un unico oggetto riutilizzabile.

---

## Carica Immagine per OCR – Fornisci il File PNG

Ora che il motore esiste, devi fornirgli l'immagine che vuoi leggere. La libreria si aspetta un oggetto `ImageStream`, che puoi creare direttamente da un percorso file.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Consiglio esperto:* Mantieni l'immagine in un formato ad alto contrasto (testo nero su sfondo bianco) ed evita artefatti di compressione; possono ostacolare l'algoritmo OCR.

---

## Limita i Caratteri – Whitelist di Cifre e Lettere Maiuscole

Spesso ti interessa solo un sottoinsieme di caratteri—ad esempio un numero di serie che contiene solo A‑Z e 0‑9. Impostando una whitelist indichi al motore di ignorare tutto il resto, migliorando notevolmente la precisione.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*Cosa succede dietro le quinte?* Il motore costruisce un filtro che scarta qualsiasi glifo non presente nella whitelist prima della fase finale di classificazione. Questo è particolarmente utile quando l'immagine contiene rumore o testo decorativo non necessario.

---

## Riconosci Testo da PNG – Avvia il Processo OCR

Con il motore pronto e l'immagine caricata, puoi finalmente **eseguire OCR su immagine**. La chiamata `recognize()` esegue l'intera pipeline e restituisce un oggetto risultato.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

Se sei curioso delle prestazioni, il metodo termina tipicamente in poche centinaia di millisecondi per un PNG di 300 × 200 px su un laptop moderno.

---

## Output e Verifica – Ottieni il Testo Riconosciuto

L'ultimo passo è estrarre il testo semplice dall'oggetto risultato. Qualsiasi cosa non corrisponda alla whitelist viene automaticamente scartata, così ottieni una stringa pulita pronta per ulteriori elaborazioni.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Output tipico:* `AB12C3D4E5` (supponendo che l'immagine contenga esattamente quel numero di serie).  

Se l'output è vuoto o illeggibile, ricontrolla la qualità dell'immagine e la whitelist; un errore comune è omettere accidentalmente caratteri necessari.

---

## Casi Limite e Problemi Comuni

| Situazione | Cosa Controllare | Correzione Suggerita |
|------------|------------------|----------------------|
| **File non trovato** | Errore di percorso o file mancante | Usa `os.path.abspath` per verificare il percorso completo prima di chiamare `set_image`. |
| **Immagine a basso contrasto** | Il testo si confonde con lo sfondo | Applica una soglia semplice (`Pillow` o `OpenCV`) prima di passare l'immagine al motore. |
| **Caratteri inattesi** | Whitelist troppo restrittiva | Aggiungi i caratteri mancanti alla stringa della whitelist. |
| **Immagini grandi** | Riconoscimento lento | Ridimensiona l'immagine a una larghezza massima di 1024 px; la qualità OCR rimane generalmente alta. |

---

## Script Completo – Pronto da Eseguire

Di seguito trovi lo script completo, autonomo, che unisce tutti i pezzi. Salvalo come `ocr_demo.py`, sostituisci `YOUR_DIRECTORY` con la cartella reale e avvia `python ocr_demo.py`.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Output console previsto* (quando il PNG contiene `SN12345`):

```
Recognized text: SN12345
```

---

## Conclusione

Ora sai esattamente come **eseguire OCR su immagine** in Python, dal **caricare l'immagine per OCR** al **riconoscere il testo da PNG** e infine estrarre un risultato pulito usando un **motore OCR** personalizzabile. L'approccio è semplice, estensibile e funziona subito per la maggior parte delle scansioni in stile numero di serie.

Cosa fare dopo? Prova a sostituire la whitelist con lettere minuscole, sperimenta con formati immagine diversi (JPEG, BMP) o integra lo script in una pipeline di elaborazione batch. Lo stesso schema—motore → immagine → impostazioni → riconoscimento → output—vale per praticamente qualsiasi compito OCR che incontrerai.

Hai domande o un'immagine ostinata che non collabora? Lascia un commento qui sotto, e buona programmazione! 

![Diagramma che illustra i passaggi per eseguire OCR su immagine usando Python](https://example.com/ocr-flow.png "Diagramma che mostra come eseguire OCR su immagine con un motore OCR Python")


## Cosa Dovresti Imparare Dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Converti Immagine in Testo – Esegui OCR su Immagine da URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Come Usare AspOCR: Filtri di Pre‑processamento Immagine per .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Come Estrarre Testo da Immagine Preparando Rettangoli in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}