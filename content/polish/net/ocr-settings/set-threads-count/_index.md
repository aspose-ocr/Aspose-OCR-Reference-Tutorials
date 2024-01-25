---
title: Ustaw liczbę wątków w rozpoznawaniu obrazu OCR
linktitle: Ustaw liczbę wątków w rozpoznawaniu obrazu OCR
second_title: Aspose.OCR .NET API
description: Odblokuj efektywność OCR w .NET. Ustaw liczbę wątków bez wysiłku dzięki Aspose.OCR. Zwiększ dokładność i szybkość.
type: docs
weight: 11
url: /pl/net/ocr-settings/set-threads-count/
---
## Wstęp

Witamy w świecie Aspose.OCR dla .NET, gdzie najnowocześniejsza technologia optycznego rozpoznawania znaków (OCR) łączy się z bezproblemową integracją z aplikacjami .NET. W tym samouczku zajmiemy się konkretnym aspektem: ustawianiem liczby wątków w rozpoznawaniu obrazu OCR. Ta zaawansowana funkcja optymalizuje wydajność zadań OCR, zapewniając wydajność i dokładność.

## Warunki wstępne

Zanim wyruszymy w tę podróż, upewnijmy się, że spełniamy następujące warunki wstępne:

-  Aspose.OCR dla .NET: Upewnij się, że masz zainstalowaną bibliotekę. Jeśli nie, możesz go pobrać[Tutaj](https://releases.aspose.com/ocr/net/).

- Przykładowy obraz: Przygotuj przykładowy obraz w wyznaczonym katalogu dokumentów.

Przejdźmy teraz do schodów.

## Importuj przestrzenie nazw

Po pierwsze, pamiętaj o uwzględnieniu niezbędnych przestrzeni nazw w aplikacji .NET:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## Krok 1: Zainicjuj instancję Aspose.OCR

Teraz zainicjuj instancję klasy AsposeOcr w swojej aplikacji:

```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";

// Zainicjuj instancję AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Krok 2: Rozpoznaj obraz

Następnie rozpoznajmy tekst na obrazie, korzystając z określonej liczby wątków:

```csharp
// Rozpoznaj obraz
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    ThreadsCount = 2 // 0 - oznacza automatyczne obliczanie
});
```

## Krok 3: Wyświetl rozpoznany tekst

Po rozpoznaniu wyświetl rozpoznany tekst:

```csharp
// Wyświetl rozpoznany tekst
Console.WriteLine(result.RecognitionText);
```

## Wniosek

Podsumowując, ustawienie liczby wątków w rozpoznawaniu obrazu OCR przy użyciu Aspose.OCR dla .NET jest prostym procesem, który znacznie zwiększa wydajność. Eksperymentuj z różnymi liczbami wątków, aby znaleźć optymalne ustawienie dla swojej aplikacji.

## Często zadawane pytania

### P1: Czy mogę ustawić liczbę wątków na zero w celu automatycznego obliczenia?

 A1: Absolutnie! Ustawienie`ThreadsCount` na zero pozwala Aspose.OCR automatycznie obliczyć optymalną liczbę wątków.

### P2: Jak mogę uzyskać tymczasową licencję na Aspose.OCR dla .NET?

 A2: Odwiedź[ten link](https://purchase.aspose.com/temporary-license/) nabyć tymczasową licencję do celów testowych.

### P3: Gdzie mogę znaleźć obszerną dokumentację dla Aspose.OCR dla .NET?

 A3: Patrz[dokumentacja](https://reference.aspose.com/ocr/net/) aby uzyskać szczegółowe wskazówki dotyczące Aspose.OCR.

### P4: Czy dostępna jest bezpłatna wersja próbna Aspose.OCR dla .NET?

 Odpowiedź 4: Tak, możesz skorzystać z bezpłatnego okresu próbnego[Tutaj](https://releases.aspose.com/).

### P5: Potrzebujesz pomocy lub chcesz nawiązać kontakt ze społecznością?

 A5: Odwiedź[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) za wsparcie i interakcję społeczną.