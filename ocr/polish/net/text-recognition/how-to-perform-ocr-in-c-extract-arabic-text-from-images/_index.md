---
category: general
date: 2026-03-17
description: Dowiedz się, jak wykonać OCR w C#, aby wyodrębnić arabski tekst, rozpoznać
  tekst z obrazu i przekształcić obraz w tekst, wraz z kompletnym przykładem kodu.
draft: false
keywords:
- how to perform OCR
- extract arabic text
- recognize text from image
- convert image to text
- extract text from image
language: pl
og_description: Jak wykonać OCR w C#? Ten przewodnik pokazuje, jak wyodrębnić arabski
  tekst, rozpoznać tekst z obrazu i przekształcić obraz w tekst w kilku prostych krokach.
og_title: Jak wykonać OCR w C# – wyodrębnić arabski tekst
tags:
- OCR
- C#
- Arabic
- ImageProcessing
title: Jak wykonać OCR w C# – wyodrębnić arabski tekst z obrazów
url: /pl/net/text-recognition/how-to-perform-ocr-in-c-extract-arabic-text-from-images/
---

/products/products-backtop-button >}}

All done.

Check for any other markdown links: none.

Make sure to keep code block placeholders unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać OCR w C# – wyodrębnić arabski tekst z obrazów

Zastanawiałeś się kiedyś **jak wykonać OCR** na arabskiej fakturze lub zeskanowanym dokumencie? Nie jesteś sam — wielu programistów napotyka trudności, gdy muszą wyciągnąć arabskie znaki z bitmapy. Dobrą wiadomością jest to, że przy kilku linijkach C# możesz rozpoznawać tekst z plików obrazów, konwertować obraz na tekst i ostatecznie **wyodrębnić arabski tekst** do dalszego przetwarzania.

W tym samouczku przeprowadzimy Cię przez kompletny, działający przykład, który pokaże dokładnie, jak wykonać OCR, dlaczego każdy krok ma znaczenie i na co zwrócić uwagę przy obsłudze skryptów od prawej do lewej. Po zakończeniu będziesz w stanie **wyodrębnić tekst z obrazu** w językach arabskim, urdu, kurdyjskim lub dowolnym języku obsługiwanym przez silnik OCR.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod kompiluje się również z .NET Core)  
- Odwołanie do biblioteki OCR, która udostępnia `OcrEngine` (np. `MyOcrSdk.dll`).  
- Plik obrazu zawierający arabski tekst, np. `invoice_arabic.png`.  
- Podstawowa znajomość aplikacji konsolowych C#.

> **Wskazówka:** Jeśli nie masz pod ręką SDK OCR, darmowa edycja społecznościowa *MyOcrSdk* działa do testów i obsługuje języki, które będziemy używać.

---

## Krok 1 – Skonfiguruj projekt i zaimportuj przestrzeń nazw OCR

Zanim będziemy mogli **rozpoznać tekst z obrazu**, potrzebujemy szkieletu projektu i odpowiednich dyrektyw `using`.

```csharp
using System;
using MyOcrSdk;          // <-- Replace with the actual namespace of your OCR library
using MyOcrSdk.IO;       // For ImageStream helper class

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the OCR workflow will go here
        }
    }
}
```

*Dlaczego to ważne:* Importowanie właściwych przestrzeni nazw daje dostęp do `OcrEngine`, `Language` i `ImageStream`. Pominięcie tego kroku skutkuje błędami kompilacji, które mogą być frustrujące dla początkujących.

---

## Krok 2 – Utwórz instancję silnika OCR (zawiera główne słowo kluczowe)

Teraz faktycznie **wykonujemy OCR**, tworząc instancję silnika.

```csharp
// Step 2: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

Obiekt `OcrEngine` jest sercem operacji; przechowuje konfigurację, wykonuje ciężką pracę i zwraca obiekt wyniku zawierający wyodrębniony ciąg znaków. Myśl o nim jak o „mózgu”, który **konwertuje obraz na tekst**.

---

## Krok 3 – Wybierz język rozpoznawania

Arabski, urdu, kurdyjski… wszystkie używają tej samej rodziny pisma, więc musimy poinformować silnik, jakiego języka się spodziewać. To znacznie zwiększa dokładność.

```csharp
// Step 3: Choose the language for recognition (Arabic, Urdu, Kurdish, etc.)
ocrEngine.Config.Language = Language.Arabic;   // You can switch to Language.Urdu, etc.
```

*Dlaczego to ważne:* Silniki OCR opierają się na modelach językowych. Wybranie właściwego modelu zmniejsza pomyłki w rozpoznawaniu podobnie wyglądających znaków, szczególnie w skryptach od prawej do lewej.

---

## Krok 4 – Załaduj obraz zawierający tekst

Potrzebujemy bitmapy, którą silnik może analizować. Pomocnicza metoda `ImageStream.FromFile` ukrywa szczegóły operacji we/wy na plikach.

```csharp
// Step 4: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_arabic.png");
```

Upewnij się, że ścieżka wskazuje na **prawidłowy obraz**. Jeśli plik jest brakujący lub uszkodzony, silnik zgłosi wyjątek i nie będziesz w stanie **wyodrębnić tekstu z obrazu**.

---

## Krok 5 – Uruchom proces OCR i pobierz wynik

Na koniec wywołujemy `Recognize()` i wyświetlamy wyodrębniony ciąg znaków.

```csharp
// Step 5: Perform the OCR operation
var ocrResult = ocrEngine.Recognize();

// Step 6: Display the extracted text
Console.WriteLine("=== Extracted Arabic Text ===");
Console.WriteLine(ocrResult.Text);
```

Właściwość `ocrResult.Text` zawiera tekstową reprezentację wszystkiego, co silnik odczytał. W większości przypadków zobaczysz mieszankę arabskich znaków i liczb, idealną do dalszego przetwarzania, takiego jak wstawianie do bazy danych czy tłumaczenie.

### Oczekiwany wynik

```
=== Extracted Arabic Text ===
فاتورة رقم: 12345
التاريخ: 2026/03/15
المبلغ: 2500.00 ريال
...
```

Jeśli widzisz zniekształcone znaki, sprawdź ponownie ustawienie języka i upewnij się, że obraz ma wysoką rozdzielczość (300 dpi lub wyższą).

---

## Pełny działający przykład

Poniżej znajduje się **kompletny, samodzielny program**, który możesz skopiować i wkleić do nowego projektu konsolowego i od razu uruchomić.

```csharp
// Full OCR demo – extracts Arabic text from an image
using System;
using MyOcrSdk;
using MyOcrSdk.IO;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Set language – Arabic (change to Urdu or Kurdish if needed)
            ocrEngine.Config.Language = Language.Arabic;

            // 3️⃣ Load the source image
            // Replace YOUR_DIRECTORY with the folder that holds your PNG/JPG
            string imagePath = @"YOUR_DIRECTORY/invoice_arabic.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            try
            {
                // 4️⃣ Run OCR
                var result = ocrEngine.Recognize();

                // 5️⃣ Output the text
                Console.WriteLine("=== Extracted Arabic Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – useful when you need to **extract text from image** in batch jobs
                Console.Error.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

> **Uwaga:** Jeśli Twoje SDK OCR wymaga licencjonowania, upewnij się, że zainicjalizujesz licencję przed krokiem 1 (np. `OcrEngine.SetLicense("YOUR_LICENSE_KEY");`). Ta linia została pominięta dla zwięzłości.

---

## Obsługa typowych przypadków brzegowych

| Sytuacja | Dlaczego się dzieje | Szybka naprawa |
|-----------|----------------|-----------|
| **Rozmyty lub niskiej rozdzielczości obraz** | Dokładność OCR spada poniżej 70 % | Skanuj w 300 dpi lub zwiększ rozdzielczość przy użyciu algorytmu bikubicznego przed przekazaniem do silnika. |
| **Mieszane języki (arabskie + angielskie)** | Silnik może zatrzymać się po pierwszym bloku językowym | Włącz tryb wielojęzykowy: `ocrEngine.Config.Language = Language.Arabic | Language.English;` |
| **Problemy z wyświetlaniem od prawej do lewej** | Konsola drukuje znaki od lewej do prawej, co powoduje odwrócenie arabskiego | Użyj `Console.OutputEncoding = System.Text.Encoding.UTF8;` i terminala obsługującego skrypty RTL. |
| **Duże pliki PDF podzielone na wiele stron** | Zużycie pamięci rośnie | Przetwarzaj jedną stronę na raz: wczytuj każdą stronę jako osobny obraz i powtarzaj przepływ OCR. |
| **Specjalne symbole (waluty, daty)** | Niektóre modele OCR traktują je jako szum | Przetwarzaj `ocrResult.Text` przy pomocy wyrażenia regularnego, aby znormalizować znane wzorce. |

---

## Rozszerzanie rozwiązania – od OCR do ekstrakcji danych

Teraz, gdy **wiesz, jak wykonać OCR**, możesz się zastanawiać: *Co mogę zrobić z wyodrębnionym arabskim tekstem?* Oto kilka pomysłów, które naturalnie wynikają:

1. **Parsowanie faktur** – użyj wyrażeń regularnych, aby wyodrębnić numery faktur, daty i kwoty.  
2. **Wysyłanie do API tłumaczeń** – wyślij arabski ciąg do Azure Translator lub Google Cloud Translate.  
3. **Przechowywanie w bazie danych** – wstaw wyczyszczony tekst do tabeli SQL w celu raportowania.  
4. **Wyzwalanie przepływów pracy** – połącz z kolejką wiadomości (np. RabbitMQ), aby rozpocząć dalsze przetwarzanie.  

Wszystkie te scenariusze opierają się na tej samej podstawowej operacji: **konwertuj obraz na tekst**, a następnie manipuluj wynikiem.

---

## Podsumowanie

Omówiliśmy wszystko, co musisz wiedzieć o **tym, jak wykonać OCR** w C#, aby **wyodrębnić arabski tekst** z obrazu. Od konfiguracji projektu, przez utworzenie `OcrEngine`, skonfigurowanie języka, załadowanie bitmapy, uruchomienie rozpoznawania i wyświetlenie wyniku. Omówiliśmy także typowe pułapki i pokazaliśmy, jak rozszerzyć podstawowy przepływ do rzeczywistych pipeline'ów.

Spróbuj — zamień ścieżkę obrazu, zmień język na urdu lub podłącz wyjście do bazy danych. Nie ma ograniczeń, gdy możesz niezawodnie **rozpoznawać tekst z obrazu** i **konwertować obraz na tekst**.

---

### Powiązane tematy, które możesz chcieć zbadać

- **Wyodrębnij tekst z obrazu** przy użyciu Tesseract OCR (alternatywa open‑source)  
- **Przetwarzanie OCR wsadowo** dla tysięcy zeskanowanych PDF‑ów  
- **Poprawa dokładności OCR** przy użyciu wstępnego przetwarzania obrazu (progowanie, usuwanie szumu)  
- **Obsługa skryptów od prawej do lewej** w frameworkach UI .NET (WPF, WinForms)

Śmiało zostaw komentarz, jeśli napotkasz problemy, lub podziel się, jak dostosowałeś ten wzorzec do własnych projektów. Szczęśliwego kodowania!  

![how to perform OCR example](images/ocr_flow.png "how to perform OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}