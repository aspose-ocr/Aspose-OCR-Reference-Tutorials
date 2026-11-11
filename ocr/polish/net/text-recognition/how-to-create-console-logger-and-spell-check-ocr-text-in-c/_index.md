---
category: general
date: 2026-08-18
description: Dowiedz się, jak stworzyć logger konsolowy w C# i używać Aspose AI do
  korekty tekstu OCR za pomocą postprocesora sprawdzającego pisownię.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create console logger
- correct ocr text
- spell check ocr
language: pl
lastmod: 2026-08-18
og_description: Utwórz logger konsolowy w C# i popraw tekst OCR przy użyciu Aspose
  AI. Skorzystaj z tego kompletnego przewodnika, aby dodać post‑procesor sprawdzania
  pisowni do swojego potoku OCR.
og_image_alt: Illustration of creating a console logger in C# code editor
og_title: Utwórz logger konsolowy i sprawdzaj pisownię tekstu OCR w C# – przewodnik
  krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: Learn how to create console logger in C# and use Aspose AI to correct
    OCR text with a spell‑check post‑processor.
  headline: How to create console logger and spell‑check OCR text in C#
  type: TechArticle
tags:
- C#
- OCR
- AI
- logging
title: Jak stworzyć logger konsolowy i sprawdzić pisownię tekstu OCR w C#
url: /pl/net/text-recognition/how-to-create-console-logger-and-spell-check-ocr-text-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak stworzyć logger konsoli i sprawdzić pisownię tekstu OCR w C#

Jeśli potrzebujesz **utworzyć logger konsoli** do diagnostycznego wyjścia podczas przetwarzania zeskanowanych dokumentów, ten przewodnik pokaże Ci pełne rozwiązanie. Po zakończeniu samouczka będziesz w stanie **poprawić tekst OCR** przy użyciu wbudowanego procesora post‑processingowego sprawdzającego pisownię, korzystając z Aspose AI SDK.

Przetwarzanie wyników OCR często pozostawia błędy ortograficzne, które wpływają na dalszą analizę danych. Dodanie kroku sprawdzania pisowni zapewnia, że tekst jest czysty i gotowy do indeksowania, tłumaczenia lub ekstrakcji danych. Poniższe sekcje przeprowadzą Cię przez każdy wymagany element, od tworzenia loggera po ostateczną weryfikację.

## Prerequisites

Przed rozpoczęciem upewnij się, że masz:

* .NET 6.0 lub nowszy zainstalowany  
* Visual Studio 2022 (lub dowolne IDE kompatybilne z C#)  
* Pakiet NuGet Aspose.AI dodany do projektu (`dotnet add package Aspose.AI`)  

Nie są wymagane dodatkowe usługi zewnętrzne, ponieważ model Aspose AI może być pobrany automatycznie.

## Step 1: How to create console logger for diagnostics

Logger przechwytuje informacje w czasie wykonywania, ułatwiając rozwiązywanie problemów z ładowaniem modelu lub wykonaniem post‑procesora. Interfejs `ILogger` pozwala wymieniać implementacje bez zmiany reszty kodu.

```csharp
// Step 1: (Optional) Create a logger for diagnostic output
ILogger logger = new ConsoleLogger();   // set to null if logging is not needed
```

`ConsoleLogger` zapisuje każdy wpis logu do standardowego strumienia wyjściowego. Użycie interfejsu utrzymuje kod testowalny i umożliwia późniejsze zastąpienie loggera loggerem plikowym lub chmurowym.

## Step 2: Configure the AI model to enable automatic download

Aspose AI może pobrać wymagane pliki modelu na żądanie. Określenie lokalnego folderu zapobiega powtarzającemu się ruchowi sieciowemu i daje kontrolę nad przechowywaniem.

```csharp
// Step 2: Configure the AI model – enable automatic download and specify a local folder
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY"
};
```

`AllowAutoDownload` zapewnia, że SDK pobierze model przy pierwszym uruchomieniu. `DirectoryModelPath` wskazuje trwałą lokalizację na Twoim komputerze, co jest przydatne w pipeline’ach CI.

## Step 3: Initialise the AsposeAI engine with the logger

Przekazanie loggera do silnika wiąże diagnostyczne wyjście ze wszystkimi wewnętrznymi operacjami, w tym ładowaniem modelu i wykonaniem post‑procesora.

```csharp
// Step 3: Initialise the AsposeAI engine with the logger
AsposeAI ai = new AsposeAI(logger);
```

Konstruktor `AsposeAI` przyjmuje instancję `ILogger`. Jeśli w kroku 1 podałeś `null`, silnik działa w trybie cichym.

## Step 4: Create the built‑in spell‑check post‑processor

Aspose AI udostępnia gotowy komponent sprawdzający pisownię, który działa bezpośrednio na wynikach OCR. Jego instancjowanie nie wymaga żadnej konfiguracji.

```csharp
// Step 4: Create the built‑in spell‑check post‑processor
SpellCheckAIProcessor spellChecker = new SpellCheckAIProcessor();
```

`SpellCheckAIProcessor` implementuje interfejs `IAIProcessor`, co pozwala zarejestrować go razem z konfiguracją modelu.

## Step 5: Register the spell‑check processor together with the model configuration

Połączenie procesora z silnikiem zapewnia, że wyniki OCR automatycznie przechodzą przez etap sprawdzania pisowni.

```csharp
// Step 5: Register the spell‑check processor together with the model configuration
ai.SetPostProcessor(spellChecker, modelConfig);
```

`SetPostProcessor` wiąże `spellChecker` z `modelConfig`. Gdy później wywołasz `RunPostprocessor`, silnik uruchomi logikę sprawdzania pisowni przy użyciu pobranego modelu.

## Step 6: Execute the post‑processor on previously obtained OCR results

Zakładając, że masz już wynik OCR zapisany w zmiennej `ocrResult`, wywołaj post‑procesor, aby uzyskać poprawiony tekst.

```csharp
// Step 6: Execute the post‑processor on previously obtained OCR results (variable `ocrResult`)
ai.RunPostprocessor(ocrResult);
```

`RunPostprocessor` przetwarza każdą stronę `ocrResult`. Algorytm sprawdzania pisowni analizuje ciągi rozpoznane, stosuje słowniki specyficzne dla języka i generuje skorygowaną wersję.

## Step 7: Retrieve and display the corrected text

Po przetworzeniu `SpellCheckAIProcessor` przechowuje wyczyszczone wyniki. Możesz je pobrać i wyświetlić w konsoli.

```csharp
// Step 7: Retrieve and display the corrected text
Console.WriteLine("CORRECTED RESULT\n");
Console.WriteLine(spellChecker.GetResult()[0].RecognitionText);
```

Pierwszy element `GetResult()` odpowiada pierwszej stronie dokumentu OCR. Jeśli przetwarzałeś plik wielostronicowy, iteruj kolekcję, aby wyświetlić poprawiony tekst każdej strony.

## Step 8: Clean up resources when finished

Zwolnienie instancji `AsposeAI` zwalnia zasoby niezarządzane i zamyka otwarte uchwyty plików.

```csharp
// Clean up resources when finished
ai.Dispose();
```

Wywołanie `Dispose` jest dobrą praktyką dla każdego obiektu implementującego `IDisposable`, szczególnie przy pracy z bibliotekami natywnymi.

## Expected output

Gdy program zakończy się pomyślnie, zobaczysz wyjście podobne do poniższego:

```
CORRECTED RESULT

The quick brown fox jumps over the lazy dog.
```

Powyższy tekst odzwierciedla oryginalny input OCR z naprawionymi błędami ortograficznymi dzięki post‑procesorowi sprawdzającemu pisownię.

## Common questions and edge cases

**Co jeśli wynik OCR jest pusty?**  
Post‑procesor elegancko obsługuje puste strony i zwraca pusty ciąg. Żadne wyjątki nie są rzucane.

**Czy mogę użyć własnego słownika?**  
`SpellCheckAIProcessor` akceptuje opcjonalną właściwość `CustomDictionaryPath`. Ustaw ją przed wywołaniem `SetPostProcessor`, jeśli potrzebujesz terminów specyficznych dla domeny.

**Czy logger konsoli jest bezpieczny wątkowo?**  
`ConsoleLogger` zapisuje do `Console.Out`, które jest synchronizowane przez środowisko .NET. W scenariuszach o wysokiej przepustowości możesz zastąpić go loggerem buforującym komunikaty.

**Co jeśli muszę przetwarzać wiele dokumentów jednocześnie?**  
Utwórz osobną instancję `AsposeAI` dla każdego wątku lub użyj wzorca puli wątkowo‑bezpiecznej. Udostępnianie jednej instancji może prowadzić do wyścigów, ponieważ wewnętrzny stan modelu nie jest lokalny dla wątku.

## Conclusion

Teraz wiesz, jak **utworzyć logger konsoli** w C# i zintegrować **post‑procesor sprawdzający pisownię OCR**, aby **poprawić tekst OCR**. Kompletny przepływ pracy — od inicjalizacji loggera, przez konfigurację modelu, przetwarzanie i czyszczenie — obejmuje wszystkie niezbędne kroki dla solidnego potoku korekcji OCR.

Następnie rozważ rozszerzenie tego potoku o dodatkowe post‑procesory, takie jak wykrywanie języka czy ekstrakcja encji. Możesz także eksperymentować z alternatywnymi frameworkami logowania, takimi jak Serilog, aby uzyskać bogatsze dane diagnostyczne. Szczęśliwego kodowania!

## What Should You Learn Next?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne, działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak wyodrębnić tekst z obrazu przy użyciu Aspose.OCR dla .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Wyodrębnianie tekstu z obrazu w C# z wyborem języka przy użyciu Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Jak stworzyć przeszukiwalny PDF przy użyciu przetwarzania wsadowego Aspose OCR – przewodnik C#](/ocr/english/net/ocr-optimization/create-searchable-pdf-with-batch-ocr-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}