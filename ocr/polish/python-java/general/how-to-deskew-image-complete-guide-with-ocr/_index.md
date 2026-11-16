---
category: general
date: 2026-03-26
description: Naucz się prostować obraz, rozpoznawać tekst z obrazu i budować pipeline
  przetwarzania obrazu, aby usuwać szumy ze skanu oraz konwertować zeskanowany obraz
  na tekst.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: pl
og_description: Jak wyprostować obraz i zamienić przekrzywiony skan w tekst przeszukiwalny.
  Postępuj zgodnie z tym przewodnikiem, aby rozpoznać tekst z obrazu, usunąć szumy
  ze skanu i przekształcić zeskanowany obraz w tekst.
og_title: Jak wyrównać obraz – Przewodnik OCR krok po kroku
tags:
- OCR
- image-processing
- Python
title: Jak prostować obraz – Kompletny przewodnik z OCR
url: /pl/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak deskewować obraz – Kompletny przewodnik z OCR

Zastanawiałeś się kiedyś **jak deskewować obraz**, który powstał w wyniku taniego skanera? Nie jesteś sam. Krzywa strona wygląda nieprofesjonalnie, a co ważniejsze, pochylenie może zakłócić działanie każdego silnika OCR próbującego **rozpoznać tekst z obrazu**.  

W tym tutorialu przeprowadzimy Cię przez pełny **image preprocessing pipeline**, który prostuje, binarizuje i odszumia skan, a następnie przekazuje go silnikowi OCR, abyś mógł **przekształcić zeskanowany obraz w tekst** bez zbędnych komplikacji. Bez magii, po prostu czysty Python i mała biblioteka, która wykona ciężką pracę.

## Co będzie potrzebne

- Python 3.9+ (kod działa również na 3.10 i nowszych)
- Pakiet `ocr` (zainstaluj przez `pip install ocr‑toolkit` – zamień na nazwę swojej biblioteki)
- Zeskanowany plik JPEG lub PNG wyraźnie pochyły (np. `skewed_scan.jpg`)
- Odrobina ciekawości, dlaczego każdy krok przetwarzania ma znaczenie

To wszystko. Bez ciężkich zależności jak OpenCV, chyba że chcesz zagłębić się później.

## Krok 1: Wczytaj zeskanowany obraz

Pierwsze, co trzeba zrobić, to wczytać plik do pamięci. Ten krok jest prosty, ale kluczowy — jeśli ścieżka jest nieprawidłowa, wszystko inne się zawiesi.

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **Dlaczego?**  
> Wczytanie obrazu daje nam obiekt, którym można manipulować i który `ocr.ImagePreprocessor` może przetwarzać. Pominięcie tego kroku spowoduje, że pipeline nie będzie miał dostępu do rzeczywistych danych pikselowych.

## Jak deskewować obraz i przygotować go do OCR

Mając już obraz, prostujemy go. Metoda `deskew()` szacuje kąt pochylenia i obraca zdjęcie z powrotem do poziomu.

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Pro tip:** Jeśli Twoje skany są tylko nieco odchylone (≤ 3°), domyślny algorytm zazwyczaj radzi sobie idealnie. Przy ekstremalnych kątach może być konieczne dostosowanie wewnętrznych parametrów — sprawdź dokumentację biblioteki pod kątem `max_angle`.

## Binarizacja obrazu – zamień go na czarno‑białe

Silniki OCR uwielbiają obrazy o wysokim kontraście. Konwersja zdjęcia do postaci binarnej (czarno‑białej) usuwa subtelne odcienie, które mogą mylić rozpoznawanie znaków.

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **Co się dzieje?**  
> Piksele jaśniejsze niż 128 stają się białe; wszystko inne zamienia się na czarne. Dostosuj próg, jeśli Twój skan jest wyjątkowo ciemny lub jasny.

## Usuń szum ze skanu przed OCR

Nawet idealnie deskewowany obraz może zawierać drobne plamki, kurz lub artefakty kompresji. Te małe plamki są zgubą każdego silnika OCR.

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **Dlaczego usuwać szum?**  
> Szum tworzy fałszywe krawędzie, które silnik OCR może zinterpretować jako znaki. Mały promień działa w większości przypadków; zwiększ go przy bardzo ziarnistych dokumentach.

## Zastosuj pipeline przetwarzania obrazu

Wszystkie ustawienia są gotowe — teraz uruchamiamy pipeline na oryginalnym obrazie.

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Wynik:** `processed_image` to wyczyszczony, prosty, wysokokontrastowy bitmap gotowy do ekstrakcji tekstu.

## Rozpoznaj tekst z obrazu przy użyciu silnika OCR

Czas naprawdę odczytać tekst. Inicjalizujemy silnik OCR, podajemy mu nasz wypolerowany obraz i żądamy surowego ciągu znaków.

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Oczekiwany wynik** (przykład):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Jeśli zobaczysz nieczytelne znaki, sprawdź ponownie krok deskewowania lub eksperymentuj z inną wartością `threshold`.

## Budowanie pełnego pipeline przetwarzania obrazu – kompletny skrypt

Łącząc wszystko razem, oto pojedynczy, gotowy do uruchomienia skrypt, który możesz zapisać w pliku `.py` i wykonać:

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Wskazówka:** Owiń cały kod w funkcję (`def ocr_from_file(path): …`), jeśli planujesz przetwarzać wiele plików jednocześnie.

## Częste pytania i przypadki brzegowe

- **Co jeśli obraz jest już prawidłowo ustawiony?**  
  Metoda `deskew()` wykrywa kąt bliski zeru i pozostawia obraz niezmieniony, więc możesz ją bezpiecznie uruchamiać na każdym pliku.

- **Mój skan jest w kolorze — czy mam go zachować?**  
  Kolor nie wnosi nic wartościowego w większości zadań OCR. Binarizacja go usuwa, przyspieszając przetwarzanie i zmniejszając zużycie pamięci.

- **Czy mogę łączyć wiele kroków przetwarzania?**  
  Oczywiście. Klasa `ImagePreprocessor` jest zaprojektowana pod kątem pipeline; możesz dodać `sharpen()`, `contrast_enhance()` lub własne filtry przed wywołaniem `apply()`.

- **Wynik OCR zawiera niechciane podziały linii — jak to naprawić?**  
  Przetwórz ciąg po fakcie przy pomocy `text.replace("\n", " ").strip()` lub użyj bardziej zaawansowanej biblioteki analizy układu, takiej jak tryby `--psm` w Tesseract.

## Kolejne kroki

Teraz, gdy wiesz **jak deskewować obraz** i masz solidny **image preprocessing pipeline**, możesz rozważyć:

- Integrację **rozpoznawania tekstu z obrazu** w API Flask do natychmiastowego przesyłania dokumentów.
- Użycie pipeline do **usuwania szumu ze skanu** historycznych dokumentów, gdzie zachowanie jest kluczowe.
- Skalowanie do przetwarzania tysięcy stron jednocześnie i generowanie przeszukiwalnego PDF przy użyciu `pdfminer` lub `PyMuPDF`.

Śmiało eksperymentuj z różnymi progami, promieniami odszumiania lub nawet zamień backend OCR na Tesseract, jeśli potrzebujesz wsparcia wielojęzycznego. Podstawy pozostają niezmienne: prostuj, czyść, a potem czytaj.

---

*Miłego kodowania! Jeśli napotkasz problemy, zostaw komentarz poniżej — chętnie pomogę dopracować pipeline.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}