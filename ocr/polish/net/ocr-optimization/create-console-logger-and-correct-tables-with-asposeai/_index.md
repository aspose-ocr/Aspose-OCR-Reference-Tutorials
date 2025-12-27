---
category: general
date: 2025-12-27
description: Utwórz logger konsoli w C# i włącz automatyczne pobieranie do poprawnych
  tabel przy użyciu AsposeAI. Dowiedz się, jak wyświetlić poprawiony wynik tabeli
  w kilku prostych krokach.
draft: false
keywords:
- create console logger
- enable auto download
- how to correct tables
- setup console logger
- display corrected table
language: pl
og_description: Utwórz logger konsoli w C# i włącz automatyczne pobieranie do właściwych
  tabel przy użyciu AsposeAI. Skorzystaj z tego przewodnika, aby szybko wyświetlić
  poprawiony wynik tabeli.
og_title: Utwórz logger konsoli i popraw tabele przy użyciu AsposeAI
tags:
- AsposeAI
- C#
- OCR
- Table processing
title: Utwórz logger konsoli i popraw tabele przy użyciu AsposeAI
url: /pl/net/ocr-optimization/create-console-logger-and-correct-tables-with-asposeai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz logger konsoli i popraw tabele przy użyciu AsposeAI

Czy kiedykolwiek potrzebowałeś **utworzyć logger konsoli** dla potoku AI w C#, ale nie wiedziałeś od czego zacząć? W tym przewodniku przejdziemy przez cały proces — jak utworzyć logger konsoli, włączyć automatyczne pobieranie plików modeli oraz w końcu **jak poprawić tabele** wyekstrahowane z OCR. Po zakończeniu będziesz mógł **wyświetlić poprawione wyniki tabel** w swojej konsoli przy użyciu kilku linii kodu.

Omówimy wszystko, od początkowej konfiguracji loggera po końcowe sprzątanie, więc nie będziesz musiał przeszukiwać rozproszonych dokumentów. Nie wymagana jest wcześniejsza znajomość AsposeAI; wystarczy podstawowa wiedza o C# i .NET. Po drodze podzielimy się wskazówkami dotyczącymi **setup console logger** najlepszych praktyk, omówimy przypadki brzegowe i pokażemy, jak powinien wyglądać wynik.

---

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod używa nowoczesnych funkcji językowych)
- Visual Studio 2022 lub dowolne IDE obsługujące projekty C#
- Pakiet NuGet **Aspose.AI** zainstalowany (`Install-Package Aspose.AI`)
- Pakiet NuGet **Aspose.OCR** zainstalowany (`Install-Package Aspose.OCR`)
- Przykładowy obiekt wyniku OCR (`ocrResult`) z wcześniejszego wywołania Aspose.OCR

Jeśli którekolwiek z nich brakuje, zatrzymaj się teraz i je zdobądź — podziękujesz sobie później.

---

## Krok 1: Utwórz logger konsoli i zainicjalizuj AsposeAI

Pierwszą rzeczą, której potrzebujemy, jest logger zapisujący bezpośrednio do konsoli. To ułatwia debugowanie i zapewnia bieżące informacje zwrotne podczas działania silnika AI.

```csharp
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

// Step 1: Create a logger that writes to the console
ILogger consoleLogger = new ConsoleLogger();

// Step 2: Initialise the AsposeAI engine with the logger
AsposeAI asposeAI = new AsposeAI(consoleLogger);
```

**Dlaczego to ważne:**  
`ConsoleLogger` implementuje interfejs `ILogger`, więc wszystkie wewnętrzne komunikaty z AsposeAI (ładowanie modelu, status post‑processora, błędy) pojawiają się natychmiast w twoim terminalu. To najprostszy sposób na **setup console logger** bez używania zewnętrznych frameworków logowania.

> **Wskazówka:** Jeśli później będziesz potrzebował logowania do pliku, po prostu zamień `ConsoleLogger` na własnyujący `ILogger` — reszta kodu pozostaje niezmieniona.

---

## Krok 2: Włącz automatyczne pobieranie modeli AI

AsposeAI może pobierać wymagane pliki modeli w locie. Włączenie tej opcji oszczędza ręczne pobieranie dużych plików binarnych.

```csharp
// Step 3: (Optional) Configure automatic model download and set the model directory
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,               // <‑‑ enable auto download
    DirectoryModelPath = "YOUR_DIRECTORY"   // change to a writable folder
};
```

**Co może pójść nie tak?**  
Jeśli `DirectoryModelPath` wskazuje na lokalizację tylko do odczytu, automatyczne pobieranie zakończy się niepowodzeniem i zobaczysz wyjątek w konsoli. Upewnij się, że folder istnieje i aplikacja ma uprawnienia do zapisu.

---

## Krok 3: Utwórz post‑procesor tabel (jak poprawić tabele)

Tabele wyodrębnione z OCR są często nieuporządkowane — scalone komórki, brakujące obramowania lub nieprawidłowo wyrównany tekst. `TableAIProcessor` z AsposeAI może je automatycznie wyczyścić.

```csharp
// Step 4: Create a table post‑processor that lets the engine decide when to run correction
TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);
```

**Dlaczego tryb AUTO?**  
`AITableDetectionMode.AUTO` pozwala silnikowi przeanalizować wynik OCR i zdecydować, czy korekta jest potrzebna. Jeśli wolisz ręczną kontrolę, możesz użyć `MANUAL` i samodzielnie wywołać `RunCorrection()`.

---

## Krok 4: Dołącz post‑procesor i jego konfigurację

Teraz łączymy wszystko razem — logger, konfigurację modelu i procesor tabel.

```csharp
// Step 5: Attach the post‑processor and its configuration to the AI engine
asposeAI.SetPostProcessor(tableProcessor, modelConfig);
```

W tym momencie silnik AI wie, *gdzie* przechowywać modele, *jak* logować i *jakie* post‑procesowanie zastosować. To czyste rozdzielenie odpowiedzialności, które ułatwia przyszłe zmiany.

---

## Krok 5: Uruchom post‑procesor na wyniku OCR

Zakładając, że masz już `ocrResult` z Aspose.OCR, po prostu przekaż go silnikowi.

```csharp
// Step 6: Run the post‑processor on the OCR result returned by Aspose.OCR
asposeAI.RunPostprocessor(ocrResult);
```

**Uwaga na przypadek brzegowy:**  
Jeśli `ocrResult` nie zawiera tabel, procesor po cichu pominie korektę. Możesz później sprawdzić `tableProcessor.GetResult().Count`, aby zweryfikować, czy coś faktycznie zostało przetworzone.

---

## Krok 6: Pobierz i **wyświetl poprawiony wynik tabeli**

Na koniec pobierzmy wyczyszczony tekst tabeli i wydrukujmy go w konsoli.

```csharp
// Step 7: Retrieve and display the corrected table text
Console.WriteLine("Corrected table output:");
Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
```

Wyjście będzie wyglądało mniej więcej tak (w zależności od obrazu źródłowego):

```
Corrected table output:
| Item   | Quantity | Price |
|--------|----------|-------|
| Apple  | 10       | $1.20 |
| Banana | 5        | $0.80 |
```

Jeśli zobaczysz pusty ciąg znaków, sprawdź ponownie, czy OCR rzeczywiście wykryło tabelę i czy `AllowAutoDownload` powiodło się.

---

## Krok 7: Posprzątaj zasoby

Dobre obywatelstwo oznacza zwalnianie ciężkich obiektów po zakończeniu pracy.

```csharp
// Step 8: Release resources used by the AI engine
asposeAI.Dispose();
```

Pomijanie tego kroku może pozostawić otwarte uchwyty plików, szczególnie w Windows, gdzie pliki modeli pozostają zablokowane.

---

## Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do nowego projektu konsolowego. Zamień `"YOUR_DIRECTORY"` na rzeczywistą ścieżkę i upewnij się, że `ocrResult` jest wypełniony przed wywołaniem `RunPostprocessor`.

```csharp
using System;
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

namespace AsposeAITableCorrection
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a console logger
            ILogger consoleLogger = new ConsoleLogger();

            // 2️⃣ Initialise AsposeAI with the logger
            AsposeAI asposeAI = new AsposeAI(consoleLogger);

            // 3️⃣ Configure auto‑download (optional but recommended)
            AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
            {
                AllowAutoDownload = true,
                DirectoryModelPath = @"C:\AsposeModels" // <-- change this
            };

            // 4️⃣ Create the table processor (auto‑detect mode)
            TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);

            // 5️⃣ Attach processor and config
            asposeAI.SetPostProcessor(tableProcessor, modelConfig);

            // 6️⃣ Obtain OCR result (replace with your own OCR call)
            // Example placeholder – you should have this from Aspose.OCR already
            OcrResult ocrResult = GetOcrResultSomehow();

            // 7️⃣ Run post‑processor on the OCR output
            asposeAI.RunPostprocessor(ocrResult);

            // 8️⃣ Display corrected table
            Console.WriteLine("Corrected table output:");
            if (tableProcessor.GetResult().Count > 0)
            {
                Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
            }
            else
            {
                Console.WriteLine("No tables were detected or corrected.");
            }

            // 9️⃣ Clean up
            asposeAI.Dispose();
        }

        // Dummy method – replace with your actual OCR logic
        static OcrResult GetOcrResultSomehow()
        {
            // For illustration only
            OcrEngine engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample-table.png");
            return engine.Recognize();
        }
    }
}
```

**Oczekiwany wynik w konsoli** (zakładając prosty obraz tabeli):

```
Corrected table output:
| Name   | Age | City      |
|--------|-----|-----------|
| Alice  | 30  | New York  |
| Bob    | 25  | Seattle   |
```

---

## Częste pytania i odpowiedzi

- **Czy potrzebuję połączenia z internetem do automatycznego pobierania?**  
  Tak. Przy pierwszym żądaniu modelu AsposeAI łączy się z jego CDN. Po zapisaniu pliku w `DirectoryModelPath` kolejne uruchomienia działają offline.

- **Co jeśli moja tabela ma scalone komórki?**  
  Model AI próbuje podzielić scalone komórki na podstawie wskazówek wizualnych. Jeśli wynik jest niepoprawny, rozważ wstępne przetworzenie obrazu (zwiększenie kontrastu, prostowanie obrotu) przed OCR.

- **Czy mogę przetwarzać wiele tabel jednocześnie?**  
  Oczywiście. `tableProcessor.GetResult()` zwraca listę; iteruj po niej, aby wydrukować każdą tabelę.

- **Czy `ConsoleLogger` jest bezpieczny wątkowo?**  
  Zapisuje bezpośrednio do `System.Console`, co jest bezpieczne wątkowo przy prostych zapisach. W przypadku intensywnych scenariuszy wielowątkowych lepszy może być własny logger z synchronizacją.

---

## Kolejne kroki i powiązane tematy

Teraz, gdy wiesz **jak poprawić tabele**, możesz chcieć:

- **Włączyć automatyczne pobieranie** dla innych modeli AsposeAI (np. tłumaczenia językowego).
- **Ustawić logger konsoli** z różnymi poziomami logowania (Info, Warning, Error) dla większej kontroli.
- Zbadać **wyświetlanie poprawionej tabeli** w interfejsie GUI (WinForms lub WPF) zamiast w konsoli.
- Połączyć korektę tabel z **ekstrakcją danych**, aby bezpośrednio wprowadzać je do bazy danych.

Każdy z tych elementów opiera się na fundamentach, które właśnie zbudowaliśmy, więc śmiało eksperymentuj.

---

## Zakończenie

Przeszliśmy przez cały cykl życia **tworzenia loggera konsoli**, włączania automatycznego pobierania i **korekcji tabel** przy użyciu AsposeAI, kończąc czystym sposobem na **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}