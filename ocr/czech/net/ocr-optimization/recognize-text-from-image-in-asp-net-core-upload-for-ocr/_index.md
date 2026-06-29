---
category: general
date: 2026-06-28
description: Rozpoznat text z obrázku v ASP.NET Core – naučte se, jak nahrát obrázek
  pro OCR a efektivně zpracovat OCR obrázek ze streamu.
draft: false
keywords:
- recognize text from image
- upload image for ocr
- ocr image from stream
language: cs
og_description: rozpoznat text z obrázku pomocí Aspose OCR v ASP.NET Core. Nahrajte
  obrázek pro OCR, zpracujte OCR obrázek ze streamu a vraťte čistý text.
og_title: Rozpoznání textu z obrázku v ASP.NET Core – kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: recognize text from image in ASP.NET Core – learn how to upload image
    for OCR and process ocr image from stream efficiently.
  headline: recognize text from image in ASP.NET Core – upload for OCR
  type: TechArticle
- description: recognize text from image in ASP.NET Core – learn how to upload image
    for OCR and process ocr image from stream efficiently.
  name: recognize text from image in ASP.NET Core – upload for OCR
  steps:
  - name: Why This Pattern Works
    text: '- **Single `OcrEngine` instance**: Instantiating the engine once avoids
      the overhead of loading language data on every request. - **Async everything**:
      By using `await` on `FromStreamAsync` and `RecognizeAsync`, the ASP.NET Core
      thread pool stays free to serve other callers. - **`IFormFile` binding*'
  - name: Edge Cases to Watch
    text: '- **Corrupt files**: If the uploaded file isn’t a valid image, `FromStreamAsync`
      throws an exception. Wrap the call in a try/catch if you need graceful error
      messages. - **Unsupported formats**: Aspose supports PNG, JPEG, BMP, TIFF, etc.
      If you need PDF input, you’ll have to convert it to an image f'
  - name: Why Not Use `Recognize` (Sync)?
    text: The synchronous version would block the ASP.NET Core thread pool until the
      CPU‑intensive OCR finishes. On a busy server that quickly becomes a bottleneck,
      leading to 504 timeouts. The async variant keeps the API snappy.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Aspose.OCR
title: Rozpoznat text z obrázku v ASP.NET Core – nahrát pro OCR
url: /cs/net/ocr-optimization/recognize-text-from-image-in-asp-net-core-upload-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rozpoznání textu z obrázku v ASP.NET Core – kompletní tutoriál

Už jste někdy potřebovali **rozpoznat text z obrázku** uvnitř webového API a nevedeli jste, kde začít? Nejste v tom sami. V mnoha projektech – například skenery faktur, sledovače účtenek nebo i jednoduchá funkce „přečti‑mě“ – získání spolehlivých výsledků OCR je nezbytná dovednost.

V tomto průvodci projdeme kompletním, připraveným příkladem, který vám ukáže, jak **nahrát obrázek pro OCR**, převést toto nahrání na **ocr image from stream**, a nakonec vrátit extrahovaný text jako čistý JSON. Žádné chybějící části, žádné vágní odkazy – jen samostatné řešení, které můžete dnes vložit do libovolného projektu ASP.NET Core.

## Co si odnesete

- Plně funkční `OcrController`, který přijímá multipart formulářové nahrávky.  
- Podrobný krok‑za‑krokem popis každého řádku, abyste pochopili *proč* děláme to, co děláme.  
- Tipy pro práci s velkými soubory, vyhýbání se blokování vláken a udržení odezvy vašeho API.  
- Náhled, jak rozšířit řešení (více jazyků, předzpracování obrázků atd.).  

**Požadavky**: .NET 6 nebo novější, Visual Studio 2022 (nebo VS Code) a licence Aspose.OCR (bezplatná zkušební verze funguje pro testování). Pokud je máte, pojďme na to.

![diagram pracovního postupu rozpoznání textu z obrázku](https://example.com/ocr-workflow.png "rozpoznání textu z obrázku – pracovní postup")

## Jak rozpoznat text z obrázku v ASP.NET Core

Jádro řešení spočívá v jediném kontroleru. Níže je **kompletní, spustitelný kód**; každý import, každá `using` direktiva a každé asynchronní volání jsou zahrnuty, takže jej můžete zkopírovat a vložit přímo do nového projektu ASP.NET Core Web API.

```csharp
using Aspose.OCR;
using Microsoft.AspNetCore.Mvc;
using System.Threading.Tasks;

[ApiController]
[Route("api/ocr")]
public class OcrController : ControllerBase
{
    // Step 1: Create a reusable OCR engine instance
    // Reusing the same OcrEngine across requests saves memory and speeds up init.
    private readonly OcrEngine _ocrEngine = new OcrEngine();

    // Step 2: Define the endpoint that accepts a file upload
    [HttpPost("recognize")]
    public async Task<IActionResult> Recognize([FromForm] IFormFile uploadedFile)
    {
        // Guard clause – make sure we actually got a file
        if (uploadedFile == null || uploadedFile.Length == 0)
            return BadRequest(new { error = "No file uploaded." });

        // Step 3: Open the uploaded file as a read‑only stream
        // This is the **ocr image from stream** part.
        await using var imageStream = uploadedFile.OpenReadStream();

        // Step 4: Load the image asynchronously for OCR processing
        // Aspose.OCR provides FromStreamAsync which off‑loads the I/O work.
        var ocrImage = await OcrImage.FromStreamAsync(imageStream);

        // Step 5: Run OCR recognition without blocking the request thread
        // RecognizeAsync runs the heavy lifting on a background thread.
        var ocrResult = await _ocrEngine.RecognizeAsync(ocrImage);

        // Step 6: Return the extracted text as a JSON response
        return Ok(new { text = ocrResult.Text });
    }
}
```

### Proč tento vzor funguje

- **Jedna instance `OcrEngine`**: Vytvoření enginu jednou eliminuje režii načítání jazykových dat při každém požadavku.  
- **Všechno asynchronně**: Použitím `await` na `FromStreamAsync` a `RecognizeAsync` zůstává pool vláken ASP.NET Core volný pro obsluhu dalších volajících.  
- **Vazba `IFormFile`**: Atribut `[FromForm]` umožňuje klientovi jednoduše odeslat POST multipart/form‑data požadavek – přesně to, co prohlížeče a nástroje jako Postman už umí.  

Nyní, když máte kód před sebou, rozebráme každou logickou část.

## Nahrání obrázku pro OCR – zpracování multipart požadavku

Když klient pošle soubor, ASP.NET Core jej sváže s `IFormFile`. Tento objekt nám poskytuje bezpečný přístup k surovým bajtům, aniž by načítal celý soubor najednou do paměti.

```csharp
[HttpPost("recognize")]
public async Task<IActionResult> Recognize([FromForm] IFormFile uploadedFile)
{
    if (uploadedFile == null || uploadedFile.Length == 0)
        return BadRequest(new { error = "No file uploaded." });

    // …
}
```

**Tip**: Pokud očekáváte obrovské obrázky (např. >10 MB), zvažte přidání kontroly velikosti a vrácení 413 Payload Too Large. To chrání server před neúmyslnými OOM pády.

## Zpracování OCR obrázku ze streamu asynchronně

Řádek `await OcrImage.FromStreamAsync(imageStream)` provádí těžkou práci dekódování bajtů obrázku do formátu, který Aspose.OCR dokáže zpracovat. Protože je asynchronní, podkladové I/O (disk nebo síť) neblokuje vlákno požadavku.

```csharp
await using var imageStream = uploadedFile.OpenReadStream();
var ocrImage = await OcrImage.FromStreamAsync(imageStream);
```

### Okrajové případy, na které si dát pozor

- **Poškozené soubory**: Pokud nahraný soubor není platný obrázek, `FromStreamAsync` vyhodí výjimku. Zabalte volání do try/catch, pokud potřebujete uživatelsky přívětivé chybové zprávy.  
- **Nepodporované formáty**: Aspose podporuje PNG, JPEG, BMP, TIFF atd. Pokud potřebujete vstupní PDF, musíte jej nejprve převést na obrázek (Aspose.PDF může pomoci).  

## Spuštění OCR enginu bez blokování

`_ocrEngine.RecognizeAsync(ocrImage)` spouští OCR algoritmus na vlákně na pozadí. To je okamžik, kdy se operace **rozpoznání textu z obrázku** skutečně provádí.

```csharp
var ocrResult = await _ocrEngine.RecognizeAsync(ocrImage);
```

Vrácený `ocrResult` obsahuje vlastnost `Text` s čistým extrahovaným řetězcem. Můžete jej dále post‑zpracovat (odstranit mezery, opravit běžné OCR chyby atd.) před odesláním zpět.

### Proč nepoužít `Recognize` (synchronní)?

Synchronní verze by blokovala pool vláken ASP.NET Core, dokud se nedokončí CPU‑intenzivní OCR. Na vytíženém serveru se to rychle stane úzkým hrdlem, což vede k 504 timeoutům. Asynchronní varianta udržuje API rychlé.

## Vrácení čistého JSON – poslední část

```csharp
return Ok(new { text = ocrResult.Text });
```

Klienti obdrží úhledný JSON payload:

```json
{
  "text": "Sample extracted text from the uploaded image."
}
```

Pokud potřebujete další metadata – skóre důvěry, detekci jazyka, ohraničující rámečky – stačí rozšířit anonymní objekt nebo definovat správný DTO.

## Testování koncového bodu

Můžete ověřit, že vše funguje, pomocí **cURL**, **Postman** nebo i jednoduchého HTML formuláře.

```bash
curl -X POST https://localhost:5001/api/ocr/recognize \
     -F "uploadedFile=@/path/to/your/image.png"
```

Úspěšná odpověď vypadá takto:

```
{"text":"Hello World"}
```

Pokud zapomenete poslat soubor, získáte:

```
{"error":"No file uploaded."}
```

## Další kroky – běžná vylepšení

| Vylepšení | Proč pomáhá | Rychlá ukázka kódu |
|------------|--------------|-----------------|
| **Výběr jazyka** | Přesnost OCR se zvyšuje, když engine informujete, jaký jazyk očekáváte. | `_ocrEngine.Language = OcrLanguage.English;` |
| **Předzpracování obrázku** | Úpravy jasu/kontrastu mohou zachránit skeny nízké kvality. | `ocrImage = OcrImage.FromBitmap(ImageProcessor` |

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak provést extrakci textu z obrázku ze streamu pomocí Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extrahovat text z obrázku – optimalizace OCR s Aspose.OCR pro .NET](/ocr/english/net/ocr-optimization/)
- [Extrahovat text z obrázku v C# s výběrem jazyka pomocí Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}