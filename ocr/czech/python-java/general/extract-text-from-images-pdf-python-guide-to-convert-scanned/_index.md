---
category: general
date: 2026-06-06
description: Extrahujte text z obrázků a PDF pomocí Python OCR. Naučte se, jak rychle
  převést naskenované dokumenty na text pomocí asynchronního dávkového rozpoznávání.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: cs
og_description: Extrahujte text z obrázků a PDF pomocí Pythonu. Tento krok‑za‑krokem
  průvodce ukazuje, jak převést naskenované dokumenty na text pomocí asynchronního
  OCR.
og_title: Extrahovat text z obrázků PDF – Python OCR tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Extrahovat text z PDF obrázků – Python průvodce pro převod naskenovaných dokumentů
  na text
url: /cs/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z PDF obrázků – Python průvodce převodem naskenovaných dokumentů na text

Už jste někdy potřebovali **extrahovat text z PDF obrázků** bez strávení hodin přepisováním? V tomto průvodci vám ukážeme, jak **převést naskenované dokumenty na text** pomocí jednoduchého asynchronního OCR workflow v Pythonu.  

Pokud jste někdy zírali na hromadu naskenovaných PDF a pomysleli si: „Musí existovat rychlejší způsob“, jste na správném místě. Projdeme každý řádek kódu, vysvětlíme, proč je každá část důležitá, a dokonce se podíváme na několik okrajových případů, na které můžete narazit.

## Co se naučíte

- Jak spustit OCR engine a nastavit jazyk rozpoznávání.  
- Mechaniku předávání smíšeného seznamu PNG a PDF souborů do dávkového rozpoznávače.  
- Spuštění OCR úlohy asynchronně, aby vaše aplikace zůstala responzivní.  
- Získání výsledků, přiřazení k jejich zdrojovým souborům a výpis čistého výstupu.  

**Prerequisites**: Python 3.8+, základní pochopení `asyncio` nebo `concurrent.futures` a OCR knihovnu, která poskytuje třídu `OcrEngine` podobnou té v příkladu (např. Aspose.OCR, obal Tesseractu nebo vlastní obal). Žádné těžké nastavení není potřeba — stačí nainstalovat knihovnu a můžete začít.

![extrahování textu z PDF obrázků](https://example.com/placeholder.png "Screenshot of OCR output – extract text from images pdf")

## Extrahování textu z PDF obrázků – Nastavení OCR engine

První věc, kterou potřebujete, je instance OCR engine nakonfigurovaná pro jazyk vašich dokumentů. V našem případě použijeme francouzštinu, ale můžete ji nahradit libovolným podporovaným jazykem.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**Why this matters**: Nastavení jazyka předem dramaticky zvyšuje přesnost. Engine používá jazykově specifické slovníky a modely znaků; předání špatného jazyka je častým zdrojem zkresleného výstupu.

## Připravte seznam souborů – Obrázky a PDF dohromady

Náš dávkový rozpoznávač zvládne jak rastrové obrázky (`.png`, `.jpg`), tak PDF kontejnery. Stačí předat obyčejný Python seznam cest k souborům.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**Tip**: Udržujte seznam plochý; engine interně rozbalí každou stránku PDF na obrázky před rozpoznáním. Pokud máte tisíce souborů, zvažte rozdělení seznamu na menší dávky, aby nedošlo k výkyvům paměti.

## Spuštění asynchronního dávkového rozpoznávání

Místo blokování hlavního vlákna spustíme OCR úlohu na pozadí. Metoda vrací `Future`, který nakonec bude obsahovat seznam objektů `OcrResult`.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**How it works**: Pod kapotou engine spouští thread pool (nebo asynchronní úlohu, podle implementace). To vám umožní pokračovat v jiných činnostech — např. aktualizovat UI, načítat další soubory nebo logovat průběh — zatímco těžká práce probíhá jinde.

## Dělejte něco užitečného, zatímco OCR běží

Častá chyba je sedět nečinně a v těsném cyklu dotazovat `future`. Místo toho můžete provádět jakoukoli nesouvisející práci. Pro demonstraci jen vypíšeme stavovou řádku.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## Shromážděte výsledky po dokončení Future

Až budete připraveni získat OCR výstup, použijte `as_completed` z `concurrent.futures`. Tento vzor funguje, ať máte jeden nebo více future.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**What you’ll see**: Každá cesta k souboru následovaná extrahovanou čistou textovou reprezentací. Pro PDF, `result.text` obsahuje konkatenovaný text ze všech stránek.

### Očekávaný výstup (příklad)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

Pokud si všimnete chybějících znaků, dvakrát zkontrolujte, že nastavený jazyk odpovídá jazyku dokumentu, a zvažte předzpracování obrázků (odklon, zvýšení kontrastu) před předáním engine.

## Řešení okrajových případů a běžných úskalí

| Situace | Co dělat |
|-----------|------------|
| **Smíšené jazyky** | Nejprve proveďte detekci jazyka, poté vytvořte samostatné enginy pro každý jazyk. |
| **Obrovské PDF (> 100 MB)** | Rozdělte PDF na jednotlivé stránky na disku (např. pomocí `PyPDF2`) a zpracovávejte je jako samostatné položky. |
| **Neslatinské skripty** | Ujistěte se, že OCR knihovna obsahuje požadovaný jazykový balíček; některé knihovny vyžadují stažení dodatečných datových souborů. |
| **Úzké místo výkonu** | Zvyšte velikost thread poolu (`engine.set_thread_pool_size(8)`) nebo přejděte na GPU‑akcelerovaný backend, pokud je k dispozici. |
| **Chybějící text v nízkokvalitních obrázcích** | Předzpracujte pomocí OpenCV: `cv2.resize`, `cv2.threshold` a `cv2.medianBlur` pro zlepšení čitelnosti. |

## Kompletní funkční příklad (připravený ke kopírování)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

Uložte tento soubor jako `extract_text_async.py`, nahraďte `YOUR_DIRECTORY` cestou k vašim souborům, nainstalujte OCR balíček (`pip install your-ocr-lib`) a spusťte `python extract_text_async.py`. V konzoli by se měl objevit výstup ilustrovaný výše.

## Další kroky – Přesah základního extrahování

- **Post‑processing**: Odstraňte nadbytečné mezery, normalizujte Unicode (`unicodedata.normalize`) nebo spusťte kontrolu pravopisu pro vyčištění OCR šumu.  
- **Strukturovaný výstup**: Exportujte výsledky do CSV, JSON nebo přímo do databáze pro následné vyhledávání.  
- **Paralelní dávky**: Pokud máte stovky souborů, spusťte více future a použijte frontu, aby CPU byla vytížená, aniž byste přetížili paměť.  
- **Integrace s webovými frameworky**: Napojte tento skript na Flask nebo FastAPI endpoint a poskytujte OCR jako službu na vyžádání.

---

### TL;DR

Nyní víte, jak **extrahovat text z PDF obrázků** pomocí minimálního Python skriptu, který spouští OCR asynchronně, což vám umožní **převést naskenované dokumenty na text**, zatímco váš program zůstává responzivní. Pohrávejte si s nastavením jazyka, velikostí dávek a předzpracovacími triky, abyste získali co nejvyšší přesnost.

Máte nějaký tip, který byste chtěli sdílet — třeba OCR na ručně psané poznámky nebo cloudovou službu? Zanechte komentář a šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, aby vám pomohly zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Extrahování textu z obrázku pomocí Aspose OCR – krok za krokem průvodce](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extrahování textu z obrázků pomocí OCR operace ve složkách](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extrahování textu z obrázků pomocí Aspose.OCR – povolené znaky](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}