---
category: general
date: 2026-07-05
description: Utwórz przeszukiwalny PDF przy użyciu Pythona. Dowiedz się, jak wykonać
  OCR zeskanowanego PNG, przekonwertować zeskanowany PDF jako obraz i uzyskać przeszukiwalny
  PDF w kilka minut.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: pl
og_description: Szybko twórz przeszukiwalne PDF. Ten przewodnik pokazuje, jak wykonać
  OCR obrazu PNG, przekonwertować zeskanowany PDF i stworzyć przeszukiwalny PDF przy
  użyciu Pythona.
og_title: Utwórz przeszukiwalny PDF ze zeskanowanego obrazu – samouczek OCR w Pythonie
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: Tworzenie przeszukiwalnego PDF z zeskanowanego obrazu – Kompletny przewodnik
  OCR w Pythonie
url: /pl/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz przeszukiwalny PDF ze zeskanowanego obrazu – Pełny przewodnik OCR w Pythonie

Zastanawiałeś się kiedyś, jak **utworzyć przeszukiwalny PDF** ze zeskanowanego obrazu, nie płacąc za drogie oprogramowanie? Nie jesteś sam. W wielu biurach PDF‑y przychodzą jako płaskie obrazy — trudne do przeszukania, niemożliwe do kopiowania i wklejania, a także koszmar dla audytów zgodności. Dobra wiadomość? Kilka linijek Pythona pozwoli zamienić ten statyczny PNG w w pełni przeszukiwalny PDF, a proces jest prostszy niż się wydaje.

W tym samouczku przeprowadzimy Cię przez kompletny **przykład rozpoznawania OCR**, obejmujący wszystko od instalacji odpowiedniej biblioteki po zapisanie finalnego pliku PDF. Po zakończeniu dokładnie będziesz wiedział, jak **konwertować zeskanowane obrazy PDF**, jak **programowo wykonywać OCR na PDF** i będziesz miał wielokrotnego użytku skrypt, który możesz wstawić do dowolnego projektu.

## Czego się nauczysz

- Zainstaluj i skonfiguruj bibliotekę OCR w Pythonie (użyjemy `pytesseract` i `pdf2image`).
- Zainicjalizuj silnik OCR i ustaw język.
- Wczytaj zeskanowany PNG (lub dowolny obraz) i uruchom na nim OCR.
- Przekształć wynik OCR w **przeszukiwalny PDF** (tablica bajtów) i zapisz go.
- Wskazówki dotyczące obsługi dokumentów wielostronicowych, różnych języków i typowych pułapek.

Wcześniejsze doświadczenie z OCR nie jest wymagane — wystarczy działające środowisko Python 3 i odrobina ciekawości.

---

## Tworzenie przeszukiwalnego PDF — przegląd

Below is a high‑level flowchart of the steps we’ll implement.  

![Diagram przepływu tworzenia przeszukiwalnego PDF](https://example.com/flowchart.png "Diagram przepływu tworzenia przeszukiwalnego PDF")

*Tekst alternatywny: Diagram przepływu tworzenia przeszukiwalnego PDF pokazujący inicjalizację silnika, wczytywanie obrazu, rozpoznawanie OCR, konwersję do PDF i zapis pliku.*

---

## Krok 1: Inicjalizacja silnika OCR (jak zrobić OCR PDF)

Po co w ogóle coś inicjalizować? Silnik OCR jest mózgiem, który interpretuje wzorce pikseli jako znaki. Tworząc instancję silnika i wyraźnie ustawiając język, informujemy bibliotekę, jakiego alfabetu się spodziewać, co znacząco zwiększa dokładność.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Wskazówka:** Jeśli potrzebujesz wykonywać OCR dokumentów w wielu językach, zainstaluj odpowiednie pakiety językowe dla Tesseract i przekaż listę taką jak `"eng+spa"` do `ocr_language`.

---

## Krok 2: Wczytanie zeskanowanego obrazu (convert scanned image pdf)

Następnym elementem układanki jest wprowadzenie danych obrazu do Pythona. Niezależnie od tego, czy masz pojedynczy PNG, czy wielostronicowy TIFF, klasa `PIL.Image` potrafi go otworzyć. Jeśli zaczynasz od PDF, który już zawiera zeskanowane obrazy, `pdf2image` przetworzy każdą stronę na obraz.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Dlaczego to ważne:** Wczytanie obrazu jako obiektu Pillow daje dostęp do surowych danych pikseli, których potrzebuje silnik OCR. Pominięcie tego kroku i podanie surowych bajtów bezpośrednio spowodowałoby błędy.

---

## Krok 3: Wykonanie rozpoznawania OCR na obrazie (ocr recognition example)

Teraz najciekawsza część — pozwolenie silnikowi na odczytanie tekstu. `pytesseract.image_to_pdf_or_hocr` zwraca strumień bajtów PDF, który już zawiera niewidzialną warstwę tekstową, co jest dokładnie tym, czego potrzebujemy do **przeszukiwalnego PDF**.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Przypadek szczególny:** Jeśli Twój obraz ma niską kontrastowość, rozważ zastosowanie prostego progowania przed OCR:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

Ten niewielki krok przetwarzania wstępnego może znacząco zwiększyć dokładność.

---

## Krok 4: Zapisanie bajtów PDF do pliku (convert png searchable pdf)

Biblioteka OCR przekazuje nam tablicę bajtów — można ją traktować jako surową zawartość pliku PDF. Wszystko, co musimy teraz zrobić, to zapisać te bajty na dysku.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**Co zobaczysz:** Otwórz powstały plik w dowolnym przeglądarce PDF i spróbuj wyszukać słowo, które wiesz, że występuje w oryginalnym obrazie. Podświetlenie powinno przenieść Cię bezpośrednio do miejsca, co potwierdza działanie niewidzialnej warstwy tekstowej.

---

## Krok 5: Rozszerzenie na dokumenty wielostronicowe (convert scanned image pdf)

Rzeczywiste umowy często obejmują wiele stron. Aby **konwertować zeskanowane obrazy PDF** zawierające kilka stron, przeiteruj każdą stronę, wykonaj OCR i połącz powstałe pliki PDF.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Dlaczego scalać?** Każde wywołanie `image_to_pdf_or_hocr` generuje samodzielny PDF. Scalanie ich zapewnia, że finalny dokument zachowuje pierwotną kolejność stron.

---

## Typowe problemy i jak je naprawić

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Brak możliwości wyszukiwania tekstu po otwarciu PDF | Tesseract nie znajduje żadnych znaków (pusty wynik) | Sprawdź jakość obrazu, zwiększ DPI lub zastosuj przetwarzanie wstępne (kontrast, binaryzacja). |
| Zniekształcone znaki (np. �) | Nieprawidłowy pakiet językowy lub brak czcionek | Zainstaluj właściwe dane językowe (`tesseract‑lang‑eng`) i upewnij się, że `ocr_language` jest zgodny. |
| Rozmiar pliku PDF ogromny (>10 MB dla jednostronicowego obrazu) | Używanie bezstratnego PNG jako źródła; OCR dodaje obraz w pełnej rozdzielczości | Zmniejsz rozmiar obrazu przed OCR (`image.thumbnail((1240, 1754))` dla A4). |
| Skrypt awaryjnie kończy działanie w Windows z komunikatem „tesseract.exe not found” | Plik binarny Tesseract nie znajduje się w PATH | Dodaj `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` (dostosuj ścieżkę). |

---

## Pełny, gotowy do uruchomienia skrypt

Łącząc wszystko razem, oto pojedynczy plik, który możesz skopiować‑wkleić i uruchomić:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

Zapisz to jako `create_searchable_pdf.py`, zamień symbole zastępcze na rzeczywiste ścieżki i uruchom:

```bash
python create_searchable_pdf.py
```

You should see a

## Co powinieneś się nauczyć dalej?

Następujące samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak wykonać OCR PDF w .NET przy użyciu Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Konwertowanie obrazów do PDF w C# – zapis wyniku OCR wielostronicowego](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Rozpoznawanie dokumentów PDF w Aspose.OCR dla Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}