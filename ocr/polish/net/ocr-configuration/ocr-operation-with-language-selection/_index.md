---
title: Operacja OCRO z wyborem języka w rozpoznawaniu obrazu OCR
linktitle: Operacja OCRO z wyborem języka w rozpoznawaniu obrazu OCR
second_title: Aspose.OCR .NET API
description: Odblokuj potężne możliwości OCR dzięki Aspose.OCR dla .NET. Płynnie wyodrębniaj tekst z obrazów.
weight: 12
url: /pl/net/ocr-configuration/ocr-operation-with-language-selection/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Operacja OCRO z wyborem języka w rozpoznawaniu obrazu OCR

## Wstęp

W świecie rozpoznawania obrazów i optycznego rozpoznawania znaków (OCR) Aspose.OCR dla .NET wyróżnia się jako potężne narzędzie dla programistów poszukujących dokładnego i wydajnego wyodrębniania tekstu z obrazów. Ten przewodnik krok po kroku przeprowadzi Cię przez proces rozpoznawania obrazu OCR przy użyciu Aspose.OCR dla .NET, koncentrując się na operacji z wyborem języka.

## Warunki wstępne

Zanim zagłębimy się w samouczek, upewnij się, że spełniasz następujące wymagania wstępne:

-  Aspose.OCR dla .NET: Upewnij się, że masz zainstalowaną bibliotekę Aspose.OCR. Można go pobrać z[Strona pobierania Aspose.OCR dla .NET](https://releases.aspose.com/ocr/net/).

- Środowisko programistyczne: skonfiguruj środowisko pracy z aplikacją .NET. Jeśli jeszcze tego nie zrobiłeś, zapoznaj się z sekcją[dokumentacja](https://reference.aspose.com/ocr/net/) szczegółowe instrukcje.

## Importuj przestrzenie nazw

W aplikacji .NET zacznij od zaimportowania niezbędnych przestrzeni nazw:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Krok 1: Zainicjuj Aspose.OCR

Rozpocznij od zainicjowania instancji klasy Aspose.OCR. To przygotowuje grunt pod wykorzystanie możliwości OCR w Twojej aplikacji.

```csharp
// ExStart:1
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";

// Zainicjuj instancję AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Krok 2: Określ ścieżkę obrazu

Następnie zdefiniuj ścieżkę do obrazu, na którym chcesz wykonać OCR. Upewnij się, że obraz jest dostępny z poziomu aplikacji.

```csharp
//Ścieżka obrazu
string fullPath = dataDir + "sample.png";
```

## Krok 3: Rozpoznaj obraz za pomocą wyboru języka

Teraz następuje podstawowa operacja OCR. Skorzystaj z biblioteki Aspose.OCR, aby rozpoznać tekst z określonego obrazu. Dostosuj ustawienia rozpoznawania, w tym wybór języka.

```csharp
// Rozpoznaj obraz
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Wybierz język: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Krok 4: Wydrukuj i wyświetl wyniki

Po operacji OCR wydrukuj i wyświetl wyniki, w tym rozpoznany tekst, obszary, ostrzeżenia i reprezentację JSON.

```csharp
// Wydrukuj wynik
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// RozwińKoniec:1
```

## Wniosek

Gratulacje! Pomyślnie wykonałeś rozpoznawanie obrazu OCR z wyborem języka przy użyciu Aspose.OCR dla .NET. W tym samouczku przedstawiono podstawowe kroki wyodrębniania tekstu z obrazów i podkreślono elastyczność opcji językowych.

## Często zadawane pytania

### P1: Czy Aspose.OCR nadaje się do rozpoznawania tekstu wielojęzycznego?

Odpowiedź 1: Tak, Aspose.OCR obsługuje różne języki, zapewniając elastyczność wielojęzycznych zadań OCR.

### P2: Czy mogę dostosować ustawienia OCR do określonych cech obrazu?

A2: Absolutnie! Dostosuj parametry, takie jak kąt pochylenia, rozpoznawanie linii i wykrywanie obszaru, aby zoptymalizować OCR dla różnych scenariuszy.

### P3: Gdzie mogę znaleźć dodatkowe wsparcie lub dyskusje społeczności?

 A3: Odwiedź[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) za wsparcie i dyskusję ze społecznością.

### P4: Czy dostępny jest bezpłatny okres próbny?

 A4: Tak, poznaj[bezpłatna wersja próbna](https://releases.aspose.com/) aby doświadczyć możliwości Aspose.OCR.

### P5: Jak mogę kupić Aspose.OCR dla .NET?

 O5: Aby dokonać zakupu, odwiedź stronę[strona zakupu](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
