---
category: general
date: 2026-04-26
description: Szybko maskuj numery kart kredytowych przy użyciu post‑procesingu OCR
  AsposeAI. Poznaj zgodność z PCI, maskowanie przy użyciu wyrażeń regularnych oraz
  sanitację danych w samouczku krok po kroku.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: pl
og_description: Maskuj numery kart kredytowych w wynikach OCR za pomocą AsposeAI.
  Ten samouczek obejmuje zgodność z PCI, maskowanie wyrażeniami regularnymi i sanitację
  danych.
og_title: Maskowanie numerów kart kredytowych – Kompletny przewodnik po post‑procesingu
  OCR w Pythonie
tags:
- OCR
- Python
- security
title: Maskowanie numerów kart kredytowych w wynikach OCR – Kompletny przewodnik Pythona
url: /pl/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maskowanie numerów kart kredytowych – Kompletny przewodnik w Pythonie

Czy kiedykolwiek musiałeś **maskować numery kart kredytowych** w tekście pochodzącym bezpośrednio z silnika OCR? Nie jesteś jedyny. W regulowanych branżach ujawnienie pełnego PAN (Primary Account Number) może wprowadzić Cię w kłopoty z audytorami zgodności PCI. Dobra wiadomość? Kilka linii Pythona i hak post‑processingowy AsposeAI pozwalają automatycznie ukryć środkowe osiem cyfr i pozostać po bezpiecznej stronie.

W tym tutorialu przejdziemy przez realistyczny scenariusz: uruchomienie OCR na obrazie paragonu, a następnie zastosowanie niestandardowej funkcji **OCR post‑processing**, która sanitizuje wszelkie dane PCI. Po zakończeniu będziesz mieć wielokrotnego użytku fragment kodu, który możesz wstawić do dowolnego przepływu pracy AsposeAI, oraz kilka praktycznych wskazówek dotyczących obsługi przypadków brzegowych i skalowania rozwiązania.

## Czego się nauczysz

- Jak zarejestrować niestandardowy post‑processor w **AsposeAI**.
- Dlaczego podejście **maskowania wyrażeniami regularnymi** jest szybkie i niezawodne.
- Podstawy **zgodności PCI** związanej z sanitacją danych.
- Sposoby rozszerzenia wzorca dla wielu formatów kart lub numerów międzynarodowych.
- Oczekiwany wynik i jak zweryfikować, że maskowanie zadziałało.

> **Prerequisites** – Powinieneś mieć działające środowisko Python 3, zainstalowany pakiet Aspose.AI for OCR (`pip install aspose-ocr`) oraz przykładowy obraz (np. `receipt.png`) zawierający numer karty kredytowej. Nie są wymagane żadne inne usługi zewnętrzne.

---

## Krok 1: Zdefiniuj post‑processor, który maskuje numery kart kredytowych

Serce rozwiązania tkwi w małej funkcji, która otrzymuje wynik OCR, wykonuje **regular expression masking** i zwraca zsanityzowany tekst.

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**Dlaczego to działa:**  
- Wyrażenie regularne `(\d{4})\d{8}(\d{4})` dopasowuje dokładnie 16 kolejnych cyfr, typowy format dla Visa, MasterCard i wielu innych.  
- Poprzez przechwycenie pierwszych i ostatnich czterech cyfr (`\1` i `\2`) zachowujemy wystarczające informacje do debugowania, jednocześnie spełniając zasady **PCI compliance**, które zakazują przechowywania pełnego PAN.  
- Podstawienie `\1****\2` ukrywa wrażliwe środkowe osiem cyfr, zamieniając `1234567812345678` na `1234****5678`.

> **Pro tip:** Jeśli potrzebujesz obsługiwać 15‑cyfrowe numery American Express, dodaj drugi wzorzec, np. `r'(\d{4})\d{6}(\d{5})'` i wykonaj oba zastąpienia kolejno.

---

## Krok 2: Zainicjalizuj silnik AsposeAI

Zanim będziemy mogli podłączyć nasz post‑processor, potrzebujemy instancji silnika OCR. AsposeAI zawiera model OCR oraz prostą API do przetwarzania niestandardowego.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Dlaczego inicjalizować tutaj?**  
Utworzenie obiektu `AsposeAI` raz i ponowne użycie go przy wielu obrazach zmniejsza narzut. Silnik dodatkowo buforuje modele językowe, co przyspiesza kolejne wywołania — przydatne przy skanowaniu partii paragonów.

---

## Krok 3: Zarejestruj niestandardową funkcję maskującą

AsposeAI udostępnia metodę `set_post_processor`, która pozwala podłączyć dowolny callable. Przekazujemy naszą funkcję `mask_pci` wraz z opcjonalnym słownikiem ustawień (na razie pustym).

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**Co się dzieje w tle?**  
Gdy później wywołasz `run_postprocessor`, AsposeAI przekaże surowy wynik OCR do `mask_pci`. Funkcja otrzymuje lekki obiekt (`data`) zawierający rozpoznany tekst i zwraca nowy ciąg znaków. Ten projekt pozostawia podstawowy OCR nietknięty, a jednocześnie pozwala wymusić polityki **data sanitization** w jednym miejscu.

---

## Krok 4: Uruchom OCR na obrazie paragonu

Teraz, gdy silnik wie, jak oczyścić wyjście, podajemy mu obraz. Dla potrzeb tego tutorialu zakładamy, że masz już skonfigurowany obiekt `engine` z odpowiednimi ustawieniami języka i rozdzielczości.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**Tip:** Jeśli nie masz wstępnie skonfigurowanego obiektu, możesz go utworzyć tak:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

Wywołanie `recognize_image` zwraca obiekt, którego atrybut `text` zawiera surowy, niezamaskowany ciąg.

---

## Krok 5: Zastosuj zarejestrowany post‑processor

Mając surowe dane OCR w ręku, przekazujemy je instancji AI. Silnik automatycznie uruchamia funkcję `mask_pci`, którą zarejestrowaliśmy wcześniej.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Dlaczego używać `run_postprocessor` zamiast wywoływać funkcję ręcznie?**  
Pozwala to zachować spójny przepływ pracy, szczególnie gdy masz wiele post‑processorów (np. sprawdzanie pisowni, wykrywanie języka). AsposeAI kolejkowuje je w kolejności rejestracji, gwarantując deterministyczny wynik.

---

## Krok 6: Zweryfikuj zsanityzowany wynik

Na koniec wydrukujmy zsanityzowany tekst i potwierdźmy, że wszystkie numery kart kredytowych zostały prawidłowo zamaskowane.

```python
print(final_result.text)
```

**Oczekiwany wynik** (fragment):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

Jeśli paragon nie zawierał numeru karty, tekst pozostaje niezmieniony — nic do maskowania, nic do martwienia się.

---

## Obsługa przypadków brzegowych i typowych wariacji

### Multiple Card Numbers in One Document
Jeśli paragon zawiera więcej niż jeden PAN (np. kartę lojalnościową i kartę płatniczą), wyrażenie regularne działa globalnie, maskując wszystkie dopasowania automatycznie. Nie wymaga dodatkowego kodu.

### Non‑Standard Formatting
Czasami OCR wstawia spacje lub myślniki (`1234 5678 1234 5678` lub `1234-5678-1234-5678`). Rozszerz wzorzec, aby ignorował te znaki:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

Dodane `[ -]?` toleruje opcjonalne spacje lub myślniki między blokami cyfr.

### International Cards
Dla 19‑cyfrowych PAN używanych w niektórych regionach możesz poszerzyć wzorzec:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

Pamiętaj, że **PCI compliance** nadal wymaga maskowania środkowych cyfr, niezależnie od długości.

### Logging Masked Values (Optional)
Jeśli potrzebujesz ścieżek audytowych, przekaż flagę przez `custom_settings` i dostosuj funkcję:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

Następnie zarejestruj tak:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## Full Working Example (Copy‑Paste Ready)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

Uruchomienie tego skryptu na paragonie zawierającym `4111111111111111` spowoduje:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

To cały pipeline — od surowego OCR po **data sanitization** — zamknięty w kilku czystych linijkach Pythona.

---

## Conclusion

Właśnie pokazaliśmy, jak **maskować numery kart kredytowych** w wynikach OCR przy użyciu hooka post‑processingowego AsposeAI, krótkiej procedury wyrażeń regularnych i kilku wskazówek dotyczących **PCI compliance**. Rozwiązanie jest w pełni samodzielne, działa z dowolnym obrazem, który silnik OCR potrafi odczytać, i może być rozszerzone o bardziej złożone formaty kart lub wymagania logowania.

Gotowy na kolejny krok? Spróbuj połączyć tę maskę z **rutiną wstawiania do bazy danych**, która przechowuje tylko ostatnie cztery cyfry w celach referencyjnych, lub zintegrować **procesor wsadowy**, który skanuje cały folder paragonów przez noc. Możesz także zbadać inne zadania **OCR post‑processing**, takie jak standaryzacja adresów czy wykrywanie języka — każde z nich podąża tym samym schematem, którego użyliśmy tutaj.

Masz pytania dotyczące przypadków brzegowych, wydajności lub adaptacji kodu do innej biblioteki OCR? Zostaw komentarz poniżej i kontynuujmy dyskusję. Szczęśliwego kodowania i bądź bezpieczny!  



![Diagram ilustrujący, jak maskowanie numerów kart kredytowych działa w potoku OCR](https://example.com/images/ocr-mask-flow.png "Diagram przepływu maskowania w post‑processing OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}