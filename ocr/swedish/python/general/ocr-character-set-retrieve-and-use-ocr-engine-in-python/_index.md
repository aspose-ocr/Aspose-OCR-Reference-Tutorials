---
category: general
date: 2026-06-06
description: 'OCR-teckenuppsättningsguide: lär dig hur du använder OCR-motorn för
  att lista stödda tecken för latin- och kyrilliska skript med fullständiga Python‑exempel.'
draft: false
keywords:
- ocr character set
- use OCR engine
- supported OCR characters
- script detection OCR
- OCR library Python
language: sv
og_description: 'OCR-teckenuppsättningsguide: upptäck hur du använder OCR-motorn i
  Python för att lista stödda tecken för olika skript, komplett med kod och tips.'
og_title: OCR-teckenuppsättning – Hämta och använd OCR-motorn
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
title: OCR-teckenuppsättning – Hämta och använd OCR-motor i Python
url: /sv/python/general/ocr-character-set-retrieve-and-use-ocr-engine-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR-teckenuppsättning – Hämta och Använd OCR-motor i Python

Vill du veta **ocr character set** som ditt bibliotek stöder? I den här handledningen visar vi hur du **use OCR engine** för att fråga efter stödda tecken för olika skript, och varför det är viktigt för verkliga projekt.

Om du någonsin har stirrat på en tom skärm och undrat varför vissa bokstäver aldrig visas efter OCR‑behandling, är du inte ensam. Svaret är ofta gömt i teckenuppsättningen som motorn känner till. I slutet av den här guiden kommer du att kunna:

* Lista varje tecken som en OCR-motor kan känna igen för ett givet skript.  
* Hantera fall där ett skript inte stöds.  
* Anslut teckenuppsättningsinformationen till efterföljande validering eller UI‑logik.

Inga magiska black‑box‑trick—bara ren Python, ett par kodrader och en liten förklaring.

---

## Förutsättningar

Innan vi hoppar in, se till att du har:

* Python 3.8+ installerat (koden använder f‑strings).  
* OCR‑biblioteket som tillhandahåller `ocr.OcrEngine`—för detta exempel antar vi att ett paket som heter `ocr` redan är installerat via `pip install ocr-lib`.  
* Grundläggande kunskap om Pythons import‑system och utskrift.

Om du saknar biblioteket, kör:

```bash
pip install ocr-lib
```

Det är allt—inga extra binärer eller inhemska beroenden behövs för de grundläggande teckenuppsättningsfrågorna vi kommer att utföra.

## Steg 1: Initiera OCR‑motorinstansen

Att skapa ett motorobjekt är det första du gör när du **use OCR engine**‑funktionalitet. Tänk på det som att slå på en skanner; utan den kan du inte ställa några frågor.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

`OcrEngine`‑klassen är ett lättviktigt omslag runt den underliggande igenkänningsmotorn. Den påbörjar inte tung bearbetning förrän du begär något, så startkostnaden är försumbar.

> **Pro tip:** Om din applikation skapar många motorinstanser, återanvänd en enda. Det sparar minne och minskar initieringslatens.

## Steg 2: Fråga OCR‑teckenuppsättningen för ett specifikt skript

Nu när vi har en motor kan vi fråga den vilka tecken den känner till för ett särskilt skriftsystem. Metoden `get_supported_characters(script_name)` returnerar en Python `list` med Unicode‑tecken.

```python
# Step 2: Get the list of characters the engine can recognize for the Latin script
latin_chars = engine.get_supported_characters("Latin")
print(f"Supported Latin chars ({len(latin_chars)}): {latin_chars}")
```

Att köra kodsnutten ovan skriver ut något liknande:

```
Supported Latin chars (26): ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
```

Den exakta utskriften beror på OCR‑bibliotekets version, men du får alltid en platt lista med tecken. Om du behöver både versaler och gemener, begär helt enkelt skriptet `"Latin"` och tillämpa sedan `.lower()` på varje element, eller fråga ett separat `"Latin‑lower"`‑skript om biblioteket skiljer dem åt.

### Varför är detta viktigt?

När du matar in en bild som innehåller ovanliga diakritiska tecken (t.ex. “ñ” eller “ø”), kan OCR‑motorn tyst ersätta dem med en platshållare eller helt enkelt släppa dem. Att känna till **ocr character set** i förväg låter dig förvalidera indata, varna användare eller falla tillbaka på en annan motor.

## Steg 3: Hämta tecken för ett annat skript – Cyrillic‑exempel

Samma metod fungerar för alla skript som motorn påstår sig stödja. Låt oss se vad som händer med Cyrillic.

```python
# Step 3: Get the list of characters the engine can recognize for the Cyrillic script
cyrillic_chars = engine.get_supported_characters("Cyrillic")
print(f"Supported Cyrillic chars ({len(cyrillic_chars)}): {cyrillic_chars}")
```

Typisk utskrift:

```
Supported Cyrillic chars (33): ['А', 'Б', 'В', 'Г', 'Д', 'Е', 'Ё', 'Ж', 'З', 'И', 'Й', 'К', 'Л', 'М', 'Н', 'О', 'П', 'Р', 'С', 'Т', 'У', 'Ф', 'Х', 'Ц', 'Ч', 'Ш', 'Щ', 'Ъ', 'Ы', 'Ь', 'Э', 'Ю', 'Я']
```

Om motorn **inte** stödjer det begärda skriptet, kastar den vanligtvis ett `ValueError` (eller returnerar en tom lista beroende på implementationen). Låt oss skydda mot det.

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

## Steg 4: Visualisera OCR‑teckenuppsättningen (valfritt)

Ibland hjälper en snabb visualisering, särskilt när du behöver visa intressenter vilka tecken som täcks. Nedan är ett minimalt exempel som använder `matplotlib` för att rendera ett rutnät av tecken.

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

> **Bildens alt‑text:** ![OCR character set diagram](ocr_character_set.png){alt="OCR character set overview"}

Diagrammet krävs inte för kärnlösningen, men det visar hur du kan **use OCR engine** metadata utöver enkel utskrift.

## Steg 5: Integrera teckenuppsättningen i verkliga arbetsflöden

Nu när vi kan hämta **ocr character set**, låt oss se ett praktiskt scenario: validera OCR‑utdata innan den lagras i en databas.

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

Detta mönster förhindrar skräpd data från att smita in i efterföljande pipelines, ett vanligt problem när man hanterar flerspråkiga dokument.

## Vanliga fallgropar och kantfall

| Pitfall | Why it Happens | How to Avoid |
|---------|----------------|--------------|
| **Script name typo** (t.ex. `"Cyrillic "` med efterföljande mellanslag) | Motorn behandlar strängen bokstavligt och kan inte hitta skriptet. | Ta bort blanksteg: `script.strip()` innan du anropar `get_supported_characters`. |
| **Tom teckenlista** | Vissa motorer exponerar ett skript men har ännu inte laddat språkmodellen. | Anropa `engine.load_language_model(script)` om biblioteket tillhandahåller en sådan metod, eller säkerställ att modellfilerna finns. |
| **Unicode‑normaliseringsproblem** | Tecken som “é” kan visas som sammansatta (`\u00E9`) eller dekomponerade (`e\u0301`). | Normalisera strängar med `unicodedata.normalize('NFC', text)` innan validering. |
| **Prestanda på stora skript** (t.ex. kinesiska) | Att hämta tusentals tecken kan vara långsamt. | Cacha resultatet efter första anropet; de flesta applikationer behöver bara listan en gång. |

## Fullt fungerande exempel

När vi sätter ihop allt, här är ett enda skript du kan kopiera‑klistra in och köra:

```python
import ocr
import matplotlib.pyplot as plt

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

def plot_character_grid(chars, title="OCR Character Set"):
    cols = 10
    rows = (len(chars) + cols - 1) // cols
    fig, ax = plt.subplots(figsize=(cols, rows))
    ax.set_axis_off()
    for idx, ch in enumerate(chars):
        row = idx // cols
        col = idx % cols
        ax.text(col / cols, 1 - row / rows, ch, fontsize=14


## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Aspose OCR Tutorial – Optical Character Recognition](/ocr/english/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}