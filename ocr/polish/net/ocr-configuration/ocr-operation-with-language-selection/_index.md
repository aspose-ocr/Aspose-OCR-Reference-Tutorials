---
date: 2025-12-21
description: Dowiedz się, jak wykonać OCR i wyodrębnić tekst z obrazu przy użyciu
  Aspose.OCR dla .NET. Ten przewodnik krok po kroku pokazuje rozpoznawanie tekstu
  wielojęzycznego oraz wybór języka.
linktitle: How to Perform OCR with Language Selection in Aspose.OCR
second_title: Aspose.OCR .NET API
title: Jak wykonać OCR z wyborem języka w Aspose.OCR
url: /pl/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak przygotować OCR z użyciem języka w Aspose.OCR

## Wstęp

Jeśli **jak wykonać OCR** ​​na obrazach i wyodrębnić tekst z plików obrazów w aplikacji .NET, Aspose.OCR dla .NET zapewnia szybkie, szczegółowe i świadome językowo rozwiązanie. W tym samouczku przeprowadziliśmy przykład, który demonstruje rozpoznawanie obrazów OCR z języka, umożliwiając korzystanie z wielojęzycznego tekstu ze zdjęć przy użyciu kilku linii kodu.

## Szybkie odpowiedzi
- **Co robi Aspose.OCR?** Rozpoznaje drukowany i odręczny tekst na obrazach i wyodrębniony tekst.
- **Czy mogę wybrać język?** Tak – można określić dowolny język taki, jak angielski, niemiecki, hiszpański, chiński, itp.
- **Czy dostępna jest wersja do rozwoju?** Wersja próbna działa do oceny; licencjat jest wymagany w środowisku produkcyjnym.
- **Jakie wersje .NET są pobierane?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.
- **Czy korekcja pochylenia jest automatyczna?** Można włączyć `AutoSkew` i precyzyjnie dostroić ustawienie `SkewAngle`.

## Dlaczego warto wybrać Aspose.OCR do zadań OCR?

- **Wysoka inna** w różnych czcionkach i jakościach obrazu.
- **Wbudowany wybór języka** dotyczący stosowania zewnętrznych pakietów językowych.
- **Proste API**, które łatwo integruje się z realizowanymi projektami C#.
- **Brak zewnętrznego zależności** – wszystko działa lokalnie, bezpieczeństwo danych.

## Warunki wstępne

Zanim przejdziemy do kodu, sprawdź się, że masz szczegółowe wymagania wstępne:

- Aspose.OCR dla .NET: obciążenie się, że masz zainstalowaną bibliotekę Aspose.OCR. Możesz ją zabrać ze [strony pobierania Aspose.OCR for .NET](https://releases.aspose.com/ocr/net/).

- Środowisko programistyczne: Skonfiguruj środowisko pracy z aplikacją .NET. Jeśli jeszcze tego nie zrobiłeś, zastosuj się do [dokumentacji](https://reference.aspose.com/ocr/net/) po szczegółowe instrukcje.

## Importuj przestrzenie nazw

W swojej aplikacji .NET rozpocznij od zaimportowania otwartej przestrzeni nazw:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Krok 1: Zainicjuj Aspose.OCR

Rozpocznij od zainicjowania instancji klasy Aspose.OCR. To przygotowuje środowisko do wykorzystania możliwości OCR w Twojej aplikacji.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Krok 2: Określ ścieżkę do obrazu

Następnie określ ścieżkę do obrazu, na którym chcesz wykonać OCR. Upewnij się, że obraz jest dostępny z Twojej aplikacji.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Krok 3: Rozpoznaj obraz z wyborem języka

Teraz następuje podstawowa operacja OCR. Skorzystaj z biblioteki Aspose.OCR, aby rozpoznać tekst z określonego obrazu. Dostosuj ustawienia rozpoznawania, w tym wybór języka.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Krok 4: Wydrukuj i wyświetl wyniki

Po operacji OCR wydrukuj i wyświetl wyniki, w tym rozpoznany tekst, obszary, ostrzeżenia oraz reprezentację w formacie JSON.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## Typowe problemy i wskazówki

- **Nieprawidłowy wybór języka** – Jeśli wynik jest zniekształcony, sprawdź ponownie, czy zalecany `Language` odpowiada językowi obrazu źródłowego.
- **Obrazy nachylone** – Włącz `AutoSkew` lub widoczne dostosuj `SkewAngle`, aby uzyskać znaczenie przy skanach pod kątem.
- **Duże pliki** – Przetwarzaj duże obrazy w części lub zmniejszona rozdzielczość przed ich udostępnieniem do `RecognizeImage`, aby zaoszczędzić pamięć.

## Wniosek

Gratulacje! Nauczyłeś się **jak wykonać OCR** z wyborem języka przy użyciu Aspose.OCR dla .NET. Ten samouczek pokazał, jak wyodrębniać tekst z plików obrazów, dostosowywać ustawienia rozpoznawania i bezproblemowo obsługiwać wielojęzyczną zawartość.

## FAQ's

### P1: Czy Aspose.OCR nadaje się do rozpoznawania tekstu wielojęzycznego?

A1: Tak, Aspose.OCR obsługuje różne języki, zapewniając elastyczność w zadaniach OCR wielojęzycznych.

### P2: Czy mogę precyzyjnie dostroić ustawienia OCR do konkretnych cech obrazu?

A2: Oczywiście! Dostosuj parametry takie jak kąt pochylenia, rozpoznawanie linii i wykrywanie obszarów, aby zoptymalizować OCR w różnych scenariuszach.

### P3: Gdzie mogę znaleźć dodatkowe wsparcie lub dyskusje społeczności?

A3: Odwiedź [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16), aby uzyskać wsparcie i dyskusje ze społecznością.

### P4: Czy dostępna jest darmowa wersja próbna?

A4: Tak, wypróbuj [darmową wersję próbną](https://releases.aspose.com/), aby poznać możliwości Aspose.OCR.

### P5: Jak mogę zakupić Aspose.OCR dla .NET?

A5: Aby dokonać zakupu, odwiedź [stronę zakupu](https://purchase.aspose.com/buy).

---

**Ostatnia aktualizacja:** 2025-12-21
**Testowano z:** Aspose.OCR 24.11 dla .NET
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}