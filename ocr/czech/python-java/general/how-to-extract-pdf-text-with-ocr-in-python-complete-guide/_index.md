---
category: general
date: 2026-06-19
description: Jak extrahovat PDF pomocí OCR v Pythonu – krok za krokem tutoriál pokrývající
  extrakci textu z PDF, rozpoznávání textu z obrázku a příklad OCR v Pythonu.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: cs
og_description: Jak extrahovat PDF pomocí OCR v Pythonu. Naučte se extrahovat text
  z PDF, rozpoznávat text z obrázku a podívejte se na kompletní příklad OCR v Pythonu.
og_title: Jak extrahovat text z PDF pomocí OCR v Pythonu – kompletní návod
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Jak extrahovat text z PDF pomocí OCR v Pythonu – Kompletní průvodce
url: /cs/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak extrahovat text z PDF pomocí OCR v Pythonu – Kompletní průvodce

Už jste se někdy zamýšleli **jak extrahovat PDF** obsah, když je soubor jen naskenovaný obrázek? Nejste v tom sami. V mnoha reálných projektech—například smlouvy, faktury nebo historické archivy—PDF, které obdržíte, neobsahuje žádný vybratelný text. Dobrá zpráva? Několik řádků Pythonu může převést tyto stránky jen s obrázkem na prohledávatelný, editovatelný text.

V tomto tutoriálu projdeme praktickým **OCR Python příkladem**, který načte PDF, vykreslí jeho první stránku jako obrázek a poté **extrahuje text z PDF** pomocí OCR enginu. Na konci přesně vědět, jak **číst PDF s OCR**, proč je každý krok důležitý a jak přizpůsobit kód pro více‑stránkové dokumenty nebo různé jazyky.

## Co se naučíte

- Nainstalujte a nastavte spolehlivou OCR knihovnu pro Python.  
- Převěďte stránky PDF na obrázky vhodné pro OCR.  
- **Rozpoznat text z obrázku** a získat čisté Unicode řetězce.  
- Běžné úskalí (PDF s nízkým rozlišením, otočené stránky) a jak se jim vyhnout.  
- Rozšíření skriptu pro zpracování více stránek nebo dávkové zpracování.

**Požadavky**: Python 3.8+, pip a základní pochopení virtuálních prostředí. Předchozí zkušenosti s OCR nejsou potřeba—stačí sledovat.

---

## ## Jak extrahovat text z PDF pomocí OCR v Pythonu

Tento H2 nadpis obsahuje naše hlavní klíčové slovo právě tam, kde ho vyhledávače milují. Ponořme se rovnou do kódu.

### Krok 1 – Instalace požadovaných balíčků

Nejprve potřebujeme OCR engine. Níže uvedený příklad používá populární balíček **ocr** (tenký wrapper kolem Tesseract). Pokud dáváte přednost jinému backendu, koncepty zůstávají stejné.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Tip:** Na Linuxu budete také potřebovat binární soubor Tesseract: `sudo apt-get install tesseract-ocr`. Uživatelé macOS si jej mohou stáhnout přes Homebrew: `brew install tesseract`.

### Krok 2 – Inicializace OCR enginu a nastavení jazyka

Nyní spustíme engine a řekneme mu, aby hledal anglické znaky. Můžete nahradit `ocr.Language.English` libovolným podporovaným kódem jazyka.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Proč je to důležité:** Specifikace jazyka výrazně zvyšuje přesnost, protože engine může použít jazykově specifické slovníky a modely znaků.

### Krok 3 – Načtení stránky PDF jako obrázku

OCR funguje na rastrových obrázcích, ne na PDF objektech. Pomocná funkce `ocr.Image.from_pdf` vykreslí vybranou stránku do bitmapy. Pro jiné stránky upravte `page_number` (indexování od 0).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Hraniční případ:** Pokud PDF obsahuje vektorovou grafiku místo naskenovaných obrázků, můžete získat ostré vykreslení. Pro skeny s nízkým rozlišením zvažte zvýšení DPI: `ocr.Image.from_pdf(..., dpi=300)`.

### Krok 4 – Rozpoznání textu z vykresleného obrázku

Zde je jádro **ocr python příkladu**. Engine zpracuje bitmapu a vrátí objekt obsahující extrahovaný řetězec.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

Atribut `ocr_result.text` obsahuje výstup plain‑textu, kde je to možné zachovává konce řádků.

### Krok 5 – Vytisknout nebo uložit extrahovaný text

Nakonec výsledek vypíšeme. Ve skutečné aplikaci byste pravděpodobně zapisovali do souboru nebo databáze.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

Spuštění skriptu by mělo zobrazit něco jako:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

To je kompletní workflow **extrahování textu z pdf** pomocí OCR.

---

## ## Rozpoznat text z obrázku – vyladění přesnosti

Pokud vás zajímá jen **rozpoznat text z obrázku** (např. JPEG účtenky), můžete krok konverze PDF přeskočit:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Tipy pro lepší výsledky:**

- **Předzpracovat** obrázek: převést na odstíny šedi, aplikovat prahování nebo deskew. Pillow to usnadňuje.
- **Zvýšit DPI** během vykreslování PDF: vyšší rozlišení poskytuje OCR engine více detailů.
- **Povolit konfiguraci OCR enginu** pro segmentaci stránek (`ocr_engine.config = "--psm 6"` pro jednotné bloky).

## ## Číst PDF s OCR – zpracování více stránek

Většina smluv má několik stránek. Procházet každou stránku je jednoduché:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

Tato funkce **čte PDF s OCR**, spojuje výstup a vkládá jasný marker pro zalomení stránky. Pak můžete `full_text` předat do vyhledávacího indexu nebo uložit jako soubor `.txt`.

## ## Běžná úskalí a jak je opravit

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Zkreslené znaky, spousta `?` | Špatný jazyk nebo chybějící soubory jazykových dat | Nainstalujte správný jazykový balíček Tesseract (`tesseract-ocr-<lang>`) a nastavte `ocr_engine.language`. |
| Chybějící řádky nebo oříznutá slova | Nízké DPI (méně než 150) | Vykreslete PDF při 300 DPI nebo vyšším (`dpi=300`). |
| Text je otočený nebo vzhůru nohama | Naskenovaná stránka není orientována | Použijte `ocr.Image.deskew(page_image)` před rozpoznáním. |
| Pomalejší zpracování velkých PDF | Zpracování stránek sekvenčně v jednom vlákně | Paralelizujte pomocí `concurrent.futures.ThreadPoolExecutor`. |

## ## Rozšíření OCR Python příkladu

- **Export do PDF/A**: Po extrakci můžete vložit text zpět do prohledávatelného PDF pomocí `reportlab` nebo `pypdf2`.
- **Detekce jazyka**: Použijte `langdetect` na výstup OCR pro dynamické přepínání `ocr_engine.language`.
- **Dávkové zpracování**: Procházejte adresář pomocí `os.listdir` a aplikujte `extract_all_pages` na každý soubor.

## ## Očekávaný výstup a ověření

Když spustíte skript na čistém skenu v angličtině, měli byste vidět čistý blok textu s správnou interpunkcí. Ověřte tím, že:

1. Porovnáte několik řádků s originálním naskenovaným obrázkem.  
2. Spustíte jednoduchý počet slov (`len(ocr_result.text.split())`), abyste se ujistili, že výstup není prázdný.  
3. Volitelně předáte výsledek do kontrolora pravopisu jako `pyspellchecker`, abyste odhalili OCR chyby.

## Závěr

Probrali jsme **jak extrahovat PDF** obsah, když tradiční parsování selže, ukázali kompletní **ocr python příklad** a vysvětlili, jak **rozpoznat text z obrázku** a **číst PDF s OCR** pro jednostránkové i více‑stránkové scénáře. S výše uvedenými úryvky kódu můžete nyní převést jakýkoli naskenovaný PDF do prohledávatelného, editovatelného textu—už žádné ruční přepisování.

Další kroky? Zkuste změnit jazyk na španělštinu (`ocr.Language.Spanish`) nebo experimentujte s technikami předzpracování obrázků pro zvýšení přesnosti. Pokud budujete systém pro správu dokumentů, zvažte indexování extrahovaného textu pomocí Elasticsearch pro bleskově rychlé vyhledávání.

Máte otázky nebo narazíte na podivný PDF? Zanechte komentář a šťastné programování!  

![How to extract PDF using OCR in Python](image.png "How to extract PDF using OCR in Python")

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Extrahovat text z obrázku pomocí Aspose OCR – krok za krokem průvodce](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Rozpoznat text PDF – OCR operace s Aspose.OCR pro Java](/ocr/english/java/ocr-operations/)
- [Extrahovat text z obrázku v C# s výběrem jazyka pomocí Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}