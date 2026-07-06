---
category: general
date: 2026-04-26
description: jak używać OCR na zeskanowanych PDF-ach, wyodrębniać tekst z PDF, uruchamiać
  OCR w PDF i konwertować zeskanowany PDF na pliki przeszukiwalne w kilku krokach
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: pl
og_description: 'jak używać OCR w Pythonie: dowiedz się, jak wyodrębnić tekst z PDF,
  uruchomić OCR na PDF i przekształcić zeskanowany PDF w dokumenty przeszukiwalne.'
og_title: jak używać OCR – szybki przewodnik po wyodrębnianiu tekstu z PDF
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Jak używać OCR – wyodrębnić tekst z PDF w Pythonie
url: /pl/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak używać OCR – wyodrębnić tekst z PDF za pomocą Pythona

Zastanawiałeś się kiedyś **jak używać OCR**, aby wyciągnąć tekst ze zeskanowanego kontraktu, paragonu lub ebooka? Nie jesteś sam. W wielu rzeczywistych projektach otrzymany PDF jest po prostu obrazem, a bez OCR nie możesz przeszukiwać, indeksować ani analizować jego zawartości.  

W tym samouczku przeprowadzimy Cię przez kompletny, działający przykład, który pokazuje **jak używać OCR**, jak **wyodrębnić tekst z PDF**, oraz dlaczego możesz chcieć **konwertować zeskanowany PDF** na dokumenty możliwe do przeszukiwania. Omówimy także subtelną sztukę **ładowania PDF jako obrazu**, aby silnik OCR mógł wyraźnie zobaczyć każdą stronę.

> **Szybki podgląd:** Po zakończeniu będziesz mieć skrypt, który ładuje wielostronicowy PDF, uruchamia OCR na każdej stronie i wypisuje rozpoznany tekst – bez konieczności korzystania z zewnętrznych usług.

## Czego będziesz potrzebować

- Python 3.9+ (dowolna nowsza wersja działa)
- pakiet `aocr` (lub dowolna kompatybilna biblioteka OCR, która udostępnia `OcrEngine` i `Image.load`)
- Zeskanowany plik PDF, który chcesz przetworzyć (np. `contract.pdf`)
- Umiarkowana ilość RAM (≈ 200 MB na 100‑stronicowy PDF zazwyczaj wystarcza)

Jeśli jeszcze nie zainstalowałeś biblioteki OCR, uruchom:

```bash
pip install aocr
```

> **Pro tip:** Użyj wirtualnego środowiska, aby utrzymać zależności w porządku.

## Krok 1: Załaduj PDF jako obraz – pierwszy element układanki

Zanim OCR może się rozpocząć, PDF musi być przedstawiony jako obraz. To tutaj wkracza drugorzędne słowo kluczowe **load pdf as image**.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Dlaczego to ważne:* `aocr.Image.load` wewnętrznie rasteryzuje każdą stronę PDF do bitmapy, którą silnik OCR może zrozumieć. Jeśli pominiesz ten krok i podasz surowy PDF, silnik zgłosi błąd, ponieważ oczekuje danych pikselowych, a nie wektorowych.

> **Uwaga:** Ścieżka może być absolutna lub względna. Upewnij się, że plik jest czytelny; w przeciwnym razie napotkasz `FileNotFoundError`.

## Krok 2: Uruchom OCR na PDF – zamiana pikseli w znaki

Teraz, gdy PDF istnieje jako obraz, możemy w końcu **run OCR on PDF**. Poniższy fragment przetwarza wszystkie strony jednocześnie:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*Co się dzieje pod maską?* `process_all_pages` przechodzi przez rasteryzowane strony, stosuje model OCR i zwraca listę obiektów wyników — po jednym na stronę. Każdy wynik zawiera rozpoznany tekst, oceny pewności oraz ramki ograniczające (jeśli będą potrzebne później).

## Krok 3: Wyodrębnij tekst z PDF – wyciąganie ciągów

Mając wyniki OCR w ręku, wyodrębnienie czystego tekstu staje się trywialne. Przejdziemy po stronach i wypiszemy wynik, demonstrując drugorzędne słowo kluczowe **extract text from pdf**.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Oczekiwany wynik** (skrócony dla przejrzystości):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

Jeśli potrzebujesz tekstu w jednej ciągłej postaci, po prostu połącz go:

```python
full_text = "\n".join(r.text for r in page_results)
```

Teraz pomyślnie **wyodrębniłeś tekst z PDF** przy użyciu OCR.

## Krok 4: Konwertuj zeskanowany PDF – uczynienie go przeszukiwalnym

Wiele narzędzi downstream (takich jak Elasticsearch czy SharePoint) oczekuje przeszukiwalnego PDF zamiast zwykłego zrzutu tekstu. Możesz osadzić wynik OCR z powrotem w oryginalnym PDF, skutecznie **convert scanned PDF** do wersji przeszukiwalnej.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Dlaczego warto?* Przeszukiwalny PDF zachowuje oryginalny układ i obrazy, jednocześnie umożliwiając zaznaczanie tekstu i indeksowanie — korzyść zarówno dla ludzi, jak i maszyn.

## Częste pułapki i przypadki brzegowe

### Wielostronicowe PDFy większe niż pamięć

Jeśli Twój PDF ma setki stron, ładowanie wszystkiego naraz może wyczerpać RAM. Biblioteka `aocr` obsługuje leniwe ładowanie:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

Następnie przetwarzaj strony po jednej:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Skanowanie niskiej jakości

Dokładność OCR spada dramatycznie przy rozmytych lub niskokontrastowych skanach. Przed podaniem obrazu silnikowi rozważ wstępne przetwarzanie:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Obsługa języków

Domyślnie silnik zakłada język angielski. Aby **run OCR on PDF** w innym języku, ustaw kod języka:

```python
ocr_engine.language = "spa"  # Spanish
```

Upewnij się, że odpowiedni model językowy jest zainstalowany.

## Pełny działający przykład

Łącząc wszystko razem, oto samodzielny skrypt, który możesz umieścić w pliku o nazwie `ocr_pdf.py` i uruchomić od razu:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Uruchom go w ten sposób:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

Zobaczysz tekst wypisany w konsoli, a jeśli podałeś `-o`, przeszukiwalny PDF pojawi się obok oryginalnego pliku.

## Pro tipy i najlepsze praktyki

- **Batch processing:** Gdy obsługujesz dziesiątki PDFów, otocz powyższą logikę pętlą i loguj sukcesy/porażki każdego pliku.
- **Confidence filtering:** Każdy `page_result` zawiera metrykę pewności. Odrzuć lub oznacz strony o niskiej pewności do ręcznej weryfikacji.
- **Parallelism:** Jeśli Twój procesor ma wiele rdzeni, rozważ użycie `concurrent.futures` do równoległego przetwarzania stron — pamiętaj jednak o zużyciu pamięci.
- **Version lock:** API `aocr` może się zmieniać. Zablokuj wersję w `requirements.txt` (np. `aocr==2.3.1`), aby uniknąć niekompatybilnych zmian.

## Zakończenie

Przeszliśmy przez **jak używać OCR** do **wyodrębnienia tekstu z PDF**, **uruchomienia OCR na PDF**, **ładowania PDF jako obrazu**, oraz **konwertowania zeskanowanego PDF** na format przeszukiwalny. Kod jest kompletny, wyjaśnienia obejmują zarówno *co*, jak i *dlaczego*, a Ty masz teraz wielokrotnego użytku wzorzec dla każdego projektu pracującego z PDF‑ami opartymi na obrazach.

Co dalej? Spróbuj przekazać wyodrębniony tekst do pipeline’u przetwarzania języka naturalnego, zaindeksować przeszukiwalne PDFy w Elasticsearch lub poeksperymentować z różnymi backendami OCR, takimi jak Tesseract czy Azure Computer Vision. Niebo jest granicą, a narzędzia masz pod ręką.

Miłego kodowania i niech Twoje PDFy zawsze będą przeszukiwalne! 

![przykład użycia OCR](/images/ocr_workflow.png "użycie OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}