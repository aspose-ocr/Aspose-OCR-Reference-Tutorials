---
category: general
date: 2026-06-25
description: Wykonaj OCR na PDF przy użyciu Pythona — dowiedz się, jak załadować PDF
  do OCR, wyodrębnić tekst z stron PDF i efektywnie podglądać rozpoznany tekst.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: pl
og_description: Wykonaj OCR na PDF w Pythonie. Ten przewodnik pokazuje, jak załadować
  PDF do OCR, wyodrębnić tekst z stron PDF i szybko podglądnąć rozpoznany tekst.
og_title: Wykonaj OCR na PDF przy użyciu Pythona – Samouczek krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Przeprowadź OCR na PDF za pomocą Pythona – Kompletny przewodnik
url: /pl/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wykonaj OCR na PDF za pomocą Pythona – Kompletny przewodnik

Czy kiedykolwiek potrzebowałeś **wykonać OCR na PDF** files but weren’t sure where to start? Maybe you’ve got a mountain of scanned contracts, or a single hefty handbook that refuses to cooperate with your usual text‑extractor. In short, you want to **load PDF for OCR**, pull the text out, and get a quick preview—all without blowing out your machine’s memory.

Cóż, jesteś we właściwym miejscu. W tym samouczku przeprowadzimy cię przez w pełni funkcjonalny skrypt w Pythonie, który **extracts text from PDF pages**, pokaże ci, jak **preview recognized text**, a także rozwiąże klasyczny problem **how to OCR large PDF** files efficiently.

Po zakończeniu będziesz mieć gotowy do uruchomienia program, jasne zrozumienie każdego ustawienia konfiguracyjnego oraz garść wskazówek, jak uniknąć typowych pułapek, które potykają nowicjuszy.

---

## Czego się nauczysz

- Jak **load PDF for OCR** przy użyciu biblioteki `aocr`.
- Dokładne kroki, aby **perform OCR on PDF** pages one‑by‑one.
- Sposoby na **extract text from PDF pages** przy zachowaniu kontrolowanego zużycia pamięci.
- Jak **preview recognized text** w celu sprawdzenia wyników.
- Strategie radzenia sobie z **large PDFs** bez wyczerpywania RAM.

> **Wskazówka:** Ten przewodnik zakłada, że masz zainstalowany Python 3.9+ oraz podstawową znajomość środowisk wirtualnych. Jeśli jesteś nowy w Pythonie, najpierw skonfiguruj virtualenv — uwierz mi, zaoszczędzi to późniejsze problemy.

---

## Wymagania wstępne

| Requirement | Why it matters |
|-------------|----------------|
| `aocr` Python package (or any compatible OCR engine) | Udostępnia klasę `OcrEngine` używaną w całym skrypcie. |
| `pip` and a virtual environment | Utrzymuje zależności odizolowane od systemowego Pythona. |
| Sufficient disk space for temporary image extracts | Niektóre silniki OCR zapisują obrazy stron na dysk przed przetworzeniem. |
| Optional: `tqdm` for progress bars | Poprawia UX przy pracy z zadaniami **how to OCR large PDF**. |

Zainstaluj niezbędne elementy za pomocą:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

Jeśli twój PDF jest zabezpieczony hasłem, będziesz musiał podać hasło później — zobacz sekcję „Edge Cases”.

---

## Krok 1: Perform OCR on PDF – Konfiguracja silnika

Na początek potrzebujemy instancji silnika OCR. Traktuj go jak mózg, który odczyta obraz każdej strony i zwróci czysty tekst.

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **Dlaczego ustawia się `max_memory_mb`?**  
> Silniki OCR często buforują obrazy stron w RAM. Ograniczając pamięć, zapobiegasz awarii skryptu przy 500‑stronnym kontrakcie.

---

## Krok 2: Load PDF for OCR i konfiguracja ustawień

Teraz faktycznie **load PDF for OCR**. Ścieżka może być bezwzględna lub względna; po prostu upewnij się, że plik istnieje.

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

Jeśli PDF jest zaszyfrowany, `engine.load_pdf` zazwyczaj zgłosi wyjątek. W takim przypadku możesz wywołać `engine.load_pdf(pdf_path, password="secret")` — więcej na ten temat później.

---

## Krok 3: Extract Text from PDF Pages – Główna pętla

Tutaj **perform OCR on PDF** strona po stronie. Dodatkowo **preview recognized text** dla pierwszych kilku setek znaków, abyś mógł zweryfikować, że wszystko działa.

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **Pro tip:** Pasek postępu `tqdm` daje wizualną wskazówkę, szczególnie przydatną przy pracy z dokumentami **how to OCR large PDF**, które zajmują kilka minut.

---

## Krok 4: Łączenie wszystkiego – gotowy do uruchomienia skrypt

Poniżej znajduje się pełny, gotowy do uruchomienia przykład. Zapisz go jako `pdf_ocr.py` i uruchom poleceniem `python pdf_ocr.py path/to/your/file.pdf`.

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### Oczekiwany wynik (fragment)

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

Zobaczysz krótki podgląd dla każdej strony, a następnie ostateczne potwierdzenie, że połączony plik tekstowy został zapisany.

---

## Przypadki brzegowe i praktyczne wskazówki

| Situation | What to Do |
|-----------|------------|
| **Encrypted PDF** | Podaj hasło: `engine.load_pdf(pdf_path, password="mySecret")`. |
| **Very large PDF (> 1000 pages)** | Zwiększ `max_memory_mb` ostrożnie lub przetwarzaj w partiach (np. po 200 stron na raz). |
| **Mixed content (printed + handwritten)** | Zmień `engine.recognition_mode` na `aocr.RecognitionMode.MIXED`, jeśli biblioteka to obsługuje. |
| **Missing fonts or poor scan quality** | Wstępnie przetwórz strony przy użyciu biblioteki do ulepszania obrazu (np. Pillow) przed wywołaniem `recognize()`. |
| **Out‑of‑memory crashes** | Zmniejsz `preview_len` lub zapisuj tekst każdej strony bezpośrednio na dysk zamiast trzymać wszystko w liście. |

---

## Jak efektywnie OCR duże PDF – Zaawansowane strategie

Podczas rozwiązywania **how to OCR large PDF**, szybkość i stabilność stają się kluczowe. Oto kilka sztuczek, które możesz dodać do skryptu:

1. **Parallelize per page** – Użyj `concurrent.futures.ThreadPoolExecutor`, jeśli silnik OCR jest bezpieczny wątkowo.
2. **Cache intermediate images** – Niektóre silniki pozwalają przechowywać rastrowane strony na SSD, co znacząco zmniejsza obciążenie CPU przy ponownych uruchomieniach.
3. **Batch write output** – Zamiast dodawać do listy w Pythonie, otwórz plik wyjściowy raz i zapisuj tekst każdej strony od razu, gdy będzie gotowy.
4. **Adjust DPI** – Obniżenie DPI podczas rasteryzacji zmniejsza zużycie pamięci, ale może wpływać na dokładność; znajdź optymalny zakres (zwykle 200‑300 DPI).

Poniżej krótki fragment pokazujący, jak można zrównoleglić krok OCR (opcjonalnie, odkomentuj, aby użyć):

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

Pamiętaj: równoległość może zwiększyć użycie CPU, więc monitoruj temperaturę systemu podczas długich uruchomień.

---

## Najczęściej zadawane pytania

**Q: Czy mogę używać tego skryptu z innymi bibliotekami OCR, takimi jak Tesseract?**  
A: Absolutely. Replace the `aocr` calls with `pytesseract.image_to

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i zbadać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak wykonać OCR PDF w .NET z Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Jak wykonać ekstrakcję tekstu z obrazu ze strumienia przy użyciu Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Jak wyodrębnić tekst z obrazu z URL przy użyciu Aspose.OCR dla Javy](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}