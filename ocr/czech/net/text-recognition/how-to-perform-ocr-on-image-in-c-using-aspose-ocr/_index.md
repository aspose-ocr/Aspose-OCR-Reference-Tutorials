---
category: general
date: 2026-10-11
description: Naučte se, jak provádět OCR na obrázku v C# pomocí Aspose.OCR, včetně
  instalace System.Drawing.Common a extrakce textu z JPG souborů.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: cs
lastmod: 2026-10-11
og_description: Proveďte OCR na obrázku v C# pomocí Aspose.OCR. Tento průvodce vám
  ukáže, jak nainstalovat System.Drawing.Common, načíst obrázek pro OCR a extrahovat
  text z JPG.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: Proveďte OCR na obrázku v C# – krok za krokem průvodce
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Jak provést OCR na obrázku v C# pomocí Aspose.OCR
url: /cs/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR na obrázku v C# pomocí Aspose.OCR

Pokud potřebujete **perform OCR on image** soubory v .NET aplikaci, tento průvodce vám ukáže kompletní řešení. Pomocí Aspose.OCR můžete rychle **recognize text from picture** soubory jako JPG a zobrazit výsledek v okně konzole.

Dozvíte se, jak:

* **install System.Drawing.Common package** – knihovna, která poskytuje třídu `Image`,
* **load image for OCR** – načíst JPEG nebo PNG do paměti,
* nakonfigurovat jazykový model,
* **perform OCR on image** a nakonec,
* **extract text from JPG** a zobrazit jej.

Kroky jsou napsány pro .NET 6+, ale fungují i s .NET Framework 4.6.1 nebo novějším.

---

## Prerequisites

| Požadavek | Proč je důležité |
|-------------|----------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | Poskytuje runtime pro C# konzolovou aplikaci. |
| Visual Studio 2022 (or any IDE) | Usnadňuje přidání NuGet balíčků a spuštění programu. |
| Internetové připojení (pouze při prvním spuštění) | Aspose.OCR automaticky stáhne jazykový modul. |
| Ukázkový obrázek obsahující cyrilické nebo latinské texty (např. `sample_cyrillic.jpg`) | Používá se k demonstraci **extract text from JPG**. |

---

## Krok 1: Instalace balíčku System.Drawing.Common

NuGet balíček `System.Drawing.Common` poskytuje třídu `Image`, kterou budete **load image for OCR**. Otevřete Package Manager Console a spusťte:

```powershell
Install-Package System.Drawing.Common
```

> **Tip:** Cílem je `net6.0-windows` nebo přidejte `<UseWindowsForms>true</UseWindowsForms>` do souboru projektu, pokud narazíte na platformově specifická varování na Linuxu/macOS.

---

## Krok 2: Přidání NuGet balíčku Aspose.OCR

Aspose.OCR obsahuje OCR engine a jazykové modely. Nainstalujte jej pomocí:

```powershell
Install-Package Aspose.OCR
```

Balíček je lehký; požadovaná jazyková data (např. Cyrillic) jsou stažena při prvním nastavení `OcrEngine.Language`.

---

## Krok 3: Jak načíst obrázek pro OCR

Načtení obrázku je prvním konkrétním krokem, než můžete **perform OCR on image**. Metoda `Image.FromFile` načte jakýkoli formát podporovaný GDI+, včetně JPG, PNG, BMP a TIFF.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*Pokud soubor neexistuje, je vyvolána výjimka `FileNotFoundException` – obalte volání try/catch blokem pro produkční kód.*

---

## Krok 4: Konfigurace engine a **perform OCR on image**

Vytvořte instanci `OcrEngine`, vyberte jazykový model, přiřaďte načtený obrázek a zavolejte `Recognize()`.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

Metoda `Recognize()` vrací objekt `OcrResult`, který obsahuje extrahovaný text, skóre důvěry a ohraničující rámečky. Jazykový modul je stažen automaticky při prvním použití, takže nejsou potřeba žádné další soubory.

---

## Krok 5: **extract text from JPG** a zobrazte jej

Nyní můžete **recognize text from picture** a výsledek vypsat. Vlastnost `Text` objektu `OcrResult` obsahuje prostý řetězec.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### Očekávaný výstup v konzoli

```
Recognized text:
Пример текста на кириллице
```

Pokud zdrojový obrázek obsahuje anglický text, výstup bude anglická věta, kterou jste umístili do obrázku.

---

## Okrajové případy a tipy pro nejlepší praxi

| Situace | Doporučení |
|-----------|----------------|
| **Large images ( > 5 MB )** | Zmenšete obrázek na ≤ 2000 px na delší straně před OCR, aby se snížila spotřeba paměti a zvýšila rychlost. |
| **Multiple languages in one picture** | Zavolejte `ocrEngine.AddLanguage(OcrLanguage.English)` kromě Cyrillic a poté nastavte `ocrEngine.Language = OcrLanguage.Multilingual`. |
| **Low‑contrast scans** | Zvyšte kontrast pomocí `System.Drawing.Graphics` před předáním bitmapy engine. |
| **Running on Linux/macOS** | Ujistěte se, že je nainstalována nativní závislost `libgdiplus` (`sudo apt-get install -y libgdiplus`). |
| **Repeated OCR calls** | Znovu použijte stejnou instanci `OcrEngine` a jen nahraďte `ocrEngine.Image`, abyste se vyhnuli opakovanému načítání modulu. |

---

## Kompletní spustitelný program

Níže je kompletní konzolová aplikace, která zahrnuje všechny předchozí kroky. Zkopírujte kód do nového C# konzolového projektu, nahraďte cestu k obrázku a spusťte jej.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Spuštění programu** vypíše rozpoznaný řetězec do konzole, což potvrzuje, že jste úspěšně **performed OCR on image** a **extracted text from JPG**.

---

## Závěr

Nyní víte, jak **perform OCR on image** soubory v C# pomocí Aspose.OCR, od instalace požadovaného **System.Drawing.Common package** po **load image for OCR**, výběr vhodného jazyka a nakonec **extract text from JPG**. Tento end‑to‑end příklad vám poskytuje pevný základ pro tvorbu pokročilejších pipeline pro zpracování dokumentů, jako je dávkové zpracování složek s obrázky nebo integrace OCR do webového API.

### Co dál?

* Prozkoumejte **recognize text from picture** v PDF konverzí každé stránky na obrázek nejprve.
* Experimentujte s vlastnostmi `OcrEngine` jako `Resolution`, `Threshold` a `MaxProcessingTime` pro doladění přesnosti na špatných skenech.
* Kombinujte výstup OCR s knihovnou pro zpracování přirozeného jazyka a automaticky kategorizujte extrahovaný obsah.

Neváhejte přizpůsobit kód pro jiné formáty obrázků, přidat ošetření chyb nebo jej integrovat do větších aplikací. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Extrahovat text z obrázku v C# – Kompletní průvodce Aspose OCR](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Extrahovat text z obrázku v C# s výběrem jazyka pomocí Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Jak provést extrakci textu z obrázku ze streamu pomocí Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}