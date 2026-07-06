---
category: general
date: 2026-06-25
description: Hoe OCR te gebruiken in Python – leer hoe je een afbeelding laadt voor
  OCR, tekst in een gebied herkent en de tekst uit dat gebied snel extraheert.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: nl
og_description: Hoe OCR te gebruiken in Python – stapsgewijze handleiding om een afbeelding
  te laden, tekst in een specifiek gebied te herkennen en het factuurnummer te extraheren.
og_title: 'Hoe OCR in Python te gebruiken: afbeelding laden en regio‑tekst extraheren'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'Hoe OCR Python te gebruiken: afbeelding laden en regio‑tekst extraheren'
url: /nl/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR in Python te gebruiken: Afbeelding laden en regio‑tekst extraheren

**Hoe OCR in Python te gebruiken** is eenvoudiger dan je denkt. Heb je ooit naar een gescande factuur gekeken en je afgevraagd hoe je alleen het factuurnummer kunt halen zonder de hele pagina te parseren? Je bent niet de enige—veel ontwikkelaars lopen tegen dat probleem aan wanneer ze voor het eerst met optische tekenherkenning spelen. In deze gids lopen we stap voor stap door het laden van een afbeelding voor OCR, het definiëren van een rechthoek, het herkennen van tekst in dat gebied, en uiteindelijk het extraheren van de regio‑tekst. Aan het einde heb je een kant‑klaar script dat elk stukje tekst dat je nodig hebt, kan isoleren.

> *Pro tip:* Als je met PDF‑bestanden werkt, converteer dan eerst elke pagina naar een afbeelding—de meeste OCR‑bibliotheken werken het beste met PNG/JPEG.

## Wat je nodig hebt

- Python 3.8+ (de nieuwste stabiele release wordt aanbevolen)  
- Een OCR‑bibliotheek die een `OcrEngine`‑klasse exposeert (bijv. **ocr** van `pip install ocr-lib`)  
- Een voorbeeldafbeelding—hier gebruiken we `invoice.png` geplaatst in een map die jij beheert  
- Basiskennis van rechthoeken (x, y, breedte, hoogte)  

Geen zware afhankelijkheden, geen GPU vereist—alleen gewone CPU‑werking, wat de draagbaarheid vergroot.

---

## Hoe OCR te gebruiken: Engine initialiseren (Stap 1)

Voordat er tekst gelezen kan worden, heb je een OCR‑engine‑instantie nodig. Beschouw het als het brein dat pixelpatronen analyseert.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Waarom dit belangrijk is:* Het initialiseren van de engine laadt taalmodellen en stelt standaardconfiguraties in. Als je deze stap overslaat, wordt er een uitzondering gegooid op het moment dat je `recognize_region` aanroept.

---

## Afbeelding laden voor OCR (Stap 2)

Nu de engine klaar is, voeren we er een afbeelding in. De `Image.load`‑methode van de bibliotheek verwerkt gangbare formaten en normaliseert de bitmap.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

Als het bestand niet wordt gevonden, zal Python een `FileNotFoundError` werpen. Zorg ervoor dat het pad absoluut is of relatief ten opzichte van de werkmap van je script.  

*Randgeval:* Sommige OCR‑engines verwachten een grijswaardenafbeelding. Als je een lage nauwkeurigheid opmerkt, converteer de afbeelding dan eerst:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## Tekst herkennen in een regio (Stap 3)

Het definiëren van de regio is het moment waarop je de engine vertelt *waar* te zoeken. De `Rectangle` accepteert zwevende‑komma‑waarden voor sub‑pixelprecisie, wat handig kan zijn bij hoge‑resolutie‑scans.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – linkerbovenhoek van de rechthoek (in pixels)  
- **breedte, hoogte** – afmetingen van de doos  

Je vraagt je misschien af hoe je deze cijfers kunt vinden. Een snelle manier is de afbeelding te openen in een editor (bijv. GIMP of Paint.NET) en het selectiegereedschap te gebruiken om de coördinaten af te lezen.  

*Waarom niet de hele pagina OCR‑en?* Het beperken van het gebied vermindert ruis, versnelt de verwerking en verbetert de nauwkeurigheid aanzienlijk voor kleine velden zoals factuurnummers.

---

## Hoe regio‑tekst extraheren (Stap 4)

Met de regio ingesteld, vraag je de engine om alleen dat fragment te herkennen. Het resultaatobject bevat de ruwe tekst en vertrouwensscores.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

Als de OCR‑engine meerdere talen ondersteunt, kun je een optionele taalcodes meegeven:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Veelvoorkomend struikelpunt:* Sommige engines retourneren een lijst van woorden in plaats van één string. In dat geval moet je ze samenvoegen:

```python
text = " ".join(region_result.words)
```

---

## Het geëxtraheerde factuurnummer weergeven (Stap 5)

Print — of sla — het geëxtraheerde tekstfragment op. Je kunt de string ook nog nabewerken om overtollige spaties of niet‑numerieke tekens te verwijderen.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

Het uitvoeren van het script met een correct uitgelijnde rechthoek zou iets moeten opleveren als:

```
Invoice number: 20231578
```

Als je onzinnige tekens krijgt, controleer dan de coördinaten van de rechthoek opnieuw of overweeg de resolutie van de afbeelding te verhogen.

---

## Volledig werkend voorbeeld

Alles bij elkaar, hier is een zelfstandige script dat je kunt kopiëren, plakken en uitvoeren:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Sla het bestand op als `extract_invoice.py`, vervang `YOUR_DIRECTORY` door de daadwerkelijke map, en voer uit:

```bash
python extract_invoice.py
```

Je zou het factuurnummer in de console moeten zien verschijnen.

---

## Veelgestelde vragen

**V: Wat als het factuurnummer in een sierlijk lettertype is gedrukt?**  
A: De meeste moderne OCR‑engines kunnen een breed scala aan lettertypen aan, maar je kunt de nauwkeurigheid verhogen door een aangepast taalmodel te trainen of de afbeelding voor te bewerken (bijv. een drempel‑filter toepassen).

**V: Kan ik meerdere velden tegelijk extraheren?**  
A: Zeker. Definieer een lijst van `Rectangle`‑objecten — één per veld — en loop erover, waarbij je elk resultaat in een woordenboek opslaat.

**V: Werkt dit op meer‑pagina‑PDF’s?**  
A: Converteer eerst elke pagina naar een afbeelding (met `pdf2image` of iets dergelijks), en pas vervolgens dezelfde regio‑gebaseerde extractie per pagina toe.

---

## Afronding

In deze tutorial hebben we behandeld **hoe OCR in Python te gebruiken** om een afbeelding te laden, tekst te herkennen in een specifiek gebied, en die regio‑tekst te extraheren — perfect voor het ophalen van factuurnummers, order‑ID’s of elk klein gegevensfragment uit gescande documenten. Door het interessegebied te isoleren, win je snelheid, nauwkeurigheid en minder nabewerking.

Klaar voor de volgende stap? Probeer het script uit te breiden zodat het **afbeeldingen voor OCR laadt** uit een map met batch‑facturen, of experimenteer met **tekst herkennen in regio** voor andere velden zoals data en totalen. Hetzelfde patroon geldt — verander alleen de coördinaten van de rechthoek.

Als je ergens tegenaan loopt of ideeën hebt voor verbetering, laat dan een reactie achter. Veel programmeerplezier, en moge je OCR‑pijplijnen altijd nauwkeurig zijn!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}