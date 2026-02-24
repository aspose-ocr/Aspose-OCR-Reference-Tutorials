---
category: general
date: 2026-02-24
description: Jak používat OCR v C# k extrakci textu z obrazových souborů. Naučte se
  převádět PNG na text, asynchronně číst obrázky a řešit běžné úskalí.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert png to text
- how to extract text
- how to read image
language: cs
og_description: Jak použít OCR v C# k extrakci textu z obrázků. Tento průvodce ukazuje
  krok za krokem asynchronní OCR s Aspose, zahrnující konverzi, zpracování chyb a
  osvědčené postupy.
og_title: Jak používat OCR v C# – kompletní průvodce
tags:
- OCR
- C#
- Aspose
title: Jak používat OCR v C# – Extrahovat text z obrázku pomocí Aspose OCR
url: /cs/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR v C# – Extrahovat text z obrázku

Už jste se někdy zamysleli **jak používat OCR** k získání textu z obrázku, aniž byste ho museli ručně psát? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují *extrahovat text z obrázku* souborů jako PNG a běžný copy‑paste přístup prostě nefunguje.  

V tomto tutoriálu vás provedeme kompletním, asynchronním řešením, které **převádí PNG na text** pomocí knihovny Aspose.OCR. Na konci přesně budete vědět, jak číst soubory s obrázky, zpracovávat chyby a integrovat výsledek do vašich aplikací.  

Probereme vše od nastavení NuGet balíčku až po ladění OCR enginu pro vyšší přesnost a přidáme tipy, co dělat, když obrázek není ostrý. Není třeba honit se za odkazy na dokumentaci – vše, co potřebujete, je zde.

## Co budete potřebovat

- .NET 6.0 nebo novější (kód funguje také na .NET Core a .NET Framework)  
- Visual Studio 2022 (nebo jakékoli IDE, které preferujete)  
- NuGet balíček **Aspose.OCR** (`Install-Package Aspose.OCR`)  
- Soubor s obrázkem (PNG, JPG, BMP), který chcete zpracovat – nazveme jej `input.png`

To je vše. Pokud máte tyto položky zaškrtnuté, můžete začít.

![Diagram ukazující OCR workflow – jak použít OCR k extrakci textu z obrázku](/images/ocr-workflow.png)

## Krok 1: Nainstalujte Aspose.OCR a přidejte jmenné prostory

Nejprve přidejte knihovnu do svého projektu. Otevřete Package Manager Console a spusťte:

```powershell
Install-Package Aspose.OCR
```

Poté na začátku vašeho C# souboru zahrňte potřebné jmenné prostory:

```csharp
using Aspose.OCR;
using System;
using System.Threading.Tasks;
```

> **Tip:** Pokud používáte .NET 6 minimal APIs, můžete tyto `using` direktivy umístit do globálního souboru, abyste je nemuseli opakovat v různých třídách.

### Proč je to důležité

`Aspose.OCR` jmenný prostor vám poskytuje přístup k `OcrEngine`, jádrové třídě, která skutečně čte obrázek. Bez něj byste museli psát vlastní kód pro analýzu pixelů – obrovská noční můra. Přidání jmenných prostorů udržuje kód přehledný a dává kompilátoru vědět, kde najít typy, které budete používat.

## Krok 2: Vytvořte asynchronní OCR engine

Zabalíme volání OCR do `async` metody, aby vaše UI zůstalo responzivní a server‑side kód mohl škálovat. Zde je kostra konzolové aplikace:

```csharp
class AsyncExample
{
    static async Task Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Recognize text from the image asynchronously
        OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");

        // Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Vysvětlení

- **`OcrEngine ocrEngine = new OcrEngine();`** – Vytvoří instanci engine s výchozím nastavením. Později můžete upravit jazyk, režim detekce nebo předzpracovat filtry.
- **`await ocrEngine.RecognizeImageAsync(...)`** – Asynchronní metoda vrací `Task<OcrResult>`. Čekáním na ni uvolníte vlákno, zatímco OCR běží na pozadí.
- **`ocrResult.Text`** – Textová reprezentace všeho, co engine dokázal přečíst. To je podstata *jak extrahovat text* z obrázku.

## Krok 3: Doladit engine pro lepší přesnost

Standardní OCR funguje dobře na čistých, vysokokontrastních obrázcích, ale reálné snímky často potřebují trochu pomoci. Před voláním `RecognizeImageAsync` můžete upravit několik vlastností:

```csharp
// Set language (English is default, but you can add more)
ocrEngine.Language = OcrLanguage.English;

// Enable automatic image preprocessing (deskew, despeckle)
ocrEngine.ImagePreprocessingOptions = ImagePreprocessingOptions.Auto;

// If you only need numbers, restrict the character set
ocrEngine.Characters = "0123456789";
```

### Kdy použít tato nastavení

- **Nízká kvalita skenů** – Zapněte `ImagePreprocessingOptions.Auto`, aby Aspose odstranil šum.
- **Vícejazyčné PDF** – Změňte `Language` na `OcrLanguage.French` nebo kombinujte jazyky pomocí bitmasky.
- **Formulářová pole** – Omezte `Characters` na číslice nebo velká písmena, aby se snížil počet falešných pozitiv.

## Krok 4: Ošetřete chyby elegantně

OCR není kouzlo; může selhat, pokud soubor chybí, je poškozený nebo v nepodporovaném formátu. Zabalte asynchronní volání do try/catch bloku:

```csharp
try
{
    OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");
    Console.WriteLine("Extracted Text:");
    Console.WriteLine(ocrResult.Text);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"File not found: {ex.Message}");
}
catch (OcrException ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

### Proč to pomáhá

Poskytování jasných chybových zpráv urychluje ladění a zlepšuje uživatelský zážitek. Místo obecného pádu získáte užitečnou výzvu, která vám řekne, zda zkontrolovat cestu, formát souboru nebo konfiguraci OCR engine.

## Krok 5: Sestavte vše dohromady – Kompletní funkční příklad

Níže je kompletní, připravený ke spuštění konzolový program, který demonstruje **jak používat OCR**, aplikuje předzpracování a ošetřuje chyby. Zkopírujte jej do nového `.csproj` a stiskněte F5.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Threading.Tasks;

class AsyncOcrDemo
{
    static async Task Main()
    {
        // 1️⃣  Initialize the OCR engine with optional tweaks
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ImagePreprocessingOptions = ImagePreprocessingOptions.Auto
        };

        // 2️⃣  Define the path to the image you want to read
        string imagePath = Path.Combine(Environment.CurrentDirectory, "input.png");

        // 3️⃣  Perform the async recognition inside a safe try/catch
        try
        {
            OcrResult result = await ocrEngine.RecognizeImageAsync(imagePath);
            Console.WriteLine("\n--- Extracted Text ---\n");
            Console.WriteLine(result.Text);
            Console.WriteLine("\n--- End of Output ---\n");
        }
        catch (FileNotFoundException fnf)
        {
            Console.Error.WriteLine($"❌ Image not found: {fnf.Message}");
        }
        catch (OcrException ocrEx)
        {
            Console.Error.WriteLine($"❌ OCR processing error: {ocrEx.Message}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Unexpected error: {ex.Message}");
        }
    }
}
```

**Očekávaný výstup** (předpokládáme, že `input.png` obsahuje frázi „Hello World“):

```
--- Extracted Text ---

Hello World

--- End of Output ---
```

Pokud je obrázek rozmazaný, můžete vidět nadbytečné znaky nebo chybějící slova – zde přicházejí na řadu předzpracovací možnosti ze Krok 3.

## Krok 6: Rozšíření řešení – z PNG na PDF nebo textové soubory

Někdy potřebujete **převést PNG na text** a poté výsledek uložit do `.txt` nebo vložit do PDF reportu. Zde je rychlý úryvek, který zapisuje OCR výstup do souboru:

```csharp
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.txt");
await File.WriteAllTextAsync(outputPath, result.Text);
Console.WriteLine($"✅ Text saved to {outputPath}");
```

Nebo pokud generujete PDF pomocí Aspose.PDF:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// ... after OCR result is obtained
Document pdfDoc = new Document();
Page page = pdfDoc.Pages.Add();
TextFragment fragment = new TextFragment(result.Text);
page.Paragraphs.Add(fragment);
pdfDoc.Save("Result.pdf");
Console.WriteLine("✅ PDF created with extracted text.");
```

Tato rozšíření ukazují, jak **číst data z obrázku** může napájet následné procesy – generování reportů, indexování pro vyhledávání nebo dokonce napájení jazykového modelu.

## Často kladené otázky a okrajové případy

| Question | Answer |
|----------|--------|
| *Jaké formáty obrázků jsou podporovány?* | Aspose.OCR podporuje PNG, JPEG, BMP, TIFF a GIF. Pokud máte PDF, nejprve extrahujte jeho stránky jako obrázky. |
| *Mohu zpracovávat více obrázků paralelně?* | Ano – zabalte každé volání `RecognizeImageAsync` do vlastního úkolu a použijte `Task.WhenAll`. Jen mějte na paměti využití paměti. |
| *Co když OCR vrátí prázdný text?* | Zkontrolujte kvalitu obrázku: nízký kontrast nebo otočený text často selhává. Aktivujte `ImagePreprocessingOptions.Deskew` nebo obrázek před OCR ručně otočte. |
| *Existuje limit na velikost obrázku?* | Velké obrázky (>10 MP) mohou způsobit `OutOfMemoryException`. Před rozpoznáním je zmenšete na rozumné rozlišení (např. 300 DPI). |
| *Potřebuji licenci pro Aspose.OCR?* | Vývojový režim funguje s dočasnou licencí, ale pro produkci budete potřebovat zakoupenou licenci k odstranění evaluačních vodoznaků. |

## Tipy pro výkon

- **Znovu použijte instanci `OcrEngine`** pro dávkové zpracování; vytvoření nového engine pro každý obrázek přidává režii.
- **Vypněte nepoužívané jazyky** pro zrychlení detekce – každý další jazyk přidává malou výpočetní zátěž.
- **Spusťte OCR na pozadí** (jak je ukázáno) pro udržení rychlých UI vláken v desktopových nebo webových aplikacích.

## Závěr

Probrali jsme **jak používat OCR** v C# od začátku do konce: instalaci Aspose.OCR, psaní asynchronní metody, ladění nastavení pro špinavé obrázky, ošetření chyb a ukládání výsledků. Nyní máte spolehlivý způsob, jak *extrahovat text z obrázku* souborů, *převést PNG na text* a dokonce tento text použít v dalších pracovních postupech, jako je generování PDF.  

Jste připraveni na další výzvu? Zkuste vložit výstup OCR do prohledávatelného indexu Azure Cognitive Search, nebo experimentujte s vícejazyčným OCR přidáním `OcrLanguage.Spanish | OcrLanguage.French` do engine. Možnosti jsou neomezené, když víte **jak programově číst data z obrázku**.  

*Pokud se vám tento průvodce líbil, dejte mu hvězdičku na GitHubu, sdílejte ho s kolegy nebo zanechte komentář níže s vašimi vlastními OCR tipy. Šťastné kódování!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}