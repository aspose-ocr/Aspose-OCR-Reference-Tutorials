---
category: general
date: 2026-05-25
description: Dowiedz się, jak wyodrębnić tekst z obrazu przy użyciu minimalnego API
  ASP.NET Core. Prześlij obraz metodą POST, odczytaj dane multipart/form-data i wykonaj
  OCR na obrazie.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: pl
og_description: Wyodrębnij tekst z obrazu za pomocą minimalnego API ASP.NET Core.
  Ten przewodnik pokazuje, jak przesłać obraz metodą POST, odczytać dane multipart/form-data
  i wykonać OCR na obrazie.
og_title: Wyodrębnij tekst z obrazu w ASP.NET Core – krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  headline: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  type: TechArticle
- description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  name: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  steps:
  - name: Breaking Down the Logic
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **ReadFormAsync** | Parses the incoming *multipart/form-data* request. | Without
      this, you can’t access the uploaded files. | | **form.Files["image"]** | Retrieves
      the file whose form‑field name is `image`. | Guarant'
  - name: 1. Large Files
    text: 'The default request body limit is 30 MB. For larger scans you might need
      to adjust:'
  - name: 2. Asynchronous OCR
    text: Some OCR libraries expose async methods (`RecognizeAsync`). If yours does,
      replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the
      lambda as `async`.
  - name: 3. Security Considerations
    text: '- **Validate file size** before loading it into memory. - **Sanitize the
      filename** if you ever write it to disk. - **Rate‑limit** the endpoint to avoid
      denial‑of‑service attacks.'
  - name: 4. GPU Acceleration
    text: If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your
      hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially
      on high‑resolution images.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Minimal API
title: Wyodrębnianie tekstu z obrazu w ASP.NET Core Minimal API – Kompletny przewodnik
url: /pl/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z obrazu w ASP.NET Core Minimal API – Kompletny przewodnik

Zastanawiałeś się kiedyś, jak **wyodrębnić tekst z obrazu** bez zmagania się z ciężkimi frameworkami? Nie jesteś sam. Wielu programistów potrzebuje szybkiego sposobu, aby pozwolić użytkownikom wrzucić zdjęcie i otrzymać surowe znaki, niezależnie od tego, czy chodzi o skanowanie paragonów, digitalizację odręcznych notatek, czy zasilanie indeksu wyszukiwania.

W tym poradniku uruchomimy małe ASP.NET Core Minimal API, które **przesyła obraz za pomocą POST**, analizuje ładunek *multipart/form‑data* i następnie **wykonuje OCR na obrazie** przy użyciu singletonu `OcrEngine`. Po zakończeniu będziesz mieć w pełni działającą aplikację, którą możesz wkleić do dowolnego projektu .NET 8 i od razu zacząć wyodrębniać tekst z obrazu.

## Co zbudujesz

- Minimalna aplikacja webowa nasłuchująca na `/ocr`.
- Endpoint, który akceptuje plik obrazu wysłany w żądaniu POST `multipart/form-data`.
- Logika, która odczytuje przesłany plik, przekazuje go do silnika OCR i zwraca wyniki w postaci czystego tekstu.
- Opcjonalny fragment przyspieszenia GPU (zakomentowany) dla posiadaczy kompatybilnej karty.

**Wymagania wstępne**  
- .NET 8 SDK (lub nowszy).  
- Podstawowa znajomość C# i wiersza poleceń.  
- Biblioteka OCR udostępniająca klasę `OcrEngine` (przykład zakłada hipotetyczny pakiet NuGet).  

Jeśli masz to wszystko, zanurzmy się.

## Krok 1: Konfiguracja projektu i dodanie pakietu OCR

Najpierw utwórz nowy projekt webowy i pobierz bibliotekę OCR.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Porada:** Utrzymuj zależności aktualne. Nowsze wersje często przynoszą zyski wydajności, szczególnie przy wnioskowaniu przyspieszonym przez GPU.

## Krok 2: Zarejestruj singletonowy silnik OCR (główna usługa)

Chcemy jedną instancję `OcrEngine` dla całej aplikacji — nie ma potrzeby uruchamiania nowego silnika przy każdym żądaniu. Zarejestruj ją w kontenerze usług buildera.

```csharp
using Awesome.Ocr;               // <-- the OCR library namespace
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using System.Drawing;            // System.Drawing.Common for Image handling

var builder = WebApplication.CreateBuilder(args);

// Register a singleton OCR engine (English language)
// Uncomment the GPU line if you have a compatible GPU and the library supports it.
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU acceleration
    return engine;
});
```

**Dlaczego singleton?**  
Tworzenie silnika OCR może być kosztowne — wyobraź sobie ładowanie wag sieci neuronowej do pamięci. Ponowne użycie tej samej instancji pozwala zaoszczędzić zarówno cykle CPU, jak i RAM, co przekłada się na szybsze czasy odpowiedzi przy każdym wywołaniu `/ocr`.

## Krok 3: Zbuduj aplikację

Teraz materializujemy obiekt `WebApplication`.

```csharp
var app = builder.Build();
```

Ta linijka wygląda prawie magicznie, ale pod maską konfiguruje routing, middleware i kontener DI, który właśnie skonfigurowaliśmy.

## Krok 4: Zdefiniuj endpoint POST – „Prześlij obraz za pomocą POST”

Oto serce poradnika: endpoint, który **przesyła obraz za pomocą POST**, odczytuje ładunek multipart i przekazuje dane do silnika OCR.

```csharp
app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    // Step 5: Read multipart form data and extract the uploaded image
    var form = await request.ReadFormAsync();               // <-- read multipart/form-data
    var file = form.Files["image"];                         // expects a field named "image"

    if (file is null || file.Length == 0)
    {
        return Results.BadRequest("No image file provided.");
    }

    // Guard against unsupported content types
    if (!file.ContentType.StartsWith("image/"))
    {
        return Results.BadRequest("Uploaded file is not an image.");
    }

    // Load the image into a System.Drawing.Image
    using var img = Image.FromStream(file.OpenReadStream());

    // Step 6: Perform OCR on the image
    string text = ocr.Recognize(img);                       // <-- perform OCR on image

    // Step 7: Return the extracted text as plain‑text
    return Results.Text(text);
});
```

### Rozbicie logiki

| Krok | Co się dzieje | Dlaczego to ważne |
|------|--------------|-------------------|
| **ReadFormAsync** | Parsuje przychodzące żądanie *multipart/form-data*. | Bez tego nie możesz uzyskać dostępu do przesłanych plików. |
| **form.Files["image"]** | Pobiera plik, którego nazwa pola formularza to `image`. | Gwarantuje przewidywalny kontrakt dla wywołujących. |
| **Content‑type check** | Sprawdza, czy plik jest obrazem (np. `image/png`). | Zapobiega zacinaniu się silnika OCR przy danych niebędących obrazem. |
| **Image.FromStream** | Konwertuje surowy strumień na `System.Drawing.Image`. | Biblioteka OCR oczekuje obiektu `Image`, a nie surowej tablicy bajtów. |
| **ocr.Recognize(img)** | Wywołuje silnik OCR, aby **rozpoznać tekst z obrazu**. | To jest kluczowy krok **wykonywania OCR na obrazie**. |
| **Results.Text** | Zwraca odpowiedź w postaci czystego tekstu. | Prosty, łatwy do przetworzenia format dla usług downstream. |

## Krok 5: Uruchom API

Na koniec uruchom serwer webowy.

```csharp
app.Run();
```

Gdy uruchomisz `dotnet run`, API będzie nasłuchiwać na `http://localhost:5000` (lub wybranym porcie). Możesz przetestować je przy pomocy `curl`:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Oczekiwany wynik:** Konsola wydrukuje rozpoznane znaki, np.:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

Jeśli obraz jest rozmyty lub język nie jest obsługiwany, silnik OCR zwróci pusty ciąg lub komunikat o błędzie — obsłuż te przypadki w kodzie produkcyjnym.

## Przypadki brzegowe i najlepsze praktyki

### 1. Duże pliki

Domyślny limit rozmiaru ciała żądania to 30 MB. Dla większych skanów może być konieczna zmiana:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. Asynchroniczny OCR

Niektóre biblioteki OCR udostępniają asynchroniczne metody (`RecognizeAsync`). Jeśli Twoja tak, zamień `ocr.Recognize(img)` na `await ocr.RecognizeAsync(img)` i oznacz wyrażenie lambda jako `async`.

### 3. Rozważania bezpieczeństwa

- **Waliduj rozmiar pliku** przed załadowaniem go do pamięci.
- **Sanitizuj nazwę pliku** jeśli kiedykolwiek zapisujesz go na dysk.
- **Ogranicz liczbę żądań** (rate‑limit) endpointu, aby uniknąć ataków typu denial‑of‑service.

### 4. Przyspieszenie GPU

Jeśli odkomentujesz linię `engine.GpuDevice = new GpuDevice(0);` i Twój sprzęt obsługuje CUDA lub DirectML, zauważysz wyraźny przyrost wydajności, szczególnie przy obrazach wysokiej rozdzielczości.

## Pełny działający przykład

Poniżej znajduje się kompletny plik `Program.cs`, który możesz skopiować i wkleić do nowego projektu Minimal API.

```csharp
using Awesome.Ocr;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Http.Features;
using System.Drawing;

var builder = WebApplication.CreateBuilder(args);

// Optional: increase multipart limit for big images
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});

// Register the OCR engine as a singleton
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU if available
    return engine;
});

var app = builder.Build();

app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    var form = await request.ReadFormAsync();
    var file = form.Files["image"];

    if (file is null || file.Length == 0)
        return Results.BadRequest("No image file provided.");

    if (!file.ContentType.StartsWith("image/"))
        return Results.BadRequest("Uploaded file is not an image.");

    using var img = Image.FromStream(file.OpenReadStream());

    // Core OCR operation
    string text = ocr.Recognize(img);

    return Results.Text(text);
});

app.Run();
```

Zapisz, uruchom `dotnet run` i będziesz gotowy do **wyodrębniania tekstu z obrazu** na żądanie.

## Zakończenie

Przeszliśmy przez **kompletną, end‑to‑end rozwiązanie** wyodrębniania tekstu z obrazu przy użyciu ASP.NET Core Minimal API. Zaczynając od szkieletu projektu, **zarejestrowaliśmy singletonowy silnik OCR**, zbudowaliśmy endpoint, który **przesyła obraz za pomocą POST**, **odczytuje dane multipart**, i w końcu **wykonuje OCR na obrazie**, aby zwrócić czysty tekst.

Od tego momentu możesz:

- Dodać opakowania JSON dla bogatszych odpowiedzi.
- Podłączyć bazę danych do przechowywania wyodrębnionego tekstu.
- Rozszerzyć wsparcie na wiele języków (`OcrLanguage.Spanish` itd.).

Wzorzec skaluje się dobrze — wystarczy wkleić ten sam endpoint do większego mikroserwisu lub udostępnić go za pośrednictwem bramki API.

Masz pytania dotyczące obsługi PDF‑ów, przetwarzania wsadowego lub strojenia GPU? zostaw komentarz i szczęśliwego kodowania!

## Powiązane tutoriale

- [Wyodrębnianie tekstu z obrazu przy użyciu Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Wyodrębnianie tekstu z obrazu – optymalizacja OCR z Aspose.OCR dla .NET](/ocr/english/net/ocr-optimization/)
- [Wyodrębnianie tekstu z obrazu C# z wyborem języka przy użyciu Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}