---
date: 2025-12-22
description: Dowiedz się, jak wyodrębnić tekst z obrazu przy użyciu Aspose.OCR dla
  .NET. Ten przewodnik przeprowadzi Cię przez przygotowywanie prostokątów do rozpoznawania
  obrazu OCR i zwiększanie dokładności.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Jak wyodrębnić tekst z obrazu, przygotowując prostokąty w OCR
url: /pl/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Przygotowanie prostokątów w rozpoznawaniu obrazu OCR

## Wprowadzenie

Rozpoznawanie znaków optycznych (OCR) jest niezbędne do konwertowania treści wizualnych na tekst możliwy do przeszukiwania i edycji. W tym samouczku **wyodrębnisz tekst z obrazu** przygotowując własne prostokąty, które skupiają silnik OCR na określonych obszarach. Korzystając z Aspose.OCR dla .NET, przeprowadzimy Cię przez każdy krok — od konfiguracji projektu po pobranie rozpoznanego tekstu — abyś mógł zintegrować potężną funkcję konwersji obrazu na tekst w swoich aplikacjach .NET.

## Szybkie odpowiedzi
- **Co oznacza „wyodrębnić tekst z obrazu”?** Oznacza to konwersję widocznych znaków na zdjęciu na ciągi znaków czytelne dla maszyny.  
- **Która biblioteka pomaga w tym w .NET?** Aspose.OCR dla .NET.  
- **Czy potrzebna jest licencja do rozwoju?** Darmowa wersja próbna działa do testów; licencja jest wymagana w produkcji.  
- **Czy mogę celować w określone obszary?** Tak, definiując prostokąty ograniczające zakres OCR.  
- **Jakie wersje .NET są obsługiwane?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Co to jest „wyodrębnić tekst z obrazu” przy użyciu prostokątów?
Kiedy definiujesz prostokątne strefy na obrazie, silnik OCR przetwarza tylko te obszary. Poprawia to dokładność, skraca czas przetwarzania i pozwala pominąć zaszumione tła lub nieistotne sekcje.

## Dlaczego przygotować prostokąty przed OCR?
- **Skup się na istotnej treści:** Pomijaj nagłówki, stopki lub elementy dekoracyjne.  
- **Zwiększ wydajność:** Mniejsze obszary oznaczają szybsze rozpoznawanie.  
- **Popraw dokładność:** Mniej szumu wizualnego prowadzi do czystszych wyników.

## Wymagania wstępne

- Znajomość C# i programowania w .NET.  
- Biblioteka Aspose.OCR dla .NET zainstalowana – możesz ją pobrać **[tutaj](https://releases.aspose.com/ocr/net/)**.  
- Przykładowy obraz (np. `sample.png`) zawierający tekst, który chcesz wyodrębnić.

## Importowanie przestrzeni nazw

Najpierw wprowadź wymagane przestrzenie nazw do zakresu:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Krok 1: Konfiguracja katalogu dokumentów

Określ, gdzie znajdują się pliki obrazów i utwórz instancję silnika OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Jak wyodrębnić tekst z obrazu przy użyciu wielu prostokątów

### Krok 2: Rozpoznawanie obrazu przy użyciu wielu prostokątów

#### 2.1 Definiowanie prostokątów

Utwórz listę obiektów `Rectangle`, które określają obszary, które ma skanować silnik OCR.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 Wykonaj rozpoznanie OCR

Przekaż ścieżkę do obrazu oraz listę prostokątów do `RecognizeImage`. Metoda zwraca kolekcję ciągów znaków — każdy element odpowiada jednemu prostokątowi.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### Krok 3: Rozpoznawanie obrazu z ustawieniami rozpoznawania (alternatywne podejście)

Jeśli wolisz używać `RecognitionSettings`, możesz uzyskać ten sam wynik przy nieco innym wywołaniu API.

#### 3.1 Definiowanie ustawień rozpoznania

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Wyświetlanie rozpoznanego tekstu

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Typowe problemy i wskazówki

- **Nieprawidłowe współrzędne prostokąta:** Upewnij się, że wartości `X`, `Y`, `Width` i `Height` prawidłowo odzwierciedlają żądany region.  
- **Jakość obrazu:** Obrazy o niskiej rozdzielczości mogą dawać słabe wyniki OCR; rozważ wstępne przetwarzanie (np. binaryzację).  
- **Puste wyniki:** Sprawdź, czy prostokąty rzeczywiście zawierają tekst; w przeciwnym razie silnik zwróci puste ciągi.

## Podsumowanie

Teraz wiesz, jak **wyodrębnić tekst z obrazu** przygotowując własne prostokąty przy użyciu Aspose.OCR dla .NET. Ta technika daje Ci precyzyjną kontrolę nad przetwarzaniem OCR, pomagając tworzyć szybsze i dokładniejsze funkcje wyodrębniania tekstu w Twoich aplikacjach.

## Najczęściej zadawane pytania

**P:** Czy mogę używać Aspose.OCR dla .NET z innymi frameworkami .NET?  
**O:** Tak, Aspose.OCR dla .NET jest kompatybilny z różnymi frameworkami .NET.

**P:** Czy dostępna jest darmowa wersja próbna Aspose.OCR dla .NET?  
**O:** Oczywiście! Darmową wersję próbną możesz uzyskać **[tutaj](https://releases.aspose.com/)**.

**P:** Jak uzyskać wsparcie dla Aspose.OCR dla .NET?  
**O:** Odwiedź **[forum Aspose.OCR](https://forum.aspose.com/c/ocr/16)**, aby uzyskać dedykowane wsparcie.

**P:** Czy mogę uzyskać tymczasową licencję do celów testowych?  
**O:** Tak, tymczasową licencję możesz nabyć **[tutaj](https://purchase.aspose.com/temporary-license/)**.

**P:** Gdzie mogę znaleźć dokumentację Aspose.OCR dla .NET?  
**O:** Dokumentacja jest dostępna **[tutaj](https://reference.aspose.com/ocr/net/)**.

---

**Last Updated:** 2025-12-22  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}