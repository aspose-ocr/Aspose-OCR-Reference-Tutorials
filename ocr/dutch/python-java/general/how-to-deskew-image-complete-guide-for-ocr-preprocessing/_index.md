---
category: general
date: 2026-07-05
description: Hoe je een afbeelding snel rechtzet. Leer hoe je een afbeelding voor
  OCR voorbewerkt, de rotatie corrigeert en een scan naar tekst converteert met Python.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: nl
og_description: Hoe je een afbeelding rechtzet en voorbereidt voor OCR. Deze gids
  laat zien hoe je de rotatie van een afbeelding corrigeert en tekst uit een afbeelding
  haalt met Python.
og_title: Hoe een afbeelding rechtzetten – Stapsgewijze OCR‑voorbewerking
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: Hoe een afbeelding rechtzetten – Complete gids voor OCR-preprocessing
url: /nl/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een afbeelding rechtzetten – Complete gids voor OCR-preprocessing

Heb je je ooit afgevraagd **how to deskew image** bestanden die eruitzien alsof ze van een scheve scanner zijn genomen? Je bent niet de enige. In veel real‑world projecten is het eerste wat je moet doen voordat je **extract text from image** kunt uitvoeren, het rechtzetten van die scheefstand.  

In deze tutorial lopen we een hands‑on, end‑to‑end voorbeeld door dat **preprocesses image for OCR**, de rotatie corrigeert, en uiteindelijk **converts scan to text** gebruikt een Python OCR‑bibliotheek. Geen vage verwijzingen, alleen een werkend script dat je kunt copy‑paste, plus tips over veelvoorkomende valkuilen.  

## Wat je zult bereiken

* Laad elke gescande JPEG of PNG die een beetje scheef staat.  
* Pas een deskew‑filter en een binarisatiestap toe om de OCR‑nauwkeurigheid te verbeteren.  
* Voer de OCR‑engine uit en **extract text from image** betrouwbaar.  
* Begrijp waarom **correct image rotation** belangrijk is voor downstream‑tekstextractie.  

### Vereisten

* Python 3.9+ geïnstalleerd op je machine.  
* Een via pip installeerbaar OCR‑pakket dat de `ocr`‑namespace nabootst die in het voorbeeld wordt gebruikt (bijvoorbeeld een dunne wrapper rond Tesseract).  
* Basiskennis van Python‑functies en concepten van beeldverwerking.  

Als je dat hebt, laten we erin duiken.

![how to deskew image example](deskew_before_after.png){alt="hoe een afbeelding rechtzetten – vóór en na correctie"}

## Stap 1: OCR-engine instellen – Hoe een afbeelding rechtzetten met Python

Allereerst: je hebt een OCR‑engine nodig die de taal van je document kan begrijpen. Het fragment hieronder toont de minimale boilerplate om de engine te maken en aan te geven dat je werkt met Engelse tekst.

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*Why this matters:*  De taalinstelling van de engine beïnvloedt de tekenset en het woordenboek dat hij gebruikt. Het overslaan van deze stap kan ertoe leiden dat de OCR veelvoorkomende woorden verkeerd interpreteert, vooral nadat je **correct image rotation** hebt toegepast.

## Stap 2: Laad de gescande afbeelding die je wilt rechtzetten

Nu brengen we het bestand in het geheugen. Vervang `"YOUR_DIRECTORY/skewed_scan.jpg"` door het pad naar je eigen afbeelding.

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

Als de afbeelding al in een NumPy‑array of een OpenCV `Mat` staat, kun je de loader dienovereenkomstig aanpassen – het belangrijkste is dat het object de `apply_filter`‑methode moet exposen die later wordt gebruikt.

## Stap 3: Afbeelding pre-processen voor OCR – Deskew en binariseren

Hier gebeurt de magie. We schakelen twee filters aaneen:

1. **Deskew** – detecteert automatisch de dominante tekstbasislijn en roteert de afbeelding terug naar horizontaal.  
2. **Binarize (Otsu)** – zet de afbeelding om in puur zwart‑wit, wat de herkenningspercentages dramatisch verbetert.

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*Pro tip:*  Als je merkt dat de tekst na binarisatie nog steeds wazig uitziet, probeer dan het contrast bij te stellen of een andere drempelmethode te gebruiken. De `ocr.Filter`‑module bevat vaak `adaptive_threshold()` voor moeilijkere gevallen.

## Stap 4: OCR uitvoeren – Tekst uit afbeelding extraheren

Met een schoon, rechtgezet canvas geven we de afbeelding aan de engine. Het result‑object bevat de herkende string, confidence‑scores, en zelfs bounding boxes als je die later nodig hebt.

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

Typische output ziet er zo uit:

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

Merk je hoe de regeleinden perfect op één lijn liggen? Dat is het voordeel van **correct image rotation** – de OCR hoeft de lijnoriëntatie niet meer te raden.

## Stap 5: Alles samenvoegen – Een één‑bestand script om scan naar tekst te converteren

Hieronder staat het volledige, uitvoerbare script dat elk besproken onderdeel combineert. Sla het op als `deskew_ocr.py` en voer `python deskew_ocr.py` uit.

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### Waarom dit werkt

* **Deskew first** – het roteren van de afbeelding vóór binarisatie zorgt ervoor dat het drempelalgoritme werkt op een vlakke horizon.  
* **Binarize after deskew** – Otsu’s methode gaat uit van een bimodale histogram; een scheve pagina zou die veronderstelling ruïneren.  
* **English language model** – vertelt de OCR welke tekens te verwachten, waardoor valse positieven worden verminderd.  

Als je andere talen moet verwerken, verwissel je simpelweg `ocr.Language.ENGLISH` voor de juiste enum.

## Veelgestelde vragen & randgevallen

| Vraag | Antwoord |
|----------|--------|
| *Wat als de scan ondersteboven is?* | Het `deskew()`‑filter detecteert meestal ook een rotatie van 180°. Als het faalt, roep `apply_filter(ocr.Filter.rotate(180))` aan vóór het deskew‑proces. |
| *Mijn document bevat gekleurde grafieken – zal binarisatie ze verwijderen?* | Ja. Voor gemengde inhoud kun je overwegen alleen `ocr.Filter.deskew()` te gebruiken, en vervolgens OCR uit te voeren op de gekleurde afbeelding. Je kunt nog steeds tekst extraheren terwijl je de grafieken behoudt. |
| *Kan ik een batch van bestanden verwerken?* | Plaats de logica in een lus, lees elk bestandspad uit een lijst, en sla elke `result.text` op in een apart `.txt`‑bestand. |
| *Hoe verbeter ik de nauwkeurigheid bij scans met lage resolutie?* | Schaal de afbeelding op met een bicubic‑filter **voordat** je deskew‑t, en pas daarna een verscherpingsfilter toe. Meer pixels geven de OCR‑engine betere aanwijzingen. |

## Bonus: Visuele verificatie van Deskew

Als je de voor‑en‑na weergave naast elkaar wilt zien, voeg dan een kort Matplotlib‑fragment toe:

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

Het zien van de gecorrigeerde uitlijning kan geruststellend zijn, vooral wanneer je een lastige batch scans debugt.

## Conclusie

We hebben behandeld **how to deskew image** bestanden, waarom **preprocess image for OCR** essentieel is, en hoe **extract text from image** tot uiteindelijk **convert scan to text**. De workflow — load → deskew → binarize → recognize — zorgt ervoor dat de OCR een schone, rechte pagina ziet, wat zich vertaalt naar hogere nauwkeurigheid en minder handmatige correcties.

Wat staat er hierna op je OCR‑reis? Probeer te experimenteren met:

* Verschillende taalpakketten (`ocr.Language.FRENCH`, etc.).  
* Een layout‑analyse stap toevoegen om kolommen of tabellen te detecteren.  
* De OCR‑resultaten exporteren naar doorzoekbare PDF’s met behulp van een PDF‑bibliotheek.

Voel je vrij een reactie achter te laten als je tegen een probleem aanloopt, of deel je eigen tweaks voor het omgaan met bijzonder koppige scans. Happy coding, en moge je afbeeldingen altijd perfect recht blijven!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑features onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe AspOCR te gebruiken: Afbeelding OCR-filters pre-processen voor .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Afbeeldingstekst extraheren C# met taalkeuze met Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Hoe een afbeelding OCR’en – OCR uitvoeren op afbeelding in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}