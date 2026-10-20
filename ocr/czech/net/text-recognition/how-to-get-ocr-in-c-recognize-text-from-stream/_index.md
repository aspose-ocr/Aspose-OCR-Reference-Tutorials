---
category: general
date: 2026-03-05
description: Jak rychle získat OCR pomocí Aspose.OCR a rozpoznat text ze streamu v
  několika jednoduchých krocích. Naučte se kompletní C# kód a tipy pro streamování
  obrazových dat.
draft: false
keywords:
- how to get OCR
- recognize text from stream
- Aspose OCR
- streaming OCR C#
- image chunk processing
language: cs
og_description: Jak získat OCR v C# a rozpoznat text ze streamu pomocí Aspose.OCR.
  Sledujte tento krok‑za‑krokem tutoriál pro připravené řešení.
og_title: Jak získat OCR v C# – Kompletní průvodce rozpoznáváním proudu
tags:
- OCR
- C#
- Aspose
title: Jak získat OCR v C# – Rozpoznat text ze streamu
url: /cs/net/text-recognition/how-to-get-ocr-in-c-recognize-text-from-stream/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak získat OCR v C# – Rozpoznat text ze streamu

Už jste se někdy zamýšleli **jak získat OCR** v .NET aplikaci, aniž byste nejprve ukládali celý obrázek na disk? Nejste v tom sami. Mnoho vývojářů potřebuje **rozpoznávat text ze streamu** – například při zpracování obrázků, které přicházejí po síti, z kamery nebo z API cloudového úložiště.  

V tomto tutoriálu projdeme kompletní, připravený příklad, který přesně to ukazuje. Na konci budete mít samostatný C# program, který vytvoří OCR engine Aspose, bude do něj streamovat části obrázku a vytiskne extrahovaný text do konzole. Žádné tajemné externí nástroje, jen přehledný kód a několik praktických tipů.

## Co se naučíte

- Jak nainstalovat a licencovat knihovnu Aspose.OCR.  
- Jak postupně předávat data obrázku pomocí metody `AppendChunk`.  
- Jak spustit a ukončit cyklus rozpoznávání (`BeginRecognize` / `EndRecognize`).  
- Jak zacházet s běžnými okrajovými případy, jako jsou neúplné chunk‑y nebo chyby licence.  
- Jak vypadá výstup a jak jej ověřit.

### Požadavky

- .NET 6.0 nebo novější (kód funguje také s .NET Core a .NET Framework).  
- Platný licenční soubor Aspose OCR (`Aspose.OCR.lic`). Můžete získat bezplatnou zkušební verzi na webu Aspose.  
- Základní znalost C# a `async`/`await`, pokud chcete číst z asynchronního streamu (v příkladu je použita synchronní ukázka pro přehlednost).

> **Proč je to důležité:** Streaming OCR vám umožní udržet nízkou spotřebu paměti a snížit latenci při práci s velkými obrázky nebo kontinuálními video kanály. Jedná se o vzor, který potkáte v reálném čase u skenerů dokumentů, mobilních aplikací i serverových zpracovatelských pipeline.

## Krok 1: Nastavení projektu a přidání Aspose.OCR

Nejprve vytvořte nový konzolový projekt a přidejte NuGet balíček Aspose.OCR.

```bash
dotnet new console -n StreamOcrDemo
cd StreamOcrDemo
dotnet add package Aspose.OCR
```

> **Tip:** Pokud používáte Visual Studio, klikněte pravým tlačítkem na projekt → *Manage NuGet Packages* → vyhledejte “Aspose.OCR” a nainstalujte nejnovější stabilní verzi.

Nyní přidejte licenční soubor do kořenového adresáře projektu a nastavte jeho vlastnost **Copy to Output Directory** na **Copy always**. Tím zajistíte, že soubor bude k dispozici za běhu.

```csharp
// Program.cs – top of the file
using System;
using System.IO;
using Aspose.OCR;
```

## Krok 2: Inicializace OCR enginu a aplikace licence

Vytvoření enginu je jednoduché, ale aplikace licence **musí** proběhnout před jakýmkoli voláním rozpoznávání; jinak narazíte na omezení zkušebního režimu.

```csharp
static OcrEngine InitializeOcrEngine()
{
    var engine = new OcrEngine();

    // Load the license – adjust the path if your file lives elsewhere
    string licensePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "Aspose.OCR.lic");
    if (!File.Exists(licensePath))
    {
        Console.Error.WriteLine("License file not found at " + licensePath);
        Environment.Exit(1);
    }

    engine.SetLicense(licensePath);
    return engine;
}
```

> **Proč to děláme:** Nastavení licence hned na začátku zaručuje, že všechny následující API volání běží v plnohodnotném režimu a nebudete mít vodoznak „evaluation version“.

## Krok 3: Simulace streamovacího zdroje

V reálné aplikaci byste četli z `NetworkStream`, `FileStream` nebo SDK kamery. Pro demonstraci napodobíme stream pomocí pomocné funkce, která vrací pole bajtů představující JPEG chunk obrázku.

```csharp
static byte[] GetNextChunk()
{
    // Replace this with your actual streaming logic.
    // Here we simply read the whole file and pretend it’s a single chunk.
    string sampleImagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");
    if (!File.Exists(sampleImagePath))
    {
        Console.Error.WriteLine("Sample image not found at " + sampleImagePath);
        Environment.Exit(1);
    }

    return File.ReadAllBytes(sampleImagePath);
}
```

> **Poznámka k okrajovým případům:** Pokud dostáváte mnoho malých chunk‑ů, můžete opakovaně volat `engine.Image.AppendChunk(chunk)` před ukončením rozpoznávání. Engine interně bufferuje, dokud nemá dostatek dat ke zpracování.

## Krok 4: Postupné předávání dat obrázku a spuštění OCR

Nyní spojíme vše dohromady. Sekvence je:

1. `BeginRecognize()` – řekne enginu, že se chystáme předávat data.  
2. `AppendChunk()` – přidá každý bajtový pole (můžete v cyklu předat mnoho chunk‑ů).  
3. `EndRecognize()` – signalizuje, že poslední chunk byl odeslán a spustí skutečné rozpoznávání.

```csharp
static string PerformOcr(OcrEngine engine, byte[] imageChunk)
{
    // Start the recognition session
    engine.BeginRecognize();

    // Feed the image data. If you have multiple chunks, call this in a loop.
    engine.Image.AppendChunk(imageChunk);

    // End the session – the engine now processes the accumulated data.
    engine.EndRecognize();

    // Retrieve the result object; .Text holds the plain string.
    return engine.GetResult().Text;
}
```

## Krok 5: Celý kód v metodě `Main`

Zde je kompletní metoda `Main`, která vše propojí, vytiskne rozpoznaný text a čistě uvolní engine.

```csharp
static void Main(string[] args)
{
    // 1️⃣ Initialize OCR engine with license
    var ocrEngine = InitializeOcrEngine();

    try
    {
        // 2️⃣ Get a chunk of image data (replace with your streaming source)
        byte[] imageChunk = GetNextChunk();

        // 3️⃣ Run OCR on the streamed data
        string recognizedText = PerformOcr(ocrEngine, imageChunk);

        // 4️⃣ Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
    catch (Exception ex)
    {
        // Helpful error handling – you’ll often see OCR exceptions when the image is corrupted.
        Console.Error.WriteLine("OCR failed: " + ex.Message);
    }
    finally
    {
        // Release any native resources held by the engine.
        ocrEngine.Dispose();
    }
}
```

### Očekávaný výstup

Pokud `sample.jpg` obsahuje frázi „Hello, World!“, měli byste vidět:

```
=== Recognized Text ===
Hello, World!
```

Pokud je obrázek rozmazaný nebo je chunk neúplný, výstup může být prázdný nebo obsahovat nesmyslné znaky – proto je důležité správně odeslat poslední chunk.

## Zpracování více chunk‑ů (pokročilé)

Při práci s opravdovými streamy pravděpodobně obdržíte mnoho malých částí. Níže uvedený vzor ukazuje, jak cyklicky číst, dokud zdroj neskončí.

```csharp
static string OcrFromStream(OcrEngine engine, Stream source)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192]; // 8 KB per read – adjust as needed
    int bytesRead;
    while ((bytesRead = source.Read(buffer, 0, buffer.Length)) > 0)
    {
        // If the last read returned fewer bytes, copy only that many.
        if (bytesRead < buffer.Length)
        {
            byte[] chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

> **Proč to pomáhá:** Streamováním přímo z `NetworkStream` nebo `FileStream` nikdy nenačítáte celý obrázek do paměti, což je zvláště výhodné u velkých PDF nebo vysoce rozlišených fotografií.

## Časté úskalí a jak se jim vyhnout

| Úskalí | Příznak | Řešení |
|--------|----------|--------|
| Licence nenalezena | `SetLicense` vyhodí `FileNotFoundException` | Ověřte cestu a nastavte *Copy to Output Directory* na *Copy always*. |
| Prázdný výsledek | Žádný text se nevypsal | Ujistěte se, že jste volali `BeginRecognize` **před** `AppendChunk` a `EndRecognize` **po** posledním chunku. |
| Únik paměti | Aplikace zpomaluje po mnoha OCR voláních | Po každém použití `Dispose` enginu `OcrEngine` nebo znovu použijte jedinou instanci s řádnými voláními `Dispose`. |
| Poškozený chunk | Nesmyslné znaky | Ověřte velikost chunku; u JPEG/PNG by první bajty měly začínat `0xFF 0xD8` nebo `0x89 0x50`. |

## Bonus: Asynchronní streamy

Pokud je vaším zdrojem odpověď `HttpClient` stream, můžete smyčku upravit na `await` čtení:

```csharp
static async Task<string> OcrFromAsyncStream(OcrEngine engine, Stream asyncSource)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192];
    int bytesRead;
    while ((bytesRead = await asyncSource.ReadAsync(buffer, 0, buffer.Length)) > 0)
    {
        if (bytesRead < buffer.Length)
        {
            var chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

To udrží UI responsivní v desktopových nebo mobilních aplikacích a maximalizuje propustnost na serverech.

## Závěr

Máte nyní **kompletní, samostatné řešení, jak získat OCR** v C# a **rozpoznávat text ze streamu** pomocí Aspose.OCR. Tutoriál pokryl vše od licencování a inicializace po předávání chunk‑ů, řešení okrajových případů a i asynchronní variantu.  

Vyzkoušejte to – nahraďte `sample.jpg` živým kanálem kamery, obrázkem uloženým v cloudu nebo multipart HTTP uploadem. Jakmile budete mít jistotu, prozkoumejte pokročilé funkce jako jazykové balíčky, vlastní předzpracování nebo hromadné zpracování více streamů.

**Další kroky:**  
- Vyzkoušejte OCR na PDF konverzí každé stránky na obrázek.  
- Experimentujte s `engine.Config` pro zvýšení přesnosti u specifických fontů.  
- Kombinujte to s Azure Functions nebo AWS Lambda pro serverless pipeline extrakce textu.

Šťastné programování a ať jsou vaše streamy vždy ostré a výsledky OCR bezchybné!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}