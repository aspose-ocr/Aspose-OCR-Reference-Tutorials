---
date: 2026-05-24
description: Dowiedz się, jak poprawić OCR, ustawiając dozwolone znaki w Aspose.OCR
  for .NET, co umożliwia dokładne rozpoznawanie cyfr i szybsze przetwarzanie. Postępuj
  zgodnie z przewodnikiem krok po kroku.
keywords:
- how to improve ocr
- set allowed characters
- recognize digits
- improve ocr accuracy
- extract serial numbers
linktitle: Jak poprawić OCR – Ustaw dozwolone znaki w Aspose.OCR for .NET
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Learn how to improve OCR by setting allowed characters with Aspose.OCR
    for .NET, enabling accurate digit recognition and faster processing. Follow a
    step‑by‑step guide.
  headline: How to Improve OCR – Set Allowed Characters with Aspose.OCR for .NET
  type: TechArticle
- description: Learn how to improve OCR by setting allowed characters with Aspose.OCR
    for .NET, enabling accurate digit recognition and faster processing. Follow a
    step‑by‑step guide.
  name: How to Improve OCR – Set Allowed Characters with Aspose.OCR for .NET
  steps:
  - name: Set the path to your image folder
    text: Define the folder that contains the sample images you want to process.
  - name: Initialize Aspose.OCR with a digit‑only whitelist
    text: '`AllowedCharacters` is a property that sets the whitelist of characters
      the OCR engine may recognize.'
  - name: Recognize a single line containing digits
    text: The `RecognizeLine` method scans the image and returns the best‑matching
      line that conforms to the whitelist.
  - name: Output the recognized digits
    text: Write the result to the console (or log) so you can verify the output instantly.
  - name: Use `RecognitionSettings` for more control
    text: '`RecognitionSettings` allows you to customize OCR parameters such as DPI,
      language packs, and processing mode.'
  - name: Confirm successful execution
    text: By following these steps, you’ve learned **how to improve OCR** accuracy
      by limiting the character set, and you can now reliably extract digit strings
      from images using Aspose.OCR for .NET.
  type: HowTo
- questions:
  - answer: It limits OCR to a predefined whitelist, dramatically increasing accuracy
      for targeted data sets.
    question: What does “specify allowed characters OCR” do?
  - answer: Any combination you need—digits (`0‑9`), uppercase letters, custom symbols,
      or a mix like “ABC‑123”.
    question: Which characters can I allow?
  - answer: Whitelisting reduces false recognitions by up to 70 % and speeds up processing
      by 30 % on average.
    question: Why limit characters?
  - answer: A free trial works for development; a commercial license is required for
      production deployments.
    question: Do I need a license?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: Which .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
title: Jak poprawić OCR – Ustaw dozwolone znaki w Aspose.OCR for .NET
url: /pl/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak poprawić OCR – Ustaw dozwolone znaki w Aspose.OCR dla .NET

W tym samouczku dowiesz się, **jak poprawić wyniki OCR** poprzez **określenie dozwolonych znaków** przy użyciu Aspose.OCR dla .NET. Ograniczenie silnika OCR do znanej białej listy — np. tylko cyfr — zwiększa dokładność, skraca czas przetwarzania i eliminuje niechciane symbole. Niezależnie od tego, czy wyodrębniasz numery seryjne, identyfikatory faktur czy odczyty liczników, poniższe kroki pozwolą zastosować tę technikę w kilka minut.

## Szybkie odpowiedzi
- **Co robi „specify allowed characters OCR”?** Ogranicza OCR do zdefiniowanej listy dozwolonych znaków, dramatycznie zwiększając dokładność dla określonych zestawów danych.  
- **Jakie znaki mogę zezwolić?** Dowolna kombinacja, której potrzebujesz — cyfry (`0‑9`), wielkie litery, własne symbole lub mieszanka, np. „ABC‑123”.  
- **Dlaczego ograniczać znaki?** Lista dozwolonych znaków zmniejsza liczbę błędnych rozpoznawań nawet o 70 % i przyspiesza przetwarzanie średnio o 30 %.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa w środowisku deweloperskim; licencja komercyjna jest wymagana w środowisku produkcyjnym.  
- **Jakie wersje .NET są wspierane?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Czy mogę łączyć to z pakietami językowymi?** Tak — połącz listę dozwolonych znaków z pakietem językowym, aby obsługiwać wielojęzyczne ciągi cyfr.

## Czym jest „specify allowed characters OCR”?

**Bezpośrednia odpowiedź:** Określenie dozwolonych znaków powoduje, że Aspose.OCR ignoruje każdy wzorzec wizualny, który nie pasuje do podanej listy znaków, więc silnik zwraca wyniki wyłącznie z tej listy. Takie podejście eliminuje szumy, podnosi wyniki pewności i zmniejsza nakład pracy po przetworzeniu. Dodatkowo przyspiesza proces rozpoznawania.

## Dlaczego używać Aspose.OCR do rozpoznawania obrazu cyfr?

**Bezpośrednia odpowiedź:** Wbudowana funkcja `AllowedCharacters` w Aspose.OCR pozwala rozpoznawać obrazy zawierające wyłącznie cyfry przy użyciu jednej linii kodu, zapewniając do 95 % dokładności przy skanach o niskiej rozdzielczości bez dodatkowej logiki filtrowania. Biblioteka obsługuje ponad 30 języków, przetwarza partie 500‑stronicowych obrazów w mniej niż 2 sekundy na stronę i działa całkowicie offline, co czyni ją idealną dla scenariuszy o wysokiej przepustowości i lokalnym wdrożeniu, takich jak odczyt liczników użyteczności czy ekstrakcja identyfikatorów faktur.

## Wymagania wstępne

- Podstawowe doświadczenie w programowaniu w .NET.  
- **Aspose.OCR for .NET** biblioteka – pobierz ją z oficjalnej strony **[tutaj](https://releases.aspose.com/ocr/net/)**.  
- Visual Studio 2019+ (lub dowolne kompatybilne IDE .NET).  

## Importowanie przestrzeni nazw

Poniższe przestrzenie nazw zapewniają dostęp do silnika OCR i jego ustawień:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## Jak poprawić OCR, określając dozwolone znaki?

`AsposeOcr` jest główną klasą silnika OCR dostarczaną przez bibliotekę Aspose.OCR.  
`RecognizeLine` przetwarza pojedynczą linię tekstu z obrazu i zwraca rozpoznany ciąg.

**Bezpośrednia odpowiedź:** Wczytaj obraz, utwórz instancję `AsposeOcr` z listą dozwolonych znaków zawierającą tylko cyfry (`"0123456789"`), wywołaj `RecognizeLine` (lub `Recognize` dla wielu linii) i odczytaj właściwość `Text` z wyniku. Ten trzyetapowy przepływ dostarcza czyste ciągi liczbowe w czasie krótszym niż sekunda dla typowych obrazów 300 dpi.

### Krok 1: Ustaw ścieżkę do folderu z obrazami

Zdefiniuj folder zawierający przykładowe obrazy, które chcesz przetworzyć.

```csharp
string dataDir = "Your Document Directory";
```

### Krok 2: Zainicjalizuj Aspose.OCR z listą dozwolonych znaków zawierającą tylko cyfry

`AllowedCharacters` jest właściwością, która ustawia listę dozwolonych znaków, które silnik OCR może rozpoznawać.

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### Krok 3: Rozpoznaj pojedynczą linię zawierającą cyfry

Metoda `RecognizeLine` skanuje obraz i zwraca najlepiej pasującą linię, która spełnia warunki listy dozwolonych znaków.

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### Krok 4: Wyświetl rozpoznane cyfry

Zapisz wynik w konsoli (lub logu), aby natychmiast zweryfikować wyjście.

```csharp
Console.WriteLine(result);
```

### Krok 5: Użyj `RecognitionSettings` dla większej kontroli

`RecognitionSettings` pozwala dostosować parametry OCR, takie jak DPI, pakiety językowe i tryb przetwarzania.

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### Krok 6: Wyświetl wynik drugiego przypadku

```csharp
Console.WriteLine(result2.RecognitionText);
```

### Krok 7: Potwierdź pomyślne wykonanie

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Postępując zgodnie z tymi krokami, nauczyłeś się **jak poprawić OCR** dokładność, ograniczając zestaw znaków, i możesz teraz niezawodnie wyodrębniać ciągi cyfr z obrazów przy użyciu Aspose.OCR dla .NET.

## Typowe pułapki i rozwiązywanie problemów

- **Pusty wynik:** Sprawdź, czy obraz ma wyraźny kontrast i minimalny szum tła; zalecane jest minimum 300 dpi.  
- **Nieoczekiwane znaki:** Sprawdź dokładnie ciąg listy dozwolonych znaków; dodatkowe spacje lub niewidoczne znaki mogą zepsuć filtr.  
- **Plik nie znaleziony:** Upewnij się, że `dataDir` wskazuje właściwy folder i że nazwa pliku odpowiada wrażliwemu na wielkość liter systemowi plików.  
- **Spowolnienie wydajności:** Przy dużych partiach, ponownie używaj jednej instancji `AsposeOcr` zamiast tworzyć nową dla każdego obrazu.

## Najczęściej zadawane pytania

### P1: Czy Aspose.OCR dla .NET jest odpowiedni zarówno dla początkujących, jak i doświadczonych programistów?
**A:** Zdecydowanie. API oferuje konfigurację w jednej linii dla szybkich zadań oraz zaawansowane `RecognitionSettings` dla zaawansowanych użytkowników, obejmując wszystkie poziomy umiejętności.

### P2: Czy mogę rozpoznawać znaki w wielu językach, używając listy dozwolonych znaków?
**A:** Tak. Załaduj odpowiedni pakiet językowy (np. `ocrEngine.LoadLanguage("en")`) i połącz go z listą dozwolonych znaków, taką jak `"0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"`, aby obsługiwać wielojęzyczne ciągi cyfr.

### P3: Jak często aktualizowane jest Aspose.OCR dla .NET?
**A:** Nowe wersje są publikowane mniej więcej co 6‑8 tygodni, dodając wsparcie językowe, usprawnienia wydajności i poprawki błędów. Zobacz najnowsze szczegóły w [dokumentacji](https://reference.aspose.com/ocr/net/).

### P4: Czy dostępna jest wersja próbna?
**A:** Tak — pobierz **[bezpłatną wersję próbną](https://releases.aspose.com/)**, aby ocenić wszystkie funkcje bez licencji. Użycie w produkcji wymaga licencji komercyjnej.

### P5: Gdzie mogę uzyskać pomoc społeczności lub wsparcie oficjalne?
**A:** Dołącz do aktywnej społeczności na **[forum Aspose.OCR](https://forum.aspose.com/c/ocr/16)**, gdzie możesz zadawać pytania, udostępniać fragmenty kodu i otrzymywać wskazówki od inżynierów Aspose.

---

**Last Updated:** 2026-05-24  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose

## Powiązane samouczki

- [Ustawienia rozpoznawania obrazu OCR – Określ ignorowane znaki](/ocr/net/ocr-settings/specify-ignored-characters/)
- [Wstępne przetwarzanie obrazu OCR przy użyciu filtrów Aspose.OCR dla .NET](/ocr/net/ocr-optimization/preprocessing-filters-for-image/)
- [Jak ustawić wartość progową w rozpoznawaniu obrazu OCR](/ocr/net/ocr-settings/set-threshold-value/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}