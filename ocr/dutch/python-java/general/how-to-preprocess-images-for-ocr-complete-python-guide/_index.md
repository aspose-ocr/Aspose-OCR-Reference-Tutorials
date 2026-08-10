---
category: general
date: 2026-06-06
description: Hoe afbeeldingen voor OCR te pre-processen met Python. Leer hoe je een
  afbeelding binariseert met Otsu, hoe je gescande documenten rechtzet en de OCR-nauwkeurigheid
  voor Duitse tekst verbetert.
draft: false
keywords:
- how to preprocess images for OCR
- binarize image using otsu
- how to deskew scanned documents
- how to improve OCR accuracy
- extract text from german image
language: nl
og_description: Hoe afbeeldingen voor OCR in Python voor te bewerken. Deze tutorial
  laat zien hoe je een afbeelding binariseert met Otsu, hoe je gescande documenten
  rechtzet, en hoe je de OCR-nauwkeurigheid voor Duitse afbeeldingen verbetert.
og_title: Hoe afbeeldingen voor OCR te preprocessen – Complete Python-gids
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  headline: How to Preprocess Images for OCR – Complete Python Guide
  type: TechArticle
- description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  name: How to Preprocess Images for OCR – Complete Python Guide
  steps:
  - name: How to Deskew Scanned Documents
    text: The `deskew` call above is the concrete answer to **how to deskew scanned
      documents**. Internally it estimates the dominant text line angle via Hough
      transform and rotates the image back. If your documents are rotated more than
      5°, bump `max_angle` up, but beware of over‑rotation artifacts.
  - name: Binarize Image Using Otsu
    text: The `binarize(method="otsu")` line directly answers the query **binarize
      image using otsu**. Otsu’s algorithm computes a threshold that minimizes intra‑class
      variance, which is perfect for documents with bimodal histograms (dark text
      vs. light background).
  - name: Expected Output
    text: 'Assuming the sample scan contains the sentence “Die schnelle braune Füchsin
      springt über den faulen Hund.” you should see something like:'
  type: HowTo
tags:
- OCR
- image preprocessing
- Python
- German language
title: Hoe afbeeldingen voor OCR te preprocessen – Complete Python-gids
url: /nl/python-java/general/how-to-preprocess-images-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe afbeeldingen voor OCR voor te bewerken – Complete Python-gids

Heb je je ooit afgevraagd **hoe je afbeeldingen voor OCR moet voorbewerken** zodat de tekst kristalhelder uitkomt? Je bent niet de enige. Gescande documenten—vooral ruisende Duitse pagina’s—kunnen een nachtmerrie zijn voor elke OCR-engine. Het goede nieuws? Een paar slimme voorbewerkingsstappen kunnen een wazige, vlekkerige scan omtoveren tot een schone, machinaal leesbare afbeelding.

In deze tutorial lopen we een praktisch voorbeeld door dat laat zien **hoe je afbeeldingen voor OCR moet voorbewerken** met Python. Je leert **afbeelding binariseren met Otsu**, **hoe je gescande documenten moet rechtzetten**, en in het algemeen **hoe je OCR-nauwkeurigheid kunt verbeteren** wanneer je **tekst wilt extraheren uit Duitse afbeelding**‑bestanden. Geen poespas, alleen een werkend script dat je vandaag nog kunt kopiëren‑plakken.

## Wat je nodig hebt

- **Python 3.9+** (elke recente versie werkt)
- Een OCR‑bibliotheek die een `OcrEngine`‑klasse exposeert – voor de demo gaan we uit van een generiek `ocr`‑pakket. Installeer het met `pip install ocr-lib`.
- Een ruisende Duitse scan (`noisy_german_scan.tif`) die je wilt testen.
- Een basisbegrip van Python‑functies (als je al een `def` hebt geschreven, ben je klaar).

> **Pro tip:** Als je een andere OCR‑SDK gebruikt (bijv. Tesseract via `pytesseract`), blijven de concepten hetzelfde—pas alleen de methodenamen aan.

## Overzicht van de oplossing

1. **Maak een OCR‑engine‑instantie.**  
2. **Stel de herkenningstaal in op Duits.**  
3. **Bouw een aangepaste voorbewerkings‑pipeline** die rechtzetten, denoising, binariseren (Otsu) en contrast‑stretching omvat.  
4. **Koppel de pipeline aan de engine** zodat elke afbeelding er automatisch doorheen gaat.  
5. **Voer de OCR uit** op een ruisende Duitse scan.  
6. **Print de geëxtraheerde tekst** om het resultaat te verifiëren.

Hieronder splitsen we elke stap uit, leggen **waarom** het belangrijk is, en tonen de exacte code die je nodig hebt.

![voorbeeld van hoe afbeeldingen voor OCR voor te bewerken](image.png "voorbeeld van hoe afbeeldingen voor OCR voor te bewerken")

## Stap 1: Maak een OCR‑engine‑instantie

Allereerst—zonder een engine gebeurt er niets. Het `OcrEngine`‑object is het toegangspunt dat alle latere verwerking coördineert.

```python
# Step 1: Initialize the OCR engine
from ocr import OcrEngine, Language

ocr_engine = OcrEngine()
```

*Waarom dit belangrijk is:* Het initialiseren van de engine zet interne bronnen (zoals taalmodellen) klaar en geeft je een schone basis om later een aangepaste pipeline aan te koppelen.

## Stap 2: Stel de herkenningstaal in op Duits

OCR‑nauwkeurigheid is sterk afhankelijk van de taal. Door de engine te laten weten dat hij Duits moet verwachten, activeer je de juiste tekenset en het juiste taalmodel.

```python
# Step 2: Tell the engine we’re working with German text
ocr_engine.set_recognition_language(Language.GERMAN)
```

Als je dit overslaat, kan de engine standaard op Engels staan en umlauts (ä, ö, ü) en het ß‑teken verkeerd herkennen—veelvoorkomende valkuilen bij Duitse scans.

## Stap 3: Bouw een aangepaste voorbewerkings‑pipeline

Dit is de kern van **hoe je afbeeldingen voor OCR moet voorbewerken**. We schakelen vier transformaties aan:

| Transformatie | Wat het doet | Waarom het helpt |
|----------------|--------------|------------------|
| **Deskew** | Roteert de afbeelding terug naar horizontaal (max 5°) | Scans zijn zelden perfect uitgelijnd; deskewing verwijdert de helling die karaktersegmentatie verstoort. |
| **Denoise** | Vermindert willekeurige vlekjes (sterkte 0.7) | Ruis creëert valse randen die de OCR-engine kan interpreteren als tekens. |
| **Binarize (Otsu)** | Converteert naar zwart‑wit met behulp van Otsu's methode | Een schone binaire afbeelding geeft de engine een scherp contrast tussen voorgrond (tekst) en achtergrond. |
| **Contrast Stretch** | Vergroot het dynamisch bereik | Verbeterde leesbaarheid van vage streken, vooral op oude documenten. |

```python
# Step 3: Assemble the preprocessing pipeline
preprocessing_pipeline = (
    ocr_engine.preprocessing()
               .deskew(max_angle=5)          # auto‑deskew up to 5°
               .denoise(strength=0.7)       # medium denoise
               .binarize(method="otsu")      # **binarize image using Otsu**
               .contrast(stretch=True)      # auto contrast stretch
)

# Explanation:
# - `deskew` corrects rotation; 5° is a safe ceiling for most scans.
# - `denoise` with 0.7 balances smoothing without erasing thin characters.
# - `binarize` with method "otsu" automatically selects the optimal threshold.
# - `contrast` stretch brightens faint ink while keeping dark ink dark.
```

### Hoe je gescande documenten moet rechtzetten

De `deskew`‑aanroep hierboven is het concrete antwoord op **hoe je gescande documenten moet rechtzetten**. Intern schat hij de dominante tekstreekhoek via een Hough‑transformatie en roteert de afbeelding terug. Als je documenten meer dan 5° gedraaid zijn, verhoog dan `max_angle`, maar wees voorzichtig met over‑rotatie‑artefacten.

### Afbeelding binariseren met Otsu

De regel `binarize(method="otsu")` beantwoordt direct de vraag **binarize image using otsu**. Otsu's algoritme berekent een drempel die de intra‑klasse‑variantie minimaliseert, perfect voor documenten met bimodale histogrammen (donkere tekst vs. lichte achtergrond).

## Stap 4: Koppel de pipeline aan de engine

Nu vertellen we de OCR‑engine om elke binnenkomende afbeelding door de pipeline te laten gaan die we zojuist hebben gebouwd.

```python
# Step 4: Register the custom pipeline
ocr_engine.set_preprocessing(preprocessing_pipeline)
```

*Waarom dit belangrijk is:* Zonder registratie zou de engine de ruwe scan verwerken, waarbij al het schoonmaken dat we hebben geconfigureerd wordt genegeerd. Deze stap zorgt ervoor dat **hoe je OCR‑nauwkeurigheid kunt verbeteren** door consequent dezelfde voorbewerking toe te passen.

## Stap 5: Herken tekst uit een ruisende Duitse scan

Tijd om alles samen te brengen. We voeren de engine een ruisende Duitse afbeelding in en laten hem het zware werk doen.

```python
# Step 5: Run OCR on the target file
image_path = "YOUR_DIRECTORY/noisy_german_scan.tif"
recognition_result = ocr_engine.recognize_image(image_path)
```

Als je nieuwsgierig bent naar de prestaties, kun je de aanroep timen:

```python
import time
start = time.time()
result = ocr_engine.recognize_image(image_path)
print(f"OCR took {time.time() - start:.2f}s")
```

## Stap 6: Output de herkende tekst

Tot slot printen we de geëxtraheerde string. Dit is het directe antwoord op **extract text from german image**.

```python
# Step 6: Display the OCR output
print("=== Recognized German Text ===")
print(recognition_result.text)
```

### Verwachte output

Als de voorbeeldscan de zin “Die schnelle braune Füchsin springt über den faulen Hund.” bevat, zie je iets als:

```
=== Recognized German Text ===
Die schnelle braune Füchsin springt über den faulen Hund.
```

Als de output nog steeds onleesbare tekens bevat, overweeg dan de `denoise`‑sterkte aan te passen of `max_angle` voor het rechtzetten te verhogen.

## Veelvoorkomende valkuilen & hoe ze op te lossen

- **Ontbrekend taalmodel:** Het vergeten van `set_recognition_language(Language.GERMAN)` leidt vaak tot ontbrekende umlauts. Controleer deze aanroep.
- **Over‑denoising:** Een sterkte boven 0.9 kan dunne streken wissen, vooral bij oudere lettertypen. Houd je aan 0.5‑0.7 voor de meeste gevallen.
- **Onjuist bestandsformaat:** Sommige OCR‑engines hebben moeite met multi‑page TIFF’s. Splits een meer‑pagina‑document eerst op in enkele pagina‑bestanden.
- **Volgorde van de pipeline:** De hier getoonde volgorde (deskew → denoise → binarize → contrast) is opzettelijk. Binariseren vóór denoising kan ruis vergrendelen; denoise altijd eerst.

## De pipeline uitbreiden (Wat is de volgende stap?)

Nu je een solide basis hebt, kun je overwegen om:

- **Een morfologische opening** toe te voegen om kleine vlekjes te verwijderen (`.morph_open(kernel=3)`).
- **Een taalmodel** te integreren voor post‑processing correctie (`ocr_engine.apply_spellcheck()`).
- **Batch‑verwerking te paralleliseren** voor grote datasets met `concurrent.futures`.

Al deze uitbreidingen behouden de kern van **hoe je afbeeldingen voor OCR moet voorbewerken** terwijl ze **hoe je OCR‑nauwkeurigheid kunt verbeteren** nog verder verhogen.

## Conclusie

We hebben net **hoe je afbeeldingen voor OCR moet voorbewerken** van begin tot eind behandeld: een engine maken, Duitse taal instellen, een pipeline bouwen die **afbeelding binariseren met Otsu**, **hoe je gescande documenten moet rechtzetten**, en uiteindelijk **tekst extraheren uit Duitse afbeelding** met hogere zekerheid. Door de zes stappen hierboven te volgen, zie je een merkbare sprong in herkenningskwaliteit—geen eindeloze handmatige correcties meer.

Probeer het script met je eigen scans, experimenteer met de parameters, en laat de resultaten voor zich spreken. Vragen over een specifieke voorbewerkings‑tweak? Laat een reactie achter, dan duiken we samen dieper in.

Happy coding, en moge je OCR altijd accuraat zijn!


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}