---
category: general
date: 2026-06-06
description: Jak předzpracovat obrázky pro OCR pomocí Pythonu. Naučte se binarizovat
  obrázek pomocí Otsu, jak vyrovnat skenované dokumenty a zlepšit přesnost OCR pro
  německý text.
draft: false
keywords:
- how to preprocess images for OCR
- binarize image using otsu
- how to deskew scanned documents
- how to improve OCR accuracy
- extract text from german image
language: cs
og_description: Jak předzpracovat obrázky pro OCR v Pythonu. Tento tutoriál ukazuje,
  jak binarizovat obrázek pomocí Otsu, jak vyrovnat skenované dokumenty a jak zlepšit
  přesnost OCR pro německé obrázky.
og_title: Jak předzpracovat obrázky pro OCR – Kompletní průvodce v Pythonu
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
title: Jak předzpracovat obrázky pro OCR – Kompletní průvodce v Pythonu
url: /cs/python-java/general/how-to-preprocess-images-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak předzpracovat obrázky pro OCR – Kompletní průvodce v Pythonu

Už jste se někdy zamýšleli **jak předzpracovat obrázky pro OCR**, aby text byl naprosto čitelný? Nejste jediní. Naskenované dokumenty — zejména špinavé německé stránky — mohou být noční můrou pro jakýkoli OCR engine. Dobrá zpráva? Několik chytrých kroků předzpracování může proměnit rozmazaný, posetý šmouhami sken na čistý, strojově čitelný obrázek.

V tomto tutoriálu projdeme praktickým příkladem, který ukazuje **jak předzpracovat obrázky pro OCR** pomocí Pythonu. Naučíte se **binarizovat obrázek pomocí Otsu**, **jak narovnat (deskew) naskenované dokumenty** a celkově **jak zlepšit přesnost OCR**, když potřebujete **extrahovat text z německých obrázkových** souborů. Žádné zbytečnosti, jen funkční skript, který můžete dnes zkopírovat‑vložit.

## Co budete potřebovat

- **Python 3.9+** (jakákoli recentní verze)
- OCR knihovnu, která poskytuje třídu `OcrEngine` — pro ukázku předpokládáme obecný balíček `ocr`. Nainstalujte jej pomocí `pip install ocr-lib`.
- Špinavý německý sken (`noisy_german_scan.tif`), který chcete otestovat.
- Základní povědomí o Python funkcích (pokud už jste někdy použili `def`, jste v pohodě).

> **Pro tip:** Pokud používáte jiný OCR SDK (např. Tesseract přes `pytesseract`), koncepty zůstávají stejné — stačí přizpůsobit názvy metod.

## Přehled řešení

1. **Vytvořit instanci OCR engine.**  
2. **Nastavit jazyk rozpoznávání na němčinu.**  
3. **Sestavit vlastní pipeline předzpracování**, která zahrnuje narovnání, odšumění, binarizaci (Otsu) a roztažení kontrastu.  
4. **Připojit pipeline k enginu**, aby každá obrázek prošel automaticky.  
5. **Spustit OCR** na špinavém německém skenu.  
6. **Vytisknout extrahovaný text** pro ověření výsledku.

Níže rozebíráme každý krok, vysvětlujeme **proč** je důležitý a ukazujeme přesný kód, který potřebujete.

![how to preprocess images for OCR example](image.png "how to preprocess images for OCR example")

## Krok 1: Vytvořit instanci OCR Engine

Nejprve – bez engine se nic neděje. Objekt `OcrEngine` je vstupní bod, který koordinuje veškeré následné zpracování.

```python
# Step 1: Initialize the OCR engine
from ocr import OcrEngine, Language

ocr_engine = OcrEngine()
```

*Proč je to důležité:* Inicializace engine nastaví interní zdroje (např. jazykové modely) a poskytne čistý základ, na který můžete později připojit vlastní pipeline.

## Krok 2: Nastavit jazyk rozpoznávání na němčinu

Přesnost OCR je silně závislá na jazyku. Když engine řeknete, že má očekávat němčinu, aktivujete správnou znakovou sadu a jazykový model.

```python
# Step 2: Tell the engine we’re working with German text
ocr_engine.set_recognition_language(Language.GERMAN)
```

Pokud tento krok přeskočíte, engine může výchozí nastavit angličtinu a špatně rozpoznávat umlauty (ä, ö, ü) a znak ß — časté úskalí při práci s německými skeny.

## Krok 3: Sestavit vlastní pipeline předzpracování

Toto je jádro **jak předzpracovat obrázky pro OCR**. Propojíme čtyři transformace:

| Transformace | Co dělá | Proč pomáhá |
|--------------|---------|-------------|
| **Deskew** | Otáčí obrázek zpět do horizontální polohy (max 5°) | Skeny nejsou často dokonale zarovnané; narovnání odstraňuje sklon, který matí segmentaci znaků. |
| **Denoise** | Snižuje náhodné šmouhy (síla 0.7) | Šum vytváří falešné hrany, které OCR může zaměnit za znaky. |
| **Binarize (Otsu)** | Převádí na černobílý obraz pomocí Otsu metody | Čistý binární obrázek poskytuje ostrý kontrast mezi popředím (text) a pozadím. |
| **Contrast Stretch** | Rozšiřuje dynamický rozsah | Zlepšuje čitelnost slabých tahů, zejména u starých dokumentů. |

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

### Jak narovnat (Deskew) naskenované dokumenty

Volání `deskew` výše je konkrétní odpovědí na **jak narovnat naskenované dokumenty**. Interně odhaduje dominantní úhel řádků textu pomocí Houghovy transformace a obrázek otočí zpět. Pokud jsou vaše dokumenty natočeny více než 5°, zvyšte `max_angle`, ale dejte pozor na artefakty při nadměrném otáčení.

### Binarizovat obrázek pomocí Otsu

Řádek `binarize(method="otsu")` přímo odpovídá dotazu **binarizovat obrázek pomocí otsu**. Otsu algoritmus vypočítá práh, který minimalizuje vnitřní varianci tříd, což je ideální pro dokumenty s bimodálními histogramy (tmavý text vs. světlé pozadí).

## Krok 4: Připojit pipeline k enginu

Nyní řekneme OCR engine, aby spouštěl každou příchozí obrázek přes pipeline, kterou jsme právě vytvořili.

```python
# Step 4: Register the custom pipeline
ocr_engine.set_preprocessing(preprocessing_pipeline)
```

*Proč je to důležité:* Bez registrace by engine zpracovával surový sken a ignoroval veškeré čištění, které jsme nastavili. Tento krok zajišťuje **jak zlepšit přesnost OCR** aplikací stejného předzpracování konzistentně.

## Krok 5: Rozpoznat text ze špinavého německého skenu

Je čas dát vše dohromady. Předáme engine špinavý německý obrázek a necháme ho udělat těžkou práci.

```python
# Step 5: Run OCR on the target file
image_path = "YOUR_DIRECTORY/noisy_german_scan.tif"
recognition_result = ocr_engine.recognize_image(image_path)
```

Pokud vás zajímá výkon, můžete měřit dobu volání:

```python
import time
start = time.time()
result = ocr_engine.recognize_image(image_path)
print(f"OCR took {time.time() - start:.2f}s")
```

## Krok 6: Vypsat rozpoznaný text

Nakonec vytiskneme extrahovaný řetězec. To je přímá odpověď na **extrahovat text z německého obrázku**.

```python
# Step 6: Display the OCR output
print("=== Recognized German Text ===")
print(recognition_result.text)
```

### Očekávaný výstup

Předpokládejme, že ukázkový sken obsahuje větu „Die schnelle braune Füchsin springt über den faulen Hund.“; měli byste vidět něco jako:

```
=== Recognized German Text ===
Die schnelle braune Füchsin springt über den faulen Hund.
```

Pokud výstup stále obsahuje poškozené znaky, zvažte úpravu síly `denoise` nebo zvýšení `max_angle` pro narovnání.

## Časté problémy a jak je řešit

- **Chybějící jazykový model:** Zapomenutí `set_recognition_language(Language.GERMAN)` často vede k chybějícím umlautům. Zkontrolujte volání.
- **Přehnané odšumění:** Síla nad 0.9 může vymazat tenké tahy, zejména ve starých fontách. Držte se 0.5‑0.7 pro většinu případů.
- **Nesprávný formát souboru:** Některé OCR enginy selžou na více‑stránkových TIFF souborech. Pokud máte více‑stránkový dokument, rozdělte jej na jednostránkové soubory.
- **Pořadí pipeline:** Ukázané pořadí (deskew → denoise → binarize → contrast) je záměrné. Binarizace před odšuměním může zachytit šum; vždy nejprve odšuměte.

## Rozšíření pipeline (Co dál?)

Nyní, když máte solidní základ, můžete chtít:

- **Přidat morfologické otevírání** pro vyčištění drobných skvrn (`.morph_open(kernel=3)`).
- **Integrovat jazykový model** pro korekci po zpracování (`ocr_engine.apply_spellcheck()`).
- **Paralelizovat dávkové zpracování** velkých datasetů pomocí `concurrent.futures`.

Všechny tyto možnosti jsou přirozenými rozšířeními, která zachovávají hlavní myšlenku **jak předzpracovat obrázky pro OCR** a zároveň dále zvyšují **jak zlepšit přesnost OCR**.

## Závěr

Prošli jsme **jak předzpracovat obrázky pro OCR** od začátku do konce: vytvořili engine, nastavili německý jazyk, postavili pipeline, která **binarizuje obrázek pomocí Otsu**, **jak narovnat naskenované dokumenty**, a nakonec **extrahuje text z německého obrázku** s vyšší důvěrou. Dodržením šesti výše uvedených kroků zaznamenáte výrazný nárůst kvality rozpoznání — už žádné nekonečné ruční opravy.

Vyzkoušejte skript na vlastních skenech, pohrávejte si s parametry a nechte výsledky mluvit za vás. Máte otázky ohledně konkrétního vylepšení předzpracování? Zanechte komentář a ponoříme se do detailů společně.

Šťastné kódování a ať je vaše OCR vždy přesné!


## Co se naučíte dál?


Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vlastních projektech.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}