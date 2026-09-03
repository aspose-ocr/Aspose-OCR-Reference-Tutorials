---
category: general
date: 2026-01-02
description: Naučte se, jak odstranit zkosení obrázku a zvýšit kontrast, abyste rychle
  získali prostý text. Obsahuje krok za krokem Python kód a tipy pro extrakci textu.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: cs
og_description: Jak odstranit zkosení obrazu a zvýšit kontrast pro získání prostého
  textu. Kompletní příklad v Pythonu s extrakcí tabulek a akcelerací na GPU.
og_title: Jak narovnat obrázek – Kompletní GPU OCR tutoriál
tags:
- OCR
- Python
- Image Processing
title: Jak zarovnat obrázek – Průvodce OCR s GPU akcelerací
url: /cs/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak deskewovat obrázek – Průvodce OCR s akcelerací GPU

Už jste se někdy zamýšleli **jak deskewovat obrázek**, když vaše účtenky přicházejí v podivném úhlu? Nejste sami; nakloněná fotografie může dokonalou čitelnou účtenku proměnit v nečitelný chaos. Dobrou zprávou je, že s několika řádky Pythonu můžete automaticky deskewovat, zvýšit kontrast a získat čistý prostý text – bez ručního Photoshopu.  

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který nejen **jak deskewovat obrázek**, ale také ukazuje **jak zvýšit kontrast**, **jak získat prostý text** a dokonce **jak extrahovat text** z tabulek, které OCR engine objeví. Na konci budete mít samostatný skript, který můžete vložit do libovolného projektu.

## Co budete potřebovat

- Nainstalovaný Python 3.9+ (kód používá typové nápovědy, takže novější interpret je výhodou)
- Knihovna `ocr`, která poskytuje `OcrEngine`, `EngineMode`, `ImageProcessingOptions` a `OcrResult` (instalujte pomocí `pip install ocr‑sdk` – nahraďte skutečným názvem balíčku, který používáte)
- GPU s kompatibilními ovladači, pokud chcete rychlostní boost (volitelné, ale doporučené)
- Soubor obrázku, který je mírně natočený nebo má nízký kontrast, např. `receipt_skewed.jpg`

> **Pro tip:** Pokud nemáte GPU, stačí změnit `EngineMode.GPU` na `EngineMode.CPU` a skript bude fungovat – jen o něco pomaleji.

## Krok‑za‑krokem implementace

Níže rozdělujeme řešení do logických částí. Každá část má popisný **H2**, který obsahuje buď primární klíčové slovo *jak deskewovat obrázek*, nebo jedno z sekundárních klíčových slov. Kód je kompletní, okomentovaný a připravený ke spuštění.

### Jak deskewovat obrázek s OCR akcelerovaným GPU

Prvním krokem je nastavit OCR engine, aby běžel na GPU, a zapnout funkci automatického deskewu. Auto‑deskew analyzuje geometrii obrázku a otočí jej zpět do svislé polohy.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Proč je to důležité:** Akcelerace GPU může zkrátit dobu zpracování ze sekund na milisekundy, což je klíčové, když zpracováváte desítky účtenek za minutu.

### Zvýšení kontrastu obrázku pro lepší rozpoznání

Nízký kontrast účtenky je noční můrou pro jakýkoli OCR systém. Zvýšením kontrastu poskytneme engine jasnější hrany, se kterými může pracovat.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **Jak zvýšit kontrast:** Metoda `set_contrast_boost` přijímá procenta; 30 % je bezpečná výchozí hodnota, která funguje pro většinu naskenovaných účtenek. Pokud jsou vaše obrázky extrémně tmavé, zvyšte ji na 50 % nebo experimentujte.

### Získání prostého textu ze zpracovaného obrázku

Jakmile je obrázek rovný a jasný, předáme jej engine a požádáme o výsledek v podobě prostého textu.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Očekávaný výstup** (zkrácený pro stručnost):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **Jak získat prostý text:** Metoda `get_text()` odstraní veškeré informace o rozložení a vrátí čistý řetězec, který můžete uložit do databáze, poslat do API nebo předat dalším analytickým procesům.

### Jak extrahovat text z detekovaných tabulek

Často účtenky obsahují tabulková data (položky, množství, ceny). SDK OCR dokáže detekovat tabulky a umožní vám iterovat přes řádky a buňky.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Ukázkový výstup tabulky**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Proč extrahovat tabulky:** Strukturovaná data usnadňují výpočet součtů, generování reportů nebo import do účetního softwaru.

### Kompletní funkční skript

Spojením všech částí získáte skript, který můžete zkopírovat do souboru `deskew_and_ocr.py`:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

Spusťte jej pomocí:

```bash
python deskew_and_ocr.py
```

Měli byste vidět vyčištěný text a případně detekované tabulky vytištěné v konzoli.

## Běžné okrajové případy a jak je řešit

| Situace | Co dělat |
|-----------|------------|
| **Obrázek je vzhůru nohama** | Zvyšte důvěru `set_auto_deskew(True)` také voláním `set_rotation_correction(True)`, pokud SDK tuto funkci nabízí. |
| **Zvýšení kontrastu udělá obrázek příliš jasný** | Snižte procento předávané do `set_contrast_boost` (např. 15 %). |
| **GPU není k dispozici** | Přepněte `EngineMode.GPU` na `EngineMode.CPU`; zbytek pipeline zůstane beze změny. |
| **Tabulky jsou přehlédnuty** | Zkuste sken s vyšším rozlišením nebo povolte `set_table_detection(True)`, pokud knihovna tuto možnost poskytuje. |

## Další kroky: Od prostého textu k strukturovaným datům

Nyní, když víte **jak deskewovat obrázek**, **jak zvýšit kontrast** a **jak získat prostý text**, můžete:

- Analyzovat prostý text pomocí regulárních výrazů a extrahovat páry klíč‑hodnota (např. `total`, `date`).
- Uložit výsledky do SQLite nebo PostgreSQL databáze pro pozdější reportování.
- Napojit skript na serverless funkci (AWS Lambda, Azure Functions) pro automatické zpracování nahrávek.

Všechny tyto rozšíření staví na stejné základně, kterou jsme zde probírali.

## Závěr

Prošli jsme **jak deskewovat obrázek** pomocí OCR engine s akcelerací GPU, ukázali **jak zvýšit kontrast** pro ostřejší rozpoznání, předvedli vám přesně **jak získat prostý text** a dokonce **jak extrahovat text** z tabulek. Kompletní, spustitelný skript vše spojuje, takže jej můžete vložit do libovolného Python projektu a okamžitě začít získávat čistá data ze skloněných, nízkokontrastních fotografií.

Vyzkoušejte to na několika vlastních účtenkách, upravte úroveň kontrastu a nechte OCR udělat těžkou práci. Pokud narazíte na podivnosti, podívejte se zpět na tabulku s okrajovými případy – většina problémů se řeší drobným nastavením.

Šťastné kódování a ať jsou vaše obrázky vždy rovné a jasné!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}