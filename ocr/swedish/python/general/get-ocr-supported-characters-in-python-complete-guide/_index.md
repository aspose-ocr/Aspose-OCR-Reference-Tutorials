---
category: general
date: 2026-06-25
description: Få snabbt OCR‑stödda tecken med aocr‑biblioteket. Lär dig hur du listar
  OCR‑tecken, ställer in språk och felsöker din OCR‑motor i Python.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: sv
og_description: Hämta OCR‑stödda tecken med aocr. Den här guiden visar hur du listar
  OCR‑tecken, väljer språk och hanterar kantfall i Python.
og_title: Hämta OCR‑stödda tecken i Python – Fullständig handledning
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
title: Hämta OCR‑stödda tecken i Python – Komplett guide
url: /sv/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hämta OCR‑stödda tecken i Python – Komplett guide

Har du någonsin funderat på hur du **hämtar OCR‑stödda tecken** för ett specifikt språk när du leker med en OCR‑motor? Du är inte ensam. Oavsett om du bygger en kvittoscanner eller en flerspråkig dokumentparser, är det en livräddare att exakt veta vilka glyfer din motor kan känna igen. I den här handledningen går vi igenom hela processen – installation av biblioteket, konfiguration av språket och slutligen listning av tecknen – så att du kan felsöka och finjustera din OCR‑pipeline på några minuter.

Vi använder **aocr**‑biblioteket, en lättviktig Python‑OCR‑motor som gör det enkelt att fråga efter språkfunktioner. När du är klar med guiden kan du **lista OCR‑tecken**, växla mellan **stödda OCR‑språk** och till och med identifiera luckor i täckningen innan de blir ett problem i produktion.

---

## Förutsättningar

Innan vi dyker ner, se till att du har:

* Python 3.8 eller nyare (aocr‑paketet slutar stödja 3.7)
* En terminal eller kommandoprompt med internetåtkomst
* Grundläggande kunskap om Python‑skriptning (om du har skrivit ett `print()` tidigare, är du redo)

Inga tunga externa beroenden – bara `aocr`‑pip‑paketet.

---

## Installera aocr‑biblioteket (OCR Engine Python)

Det första du behöver är en fungerande **OCR engine Python**‑installation. aocr‑paketet finns på PyPI, så ett enda pip‑kommando räcker:

```bash
pip install aocr
```

Om du använder en virtuell miljö (starkt rekommenderat), aktivera den först:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **Pro tip:** Fäst versionen (`pip install aocr==1.2.4`) för att undvika oväntade API‑ändringar senare.

---

## Välj ett språk (Supported OCR Languages)

aocr levereras med ett fåtal inbyggda språkpaket. Varje paket definierar den uppsättning Unicode‑kodpunkter som motorn kan känna igen. För att fråga efter dessa paket måste du sätta `language`‑attributet på motorinstansen.

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

Du kan ersätta `aocr.Language.ENGLISH` med vilket annat enum‑värde som helst (`FRENCH`, `GERMAN` osv.). Om du försöker tilldela ett språk som inte är med i paketet, kastar aocr ett `ValueError`. Därför är det en bra idé att först kontrollera listan över **supported OCR languages**:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## Hämta teckenuppsättningen (Get OCR Supported Characters)

Nu kommer hjärtat i handledningen: faktiskt **hämta OCR‑stödda tecken**. Motorn exponerar en praktisk metod som heter `get_supported_characters()` och som returnerar en lista med en‑tecken‑strängar.

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

Bakom kulisserna läser aocr en JSON‑fil som följer med språkpaketet och konverterar varje Unicode‑kodpunkt till en Python‑sträng. Resultatet är deterministiskt, vilket betyder att du får exakt samma lista varje gång du kör skriptet med samma språkversion.

---

## Visa hur många tecken som stöds

Att känna till antalet hjälper dig snabbt att bedöma täckningsbredden. För engelska ser du vanligtvis några tusen tecken (inklusive skiljetecken och siffror).

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

`len()`‑anropet är O(1) eftersom Python lagrar listlängden internt, så det finns ingen prestandapåverkan även för stora alfabet.

---

## Förhandsgranska de första 100 stödda tecknen

En snabb visuell kontroll kan avslöja om motorn innehåller de symboler du behöver (tänk på eurosymbolen eller smarta citationstecken). Låt oss skriva ut de första hundra tecknen:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

`join`‑operationen sammanfogar skivan till en enda sträng, vilket är mer läsbart än att skriva ut en Python‑lista.

---

## Fullt skript – Alla steg på ett ställe

Nedan är det kompletta, körbara exemplet som binder ihop allt. Spara det som `list_supported_chars.py` och kör `python list_supported_chars.py` från din terminal.

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

**Förväntad output (avkortad för korthet):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

Det exakta antalet kan variera något beroende på aocr‑versionen, men du kommer alltid att se ett långt alfabet plus vanliga skiljetecken.

---

## Hantera kantfall

### Vad händer om språkpaketet saknas?

Om du begär ett språk som inte finns med, innehåller inte `aocr.Language` enum‑värdet och du får ett `AttributeError`. Skydda dig mot detta med en enkel kontroll:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### Tom teckenlista

Vissa nischade språk kan returnera en tom lista om den underliggande träningsdatan är ofullständig. I så fall kan du falla tillbaka till ett standardalternativ (t.ex. engelska) eller kasta en varning:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Unicode‑normalisering

Listan kan innehålla kombinerade tecken (t.ex. “é” som `e` + akut accent). Om din efterföljande bearbetning förväntar sig förkomponerade glyfer, kör ett normaliseringssteg:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## Pro‑tips för verkliga projekt

* **Cacha teckenlistan** – Om du bearbetar tusentals bilder, lägger `get_supported_characters()` på varje iteration onödig belastning. Spara listan i en modul‑nivåvariabel eller serialisera den till JSON för återanvändning.
* **Validering över språk** – När du stödjer flera språk i en app, intersecta teckenuppsättningarna för att hitta en gemensam delmängd. Detta hjälper dig att designa UI‑element som förblir konsistenta över lokaler.
* **Felsökning av OCR‑fel** – Om motorn felklassificerar ett tecken, jämför det felande tecknet med resultatet från `list_supported_chars`. Om det saknas har du identifierat ett täckningsgap som kan kräva en anpassad träningssteg.
* **Kombinera med anpassade typsnitt** – aocr respekterar Unicode‑intervallet, men renderingskvaliteten kan variera per typsnitt. Testa dina stödda tecken med exakt det typsnitt du kommer att använda i produktion för att undvika överraskningar.

---

## Vanliga frågor

**Q: Fungerar detta med aocr version 2.x?**  
A: Ja, metoden `get_supported_characters()` är stabil över 1.x och 2.x. Den enda förändringen är att språk‑enum‑erna flyttades till `aocr.languages`.

**Q: Kan jag få Unicode‑kodpunkten för varje tecken?**  
A: Absolut. Använd `ord(ch)` i en list comprehension:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**Q: Vad händer med höger‑till‑vänster‑skript som arabiska?**  
A: aocr inkluderar ett `ARABIC`‑enum. Teckenlistan kommer att innehålla arabiska glyfer, men du kan behöva aktivera RTL‑rendering i ditt efterföljande UI.

---

## Slutsats

Du vet nu **hur du hämtar OCR‑stödda tecken** med aocr‑biblioteket i Python, hur du växlar mellan **stödda OCR‑språk**, och varför **listning av OCR‑tecken** är avgörande för robusta text‑igenkännings‑pipelines. Med det kompletta skriptet och tipsen ovan kan du snabbt verifiera språk‑täckning, felsöka saknade glyfer och bygga smartare OCR‑drivna applikationer.

Redo för nästa steg? Prova att kombinera den här teckenlistan med ett anpassat ordlistfilter, eller experimentera med en annan OCR‑motor (Tesseract, EasyOCR) och jämför resultaten. Ju mer du utforskar, desto bättre blir dina OCR‑lösningar.

Happy coding, and may your character sets always be complete!

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Specify Allowed Characters OCR – Using Aspose.OCR for .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}