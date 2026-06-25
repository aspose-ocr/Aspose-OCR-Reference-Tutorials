---
category: general
date: 2026-06-25
description: Krijg snel OCR‑ondersteunde tekens met de aocr‑bibliotheek. Leer hoe
  je OCR‑tekens kunt opsommen, talen kunt instellen en je OCR‑engine in Python kunt
  debuggen.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: nl
og_description: Haal OCR‑ondersteunde tekens op met aocr. Deze gids laat zien hoe
  je OCR‑tekens kunt opsommen, talen kunt kiezen en randgevallen in Python kunt afhandelen.
og_title: Ophalen van OCR‑ondersteunde tekens in Python – Volledige tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: OCR‑ondersteunde tekens ophalen in Python – Complete gids
url: /nl/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR‑ondersteunde tekens ophalen in Python – Complete gids

Heb je je ooit afgevraagd hoe je **OCR‑ondersteunde tekens** voor een specifieke taal kunt **krijgen** terwijl je met een OCR‑engine experimenteert? Je bent niet de enige. Of je nu een kassabon‑scanner bouwt of een meertalige document‑parser, precies weten welke glyphs je engine kan herkennen, is een levensredder. In deze tutorial lopen we het volledige proces door – de bibliotheek installeren, de taal configureren en uiteindelijk die tekens opsommen – zodat je je OCR‑pipeline in enkele minuten kunt debuggen en afstemmen.

We gebruiken de **aocr**‑bibliotheek, een lichte Python‑OCR‑engine die het eenvoudig maakt om de mogelijkheden van een taal op te vragen. Aan het einde van deze gids kun je **OCR‑tekens opsommen**, schakelen tussen **ondersteunde OCR‑talen**, en zelfs hiaten in de dekking ontdekken voordat ze je in productie verrassen.

---

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

* Python 3.8 of nieuwer (het aocr‑pakket ondersteunt 3.7 niet meer)
* Een terminal of opdrachtprompt met internettoegang
* Basiskennis van Python‑scripting (als je eerder een `print()` hebt geschreven, ben je klaar)

Geen zware externe afhankelijkheden – alleen het `aocr`‑pip‑pakket.

---

## De aocr‑bibliotheek installeren (OCR‑engine Python)

Het eerste wat je nodig hebt, is een werkende **OCR‑engine Python**‑installatie. Het aocr‑pakket staat op PyPI, dus één enkele pip‑opdracht doet het werk:

```bash
pip install aocr
```

Gebruik je een virtuele omgeving (sterk aanbevolen), activeer deze dan eerst:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **Pro tip:** Pin de versie (`pip install aocr==1.2.4`) om onverwachte API‑wijzigingen later te voorkomen.

---

## Een taal kiezen (ondersteunde OCR‑talen)

aocr wordt geleverd met een handvol ingebouwde taal‑pakketten. Elk pakket definieert de set Unicode‑codepunten die de engine kan herkennen. Om die pakketten op te vragen, moet je het `language`‑attribuut op de engine‑instantie instellen.

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

Je kunt `aocr.Language.ENGLISH` vervangen door elke andere enum‑waarde (`FRENCH`, `GERMAN`, enz.). Als je probeert een taal toe te wijzen die niet is meegeleverd, gooit aocr een `ValueError`. Daarom is het verstandig eerst de lijst met **ondersteunde OCR‑talen** te controleren:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## De set tekens ophalen (OCR‑ondersteunde tekens krijgen)

Nu volgt het hart van de tutorial: daadwerkelijk **OCR‑ondersteunde tekens** **krijgen**. De engine biedt een handige methode `get_supported_characters()` die een lijst van één‑karakter‑strings teruggeeft.

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

Achter de schermen leest aocr een JSON‑bestand dat bij het taal‑pakket hoort en zet elk Unicode‑codepunt om in een Python‑string. Het resultaat is deterministisch, wat betekent dat je elke keer dat je het script op dezelfde taalversie draait, dezelfde lijst krijgt.

---

## Aantal ondersteunde tekens weergeven

Het weten van het aantal helpt je snel de breedte van de dekking in te schatten. Voor Engels zie je doorgaans enkele duizenden tekens (inclusief interpunctie en cijfers).

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

De `len()`‑aanroep is O(1) omdat Python de lijstlengte intern opslaat, dus er is geen prestatie‑penalty, zelfs niet voor grote alfabetten.

---

## Voorbeeld van de eerste 100 ondersteunde tekens

Een snelle visuele controle kan onthullen of de engine de symbolen bevat die je nodig hebt (denk aan het euro‑teken of slimme aanhalingstekens). Laten we de eerste honderd tekens afdrukken:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

De `join`‑operatie plakt de slice aan elkaar tot één string, wat leesbaarder is dan het afdrukken van een Python‑lijst.

---

## Volledig script – alle stappen op één plek

Hieronder vind je het complete, uitvoerbare voorbeeld dat alles samenbrengt. Sla het op als `list_supported_chars.py` en voer `python list_supported_chars.py` uit in je terminal.

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**Verwachte output (afgekapt voor beknoptheid):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

Het exacte aantal kan iets afwijken afhankelijk van de aocr‑versie, maar je zult altijd een lang alfabet plus veelvoorkomende interpunctie zien.

---

## Edge‑cases afhandelen

### Wat als het taal‑pakket ontbreekt?

Als je een taal vraagt die niet is meegeleverd, bevat `aocr.Language` de enum niet en krijg je een `AttributeError`. Bescherm je code met een eenvoudige controle:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### Lege tekenlijst

Sommige niche‑talen kunnen een lege lijst teruggeven als de onderliggende trainingsdata onvolledig is. In dat geval kun je terugvallen op een standaard (bijv. Engels) of een waarschuwing geven:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Unicode‑normalisatie

De lijst kan samengestelde tekens bevatten (bijv. “é” als `e` + acute accent). Als je downstream‑verwerking samengestelde glyphs niet ondersteunt, voer dan een normalisatiestap uit:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## Pro‑tips voor real‑world projecten

* **Cache de tekenlijst** – Als je duizenden afbeeldingen verwerkt, voegt het telkens aanroepen van `get_supported_characters()` onnodige overhead toe. Sla de lijst op in een module‑niveau variabele of serialiseer hem naar JSON voor later hergebruik.
* **Cross‑language validatie** – Wanneer je meerdere talen in één app ondersteunt, intersecteer je de teken‑sets om een gemeenschappelijke subset te vinden. Dit helpt je UI‑elementen consistent te houden over locale‑s heen.
* **OCR‑fouten debuggen** – Als de engine een glyph verkeerd classificeert, vergelijk dan het problematische teken met de output van `list_supported_chars`. Als het ontbreekt, heb je een dekking‑gat geïdentificeerd dat een aangepaste training vereist.
* **Combineren met aangepaste fonts** – aocr respecteert het Unicode‑bereik, maar de weergavekwaliteit kan per font verschillen. Test je ondersteunde tekens met exact het font dat je in productie gaat gebruiken om verrassingen te voorkomen.

---

## Veelgestelde vragen

**Q: Werkt dit met aocr versie 2.x?**  
A: Ja, de `get_supported_characters()`‑methode is stabiel in zowel 1.x als 2.x. Het enige verschil is dat taal‑enums zijn verplaatst naar `aocr.languages`.

**Q: Kan ik de Unicode‑codepunt voor elk teken krijgen?**  
A: Zeker. Gebruik `ord(ch)` binnen een list comprehension:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**Q: Hoe zit het met rechts‑naar‑links scripts zoals Arabisch?**  
A: aocr bevat een `ARABIC`‑enum. De tekenlijst zal Arabische glyphs bevatten, maar je moet mogelijk RTL‑rendering inschakelen in je downstream UI.

---

## Conclusie

Je weet nu **hoe je OCR‑ondersteunde tekens** kunt **krijgen** met de aocr‑bibliotheek in Python, hoe je kunt schakelen tussen **ondersteunde OCR‑talen**, en waarom **OCR‑tekens opsommen** essentieel is voor robuuste tekst‑herkennings‑pipelines. Met het volledige script en de bovenstaande tips kun je snel taal‑dekking verifiëren, ontbrekende glyphs debuggen en slimmere OCR‑gedreven toepassingen bouwen.

Klaar voor de volgende stap? Probeer deze tekenlijst te combineren met een aangepaste woord‑lijstfilter, of experimenteer met een andere OCR‑engine (Tesseract, EasyOCR) en vergelijk de resultaten. Hoe meer je verkent, hoe beter je OCR‑oplossingen worden.

Happy coding, en moge je teken‑sets altijd compleet zijn!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑features onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Specify Allowed Characters OCR – Using Aspose.OCR for .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}