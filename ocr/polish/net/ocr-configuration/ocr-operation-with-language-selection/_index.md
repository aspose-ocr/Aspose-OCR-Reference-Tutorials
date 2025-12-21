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

# Jak wykonać OCR z wyborem języka w Aspose.OCR

## Introduction

Jeśli potrzebujesz **jak wykonać OCR** na obrazach i wyodrębnić tekst z plików obrazów w aplikacji .NET, Aspose.OCR for .NET zapewnia szybkie, dokładne i świadome językowo rozwiązanie. W tym samouczku przeprowadzimy rzeczywisty przykład, który demonstruje rozpoznawanie obrazów OCR z wyborem języka, abyś mógł wyciągać wielojęzyczny tekst ze zdjęć przy użyciu kilku linii kodu.

## Quick Answers
- **Co robi Aspose.OCR?** Rozpoznaje drukowany i odręczny tekst na obrazach i zwraca wyodrębniony tekst.  
- **Czy mogę wybrać język?** Tak – możesz określić dowolny obsługiwany język, taki jak English, German, Spanish, Chinese, itp.  
- **Czy potrzebuję licencji do rozwoju?** Darmowa wersja próbna działa do oceny; licencja jest wymagana w środowisku produkcyjnym.  
- **Jakie wersje .NET są obsługiwane?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Czy korekcja pochylenia jest automatyczna?** Możesz włączyć `AutoSkew` i precyzyjnie dostroić ustawienie `SkewAngle`.

## Why Choose Aspose.OCR for OCR Tasks?

- **Wysoka dokładność** w różnych czcionkach i jakościach obrazu.  
- **Wbudowany wybór języka** eliminuje potrzebę zewnętrznych pakietów językowych.  
- **Proste API**, które łatwo integruje się z istniejącymi projektami C#.  
- **Brak zewnętrznych zależności** – wszystko działa lokalnie, zapewniając bezpieczeństwo danych.

## Prerequisites

Zanim przejdziemy do kodu, upewnij się, że masz następujące wymagania wstępne:

- Aspose.OCR for .NET: Upewnij się, że masz zainstalowaną bibliotekę Aspose.OCR. Możesz ją pobrać ze [strony pobierania Aspose.OCR for .NET](https://releases.aspose.com/ocr/net/).

- Środowisko programistyczne: Skonfiguruj środowisko pracy z aplikacją .NET. Jeśli jeszcze tego nie zrobiłeś, odwołaj się do [dokumentacji](https://reference.aspose.com/ocr/net/) po szczegółowe instrukcje.

## Import Namespaces

W swojej aplikacji .NET rozpocznij od zaimportowania niezbędnych przestrzeni nazw:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Step 1: Initialize Aspose.OCR

Rozpocznij od zainicjowania instancji klasy Aspose.OCR. To przygotowuje środowisko do wykorzystania możliwości OCR w Twojej aplikacji.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Step 2: Specify Image Path

Następnie określ ścieżkę do obrazu, na którym chcesz wykonać OCR. Upewnij się, że obraz jest dostępny z Twojej aplikacji.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Step 3: Recognize Image with Language Selection

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

## Step 4: Print and Display Results

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

## Common Issues and Tips

- **Nieprawidłowy wybór języka** – Jeśli wynik jest zniekształcony, sprawdź ponownie, czy właściwość `Language` odpowiada językowi obrazu źródłowego.  
- **Obrazy nachylone** – Włącz `AutoSkew` lub ręcznie dostosuj `SkewAngle`, aby uzyskać lepszą dokładność przy skanach pod kątem.  
- **Duże pliki** – Przetwarzaj duże obrazy w częściach lub zmniejsz rozdzielczość przed przekazaniem ich do `RecognizeImage`, aby oszczędzić pamięć.

## Conclusion

Gratulacje! Nauczyłeś się **jak wykonać OCR** z wyborem języka przy użyciu Aspose.OCR dla .NET. Ten samouczek pokazał, jak wyodrębniać tekst z plików obrazów, dostosowywać ustawienia rozpoznawania i bezproblemowo obsługiwać wielojęzyczną zawartość.

## FAQ's

### Q1: Is Aspose.OCR suitable for multilingual text recognition?

### P1: Czy Aspose.OCR nadaje się do rozpoznawania tekstu wielojęzycznego?

A1: Tak, Aspose.OCR obsługuje różne języki, zapewniając elastyczność w zadaniach OCR wielojęzycznych.

### Q2: Can I fine‑tune OCR settings for specific image characteristics?

### P2: Czy mogę precyzyjnie dostroić ustawienia OCR do konkretnych cech obrazu?

A2: Oczywiście! Dostosuj parametry takie jak kąt pochylenia, rozpoznawanie linii i wykrywanie obszarów, aby zoptymalizować OCR w różnych scenariuszach.

### Q3: Where can I find additional support or community discussions?

### P3: Gdzie mogę znaleźć dodatkowe wsparcie lub dyskusje społeczności?

A3: Odwiedź [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16), aby uzyskać wsparcie i dyskusje ze społecznością.

### Q4: Is there a free trial available?

### P4: Czy dostępna jest darmowa wersja próbna?

A4: Tak, wypróbuj [darmową wersję próbną](https://releases.aspose.com/), aby poznać możliwości Aspose.OCR.

### Q5: How can I purchase Aspose.OCR for .NET?

### P5: Jak mogę zakupić Aspose.OCR dla .NET?

A5: Aby dokonać zakupu, odwiedź [stronę zakupu](https://purchase.aspose.com/buy).

---

**Last Updated:** 2025-12-21  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}