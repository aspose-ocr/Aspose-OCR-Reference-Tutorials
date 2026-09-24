---
category: general
date: 2026-01-12
description: jak nastavit jazyk v Aspose OCR Python a extrahovat text z obrázku pomocí
  vlastního slovníku. krok za krokem tutoriál pro vývojáře
draft: false
keywords:
- how to set language
- extract text from image
- how to extract text
- how to add dictionary
- how to process image
language: cs
og_description: Jak nastavit jazyk v Aspose OCR Python a extrahovat text z obrázku
  pomocí vlastního slovníku. Naučte se celý pracovní postup během několika minut.
og_title: Jak nastavit jazyk v Aspose OCR Python – Kompletní průvodce
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Jak nastavit jazyk v Aspose OCR Python – Kompletní průvodce
url: /cs/python-java/general/how-to-set-language-in-aspose-ocr-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak nastavit jazyk v Aspose OCR Python – Kompletní průvodce

Už jste se někdy zamysleli nad **jak nastavit jazyk** při použití Aspose OCR v Pythonu? Nejste sami – mnoho vývojářů narazí na tento problém, když výchozí anglický model nepozná produktové kódy, sériová čísla nebo vícejazyčný text. Dobrou zprávou je, že řešení je jednoduché i výkonné. V tomto tutoriálu vás provedeme nastavením jazyka, přidáním vlastního slovníku, extrakcí textu z obrázku a nakonec zpracováním obrázku pro nejlepší výsledky OCR.

Probereme vše, co potřebujete vědět: od instalace knihovny až po spuštění kompletního příkladu, který vypíše extrahovaný text. Na konci budete schopni **extrahovat text z obrázku** souborů s jistotou, i když obsahuje neobvyklé kódy nebo smíšené jazyky.

## Požadavky

* Nainstalovaný Python 3.8+ (kód používá f‑stringy, takže starší verze nebudou fungovat).
* Aktivní licence Aspose OCR pro Python nebo klíč pro bezplatnou zkušební verzi.
* Balíček `asposeocr` nainstalovaný pomocí `pip install asposeocr`.
* Vzorek obrázku (`product_label.png`), který obsahuje text, který chcete přečíst.

Pokud už tyto komponenty máte, skvělé – pojďme dál. Pokud ne, stáhněte si bezplatnou zkušební verzi z webu Aspose a spusťte instalační příkaz; zabere to jen minutu.

## Krok 1: Importujte modul Aspose OCR

Prvním krokem je přidat třídy OCR do vašeho skriptu. Toto je základ pro **jak nastavit jazyk** později.

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr
```

> **Tip:** Uchovávejte importy na začátku souboru. Usnadní to čtení skriptu, zejména když se k němu později vrátíte.

## Krok 2: Jak nastavit jazyk

Ve výchozím nastavení Aspose OCR předpokládá angličtinu. Pokud váš obrázek obsahuje francouzštinu, němčinu nebo jakýkoli jiný jazyk, musíte motoru sdělit, který jazyk má použít. Zde se ukáže síla hlavního klíčového slova.

```python
# Step 2: Create an OCR engine and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # change to ocr.Language.FRENCH, etc.
```

Proč je to důležité? OCR motory se spoléhají na jazykově specifické modely znaků. Poskytnutí správného jazyka dramaticky zvyšuje přesnost – zejména u znaků s diakritikou nebo jazykově specifických ligatur.

> **Poznámka:** Pokud potřebujete podporovat více jazyků současně, můžete předat seznam jako `ocr.Language.ENGLISH | ocr.Language.SPANISH`.

## Krok 3: Jak přidat slovník (uživatelem definovaná slova)

Někdy OCR motor špatně rozpozná produktové kódy jako “AB‑1234”. Můžete zvýšit jistotu tím, že poskytnete vlastní slovník. To přímo odpovídá na **jak přidat slovník** v Aspose OCR.

```python
# Step 3: Supply product codes that must be recognized with higher confidence
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])
```

Motor považuje tato slova za „známá“ a bude je upřednostňovat před podobně vypadajícími znaky. To je zvláště užitečné pro SKU čísla, sériové kódy nebo názvy značek, které nejsou součástí přirozeného jazyka.

## Krok 4: Jak zpracovat obrázek

Jakmile je motor nakonfigurován, musíte načíst obrázek, který chcete analyzovat. To řeší **jak zpracovat obrázek** čistým a opakovatelným způsobem.

```python
# Step 4: Load the image containing the product label
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")
```

Pokud pracujete s PDF soubory, můžete nejprve každou stránku převést na obrázek – Aspose OCR to podporuje přímo.

## Krok 5: Jak extrahovat text z obrázku

Po nastavení všeho je posledním krokem spustit OCR a získat text. To je jádro **jak extrahovat text** z obrázku.

```python
# Step 5: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)

# Step 6: Print the extracted text
print(ocr_result.text)
```

Po spuštění skriptu byste měli vidět něco jako:

```
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

Pokud výstup vypadá poškozeně, zkontrolujte, že jste nastavili správný jazyk a že váš vlastní slovník obsahuje přesně řetězce, které očekáváte.

## Kompletní funkční příklad

Spojením všech částí zde máte celý skript, který můžete zkopírovat do souboru nazvaného `extract_label.py`. Nezapomeňte nahradit `YOUR_DIRECTORY` skutečnou cestou k vašemu obrázku.

```python
import asposeocr as ocr

# Create OCR engine and set language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # Change if needed

# Add custom dictionary entries
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])

# Load the target image
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")

# Perform OCR
ocr_result = ocr_engine.process(image)

# Output the result
print("=== OCR Extraction Result ===")
print(ocr_result.text)
```

### Očekávaný výstup

```
=== OCR Extraction Result ===
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

Pokud vidíte přesně kódy, které jste přidali do slovníku, úspěšně jste zvládli **jak nastavit jazyk**, **jak přidat slovník** a **jak extrahovat text z obrázku** pomocí Aspose OCR.

## Řešení běžných okrajových případů

| Situace | Co dělat |
|-----------|------------|
| **Obrázek je rozmazaný** | Předzpracujte pomocí `ocr.Image.apply_filter()` pro zaostření před voláním `process()`. |
| **Více jazyků na jednom obrázku** | Nastavte `ocr_engine.language = ocr.Language.ENGLISH | ocr.Language.SPANISH`. |
| **Velké PDF soubory** | Procházejte každou stránku, převádějte na `ocr.Image` a volajte `process()` pro každou stránku. |
| **Neočekávané znaky** | Přidejte je do seznamu uživatelem definovaných slov; Aspose OCR je považuje za tokeny s vysokou jistotou. |

## Vizuální reference

![jak nastavit jazyk v Aspose OCR příklad](image.png "Snímek obrazovky ukazující nastavení jazyka v Aspose OCR Python příkladu")

*Alt text:* **jak nastavit jazyk** snímek obrazovky ilustrující přiřazení vlastnosti jazyka v Python IDE.

## Závěr

Nyní víte **jak nastavit jazyk** v Aspose OCR Python, jak **přidat položky do slovníku** a přesné kroky k **extrakci textu z obrázku** a **zpracování obrázku** pro optimální výsledky. Výše uvedený kompletní příklad můžete vložit do libovolného projektu, upravit pro různé jazyky a rozšířit pro dávkové zpracování nebo vstupy PDF.

Jste připraveni na další výzvu? Vyzkoušejte zaměnit `ocr.Language.ENGLISH` za `ocr.Language.FRENCH` a pozorujte zvýšení přesnosti na francouzských štítcích. Nebo experimentujte s metodou `set_user_defined_words` a zahrňte celý katalog produktů – váš OCR motor bude považovat každý záznam za vysoce jistou shodu.

Šťastné programování a ať jsou vaše OCR výsledky vždy krystalicky čisté!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}