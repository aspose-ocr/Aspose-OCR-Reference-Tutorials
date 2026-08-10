---
category: general
date: 2026-06-19
description: Vytvořte prohledávatelný PDF z obrázku pomocí Python OCR. Naučte se převádět
  OCR do PDF, extrahovat text z obrázku a rychle provádět OCR na obrázku.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: cs
og_description: Vytvořte prohledávatelný PDF z obrázku pomocí OCR v Pythonu. Tento
  průvodce ukazuje, jak převést OCR na PDF, extrahovat text z obrázku a provést OCR
  na obrázku.
og_title: Vytvořte prohledávatelný PDF v Pythonu – kompletní programovací průvodce
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: Vytvořte prohledávatelný PDF v Pythonu – kompletní krok‑za‑krokem průvodce
url: /cs/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF v Pythonu – Kompletní krok‑za‑krokem průvodce

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** ze skenovaného účtenky, ale nevedeli jste, kde začít? Nejste sami – mnoho vývojářů narazí na stejnou překážku, když poprvé zkusí převést obrázek textu na PDF, které můžete skutečně prohledávat.  

V tomto tutoriálu vás provedeme praktickým řešením, které vám umožní **provést OCR na obrázku**, převést výsledek OCR na **prohledávatelné PDF** a dokonce získat surový text, pokud ho potřebujete pro další zpracování. Žádné zbytečnosti, jen funkční příklad, který můžete dnes zkopírovat a vložit do svého projektu.

## Co se naučíte

- Jak nastavit lehký OCR engine v Pythonu  
- Přesné kroky k **převodu OCR na PDF** a uložení jako prohledávatelný dokument  
- Způsoby, jak **extrahovat text z obrázku** pro následnou analýzu  
- Tipy pro řešení běžných problémů, jako je orientace obrázku a velké soubory  
- Kompletní, spustitelný skript, který můžete přizpůsobit svému vlastnímu případu použití

### Požadavky

- Python 3.8+ nainstalovaný na vašem počítači  
- Základní znalost pip a virtuálních prostředí (volitelné, ale doporučené)  
- Obrázkový soubor (PNG, JPEG, atd.), který obsahuje jasný, strojově čitelný text  

Pokud je máte, pojďme na to.

## Krok 1: Instalace požadované knihovny

Ukázkový kód, který jste viděli dříve, používá fiktivní balíček `ocr`, ale stejné principy platí pro reálné knihovny jako **EasyOCR**, **pytesseract** nebo **pdfminer.six**. Pro tento průvodce použijeme **EasyOCR**, protože je čistě v Pythonu, podporuje mnoho jazyků a poskytuje užitečnou metodu pro převod do PDF pomocí pomocného nástroje.

```bash
pip install easyocr pillow
```

> **Tip:** Instalujte uvnitř virtuálního prostředí (`python -m venv venv && source venv/bin/activate`), aby byly vaše závislosti přehledné.

## Krok 2: Inicializace OCR engine – Provést OCR na obrázku

Jakmile je knihovna připravena, vytvoříme OCR engine a řekneme mu, aby pracoval s anglickým textem. Toto je první místo, kde **provádíme OCR na obrázku**.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

Proč potřebujeme dedikovaný objekt čtečky? EasyOCR přednačítá jazykové modely, takže opětovné použití stejného `reader` pro více obrázků je mnohem efektivnější než jeho opakovaná inicializace při každém použití.

## Krok 3: Načtení obrázku – Extrahovat text z obrázku

Načteme obrázek do paměti. Tento krok je místem, kde později **extrahujeme text z obrázku**, ale nejprve jej jen načteme.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

Pokud je váš obrázek vzhůru nohama nebo nakřivo, zvažte použití metod `rotate` nebo `transpose` z Pillow před předáním OCR engine. Rychlá vizuální kontrola vám může později ušetřit hodiny ladění.

## Krok 4: Spuštění OCR engine a zachycení výsledků

Zde je jádro procesu – odeslání obrázku do OCR engine a získání strukturovaných dat.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

Příznak `detail=1` nám poskytuje ohraničující rámečky, které budeme později potřebovat při **převodu OCR na PDF**. Pokud vás zajímají jen surové řetězce, nastavte `detail=0`.

## Krok 5: Převod výsledku OCR na prohledávatelné PDF – Převod OCR na PDF

EasyOCR neposkytuje přímý PDF zapisovač, ale můžeme PDF sestavit sami pomocí Pillow a knihovny `reportlab`. Aby byl tutoriál lehký, použijeme `fpdf2`, který nám umožní vložit původní obrázek a překrýt jej neviditelným textem.

```bash
pip install fpdf2
```

```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

Co se právě stalo? Umístili jsme naskenovaný obrázek jako viditelnou vrstvu a poté jsme na něj napsali rozpoznaná slova pomocí bílého textu, který se slévá s bílým pozadím. Vyhledávací nástroje stále čtou skrytou vrstvu, takže PDF se stane **prohledávatelným** bez změny vizuálního vzhledu.

## Krok 6: Uložení PDF bajtů – Převod obrázku na PDF

Pokud dáváte přednost práci s PDF v paměti (např. odesílání přes API), můžete zachytit bajty místo přímého zápisu na disk.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

Tento řádek ukazuje klasický workflow **převodu obrázku na PDF**: začnete obrázkem, spustíte OCR, překryjete text a nakonec vytvoříte PDF stream.

## Krok 7: Ověření výsledku – Rychlé kontroly

Po spuštění skriptu otevřete `receipt_searchable.pdf` v libovolném PDF prohlížeči a vyzkoušejte vyhledávací pole (Ctrl + F). Zadejte slovo, o kterém víte, že se v účtence vyskytuje – pokud skočí na správné místo, úspěšně jste **vytvořili prohledávatelné PDF**!  

Pokud vyhledávání selže, zkontrolujte:

1. Skóre důvěryhodnosti OCR (`conf` hodnoty). Nízká důvěra může znamenat, že je obrázek rozmazaný.  
2. Souřadnice ohraničujících rámečků – někdy EasyOCR hlásí jiné orientace.  
3. Že PDF prohlížeč není nastaven do režimu „pouze obrázek“ (vzácné, ale některé prohlížeče tuto možnost mají).

## Kompletní funkční skript

Spojením všeho dohromady, zde je kompletní, připravený ke spuštění Python soubor:

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

Uložte to jako `searchable_pdf.py`, nahraďte zástupné řetězce `YOUR_DIRECTORY` skutečnými cestami a spusťte:

```bash
python searchable_pdf.py
```

Měli byste vidět potvrzovací zprávu a zcela nové prohledávatelné PDF ve vaší složce.

## Časté otázky a okrajové případy

**Co když je obrázek barevný?**  
EasyOCR funguje jak s odstíny šedi, tak s barevnými obrázky, ale převod na odstíny šedi (`pil_image.convert("L")`) může někdy zlepšit přesnost u špinavých skenů.

**Mohu zpracovávat vícestránkové PDF?**  
Ano – projděte každým obrázkem stránky, spusťte kroky OCR a přidejte každou stránku do stejného objektu `FPDF`. Jen nezapomeňte resetovat kurzor (`self.add_page()`) pro každý nový obrázek.

**Existuje způsob, jak zachovat původní textovou vrstvu místo neviditelného bílého textu?**  
Pokud potřebujete skutečné PDF „text‑pod‑obrázkem“ (např. pro přístupnost), zvažte použití `pdfminer` nebo `pikepdf` k vložení skryté textové vrstvy s odpovídajícími PDF tagy. Je to pokročilejší, ale princip zůstává stejný: obrázek na pozadí + překrytý text.

**Co když je důvěra OCR nízká?**  
Můžete filtrovat slova s nízkou důvěrou:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## Závěr – Co jsme dosáhli

Začali jsme s jednoduchým obrázkem účtenky, **provedli OCR na obrázku**, extrahovali rozpoznané řetězce a nakonec **vytvořili prohledávatelné PDF**, které se chová jako jakýkoli profesionálně skenovaný dokument. Proces pokryl všechna sekundární klíčová slova – **convert OCR to PDF**, **extract text from image**, **convert image to PDF** a **perform OCR on image** – takže nyní máte znovupoužitelnou sadu nástrojů pro jakýkoli podobný projekt.

### Další kroky

- Experimentujte s dalšími jazyky předáním jejich ISO kódů do `easyocr.Reader(['en', 'es'])`.  
- Vyměňte EasyOCR za Tesseract, pokud potřebujete plně offline řešení; zbytek pipeline zůstává stejný.  
- Přidejte vizualizaci důvěry OCR (nakreslete ohraničující rámečky na obrázek) pro ladění problematických skenů.  

Máte nápad, který byste chtěli sdílet? Zanechte komentář, fork


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Extrahovat text z obrázku pomocí Aspose OCR – Krok‑za‑krokem průvodce](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Převod obrázků na PDF C# – Uložit vícestránkový OCR výsledek](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Jak OCR obrázek – Provést OCR na obrázku v OCR rozpoznávání obrázků](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}