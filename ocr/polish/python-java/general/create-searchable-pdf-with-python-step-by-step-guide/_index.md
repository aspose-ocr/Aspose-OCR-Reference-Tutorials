---
category: general
date: 2026-05-31
description: Utwórz przeszukiwalny PDF ze skanowanych obrazów przy użyciu OCR w Pythonie.
  Dowiedz się, jak konwertować PDF ze skanowanymi obrazami, konwertować TIFF na PDF
  i dodać warstwę tekstową OCR w kilka minut.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: pl
og_description: Twórz przeszukiwalne PDF natychmiast. Ten przewodnik pokazuje, jak
  uruchomić OCR, konwertować zeskanowane PDF‑y obrazu i dodać warstwę tekstu OCR za
  pomocą jednego skryptu Pythona.
og_title: Utwórz przeszukiwalny PDF w Pythonie – Kompletny poradnik
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Tworzenie przeszukiwalnego PDF za pomocą Pythona – Przewodnik krok po kroku
url: /pl/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz przeszukiwalny PDF w Pythonie – Przewodnik krok po kroku

Zastanawiałeś się kiedyś, jak **utworzyć przeszukiwalny PDF** ze zeskanowanej strony bez używania dziesiątek narzędzi? Nie jesteś sam. W wielu procesach biurowych zeskanowany plik TIFF lub JPEG trafia na współdzielony dysk, a kolejna osoba musi ręcznie kopiować‑wklejać tekst — bolesne, podatne na błędy i marnujące czas.  

W tym samouczku przeprowadzimy Cię przez czyste, programistyczne rozwiązanie, które pozwala **konwertować zeskanowany obraz PDF**, **konwertować TIFF do PDF** i **dodać warstwę tekstu OCR** w jednym kroku. Po zakończeniu będziesz mieć gotowy do użycia skrypt, który uruchamia OCR, osadza ukryty tekst i generuje przeszukiwalny PDF, który możesz indeksować, przeszukiwać lub udostępniać z pewnością.

## Czego będziesz potrzebować

- Python 3.9+ (dowolna aktualna wersja działa)
- `aspose-ocr` i `aspose-pdf` pakiety (instalowane za pomocą `pip install aspose-ocr aspose-pdf`)
- Zeskanowany plik obrazu (`.tif`, `.png`, `.jpg` lub nawet strona PDF będąca jedynie obrazem)
- Umiarkowana ilość RAM (silnik OCR jest lekki; nawet laptop sobie radzi)

> **Wskazówka:** Jeśli używasz systemu Windows, najłatwiejszy sposób na uzyskanie pakietów to uruchomienie polecenia w podniesionym oknie PowerShell.

```bash
pip install aspose-ocr aspose-pdf
```

Teraz, gdy wymagania wstępne są załatwione, zanurzmy się w kod.

## Krok 1: Utwórz instancję silnika OCR – *create searchable pdf*

Pierwszą rzeczą, którą robimy, jest uruchomienie silnika OCR. Traktuj go jak mózg, który odczyta każdy piksel i przekształci go w znaki.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **Dlaczego to ważne:** Inicjalizacja silnika tylko raz utrzymuje niskie zużycie pamięci. Gdybyś wywoływał `OcrEngine()` w pętli dla każdej strony, szybko wyczerpałbyś zasoby.

## Krok 2: Załaduj zeskanowany obraz – *convert tiff to pdf* & *convert scanned image pdf*

Następnie skieruj silnik na plik, który chcesz przetworzyć. API akceptuje dowolny obraz rastrowy, więc TIFF działa tak samo dobrze jak JPEG.

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

Jeśli masz PDF zawierający jedynie zeskanowany obraz, nadal możesz użyć `load_image`, ponieważ Aspose automatycznie wyodrębni pierwszą stronę.

## Krok 3: Przygotuj opcje zapisu PDF – *add OCR text layer*

Tutaj konfigurujemy, jak ma wyglądać końcowy PDF. Kluczową flagą jest `create_searchable_pdf`; ustawienie jej na `True` informuje bibliotekę, aby osadziła niewidoczną warstwę tekstu odzwierciedlającą zawartość wizualną.

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **Co robi warstwa tekstowa:** Gdy otworzysz powstały plik w Adobe Reader i spróbujesz zaznaczyć tekst, zobaczysz ukryte znaki. Wyszukiwarki również mogą je indeksować — idealne dla zgodności lub archiwizacji.

## Krok 4: Uruchom OCR i zapisz – *how to run OCR* w jednym wywołaniu

Teraz dzieje się magia. Jedno wywołanie metody uruchamia silnik rozpoznawania i zapisuje przeszukiwalny PDF na dysku.

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

Metoda `recognize` zwraca obiekt statusu, który możesz sprawdzić pod kątem błędów, ale w większości prostych scenariuszy wystarczy powyższe proste wywołanie.

### Oczekiwany wynik

Uruchomienie skryptu wypisuje:

```
PDF saved as searchable PDF.
```

Jeśli otworzysz `scanned_page_searchable.pdf`, zauważysz, że możesz zaznaczyć tekst, skopiować‑wkleić go i nawet wykonać wyszukiwanie `Ctrl+F`. To znak rozpoznawczy przepływu pracy **create searchable pdf**.

## Pełny działający skrypt

Poniżej znajduje się kompletny, gotowy do uruchomienia skrypt. Wystarczy zamienić ścieżki zastępcze na rzeczywiste lokalizacje plików.

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

Zapisz to jako `create_searchable_pdf.py` i uruchom:

```bash
python create_searchable_pdf.py
```

## Częste pytania i przypadki brzegowe

### 1️⃣ Czy mogę przetwarzać wielostronicowe PDFy?

Tak. Użyj `ocr_engine.load_image("file.pdf")`, a następnie iteruj po każdej stronie za pomocą `ocr_engine.recognize(pdf_save_options, page_number)`. Biblioteka automatycznie wygeneruje wielostronicowy przeszukiwalny PDF.

### 2️⃣ Co jeśli mój plik źródłowy to wysokiej rozdzielczości TIFF (300 dpi+)?

Wyższe DPI zapewnia lepszą dokładność OCR, ale także większe zużycie pamięci. Jeśli napotkasz `MemoryError`, najpierw zmniejsz rozdzielczość obrazu:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ Jak zmienić język OCR?

Ustaw właściwość `language` w silniku przed załadowaniem obrazu:

```python
ocr_engine.language = "fra"   # French
```

Pełna lista obsługiwanych kodów językowych znajduje się w dokumentacji Aspose.

### 4️⃣ Co jeśli muszę zachować oryginalną jakość obrazu?

Klasa `PdfSaveOptions` posiada właściwość `compression`. Ustaw ją na `PdfCompression.None`, aby zachować dane rastrowe dokładnie tak, jak były.

```python
pdf_save_options.compression = "None"
```

## Wskazówki dla wdrożeń gotowych do produkcji

- **Przetwarzanie wsadowe:** Owiń główną logikę w funkcję przyjmującą listę ścieżek plików. Zapisuj każde powodzenie/porażkę do pliku CSV w celu audytu.
- **Równoległość:** Użyj `concurrent.futures.ThreadPoolExecutor`, aby uruchamiać OCR na wielu rdzeniach. Pamiętaj, że każdy wątek potrzebuje własnej instancji `OcrEngine`.
- **Bezpieczeństwo:** Jeśli przetwarzasz poufne dokumenty, uruchom skrypt w środowisku sandbox i usuń tymczasowe pliki natychmiast po przetworzeniu.

## Zakończenie

Teraz wiesz, jak **utworzyć przeszukiwalny PDF** z zeskanowanych obrazów przy użyciu zwięzłego skryptu w Pythonie. Inicjalizując silnik OCR, ładując TIFF (lub dowolny raster), konfigurując `PdfSaveOptions` do **add OCR text layer**, a na końcu wywołując `recognize`, cały pipeline **convert scanned image pdf** i **convert TIFF to PDF** staje się pojedynczym, powtarzalnym poleceniem.

Kolejne kroki? Spróbuj połączyć ten skrypt z obserwatorem plików, aby każdy nowy skan umieszczony w folderze automatycznie stawał się przeszukiwalny. Albo eksperymentuj z różnymi językami OCR, aby obsługiwać wielojęzyczne archiwa. Nie ma ograniczeń, gdy łączysz OCR z generowaniem PDF.

Masz więcej pytań o **how to run OCR** w innych językach lub frameworkach? zostaw komentarz poniżej i szczęśliwego kodowania! 

![Diagram pokazujący przepływ od zeskanowanego obrazu → silnika OCR → przeszukiwalnego PDF (create searchable pdf)](searchable-pdf-flow.png "Diagram przepływu tworzenia przeszukiwalnego pdf")


## Co powinieneś nauczyć się dalej?

- [Jak wykonać OCR PDF w .NET z Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Konwertuj obrazy do PDF C# – Zapisz wynik OCR wielostronicowy](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Jak wykonać OCR tekstu obrazu z językiem przy użyciu Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}