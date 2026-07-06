---
category: general
date: 2026-03-26
description: Jak uruchomić OCR na pliku PNG i wyodrębnić tekst z obrazu przy użyciu
  własnego słownika w celu zwiększenia dokładności OCR. Dowiedz się, jak szybko wczytać
  obraz do OCR.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: pl
og_description: Jak uruchomić OCR na pliku PNG i wyodrębnić tekst z obrazu przy użyciu
  własnego słownika w celu zwiększenia dokładności OCR. Przewodnik krok po kroku.
og_title: Jak uruchomić OCR – wyodrębnić tekst z obrazu w Pythonie
tags:
- OCR
- Python
- Image Processing
title: Jak uruchomić OCR – wyodrębnić tekst z obrazu w Pythonie
url: /pl/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uruchomić OCR – wyodrębnić tekst z obrazu w Pythonie

Zastanawiałeś się kiedyś **jak uruchomić OCR** na zeskanowanej fakturze lub zrzucie ekranu i uzyskać czysty, przeszukiwalny tekst? Nie jesteś sam. W wielu projektach wąskim gardłem jest po prostu wczytanie obrazu do OCR i nakłonienie silnika do zrozumienia słów specyficznych dla domeny.  

W tym tutorialu przejdziemy przez kompletny, gotowy do uruchomienia przykład, który **wyodrębnia tekst z plików obrazu**, pokazuje, jak **rozpoznawać tekst z zasobów PNG**, a także demonstruje sztuczki, aby **poprawić dokładność OCR** przy użyciu własnych słowników i znaków specjalnych. Po zakończeniu będziesz mieć samodzielny skrypt, który możesz wstawić do dowolnego kodu w Pythonie.

## Czego będziesz potrzebować

- Python 3.8+ (kod używa podpowiedzi typów, ale działa także na wcześniejszych wersjach 3.x)
- Biblioteka `ocr` dostarczana wraz z silnikiem OCR, którego używasz (zainstaluj przez `pip install ocr‑engine` – zamień na rzeczywistą nazwę pakietu)
- Plik obrazu (`input.png`), który chcesz przetworzyć
- Opcjonalnie: plik tekstowy (`invoice_terms.txt`) zawierający słowa specyficzne dla domeny, po jednym wierszu

Brak ciężkich zależności zewnętrznych, brak kluczy API do chmury – tylko lokalny silnik OCR.

---

## Krok 1: Zainstaluj i zaimportuj bibliotekę OCR

Najpierw upewnij się, że pakiet OCR jest zainstalowany. Jeśli używasz hipotetycznego pakietu `ocr-engine`, uruchom:

```bash
pip install ocr-engine
```

Teraz zaimportuj potrzebne klasy:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **Pro tip:** Jeśli pracujesz w wirtualnym środowisku, aktywuj je przed instalacją, aby nie zaśmiecać globalnej instalacji Pythona.

## Krok 2: Utwórz instancję silnika OCR

Utworzenie obiektu silnika jest punktem wyjścia dla każdego zadania OCR. Pomyśl o tym jak o włączeniu skanera sprzętowego w oprogramowaniu.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

Dlaczego to ważne: silnik przechowuje konfigurację, taką jak pakiety językowe, tryby rozpoznawania i wszelkie niestandardowe zasoby, które podłączysz później. Bez niego nie możesz **load image for OCR** ani uruchomić potoku rozpoznawania.

## Krok 3: Wczytaj obraz, który chcesz rozpoznać

Tutaj faktycznie **load image for OCR**. Metoda `Imaging.Image.load()` odczytuje plik i konwertuje go do wewnętrznego formatu bitmapy, którego oczekuje silnik.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

Jeśli masz JPEG lub TIFF, ta sama metoda działa – wystarczy zmienić rozszerzenie. Silnik automatycznie wykrywa format.

> **Edge case:** Bardzo duże obrazy (powyżej 5 MP) mogą powodować skoki pamięci. Rozważ zmniejszenie rozdzielczości przy pomocy Pillow przed wczytaniem, jeśli napotkasz problemy z wydajnością.

## Krok 4: Dostarcz własny słownik, aby zwiększyć dokładność

Większość silników OCR dostarcza ogólne modele językowe. Dla faktur, paragonów czy dokumentów prawnych często pojawiają się pominięte słowa. Dostarczenie własnej listy słów mówi silnikowi: „te terminy są prawidłowe, traktuj je jako poprawne”.

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

Typowe wpisy mogą wyglądać tak:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

Dodanie ich znacząco poprawia metrykę **improve OCR accuracy** – szczególnie dla znaków nie‑ASCII.

## Krok 5: Dodaj znaki specjalne nieobjęte domyślnym zestawem

Jeśli Twoja domena używa symboli takich jak znak euro (€) czy skandynawska Ø, możesz je wyraźnie dodać:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

Silnik będzie teraz traktował te glify jako prawidłowe podczas fazy rozpoznawania, zmniejszając szansę na „śmieciowy” wynik.

## Krok 6: Uruchom proces OCR i pobierz tekst

Na koniec wywołaj rozpoznawacz i pobierz wynik w postaci czystego tekstu. Wywołanie `recognize()` zwraca rozbudowany obiekt; w większości przypadków potrzebujemy tylko surowego łańcucha znaków.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**Expected output** (skrócone dla przejrzystości):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

Jeśli wynik wygląda na zniekształcony, sprawdź ponownie, czy własny słownik i znaki specjalne zostały poprawnie załadowane.

---

## Przegląd wizualny

![how to run OCR diagram](ocr-workflow.png){alt="diagram jak uruchomić OCR"}

Diagram powyżej ilustruje przepływ od wczytania obrazu do uzyskania czystego tekstu, podkreślając miejsca, w których możesz wstrzyknąć własne słowniki i zestawy znaków.

---

## Częste pytania i pułapki

### Czy to działa z wielostronicowymi PDF‑ami?

Tak – po prostu przekonwertuj każdą stronę na PNG (używając `pdf2image` lub podobnego) i podawaj je kolejno tej samej instancji `ocr_engine`. Silnik przetwarza każdy obraz niezależnie, więc otrzymasz listę łańcuchów, które możesz połączyć.

### Co zrobić, gdy obraz jest obrócony?

Większość nowoczesnych silników OCR automatycznie wykrywa orientację, ale możesz wymusić obrót za pomocą:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### Jak obsłużyć języki inne niż angielski?

Zamień model językowy przed wczytaniem obrazu:

```python
ocr_engine.set_language("de")  # German
```

Upewnij się, że odpowiedni pakiet językowy jest zainstalowany.

---

## Pełny skrypt – gotowy do kopiowania i wklejania

Poniżej znajduje się cały program, gotowy do uruchomienia po zamianie ścieżek zastępczych.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

Uruchom go za pomocą:

```bash
python run_ocr.py
```

Powinieneś zobaczyć wyodrębniony tekst wypisany w konsoli. Stamtąd możesz zapisać go do pliku, wprowadzić do bazy danych lub przekazać do kolejnych potoków NLP.

---

## Podsumowanie i kolejne kroki

Omówiliśmy **jak uruchomić OCR** na PNG, jak **wyodrębnić tekst z obrazu**, oraz pokazaliśmy praktyczne sposoby **rozpoznawania tekstu z PNG** przy **poprawianiu dokładności OCR** dzięki słownikom i znakom specjalnym.  

Następnie rozważ:

- **Przetwarzanie wsadowe:** Pętla po katalogu obrazów.
- **Post‑processing:** Użycie wyrażeń regularnych do wyciągania numerów faktur lub dat.
- **Integracja:** Podłączenie skryptu do API Flask, aby oferować OCR na żądanie.

Jeśli interesują Cię bardziej zaawansowane tematy, sprawdź tutoriale o **load image for OCR** z wstępnym przetwarzaniem w OpenCV lub zagłęb się w modele OCR oparte na deep learning, takie jak Tesseract 4+ z warstwami LSTM.

---

### Kontynuuj eksperymentowanie!

Spróbuj zamienić `invoice_terms.txt` na listę terminologii medycznej, dodaj greckie znaki lub podaj silnikowi zdjęcie o niskiej rozdzielczości, aby zobaczyć, jak daleko może posunąć się dokładność. Im więcej bawisz się konfiguracją, tym lepiej zrozumiesz kompromisy między wstępnym przetwarzaniem, własnymi słownikami a ustawieniami silnika.

Happy coding, and may your OCR results be ever crisp!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}