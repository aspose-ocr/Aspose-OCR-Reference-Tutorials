---
category: general
date: 2026-04-29
description: Wyodrębnij tekst z PDF przy użyciu Aspose OCR w Pythonie. Dowiedz się,
  jak przetwarzać PDF w trybie wsadowym OCR, konwertować tekst zeskanowanego PDF oraz
  obsługiwać strony o niskim poziomie pewności.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: pl
og_description: Wyodrębnij tekst z PDF przy użyciu Aspose OCR w Pythonie. Ten przewodnik
  pokazuje przetwarzanie PDF w trybie wsadowym OCR, konwertowanie zeskanowanego tekstu
  PDF oraz obsługę wyników o niskim poziomie pewności.
og_title: Wyodrębnij tekst z PDF – OCR PDF w Pythonie
tags:
- OCR
- Python
- PDF processing
title: Wyodrębnij tekst z PDF – OCR PDF w Pythonie
url: /pl/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z PDF – OCR PDF w Pythonie

Kiedykolwiek potrzebowałeś **wyodrębnić tekst z PDF**, a plik był jedynie zeskanowanym obrazem? Nie jesteś sam — wielu programistów napotyka ten problem, próbując przekształcić PDF‑y w dane przeszukiwalne. Dobra wiadomość? Dzięki Aspose OCR for Python możesz konwertować zeskanowany tekst PDF w kilku linijkach kodu, a nawet uruchomić **przetwarzanie wsadowe OCR PDF**, gdy masz dziesiątki plików do obsłużenia.

W tym tutorialu przejdziemy przez cały proces: skonfigurujemy bibliotekę, uruchomimy OCR na pojedynczym PDF, skalujemy do trybu wsadowego i zajmiemy się stronami o niskim poziomie pewności, abyś wiedział, kiedy wymagana jest ręczna weryfikacja. Po zakończeniu będziesz mieć gotowy skrypt, który wyodrębnia tekst z dowolnego zeskanowanego PDF, oraz zrozumiesz, dlaczego wykonujemy poszczególne kroki.

## Co będzie potrzebne

Zanim zaczniemy, upewnij się, że masz:

- Python 3.8 lub nowszy (kod używa f‑stringów, więc 3.6+ działa, ale zalecane jest 3.8+)
- Licencję Aspose OCR for Python lub klucz darmowej wersji próbnej (można go pobrać ze strony Aspose)
- Folder z jednym lub większą liczbą zeskanowanych PDF‑ów, które chcesz przetworzyć
- Umiarkowaną ilość miejsca na dysku na generowane raporty *.txt*

To wszystko — bez ciężkich zewnętrznych zależności, bez akrobacji OpenCV. Silnik Aspose OCR wykona ciężką pracę za Ciebie.

## Konfiguracja środowiska

Najpierw zainstaluj pakiet Aspose OCR z PyPI:

```bash
pip install aspose-ocr
```

Jeśli masz plik licencyjny (`Aspose.OCR.lic`), umieść go w katalogu głównym projektu i aktywuj w następujący sposób:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Pro tip:** Trzymaj plik licencji poza systemem kontroli wersji; dodaj go do `.gitignore`, aby uniknąć przypadkowego ujawnienia.

## Przeprowadzanie OCR na pojedynczym PDF

Teraz wyodrębnijmy tekst z jednego zeskanowanego PDF. Główne kroki to:

1. Utwórz instancję `OcrEngine`.
2. Wskaż plik PDF.
3. Pobierz `OcrResult` dla każdej strony.
4. Zapisz wynikowy tekst do pliku.
5. Zwolnij zasoby natywne, wywołując `dispose`.

Oto pełny, gotowy do uruchomienia skrypt:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**Co zobaczysz:** Dla każdej strony skrypt wypisze coś w stylu `Page 1: confidence 97.45%`. Jeśli strona spadnie poniżej progu 80 %, pojawi się ostrzeżenie, informujące, że OCR mógł pominąć znaki.

### Dlaczego to działa

- **`OcrEngine`** to brama do natywnej biblioteki Aspose OCR; obsługuje wszystko, od wstępnego przetwarzania obrazu po rozpoznawanie znaków.
- **`extract_from_pdf`** automatycznie rasteryzuje każdą stronę PDF, więc nie musisz samodzielnie konwertować PDF‑ów na obrazy.
- **Wyniki pewności** pozwalają automatyzować kontrole jakości — co jest kluczowe przy przetwarzaniu dokumentów prawnych lub medycznych, gdzie dokładność ma znaczenie.

## Przetwarzanie wsadowe OCR PDF w Pythonie

Większość projektów w praktyce obejmuje więcej niż jeden plik. Rozszerzmy skrypt jednoplikowy do **przetwarzania wsadowego OCR PDF**, które przeszukuje katalog, przetwarza każdy PDF i zapisuje wyniki w odpowiadającym podkatalogu.

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### Jak to pomaga

- **Skalowalność:** Funkcja przeszukuje folder raz, tworząc dedykowany podkatalog wyjściowy dla każdego PDF. Dzięki temu porządek pozostaje zachowany, nawet przy dziesiątkach dokumentów.
- **Wielokrotne użycie:** `ocr_pdf_file` może być wywoływana z innych skryptów (np. usługi webowej), ponieważ jest czystą funkcją.
- **Obsługa błędów:** Skrypt wypisuje przyjazny komunikat, jeśli folder wejściowy jest pusty, co zapobiega cichej awarii.

## Konwersja tekstu ze zeskanowanego PDF — obsługa przypadków brzegowych

Choć powyższy kod działa dla większości PDF‑ów, możesz napotkać kilka specyficznych sytuacji:

| Sytuacja | Dlaczego się pojawia | Jak złagodzić |
|----------|----------------------|---------------|
| **Zaszyfrowane PDF‑y** | PDF jest zabezpieczony hasłem. | Przekaż hasło do `extract_from_pdf(pdf_path, password="yourPwd")`. |
| **Dokumenty wielojęzyczne** | Aspose OCR domyślnie używa języka angielskiego. | Ustaw `ocr_engine.language = "spa"` dla hiszpańskiego lub podaj listę języków dla mieszanych dokumentów. |
| **Bardzo duże PDF‑y (>500 stron)** | Zużycie pamięci rośnie, ponieważ każda strona jest ładowana do RAM. | Przetwarzaj PDF w partiach używając `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` i iteruj. |
| **Słaba jakość skanu** | Niska rozdzielczość DPI lub duży szum obniża pewność. | Włącz wstępne przetwarzanie obrazu `engine.image_preprocessing = True` lub zwiększ DPI poprzez `engine.dpi = 300`. |

> **Uwaga:** Włączenie wstępnego przetwarzania obrazu może zauważalnie wydłużyć czas CPU. Jeśli uruchamiasz nocny batch, zaplanuj wystarczająco dużo czasu lub uruchom osobny worker.

## Weryfikacja wyników

Po zakończeniu skryptu znajdziesz strukturę katalogów podobną do tej:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

Otwórz dowolny plik `.txt`; powinieneś zobaczyć czysty, zakodowany w UTF‑8 tekst odzwierciedlający oryginalną zeskanowaną treść. Jeśli zauważysz nieczytelne znaki, sprawdź ustawienia języka PDF oraz upewnij się, że na maszynie zainstalowane są odpowiednie pakiety czcionek.

## Czyszczenie zasobów

Aspose OCR korzysta z natywnych DLL‑ów, dlatego ważne jest wywołanie `engine.dispose()` po zakończeniu pracy. Zapomnienie tego kroku może prowadzić do wycieków pamięci, szczególnie w długotrwale działających zadaniach wsadowych.

```python
# Always the last line of your script
engine.dispose()
```

## Pełny przykład od początku do końca

Łącząc wszystkie elementy, oto kompletny skrypt:

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}