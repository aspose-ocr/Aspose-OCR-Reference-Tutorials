---
category: general
date: 2026-04-01
description: Utwórz przeszukiwalny PDF w C# przy użyciu Aspose OCR – dowiedz się,
  jak konwertować zeskanowane PDF, dodać OCR do PDF i włączyć przyspieszenie GPU dla
  szybkich wyników.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- convert pdf to searchable
- add OCR to pdf
- enable GPU acceleration
language: pl
og_description: Szybko twórz przeszukiwalne PDF w C# — konwertuj zeskanowane PDF,
  dodaj OCR do PDF i włącz przyspieszenie GPU dla wysokowydajnego przetwarzania.
og_title: Utwórz przeszukiwalny PDF przy użyciu Aspose OCR w C#
tags:
- Aspose OCR
- C#
- PDF processing
title: Utwórz przeszukiwalny PDF przy użyciu Aspose OCR w C#
url: /pl/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie przeszukiwalnego PDF przy użyciu Aspose OCR w C#

Czy kiedykolwiek potrzebowałeś **utworzyć przeszukiwalne pliki PDF** z stosu zeskanowanych dokumentów? Nie jesteś jedyny — wiele zespołów zmaga się z przekształcaniem PDF‑ów zawierających jedynie obrazy w zasoby, które można przeszukiwać tekstowo. Dobra wiadomość? Dzięki Aspose OCR możesz **przekonwertować zeskanowany PDF** na w pełni przeszukiwalną wersję w kilku linijkach kodu C#. W tym przewodniku przeprowadzimy Cię przez cały proces, od dodania OCR do PDF po opcjonalne **włączenie przyspieszenia GPU** dla zwiększenia wydajności.

Pokażemy także, jak **przekształcić pdf do formatu przeszukiwalnego**, omówimy, dlaczego warto **dodać OCR do PDF**, i podamy praktyczne wskazówki dotyczące obsługi dużych partii. Po zakończeniu będziesz mieć gotową aplikację konsolową, która generuje przeszukiwalny PDF gotowy do wstawienia w dowolnym systemie zarządzania dokumentami.

---

## Czego będziesz potrzebować

Zanim zaczniemy, upewnij się, że masz następujące elementy:

- **.NET 6.0** lub nowszy (API działa również z .NET Framework, ale .NET 6+ to optymalne rozwiązanie).
- Pakiet NuGet **Aspose.OCR for .NET** (`Install-Package Aspose.OCR`).
- Zeskanowany plik PDF (tylko obrazy), który posłuży jako wejście.
- Opcjonalnie: maszyna kompatybilna z GPU z zainstalowanym CUDA®, jeśli chcesz **włączyć przyspieszenie GPU**.

To wszystko — żadnych ciężkich silników OCR, żadnych zewnętrznych usług. Wszystko działa lokalnie.

---

## Tworzenie przeszukiwalnego PDF — przegląd krok po kroku

Poniżej przedstawiamy wysokopoziomowy przepływ, którego będziemy się trzymać:

1. **Zainicjalizuj silnik OCR** – określ Aspose, jakiego języka szukać i czy używać GPU.
2. **Wskaż silnikowi Twój zeskanowany PDF** – zdefiniuj ścieżki wejścia i wyjścia.
3. **Uruchom konwersję** – Aspose wykona ciężką pracę i zapisze przeszukiwalny PDF.
4. **Zweryfikuj wynik** – otwórz plik wyjściowy i spróbuj wyszukać tekst.

Każdy krok jest opisany w osobnej sekcji, dzięki czemu możesz wybrać te, które są dla Ciebie najważniejsze.

---

## Konwersja zeskanowanego PDF do przeszukiwalnego PDF

Pierwszą rzeczą, którą musisz zrobić, jest utworzenie instancji `OcrEngine`. Ten obiekt jest „silnikiem”, który odczytuje obrazy rastrowe wewnątrz Twojego PDF i wyodrębnia tekst.

```csharp
using Aspose.OCR;
using System;

class PdfSearchableDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Optional: enable GPU for faster processing
            UseGpuAcceleration = true
        };

        // Step 2: Specify the input scanned PDF and the output searchable PDF paths
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string searchablePdfPath = @"C:\Docs\output.pdf";

        // Step 3: Convert the scanned PDF into a searchable PDF
        ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

        // Step 4: Notify the user where the searchable PDF was saved
        Console.WriteLine("Searchable PDF created at: " + searchablePdfPath);
    }
}
```

**Dlaczego to działa:** `ConvertToSearchablePdf` odczytuje każdą stronę, wykonuje OCR na zawartości rastrowej, a następnie osadza niewidoczną warstwę tekstową za oryginalnym obrazem. Wynik wygląda dokładnie tak jak oryginalny zeskanowany dokument, ale teraz możesz kopiować, zaznaczać i wyszukiwać tekst.

---

## Dodawanie OCR do PDF przy użyciu Aspose

Jeśli już masz PDF i chcesz po prostu **dodać OCR do PDF** bez konwertowania całego pliku, możesz wywołać tę samą metodę — Aspose traktuje operację jako „dodawanie OCR”. Powyższy kod już to robi, ale oto szybka wariacja, która pokazuje, jak można przetwarzać wiele plików w pętli:

```csharp
string[] pdfFiles = Directory.GetFiles(@"C:\Docs\Scanned", "*.pdf");
foreach (var file in pdfFiles)
{
    string output = Path.Combine(@"C:\Docs\Searchable", Path.GetFileNameWithoutExtension(file) + "_searchable.pdf");
    ocrEngine.ConvertToSearchablePdf(file, output);
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(output)}");
}
```

**Wskazówka:** Utrzymuj tę samą instancję `OcrEngine` dla całej partii. Tworzenie jej za każdym razem generuje niepotrzebny narzut, szczególnie gdy **włączasz przyspieszenie GPU**.

---

## Włączenie przyspieszenia GPU dla szybszego OCR

Przyspieszenie GPU może zaoszczędzić minuty przy dużych partiach. Aspose OCR wykorzystuje NVIDIA CUDA pod maską, więc wystarczy przełączyć flagę boolowską:

```csharp
ocrEngine.UseGpuAcceleration = true; // set to false if no compatible GPU
```

**Kiedy używać:** Jeśli przetwarzasz PDF‑y większe niż 10 MB lub obsługujesz więcej niż kilkadziesiąt plików, GPU zazwyczaj zapewni 2‑3‑krotny przyrost szybkości. Na skromnym laptopie bez GPU obsługującego CUDA pozostaw `false` — biblioteka automatycznie przełączy się na CPU.

**Typowy problem:** Zapomnienie o zainstalowaniu właściwej wersji sterownika CUDA może spowodować wyjątek w czasie wykonywania (`CudaException`). Upewnij się, że sterownik pasuje do wersji oczekiwanej przez Aspose (sprawdź notatki wydania na stronie NuGet).

---

## Pełny działający przykład (wszystkie kroki razem)

Poniżej znajduje się samodzielna aplikacja konsolowa, którą możesz skopiować i wkleić do nowego projektu .NET. Zawiera przydatne komentarze, obsługę błędów oraz końcowy krok weryfikacji, który wypisuje liczbę przetworzonych stron.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class PdfSearchableDemo
{
    static void Main()
    {
        try
        {
            // 1️⃣ Initialize OCR engine – English language, GPU on if available
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                UseGpuAcceleration = true // set to false on non‑GPU machines
            };

            // 2️⃣ Define input and output paths
            string sourcePdfPath = @"C:\Docs\input.pdf";
            string searchablePdfPath = @"C:\Docs\output.pdf";

            // 3️⃣ Perform the conversion – this creates a searchable PDF
            ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

            // 4️⃣ Simple verification – count pages in the new file
            int pageCount = new Aspose.Pdf.Facades.PdfFileInfo(searchablePdfPath).NumberOfPages;
            Console.WriteLine($"✅ Searchable PDF created at: {searchablePdfPath}");
            Console.WriteLine($"📄 The new file contains {pageCount} pages.");

            // 5️⃣ Optional: open the file automatically (Windows only)
            // System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(searchablePdfPath) { UseShellExecute = true });
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
        }
    }
}
```

**Oczekiwany wynik**

```
✅ Searchable PDF created at: C:\Docs\output.pdf
📄 The new file contains 12 pages.
```

Otwórz `output.pdf` w dowolnym przeglądarce PDF i spróbuj wpisać słowo, które pojawia się na zeskanowanych obrazach. Jeśli tekst zostanie podświetlony, pomyślnie **utworzyłeś przeszukiwalny pdf**.

---

## Typowe problemy i wskazówki profesjonalne

| Problem | Dlaczego się pojawia | Jak naprawić / uniknąć |
|-------|----------------|--------------------|
| **GPU nie wykryte** | Brak lub niezgodny sterownik CUDA. | Zainstaluj wersję sterownika podaną w notatkach wydania Aspose; ustaw `UseGpuAcceleration = false` jako awaryjne rozwiązanie. |
| **Nieprawidłowy język** | OCR domyślnie używa angielskiego; inne języki wymagają wyraźnego ustawienia. | Ustaw `Language = Language.Spanish` (lub dowolny obsługiwany enum) przed konwersją. |
| **Duże PDF‑y powodują OutOfMemory** | Silnik ładuje całe strony do pamięci. | Przetwarzaj PDF w partiach, używając `ocrEngine.PageRange = new PageRange(1, 5)` dla każdego zestawu. |
| **Plik wyjściowy jest uszkodzony** | Folder docelowy nie ma uprawnień do zapisu. | Uruchom aplikację z podwyższonymi uprawnieniami lub wybierz ścieżkę zapisu, do której masz dostęp. |
| **Warstwa tekstowa nie jest przeszukiwalna** | Przeglądarka buforuje starą wersję. | Odśwież przeglądarkę PDF lub ponownie otwórz plik. |

**Wskazówka pro:** Gdy masz mieszankę zeskanowanych i natywnych PDF‑ów, sprawdzaj flagę `HasText` każdej strony (`PdfPageInfo.HasText`) przed uruchomieniem OCR. To oszczędza cykle CPU i zapobiega podwójnemu OCR na stronach, które już są przeszukiwalne.

---

## Programowa weryfikacja wyniku (opcjonalnie)

Jeśli chcesz zautomatyzować weryfikację, Aspose.PDF może wyodrębnić ukryty tekst:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the searchable PDF
Document doc = new Document(searchablePdfPath);
TextAbsorber absorber = new TextAbsorber();
doc.Pages.Accept(absorber);
string extracted = absorber.Text;

// Simple check – does the word "Invoice" appear?
if (extracted.Contains("Invoice"))
    Console.WriteLine("✅ OCR succeeded – 'Invoice' found.");
else
    Console.WriteLine("⚠️ OCR may have missed some text.");
```

Ten fragment kodu dowodzi, że naprawdę **konwertujesz pdf do formatu przeszukiwalnego**, a nie tylko nakładasz obraz.

---

## Przykład obrazu

![Przykład wyniku przeszukiwalnego PDF](https://example.com/images/searchable-pdf.png "Tworzenie przeszukiwalnego PDF przy użyciu Aspose OCR")

*Tekst alternatywny:* **przykład tworzenia przeszukiwalnego pdf** pokazujący przed (zeskanowany) i po (przeszukiwalny) widok.

---

## Kolejne kroki i tematy powiązane

- **Przetwarzanie wsadowe:** Umieść pętlę z sekcji „Dodawanie OCR do PDF” w usłudze Windows Service lub Azure Function, aby uruchamiać zadania nocne.
- **Zaawansowane wsparcie językowe:** Zbadaj `ocrEngine.Language = Language.Multilingual` dla dokumentów zawierających mieszane skrypty.
- **Czyszczenie po OCR:** Skorzystaj z `TextFragmentAbsorber` w Aspose.PDF, aby korygować typowe błędy OCR (np. „0” vs „O”).
- **Security

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}