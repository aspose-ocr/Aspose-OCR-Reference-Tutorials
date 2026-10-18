---
category: general
date: 2026-06-06
description: Jak pomocí Pythonu provést OCR PDF, extrahovat text z PDF, převést text
  naskenovaného PDF a změnit jazyk OCR během několika řádků kódu.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: cs
og_description: 'Jak provést OCR PDF pomocí Pythonu: praktický průvodce, který vám
  ukáže, jak extrahovat text z PDF, převést text naskenovaného PDF a snadno změnit
  jazyk OCR.'
og_title: Jak provést OCR PDF v Pythonu – Kompletní programovací tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Jak provést OCR PDF v Pythonu – Kompletní krok za krokem průvodce
url: /cs/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR PDF v Pythonu – Kompletní krok‑za‑krokem průvodce

Už jste se někdy zamýšleli, **jak provést OCR PDF** soubory, aniž byste museli platit za drahé SaaS nástroje? Nejste v tom sami. Ať už digitalizujete staré knihy, získáváte data z faktur, nebo jen potřebujete prohledávat text ze skenovaného výkazu, zvládnutí OCR PDF v Pythonu vám může ušetřit hodiny ručního přepisování.

V tomto tutoriálu projdeme stručný, funkční příklad, který **extrahuje text z PDF**, ukáže vám, jak **převést text skenovaného PDF** na editovatelné řetězce, a dokonce demonstruje, jak **změnit jazyk OCR**, pokud váš dokument není v angličtině. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do libovolného projektu.

## Požadavky a nastavení

Než se pustíme do kódu, ujistěte se, že máte:

- Python 3.8+ nainstalovaný (kód funguje na 3.9, 3.10 a novějších)
- Balíček `ocr`, který poskytuje třídu `OcrEngine` (nainstalujete ho pomocí `pip install ocr-lib` – nahraďte skutečným názvem balíčku, který používáte)
- PDF soubor, který chcete zpracovat; pro ukázku použijeme `high_res_book.pdf` umístěný ve složce `YOUR_DIRECTORY`

Pokud používáte virtuální prostředí (vřele doporučeno), aktivujte ho nejprve:

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **Tip:** Ukládejte své PDF soubory do vyhrazené složky `data/`, abyste se později vyhnuli problémům s cestami.

## Krok 1: Vytvoření instance OCR enginu (Jak provést OCR PDF – inicializace)

První věc, kterou musíte udělat, když chcete **provést OCR na PDF** souborech, je vytvořit instanci enginu. Přemýšlejte o enginu jako o mozku, který přečte každou stránku, interpretuje glyfy a vrátí vám čistý text.

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

Proč je to důležité: bez enginu nemáte žádný kontext pro nastavení jazyka, možnosti renderování ani zpracování PDF. Objekt `OcrEngine` obsahuje všechna výchozí nastavení a umožňuje je později upravit.

## Krok 2: Nastavení rozpoznávacího jazyka (Změna jazyka OCR)

Většina OCR knihoven má jako výchozí jazyk angličtinu, ale co když je váš dokument ve francouzštině, němčině nebo dokonce v japonštině? Změna jazyka je tak jednoduchá jako zavolat `set_recognition_language`. Tím splníte požadavek **změnit jazyk OCR** a zajistíte vyšší přesnost.

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **Proč to můžete potřebovat:** Vícejazyčný archiv často obsahuje stránky v různých jazycích. Přepínání jazyků za běhu zabraňuje nesprávnému rozpoznání znaků jako “ß” nebo “ñ”.

## Krok 3: Konfigurace možností renderování PDF (Efektivní převod skenovaného PDF na text)

Při práci se skenovanými PDF má rozlišení a barevný režim zásadní vliv na kvalitu OCR. Renderování při 300 DPI v odstínech šedi je optimální pro většinu dokumentů – dostatečně detailní, ale zároveň šetří paměť.

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

Řetězené volání může vypadat sofistikovaně, ale jde jen o fluent API, které pokaždé vrací stejný objekt možností. Pokud potřebujete barvu (např. pro barevné diagramy), nahraďte `"grayscale"` za `"color"`.

## Krok 4: Rozpoznání PDF a získání textu z první stránky (Extrahování textu z PDF)

Nyní přichází jádro **jak provést OCR PDF**: předáte enginu cestu k souboru a získáte rozpoznaný text. Metoda vrací seznam výsledků po stránkách; každý výsledek obsahuje atribut `text`.

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

Pokud potřebujete celý dokument, projděte `results`:

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### Co když je PDF šifrované?

Některá PDF jsou chráněna heslem. V takovém případě můžete heslo předat metodě `recognize_pdf`:

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

Engine dešifruje za běhu před provedením OCR – žádné další kroky nejsou potřeba.

## Krok 5: Post‑zpracování extrahovaného textu (Doladění extrahovaného textu z PDF)

Surový výstup OCR často obsahuje zalomení řádků, nadbytečné mezery nebo občas špatně rozpoznané znaky. Rychlá čistící rutina připraví extrahovaný řetězec na další zpracování (indexování, ukládání do databáze atd.).

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

Nyní můžete bezpečně **extrahovat text z PDF** a předat ho libovolnému NLP pipeline, vyhledávači nebo jednoduché operaci `open(...).write()`.

## Bonus: Dávkové zpracování více PDF (Škálování OCR na PDF)

Pokud máte složku plnou skenovaných PDF, zabalte logiku do smyčky:

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

Tento úryvek ukazuje, jak **provést OCR na PDF** souborech hromadně, což je častá potřeba u digitalizačních projektů.

## Očekávaný výstup

Spuštění jednostránkového příkladu (Krok 4) by mělo vypsat něco jako:

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

Pokud jste zpracovali více‑stránkovou knihu, konzole zobrazí vyčištěný text každé stránky a dávkový skript vytvoří soubor `.txt` vedle každého PDF.

## Časté problémy a jak se jim vyhnout

| Problém | Příznaky | Řešení |
|---------|----------|--------|
| PDF s nízkým rozlišením | Zkreslené znaky, chybějící slova | Zvyšte DPI (`set_dpi(400)` nebo vyšší) |
| Špatně nastavený jazyk | Mnoho neznámých symbolů, zejména s diakritikou | Použijte `engine.set_recognition_language(ocr.Language.FRENCH)` nebo příslušný enum |
| Velké PDF způsobuje chybu paměti | `MemoryError` nebo pád po několika stránkách | Zpracovávejte stránky po částech (`engine.recognize_pdf(..., max_pages=10)`) |
| Chybějící fonty v PDF | Prázdný výstup u některých stránek | Ujistěte se, že PDF skutečně obsahuje rastrové obrázky; některá PDF jsou jen vektorová a vyžadují jiný přístup |

## Ilustrace

Níže je rychlá vizualizace pracovního postupu. Alt text je úmyslně SEO‑přátelský.

![diagram pracovního postupu OCR PDF ukazující inicializaci enginu, nastavení jazyka, možnosti renderování, rozpoznání a extrakci textu](/images/ocr-workflow.png)

*Diagram není nutný pro spuštění kódu, ale pomáhá vizuálním typům pochopit, kde se který krok nachází.*

## Závěr

Probrali jsme **jak provést OCR PDF** soubory v Pythonu od začátku do konce: vytvoření OCR enginu, **změnu jazyka OCR**, nastavení renderování pro **převod skenovaného PDF na text** a nakonec **extrahování textu z PDF** pro další využití. Kompletní, spustitelný příklad je připraven k vložení do libovolného projektu a volitelný dávkový skript ukazuje, jak řešení škálovat.

Dále můžete zkusit:

- Přidat **provádění OCR na PDF** pro vícejazyčné archivy pomocí smyčky přes seznam jazyků.
- Integrovat extrahovaný text s Elasticsearch pro full‑textové vyhledávání.
- Použít OCR k vytvoření prohledávatelných PDF tím, že vložíte textovou vrstvu zpět do původního souboru (mnoho knihoven nabízí metodu `save_as_searchable_pdf`).

Nebojte se experimentovat, ladit nastavení DPI nebo přejít na jiný OCR backend. Základy zůstávají stejné a nyní máte solidní základ, na kterém můžete stavět.

Šťastné kódování a ať se vaše skenované dokumenty konečně stanou prohledávatelnými!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční kódové příklady s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}