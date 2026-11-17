---
category: general
date: 2026-04-26
description: Hoe threading te gebruiken om een afbeelding te laden voor OCR in Python.
  Leer asynchrone OCR-verwerking met callbacks, achtergrondthreads en het laden van
  afbeeldingen in slechts een paar stappen.
draft: false
keywords:
- how to use threading
- load image for OCR
- python threading OCR
- async OCR callback
- background thread image processing
language: nl
og_description: Hoe je threading gebruikt om een afbeelding te laden voor OCR in Python.
  Deze gids toont een volledig, uitvoerbaar voorbeeld met callbacks en achtergronduitvoering.
og_title: Hoe threading te gebruiken om een afbeelding te laden voor OCR
tags:
- Python
- Threading
- OCR
- Image Processing
title: Hoe threading te gebruiken om een afbeelding te laden voor OCR
url: /nl/python-java/general/how-to-use-threading-to-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe threading te gebruiken om een afbeelding te laden voor OCR

Heb je je ooit afgevraagd **hoe je threading** kunt gebruiken om een afbeelding te laden voor OCR zonder je app te laten bevriezen? Het is een scenario dat zich voordoet, of je nu een desktop‑scanner, een webservice of een simpel script maakt dat enorme afbeeldingen verwerkt. Het goede nieuws? Een paar regels Python en het juiste threading‑patroon houden je UI soepel terwijl de OCR‑engine zijn magie doet.

In deze tutorial lopen we een volledig, end‑to‑end voorbeeld door: een grote PNG laden, OCR starten op een achtergrondthread, en het resultaat afhandelen met een callback. Aan het einde weet je niet alleen **hoe je threading** moet gebruiken, maar ook hoe je **een afbeelding laadt voor OCR** op een nette, herbruikbare manier.

## Wat je nodig hebt

- Python 3.9+ (de syntaxis die we gebruiken werkt op elke recente versie)
- `pillow` voor afbeeldingsverwerking (`pip install pillow`)
- `pytesseract` als een dunne wrapper rond Tesseract OCR (`pip install pytesseract`)
- Tesseract OCR‑engine geïnstalleerd op je machine (download van [tesseract‑ocr.org](https://github.com/tesseract-ocr/tesseract))
- Een groot afbeeldingsbestand dat je wilt verwerken (`large_image.png` in deze gids)

Geen extra frameworks, geen async/await—alleen klassieke `threading` en een callback.

## Stap 1: Importeer de Threading‑module (vereist voor achtergronduitvoering)

Het eerste wat we doen is de `threading`‑module importeren. Deze levert de `Thread`‑klasse, waarmee we elke functie in een aparte OS‑thread kunnen uitvoeren.

```python
import threading
```

*Waarom dit belangrijk is*: Als je OCR op de hoofdthread uitvoert, bevriest je programma (vooral een GUI) totdat de OCR klaar is. Door het werk naar een achtergrondthread te delegeren, blijft de hoofdthread vrij om de UI bij te werken, gebruikersinvoer af te handelen of andere taken te starten.

## Stap 2: Definieer een callback die wordt aangeroepen wanneer OCR klaar is

Een callback is simpelweg een functie die door een ander stuk code wordt aangeroepen wanneer het klaar is. Hier printen we de herkende tekst, maar je zou het kunnen opslaan, over het netwerk kunnen sturen of een UI‑widget kunnen bijwerken.

```python
def ocr_done(result_text: str) -> None:
    """Called when the OCR thread finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)   # Display the recognized text
```

*Pro tip*: Houd de callback lichtgewicht. Zware verwerking binnen de callback ondermijnt het nut van threading, omdat het nog steeds de thread blokkeert die hem heeft aangeroepen (meestal de hoofdthread).

## Stap 3: Laad de afbeelding die je wilt verwerken

Het laden van de afbeelding is een apart aspect van OCR, maar maakt nog steeds deel uit van de algehele workflow. Met Pillow is dit triviaal.

```python
from PIL import Image

def load_image(path: str) -> Image.Image:
    """Loads an image from disk and returns a Pillow Image object."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img
    except Exception as exc:
        raise RuntimeError(f"Failed to load image: {exc}") from exc
```

*Waarom we het hier doen*: Als de afbeelding enorm is, kan het laden op de hoofdthread al een hapering veroorzaken. In veel real‑world apps zou je het laden ook naar een thread verplaatsen, maar voor de duidelijkheid houden we het synchronisch.

## Stap 4: Maak een kleine OCR‑engine wrapper

Het oorspronkelijke fragment gebruikte `engine.process_async`. We bootsen dat na met een kleine klasse die intern een thread start en de meegegeven callback aanroept wanneer het klaar is.

```python
import pytesseract

class SimpleOcrEngine:
    """A minimal OCR engine that runs pytesseract in a background thread."""

    def __init__(self, image: Image.Image):
        self.image = image

    def _run_ocr(self, callback):
        """Internal method executed in the worker thread."""
        try:
            # pytesseract returns the recognized text as a plain string
            text = pytesseract.image_to_string(self.image)
            callback(text)
        except Exception as exc:
            callback(f"OCR failed: {exc}")

    def process_async(self, callback):
        """Public method to start OCR on a new thread."""
        worker = threading.Thread(target=self._run_ocr, args=(callback,))
        worker.daemon = True          # Daemon so it won’t block program exit
        worker.start()
        print("OCR thread started…")
```

*Uitleg*:  
- `_run_ocr` doet het zware werk.  
- `process_async` maakt een `Thread`‑object, markeert het als daemon (zodat de interpreter kan afsluiten zelfs als de thread nog draait), en start het.  
- De callback ontvangt ofwel de OCR‑tekst of een foutmelding.

## Stap 5: Koppel alles samen en doe ander werk terwijl OCR draait

Nu orkestreren we de volledige stroom: laad de afbeelding, instantiate de engine, start de async OCR, en houd de hoofdthread bezig met iets anders (hier printen we gewoon een bericht).

```python
if __name__ == "__main__":
    # 1️⃣ Load the image you want to OCR
    img_path = "YOUR_DIRECTORY/large_image.png"
    image = load_image(img_path)

    # 2️⃣ Create the OCR engine instance
    engine = SimpleOcrEngine(image)

    # 3️⃣ Start OCR on a background thread, passing our callback
    engine.process_async(callback=ocr_done)

    # 4️⃣ Do other work while OCR runs (simulated with a loop)
    for i in range(5):
        print(f"Main thread doing other work… ({i+1}/5)")
        # In a real app you might update a progress bar, handle UI events, etc.
        threading.Event().wait(0.5)  # Sleep 0.5 s without blocking the OS thread

    # Give the OCR thread a moment to finish before the script exits
    threading.Event().wait(2)
    print("Script finished.")
```

**Verwachte output (ingekort voor de leesbaarheid):**

```
Image 'YOUR_DIRECTORY/large_image.png' loaded – size: (3840, 2160)
OCR thread started…
Main thread doing other work… (1/5)
Main thread doing other work… (2/5)
...
--- Async OCR finished ---
The quick brown fox jumps over the lazy dog.
Script finished.
```

Als de OCR faalt, zal de callback een foutmelding printen in plaats van de tekst.

---

## Waarom deze aanpak beter werkt dan een eenvoudige lus

- **Responsiveness**: De hoofdthread blokkeert nooit op de OCR‑aanroep, die seconden kan duren voor grote afbeeldingen.
- **Scalability**: Je kunt meerdere `SimpleOcrEngine`‑instanties opstarten, elk in zijn eigen thread, om een batch afbeeldingen gelijktijdig te verwerken.
- **Separation of Concerns**: Laden, verwerken en resultaatafhandeling zijn duidelijk gescheiden, waardoor de code makkelijker te testen en te onderhouden is.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Probleem | Wat gebeurt er | Oplossing |
|----------|----------------|-----------|
| Vergeten de thread als *daemon* te markeren | Het script blijft hangen nadat het hoofdwerk klaar is omdat de OCR‑thread nog leeft. | Zet `worker.daemon = True` **of** `join()` de thread vóór het afsluiten. |
| Een globale variabele voor het resultaat gebruiken zonder locks | Race‑conditions kunnen de data corrupt maken wanneer meerdere threads tegelijk schrijven. | Geef het resultaat via een callback (zoals we doen) of gebruik thread‑veilige containers zoals `queue.Queue`. |
| Een enorme afbeelding laden op de hoofdthread | UI bevriest voordat de achtergrond‑OCR zelfs maar start. | Laad de afbeelding ook naar een thread, of gebruik lazy‑loading technieken. |
| Geen uitzonderingen afhandelen in de worker‑thread | Niet‑afgevangen uitzonderingen doden de thread stilletjes, waardoor je geen resultaat krijgt. | Omring OCR‑logica met `try/except` en stuur de fout door naar de callback. |

## Deze patroon uitbreiden

- **Voortgangsrapportage**: Gebruik een gedeelde `queue.Queue` om tussentijdse voortgangspercentages van de OCR‑thread naar de hoofdthread te sturen.
- **Thread‑pool**: Voor batchverwerking, vervang individuele `Thread`‑objecten door een `concurrent.futures.ThreadPoolExecutor`.
- **GUI‑integratie**: In een Tkinter‑ of PyQt‑app, plan de callback met `after()` (Tkinter) of `QTimer.singleShot` (Qt) om er zeker van te zijn dat UI‑updates op de hoofdthread plaatsvinden.

## Volledig werkend voorbeeld (Kopieer‑en‑Plak klaar)

```python
import threading
from PIL import Image
import pytesseract

def ocr_done(result_text: str) -> None:
    """Callback invoked when OCR finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)

def load_image(path: str) -> Image.Image:
    """Load an image and report its size."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}