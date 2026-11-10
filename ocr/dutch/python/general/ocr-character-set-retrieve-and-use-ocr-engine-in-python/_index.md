---
category: general
date: 2026-06-06
description: 'OCR-tekensetgids: leer hoe je de OCR-engine gebruikt om ondersteunde
  tekens voor Latijnse en Cyrillische scripts te tonen met volledige Python‑voorbeelden.'
draft: false
keywords:
- ocr character set
- use OCR engine
- supported OCR characters
- script detection OCR
- OCR library Python
language: nl
og_description: 'OCR-tekensetgids: ontdek hoe je de OCR-engine in Python gebruikt
  om ondersteunde tekens voor verschillende scripts weer te geven, compleet met code
  en tips.'
og_title: OCR-tekenset – Ophalen en gebruiken van OCR-engine
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: 'OCR character set guide: learn how to use OCR engine to list supported
    characters for Latin and Cyrillic scripts with full Python examples.'
  headline: OCR Character Set – Retrieve and Use OCR Engine in Python
  type: TechArticle
tags:
- OCR
- Python
- Character Sets
title: OCR-tekenset – Ophalen en gebruiken van OCR‑engine in Python
url: /nl/python/general/ocr-character-set-retrieve-and-use-ocr-engine-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR‑tekenreeks – Ophalen en gebruiken van OCR‑engine in Python

Wil je de **ocr character set** weten die je bibliotheek ondersteunt? In deze tutorial laten we je zien hoe je de **use OCR engine** kunt gebruiken om ondersteunde tekens voor verschillende scripts op te vragen, en waarom dat belangrijk is voor projecten in de echte wereld.

Als je ooit naar een leeg scherm hebt gestaren en je afvroeg waarom sommige letters nooit verschijnen na OCR‑verwerking, ben je niet de enige. Het antwoord zit vaak verborgen in de tekenreeks die de engine kent. Aan het einde van deze gids kun je:

* Lijst elk teken dat een OCR‑engine kan herkennen voor een gegeven script.  
* Omgaan met gevallen waarin een script niet wordt ondersteund.  
* De character‑set informatie integreren in downstream validatie of UI‑logica.

Geen magische black‑box trucjes—gewoon plain Python, een paar regels code, en een beetje uitleg.

---

## Vereisten

Voordat we beginnen, zorg ervoor dat je het volgende hebt:

* Python 3.8+ geïnstalleerd (de code gebruikt f‑strings).  
* De OCR‑bibliotheek die `ocr.OcrEngine` levert—voor dit voorbeeld gaan we ervan uit dat een pakket genaamd `ocr` al geïnstalleerd is via `pip install ocr-lib`.  
* Basiskennis van het import‑systeem van Python en van afdrukken.

Als je de bibliotheek mist, voer dan uit:

```bash
pip install ocr-lib
```

Dat is alles—geen extra binaries of native dependencies nodig voor de basis character‑set queries die we gaan uitvoeren.

---

## Stap 1: Initialiseer de OCR‑engine instantie

Het maken van een engine‑object is het eerste wat je doet wanneer je de **use OCR engine** functionaliteit gebruikt. Beschouw het als het inschakelen van een scanner; zonder deze kun je geen vragen stellen.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

De `OcrEngine`‑klasse is een lichtgewicht wrapper rond de onderliggende herkenningsengine. Het start geen zware verwerking totdat je iets vraagt, dus de opstartkosten zijn verwaarloosbaar.

> **Pro tip:** Als je applicatie veel engine‑instanties maakt, hergebruik er dan één. Het bespaart geheugen en vermindert de initialisatielatentie.

---

## Stap 2: Vraag de OCR‑tekenreeks op voor een specifiek script

Nu we een engine hebben, kunnen we hem vragen welke tekens hij kent voor een bepaald schrijfsysteem. De methode `get_supported_characters(script_name)` retourneert een Python `list` van Unicode‑tekens.

```python
# Step 2: Get the list of characters the engine can recognize for the Latin script
latin_chars = engine.get_supported_characters("Latin")
print(f"Supported Latin chars ({len(latin_chars)}): {latin_chars}")
```

Het uitvoeren van de bovenstaande code print iets als:

```
Supported Latin chars (26): ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
```

De exacte output hangt af van de versie van de OCR‑bibliotheek, maar je krijgt altijd een platte lijst van tekens. Als je zowel hoofdletters als kleine letters nodig hebt, vraag dan simpelweg het `"Latin"`‑script op en pas vervolgens `.lower()` toe op elk element, of vraag een apart `"Latin‑lower"`‑script op als de bibliotheek ze onderscheidt.

### Waarom is dit belangrijk?

Wanneer je een afbeelding met ongebruikelijke diakritische tekens (bijv. “ñ” of “ø”) invoert, kan de OCR‑engine ze stilletjes vervangen door een placeholder of ze volledig weglaten. Het kennen van de **ocr character set** van tevoren stelt je in staat om invoer vooraf te valideren, gebruikers te waarschuwen, of terug te vallen op een andere engine.

---

## Stap 3: Haal tekens op voor een ander script – Cyrillic‑voorbeeld

Dezelfde methode werkt voor elk script dat de engine claimt te ondersteunen. Laten we zien wat er gebeurt met Cyrillic.

```python
# Step 3: Get the list of characters the engine can recognize for the Cyrillic script
cyrillic_chars = engine.get_supported_characters("Cyrillic")
print(f"Supported Cyrillic chars ({len(cyrillic_chars)}): {cyrillic_chars}")
```

Typische output:

```
Supported Cyrillic chars (33): ['А', 'Б', 'В', 'Г', 'Д', 'Е', 'Ё', 'Ж', 'З', 'И', 'Й', 'К', 'Л', 'М', 'Н', 'О', 'П', 'Р', 'С', 'Т', 'У', 'Ф', 'Х', 'Ц', 'Ч', 'Ш', 'Щ', 'Ъ', 'Ы', 'Ь', 'Э', 'Ю', 'Я']
```

Als de engine **niet** het gevraagde script ondersteunt, werpt hij meestal een `ValueError` (of retourneert een lege lijst, afhankelijk van de implementatie). Laten we daar tegen beschermen.

```python
def safe_get_characters(engine, script):
    try:
        chars = engine.get_supported_characters(script)
        if not chars:
            print(f"No characters returned for script '{script}'.")
        else:
            print(f"Supported {script} chars ({len(chars)}): {chars}")
        return chars
    except Exception as e:
        print(f"Error retrieving characters for script '{script}': {e}")
        return []

# Example usage:
safe_get_characters(engine, "Arabic")   # Might trigger the error branch
```

---

## Stap 4: Visualiseer de OCR‑tekenreeks (optioneel)

Soms helpt een snelle visualisatie, vooral wanneer je belanghebbenden wilt laten zien welke tekens gedekt zijn. Hieronder staat een minimaal voorbeeld met `matplotlib` om een raster van tekens weer te geven.

```python
import matplotlib.pyplot as plt

def plot_character_grid(chars, title="OCR Character Set"):
    cols = 10
    rows = (len(chars) + cols - 1) // cols
    fig, ax = plt.subplots(figsize=(cols, rows))
    ax.set_axis_off()
    for idx, ch in enumerate(chars):
        row = idx // cols
        col = idx % cols
        ax.text(col / cols, 1 - row / rows, ch, fontsize=14, ha='center', va='center')
    plt.title(title)
    plt.show()

# Visualize Latin characters
plot_character_grid(latin_chars, title="Latin OCR Character Set")
```

> **Image alt text:** ![OCR‑tekenreeks diagram](ocr_character_set.png){alt="Overzicht van OCR‑tekenreeks"}

Het diagram is niet vereist voor de kernoplossing, maar het toont hoe je de **use OCR engine** metadata kunt gebruiken buiten eenvoudige afdrukken.

---

## Stap 5: Integreer de tekenreeks in real‑world workflows

Nu we de **ocr character set** kunnen ophalen, bekijken we een praktisch scenario: het valideren van OCR‑output voordat deze in een database wordt opgeslagen.

```python
def validate_ocr_output(text, allowed_chars):
    """Return True if every character in `text` exists in `allowed_chars`."""
    invalid = [c for c in text if c not in allowed_chars]
    if invalid:
        print(f"Invalid characters found: {invalid}")
        return False
    return True

# Suppose we ran OCR on an image and got this result:
ocr_result = "HELLO WORLD!"

# Use the previously fetched Latin set for validation:
if validate_ocr_output(ocr_result, set(latin_chars)):
    print("All characters are supported – safe to store.")
else:
    print("Result contains unsupported symbols – consider manual review.")
```

Dit patroon voorkomt dat vuildata in downstream‑pijplijnen terechtkomt, een veelvoorkomend pijnpunt bij het omgaan met meertalige documenten.

---

## Veelvoorkomende valkuilen en randgevallen

| Valkuil | Waarom het gebeurt | Hoe te vermijden |
|---------|--------------------|------------------|
| **Script name typo** (bijv. `"Cyrillic "` met een spatie aan het einde) | De engine behandelt de string letterlijk en kan het script niet vinden. | Verwijder witruimte: `script.strip()` voordat `get_supported_characters` wordt aangeroepen. |
| **Empty character list** | Sommige engines tonen een script maar hebben het taalmodel nog niet geladen. | Roep `engine.load_language_model(script)` aan als de bibliotheek zo’n methode biedt, of zorg dat de modelbestanden aanwezig zijn. |
| **Unicode normalization issues** | Tekens zoals “é” kunnen verschijnen als samengesteld (`\u00E9`) of gedecomposeerd (`e\u0301`). | Normaliseer strings met `unicodedata.normalize('NFC', text)` vóór validatie. |
| **Performance on huge scripts** (bijv. Chinees) | Het ophalen van duizenden tekens kan traag zijn. | Cache het resultaat na de eerste oproep; de meeste applicaties hebben de lijst slechts één keer nodig. |

---

## Volledig werkend voorbeeld

Alles samengevoegd, hier is een enkel script dat je kunt kopiëren‑plakken en uitvoeren:



## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Aspose OCR Tutorial – Optische tekenherkenning](/ocr/english/)
- [OCR‑nabewerking – Haal tekenkeuzes op](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Hoe drempelwaarde in te stellen bij OCR‑beeldherkenning](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}