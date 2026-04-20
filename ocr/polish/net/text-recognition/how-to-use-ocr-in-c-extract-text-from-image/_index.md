---
category: general
date: 2026-03-05
description: Jak używać OCR w C#, aby wyodrębnić tekst z obrazu. Dowiedz się, jak
  konwertować obraz na tekst, odczytywać koreańskie znaki i szybko wczytywać obraz
  do OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: pl
og_description: Jak używać OCR w C# i natychmiastowo wyodrębniać tekst z obrazu. Ten
  przewodnik pokazuje, jak konwertować obraz na tekst, odczytywać koreańskie znaki
  i ładować obraz do OCR.
og_title: Jak używać OCR w C# – wyodrębnianie tekstu z obrazu
tags:
- OCR
- C#
- Aspose
title: Jak używać OCR w C# – wyodrębnianie tekstu z obrazu
url: /pl/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR w C# – Wyodrębnianie tekstu z obrazu

Zastanawiałeś się kiedyś **jak używać OCR**, gdy masz zrzut ekranu pełen koreańskiego tekstu i potrzebujesz zwykłego ciągu znaków? Nie jesteś jedynym, który się nad tym zastanawia. W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który **wyodrębnia tekst z obrazu**, **konwertuje obraz na tekst**, a nawet pokazuje, jak **odczytać koreańskie znaki** przy użyciu Aspose.OCR.

Omówimy także często pomijaną czynność **ładowania obrazu do OCR**, aby nie napotkać później niespodzianki „plik nie znaleziony”. Po zakończeniu będziesz mieć samodzielny program, który możesz wkleić do dowolnego projektu .NET.

## Czego będziesz potrzebować

- .NET 6+ (lub .NET Framework 4.7.2 i nowszy) – kod działa na obu.
- Aspose.OCR for .NET – możesz pobrać darmową wersję próbną ze strony Aspose.
- Przykładowy obraz (`korean_doc.png`) zawierający koreański tekst.
- Twoje ulubione IDE (Visual Studio, Rider, VS Code – cokolwiek lubisz).

Żadne inne biblioteki zewnętrzne nie są wymagane.

## Krok 1: Konfiguracja projektu i dodanie Aspose.OCR

Najpierw utwórz nową aplikację konsolową:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Następnie dodaj pakiet NuGet Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

> **Wskazówka:** Jeśli masz plik licencji, umieść go w katalogu głównym projektu; w przeciwnym razie wersja próbna będzie działać, ale doda znak wodny do wyniku.

## Krok 2: Jak używać OCR – Inicjalizacja silnika

Teraz napiszemy kod C#. Pierwszą rzeczą, którą należy zrobić, gdy **jak używać OCR**, jest utworzenie instancji `OcrEngine`. Ten obiekt jest sercem biblioteki; przechowuje wszystkie ustawienia, które będą potrzebne później.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Dlaczego to ważne:** Bez prawidłowej instancji silnika nie możesz ustawić języka, załadować obrazów ani pobrać wyników. Silnik zarządza także zasobami wewnętrznymi, więc utworzenie go raz i ponowne użycie jest bardziej wydajne niż wielokrotne tworzenie nowych obiektów.

## Krok 3: Wybór języka – Odczyt koreańskich znaków

Następna linia informuje silnik, jakiego języka szukać. Ponieważ naszym celem jest **odczyt koreańskich znaków**, ustawiamy `OcrLanguage.Korean`. Możesz zamienić to na arabski, tajski, gudżarati itp., w zależności od potrzeb.

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**Dlaczego to ważne:** Wybór języka znacząco zwiększa dokładność. Silnik OCR używa słowników i modeli znaków specyficznych dla języka; podanie niewłaściwego języka może skutkować zniekształconym wynikiem.

## Krok 4: Ładowanie obrazu do OCR – Konwersja obrazu na tekst

Zanim silnik będzie mógł wykonać jakąkolwiek pracę, musisz **załadować obraz do OCR**. Metoda `ImageStream.FromFile` odczytuje plik w formacie, który silnik rozumie.

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

Jeśli obraz znajduje się w innym folderze, po prostu dostosuj ścieżkę. Pamiętaj, aby ustawić *Build Action* pliku na „Copy if newer”, aby wykonywalny plik mógł go znaleźć w czasie działania.

> **Częsty błąd:** Podanie ścieżki z backslashami (`\`) w literału łańcucha bez ich ucieczki spowoduje błąd kompilacji. Użyj podwójnych backslashów (`\\`) lub dosłownego łańcucha (`@"C:\\path\\file.png"`).

## Krok 5: Wykonanie OCR – Wyodrębnianie tekstu z obrazu

Teraz następuje najcięższa część. Wywołanie `Recognize()` uruchamia algorytm OCR, a właściwość `Text` zwraca surowy łańcuch znaków.

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

W tym momencie **wyodrębniłeś tekst z obrazu** i efektywnie **przekonwertowałeś obraz na tekst**. Wynik może zawierać znaki nowej linii, jeśli oryginalny układ miał podziały wierszy.

## Krok 6: Wyświetlenie wyniku – Weryfikacja wyjścia

Na koniec wypiszmy wynik w konsoli, abyś mógł zweryfikować, że działa.

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

Uruchom program:

```bash
dotnet run
```

### Oczekiwany wynik

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

Jeśli zobaczysz koreańskie znaki podobne do tych na obrazie, gratulacje — opanowałeś **jak używać OCR** z Aspose.OCR!

![Diagram przykładu użycia OCR pokazujący przepływ od ładowania obrazu do drukowania rozpoznanego tekstu.](image.png)

*Diagram przykładu użycia OCR pokazujący przepływ od ładowania obrazu do drukowania rozpoznanego tekstu.*

## Przypadki brzegowe i warianty

### 1. Obsługa wielu stron

Jeśli musisz **wyodrębnić tekst z obrazu** z plików zawierających kilka stron (np. wielostronicowy TIFF), przeiteruj każdą stronę i wywołaj `Recognize()` dla każdej instancji `ImageStream`.

### 2. Radzenie sobie z niskiej jakości skanami

Obrazy o niskiej rozdzielczości mogą obniżać dokładność. Przed wywołaniem `Recognize()` możesz poprawić obraz za pomocą narzędzi przetwarzania wstępnego Aspose:

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. Dynamiczna zmiana języków

Załóżmy, że masz dokument wielojęzyczny. Możesz zmienić `ocrEngine.Language` pomiędzy rozpoznaniami:

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. Zapis wyniku do pliku

Jeśli wolisz **przekonwertować obraz na tekst** i zapisać go, po prostu zapisz łańcuch do pliku `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## Najczęściej zadawane pytania

- **Czy potrzebuję licencji, aby uruchomić ten kod?**  
  Nie. Wersja próbna działa dobrze do eksperymentów, ale dodaje znak wodny do wyniku. Zakupiona licencja usuwa znak wodny i odblokowuje pełną wydajność.

- **Czy mogę używać tego na Linuksie?**  
  Oczywiście. Aspose.OCR jest wieloplatformowy; wystarczy zapewnić wymagane natywne zależności (libgdiplus dla .NET Core na Linuksie).

- **Co zrobić, jeśli mój obraz znajduje się w strumieniu zamiast w pliku?**  
  Użyj `ImageStream.FromStream(yourStream)` – API akceptuje dowolny `System.IO.Stream`.

## Zakończenie

Przeprowadziliśmy Cię krok po kroku przez **jak używać OCR** w C#, aby **wyodrębnić tekst z obrazu**, **przekonwertować obraz na tekst** i **odczytać koreańskie znaki**, jednocześnie prawidłowo **ładować obraz do OCR**. Pełny, gotowy do uruchomienia przykład powyżej powinien działać od razu, a dodatkowe wskazówki dają Ci mapę drogową do bardziej zaawansowanych scenariuszy.

Gotowy na kolejne wyzwanie? Spróbuj zamienić język, przetwarzać pliki PDF strona po stronie lub zintegrować wywołanie OCR z interfejsem web API, aby użytkownicy mogli przesyłać obrazy i otrzymywać natychmiastowe wyniki tekstowe. Możliwości są nieograniczone, a teraz masz solidne podstawy do dalszego rozwoju.

Miłego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}