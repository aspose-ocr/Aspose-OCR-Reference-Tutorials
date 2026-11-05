---
category: general
date: 2026-04-26
description: Jak dávkově provádět OCR vašich dokumentů a extrahovat text ze skenů
  v Pythonu. Naučte se krok za krokem dávkové zpracování s OcrEngine pro výstup ve
  formátu JSON.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: cs
og_description: Jak hromadně provést OCR vašich naskenovaných souborů a extrahovat
  text ze skenů v jediném skriptu. Kompletní kód, tipy a řešení okrajových případů.
og_title: Jak provádět dávkové OCR – Rychlý průvodce Pythonem
tags:
- OCR
- Python
- Automation
title: Jak provádět hromadné OCR – Efektivně extrahovat text ze skenů
url: /cs/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provádět hromadné OCR – Efektivně extrahovat text ze skenů

Už jste se někdy zamýšleli **jak provádět hromadné OCR** na hromadě naskenovaných PDF, aniž byste ztratili rozum? Nejste jediní — vývojáři se neustále ptají, *„Jak mohu extrahovat text ze skenů najednou?“* Dobrou zprávou je, že několik řádků Pythonu může tuto nudnou práci proměnit v plynulý, automatizovaný proces.

V tomto tutoriálu projdeme kompletním, připraveným řešením, které **extrahuje text ze skenů**, uloží výsledky jako JSON a na konci vám poskytne rychlou kontrolu. Žádné externí služby, žádná magie — jen čistý Python, třída `OcrEngine` a trochu práce se složkami.

## Co si z toho odnesete

- Plně funkční skript, který **provádí hromadné OCR** nad libovolnou složkou s obrázky.
- Jasná vysvětlení *proč* každá řádka existuje, nejen *co* dělá.
- Tipy pro práci s prázdnými složkami, soubory, které nejsou obrázky, a velkými dávkami.
- Způsob, jak ověřit, že výstupní JSON skutečně obsahuje extrahovaný text.

### Předpoklady (minimum)

| Požadavek | Proč je důležitý |
|-------------|----------------|
| Python 3.8+ | Moderní syntaxe a typové nápovědy |
| `OcrEngine` library (or a compatible wrapper) | Knihovna `OcrEngine` (nebo kompatibilní obal) – Základní OCR funkčnost |
| A directory with scanned image files (PNG, JPG, TIFF) | Adresář s naskenovanými soubory obrázků (PNG, JPG, TIFF) – Vstupní data |
| Write permissions for the output folder | Oprávnění k zápisu do výstupní složky – Ukládání výsledků JSON |

Pokud už to máte, skvělé — ponořme se do toho.

![workflow hromadného OCR](image-placeholder.png){alt="workflow hromadného OCR"}

## Krok 1 – Inicializace OCR enginu (jak provádět hromadné OCR)

Než budeme moci něco zpracovat, potřebujeme instanci OCR enginu. Považujte ji za „mozek“, který přečte každý obrázek a vypíše text. Jednorázová inicializace a opakované používání během celé dávky je nejefektivnější vzor.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **Proč znovu použít stejnou instanci?**  
> Vytváření nového enginu pro každý soubor by opakovaně načítalo těžké modely do paměti, což by výrazně zpomalilo dávku. Jedna instance udržuje model v RAM a umožní vám zpracovat tisíce obrázků bez znatelného zpomalení.

## Krok 2 – Nastavte složku se skeny (extrahovat text ze skenů)

Vaše skeny jsou uložené někde na disku. Řekněme skriptu, kde je najde. Použití absolutních cest zabraňuje překvapením typu „soubor nenalezen“, když je skript spuštěn z jiného pracovního adresáře.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **Tip:**  
> Pokud používáte Windows, lomítka (`/`) fungují naprosto v pořádku s `os.path.abspath`, takže nemusíte escapovat zpětná lomítka.

## Krok 3 – Vyberte, kam mají jít výsledky JSON

Pravděpodobně chcete mít uklizenou složku pro OCR výsledky. Udržení výstupu odděleně od zdrojů usnadňuje pozdější úklid nebo předání JSONu do dalšího pipeline.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **Proč vytvořit složku programově?**  
> Zajišťuje, že skript nespadne, pokud adresář chybí, a `exist_ok=True` dělá operaci idempotentní — spusťte skript několikrát bez chyb.

## Krok 4 – Spusťte hromadný proces (jak provádět hromadné OCR)

Nyní jádro věci: říct `ocr_engine`, aby procházel každý soubor v `input_dir`, spustil OCR a uložil JSON do `output_dir`. Příznak `format="json"` říká enginu, aby výsledek serializoval strukturovaným způsobem, který milují downstream nástroje.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### Co se děje pod kapotou?

1. **Objevování souborů** – Engine rekurzivně prohledává `input_folder`, ignoruje skryté soubory.
2. **Validace souborů** – Do OCR modelu jsou předány jen podporované přípony obrázků (`.png`, `.jpg`, `.tif` atd.).
3. **Spuštění OCR** – Každý obrázek je odeslán do OCR enginu; zachytí se text, skóre důvěry a data o rozložení.
4. **Serializace do JSON** – Výsledek je zapsán do souboru se stejným základním názvem, ale s příponou `.json` ve `output_folder`.

> **Zvládání okrajových případů:**  
> - **Prázdná složka:** Engine zaznamená „No files found“ a vrátí se elegantně.  
> - **Poškozený obrázek:** Přeskočí soubor, zaznamená chybu do `batch_errors.log` a pokračuje.  
> - **Obrovská dávka (10 000+ souborů):** Spotřeba paměti zůstává nízká, protože každý obrázek je zpracován samostatně.

## Krok 5 – Potvrďte, že konverze byla dokončena

Jednoduchý příkaz `print` poskytne okamžitou zpětnou vazbu v konzoli. Pro produkční pipeline můžete nahradit tento výpis voláním logování nebo e‑mailovým upozorněním.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

Když uvidíte tento řádek, můžete bezpečně prozkoumat složku `json_output`. Každý JSON soubor bude vypadat zhruba takto:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

Nyní můžete tyto JSON soubory vložit do databáze, vyhledávacího indexu nebo jakéhokoli downstream analytického nástroje.

## Často kladené otázky (a rychlé odpovědi)

**Q: Co když potřebuji zpracovávat PDF místo obrázků?**  
A: Nejprve převést každou stránku PDF na obrázek (např. pomocí `pdf2image`) a umístit vzniklé PNG/JPG soubory do `input_dir`. Logika hromadného OCR zůstane beze změny.

**Q: Můžu změnit výstupní formát na prostý text?**  
A: Rozhodně. Nahraďte `format="json"` za `format="txt"` a engine zapíše soubor `.txt` obsahující pouze extrahovaný text.

**Q: Mé skeny jsou v několika podadresářích — bude skript procházet rekurzivně?**  
A: Ano. `batch_process` standardně prochází strom adresářů. Pokud chcete plochý výstup, nastavte `flatten=True` (pokud knihovna podporuje) nebo po‑zpracujte názvy JSON souborů.

**Q: Jak zacházet s ne-latinskými skripty?**  
A: Inicializujte `OcrEngine` s parametrem jazyka, např. `OcrEngine(lang="spa+eng")`. Samotná smyčka dávky nevyžaduje žádné změny.

## Profesionální tipy a běžné úskalí

- **Velikost dávky má význam:** Pokud zaznamenáte špičky CPU, omezte proces jednoduchým `time.sleep(0.1)` mezi soubory.
- **Logování:** Vyměňte volání `print` za Python modul `logging` pro zachycení časových razítek a úrovní chyb.
- **Kolize názvů souborů:** Pokud dva skeny mají stejný základní název, ale jsou v různých podadresářích, JSON soubory se přepíší. Přidejte hash relativní cesty k výstupnímu názvu, abyste tomu předešli.
- **Úniky paměti:** Některé OCR backendy drží nativní zdroje. Na konci skriptu zavolejte `ocr_engine.close()`, pokud knihovna poskytuje metodu pro úklid.

## Kompletní skript – připravený ke zkopírování a vložení

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**Očekávaný výstup v konzoli**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

Můžete ověřit JSON otevřením libovolného souboru v `json_output` v textovém editoru nebo načtením v Pythonu:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

Měli byste vidět surový OCR‑extrahovaný text vytištěný v konzoli.

## Závěr

Právě jsme probrali **jak provádět hromadné OCR** na celém adresáři naskenovaných obrázků a **extrahovat text ze skenů** do čistých, strojově čitelných JSON souborů. Přístup je úmyslně jednoduchý: nastavit engine jednou, nasměrovat ho na složku a nechat knihovnu udělat těžkou práci. Odtud můžete:

- Připojit JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}