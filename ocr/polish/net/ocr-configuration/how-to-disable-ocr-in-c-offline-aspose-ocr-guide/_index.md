---
category: general
date: 2026-04-11
description: Dowiedz się, jak wyłączyć OCR w Aspose OCR dla C#, aby działało offline,
  wyodrębnić tekst z obrazu bez internetu i prawidłowo załadować obraz do OCR.
draft: false
keywords:
- how to disable OCR
- extract text from image
- load image for OCR
- offline OCR C#
- Aspose OCR resources
language: pl
og_description: Jak wyłączyć OCR w Aspose OCR dla C# i uruchomić go offline, wyodrębnić
  tekst z obrazu bez potrzeby połączenia z internetem oraz łatwo wczytać obraz do
  OCR.
og_title: Jak wyłączyć OCR w C# – Przewodnik po offline Aspose OCR
tags:
- C#
- OCR
- Aspose
- Offline Processing
title: Jak wyłączyć OCR w C# – Przewodnik po offline OCR Aspose
url: /pl/net/ocr-configuration/how-to-disable-ocr-in-c-offline-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyłączyć OCR w C# – Przewodnik po offline Aspose OCR

Zastanawiałeś się kiedyś **jak wyłączyć OCR**, gdy potrzebujesz naprawdę offline rozwiązania? Może tworzysz bezpieczną aplikację desktopową, która nie może polegać na połączeniu sieciowym, albo po prostu chcesz uniknąć nieoczekiwanych pobrań. Tak czy inaczej, dobra wiadomość jest taka, że Aspose OCR pozwala wyłączyć automatyczne pobieranie zasobów, wskazać lokalny folder i trzymać wszystko na miejscu. W tym samouczku zobaczysz także, jak **wyodrębnić tekst z obrazu** oraz poprawnie **załadować obraz do OCR** bez żadnych problemów.

Przejdziemy przez kompletny, gotowy do uruchomienia przykład, który pokazuje każdy krok — od inicjalizacji silnika po wypisanie rozpoznanego japońskiego tekstu. Bez zewnętrznych dokumentów, bez ukrytej magii; po prostu czysty kod C#, który możesz wkleić do swojego projektu już dziś. Po zakończeniu będziesz wiedział, dlaczego wyłączenie funkcji automatycznego pobierania ma znaczenie, jak ustawić ścieżkę zasobów i na jakie pułapki należy uważać.

## Wymagania wstępne

- .NET 6.0 (lub dowolna nowsza wersja .NET) zainstalowana na twoim komputerze.  
- Pakiet NuGet Aspose.OCR dla .NET (`Install-Package Aspose.OCR`).  
- Folder, który już zawiera potrzebne zasoby językowe (np. model japoński).  
- Plik obrazu (`japan_doc.png`), na którym chcesz wykonać OCR.  

Jeśli brakuje ci pakietów językowych, pobierz je raz z portalu Aspose, rozpakuj do folderu, np. `AsposeOCRResources`, i gotowe. Żadne dalsze pobrania nie będą się odbywać po wyłączeniu funkcji automatycznego pobierania.

![How to disable OCR offline](/images/how-to-disable-ocr.png "how to disable OCR illustration")

## Krok 1 – Utwórz instancję silnika OCR  

Pierwszą rzeczą, którą robisz, jest utworzenie instancji `OcrEngine`. Traktuj ten obiekt jako mózg, który będzie czytał twój obraz.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Dlaczego to ważne:** Bez silnika nie możesz niczego skonfigurować. Obiekt przechowuje wszystkie ustawienia, w tym kluczową flagę, która określa, czy biblioteka może łączyć się z internetem.

## Krok 2 – Wyłącz automatyczne pobieranie zasobów  

Domyślnie Aspose OCR będzie próbował pobrać brakujące pliki językowe w locie. Aby wszystko pozostało offline, ustaw przełącznik `AutoDownloadResources` na `false`.

```csharp
        // Step 2: Disable automatic resource download to work offline
        ocrEngine.Settings.AutoDownloadResources = false;
```

> **Porada:** Wyłączenie tej opcji nie tylko zapewnia prywatność, ale także przyspiesza pierwsze uruchomienie rozpoznawania, ponieważ silnik nie traci czasu na sprawdzanie aktualizacji.

## Krok 3 – Wskaż lokalny folder zasobów  

Teraz powiedz silnikowi, gdzie znajdują się wcześniej pobrane pakiety językowe. To jest ścieżka, którą ustawiłeś w wymaganiach wstępnych.

```csharp
        // Step 3: Point the engine to the folder containing pre‑downloaded resources
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";
```

> **Co może pójść nie tak?** Jeśli ścieżka jest nieprawidłowa lub brak wymaganego pliku językowego, silnik wyrzuci `ResourceNotFoundException`. Sprawdź dokładnie pisownię folderu i czy model japoński (`jpn.traineddata`) jest obecny.

## Krok 4 – Wybierz lokalny model językowy  

Wybierz język, który faktycznie masz na dysku. W naszym przykładzie używamy japońskiego, ale możesz zamienić `Language.Japanese` na dowolny inny język, który pobrałeś.

```csharp
        // Step 4: Select the language model that is available locally
        ocrEngine.Settings.Language = Language.Japanese;
```

> **Przypadek brzegowy:** Niektóre języki wymagają dodatkowych słowników (np. chiński). Upewnij się, że te dodatkowe pliki również znajdują się w tym samym folderze zasobów.

## Krok 5 – Załaduj obraz do OCR  

Tutaj **ładujemy obraz do OCR**. Metoda `ImageStream.FromFile` odczytuje plik do strumienia, który Aspose może przetworzyć.

```csharp
        // Step 5: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/japan_doc.png");
```

> **Wskazówka:** Obsługiwane formaty to PNG, JPEG, BMP i TIFF. Jeśli musisz obsłużyć PDF-y, najpierw przekonwertuj każdą stronę na obraz.

## Krok 6 – Uruchom proces rozpoznawania  

Teraz silnik faktycznie odczytuje piksele i próbuje przekształcić je w tekst.

```csharp
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Dlaczego ten krok może być wolny:** OCR jest intensywny pod względem CPU, szczególnie przy obrazach wysokiej rozdzielczości. Jeśli wydajność jest istotna, rozważ zmniejszenie rozmiaru obrazu przed rozpoznawaniem.

## Krok 7 – Wyświetl wyodrębniony tekst  

Na koniec **wyodrębniamy tekst z obrazu** i wypisujemy go w konsoli.

```csharp
        // Step 7: Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Uruchomienie programu powinno wyświetlić japońskie znaki, które znajdowały się w `japan_doc.png`. Jeśli wszystko jest poprawnie skonfigurowane, zobaczysz czysty blok tekstu Unicode w konsoli.

### Oczekiwany wynik

```
これはサンプルの日本語テキストです。
```

(Rzeczywisty wynik będzie zależał od zawartości obrazu.)

## Częste pułapki i jak ich uniknąć  

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| **Brak pliku językowego** | `AutoDownloadResources` jest ustawione na false, więc silnik nie może go pobrać. | Sprawdź, czy `ResourcesPath` wskazuje na folder zawierający `jpn.traineddata`. |
| **Nieprawidłowa ścieżka obrazu** | `ImageStream.FromFile` wyrzuca `FileNotFoundException`. | Użyj ścieżek bezwzględnych lub upewnij się, że katalog roboczy jest ustawiony prawidłowo. |
| **Nieobsługiwany format obrazu** | Aspose odczytuje tylko określone formaty. | Przekonwertuj obraz na PNG lub JPEG przed wywołaniem `FromFile`. |
| **Brak pamięci przy dużych obrazach** | OCR ładuje cały obraz do pamięci. | Zmniejsz rozmiar lub podziel obraz na części, albo zwiększ limit pamięci procesu. |

## Rozszerzanie przykładu  

- **Przetwarzanie wsadowe:** Przejdź pętlą po katalogu obrazów, wywołaj ten sam kod rozpoznawania i zapisz każdy wynik do osobnego pliku `.txt`.  
- **Różne języki:** Zamień `Language.Japanese` na `Language.English` (lub inny) po umieszczeniu odpowiednich plików zasobów.  
- **Niestandardowe przetwarzanie wstępne:** Użyj Aspose.Imaging do prostowania lub poprawy kontrastu przed OCR, aby uzyskać lepszą dokładność.

## Podsumowanie  

Teraz wiesz **jak wyłączyć OCR** w Aspose OCR dla C# i uruchomić go całkowicie offline. Ustawiając `AutoDownloadResources` na `false`, wskazując silnik na lokalny folder zasobów i poprawnie **ładując obraz do OCR**, możesz niezawodnie **wyodrębnić tekst z obrazu** bez konieczności łączenia się z internetem. To podejście jest idealne dla bezpiecznych środowisk, potoków CI lub wszelkich scenariuszy, w których dostęp do sieci jest ograniczony.

Gotowy na kolejny krok? Spróbuj przetworzyć cały folder zeskanowanych PDF‑ów, eksperymentuj z różnymi pakietami językowymi lub zintegrować wynik OCR z przeszukiwalną bazą danych. Offline konfiguracja, którą dziś stworzyłeś, jest solidną podstawą dla każdego lokalnego przepływu przetwarzania dokumentów.

Miłego kodowania i nie wahaj się zostawić komentarza, jeśli napotkasz jakiekolwiek problemy!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}