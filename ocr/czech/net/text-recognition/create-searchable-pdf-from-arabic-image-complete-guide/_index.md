---
category: general
date: 2026-02-11
description: Vytvořte prohledávatelný PDF z arabského obrázku v C#. Naučte se, jak
  převést obrázek na PDF, extrahovat arabský text a přidat skrytý text pomocí Aspose
  OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract arabic text
- pdf with hidden text
- ocr arabic image
language: cs
og_description: Vytvořte prohledávatelný PDF z arabského obrázku pomocí Aspose OCR
  v C#. Postupujte podle tohoto návodu, abyste obrázek převedli na PDF, extrahovali
  arabský text a vložili skrytý text.
og_title: Vytvořte prohledávatelný PDF z arabského obrázku – krok po kroku
tags:
- Aspose
- OCR
- PDF
- C#
- Arabic
title: Vytvořte prohledávatelný PDF z arabského obrázku – kompletní průvodce
url: /cs/net/text-recognition/create-searchable-pdf-from-arabic-image-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF z arabského obrázku – Kompletní průvodce

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** ze skenované arabské faktury, ale nebyli jste si jisti, jak zachovat původní vzhled a zároveň učinit text výběratelným? Nejste v tom sami. V mnoha projektech automatizace dokumentů není výzvou jen převod obrázku na PDF, ale také zachování vizuálního rozvržení a přidání skryté textové vrstvy, kterou mohou indexovat vyhledávače.

V tomto tutoriálu projdeme celý proces: **převod obrázku na PDF**, **extrakci arabského textu** pomocí Aspose OCR a nakonec vložíme tento text jako **PDF se skrytým textem**, takže výsledný soubor bude plně prohledávatelný. Na konci budete mít připravený úryvek kódu v C#, který můžete vložit do jakéhokoli .NET řešení. Žádné externí služby, jen knihovny Aspose, které již máte.

## Co budete potřebovat

- .NET 6 nebo novější (kód funguje také s .NET Core)  
- **Aspose.OCR** a **Aspose.Pdf** NuGet balíčky (nejnovější verze k únoru 2026)  
- Arabský obrázek (např. `arabic_invoice.jpg`), který chcete převést na prohledávatelné PDF  
- Trochu znalostí C# – koncepty jsou jednoduché, ale vysvětlíme „proč“ za každým řádkem.

> **Tip:** Pokud jste ještě nepřidali NuGet balíčky, spusťte  
> `dotnet add package Aspose.OCR` a  
> `dotnet add package Aspose.Pdf` z adresáře projektu.

Nyní, když jsou předpoklady za sebou, pojďme se ponořit do krok‑za‑krokem implementace.

## Krok 1 – Nastavení OCR enginu pro arabský text

První věc, kterou musíme udělat, je nakonfigurovat Aspose OCR tak, aby rozpoznával arabské znaky. Arabština je skript psaný zprava doleva, takže musíme enginu sdělit, jaký jazyk načíst, a povolit automatické stahování zdrojů pro případ, že jazyková data nejsou již na počítači.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Configure OCR for Arabic and let Aspose fetch the language pack if needed
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Arabic,
    AutomaticResourceDownload = true
};
```

**Proč je to důležité:**  
Pokud vynecháte nastavení `Language = OcrLanguage.Arabic`, engine bude ve výchozím nastavení používat angličtinu a skončíte s nečitelnými znaky. Povolení `AutomaticResourceDownload` vás ušetří od ručního umisťování jazykových souborů na server.

## Krok 2 – Načtení zdrojového obrázku

Dále načteme obrázek, který obsahuje arabský text. Použití `Image.FromFile` zajistí, že obrázek bude načten do objektu GDI+ `Image`, který Aspose OCR očekává.

```csharp
using System.Drawing;          // For Image
using System.IO;                // For MemoryStream

// Replace with the actual path to your Arabic invoice
string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";

using (var inputImage = Image.FromFile(imagePath))
{
    // The rest of the workflow lives inside this using block
```

**Hraniční případ:**  
Pokud je obrázek obrovský (např. skenovaná stránka A3), zvažte nejprve jeho zmenšení pro zlepšení výkonu. OCR engine dokáže zpracovat velké soubory, ale spotřeba paměti rychle roste.

## Krok 3 – Rozpoznání arabského textu a zachycení výsledku

Nyní skutečně spustíme OCR. Metoda `Recognize` vrací objekt `OcrResult`, který obsahuje detekovaný text, skóre spolehlivosti a ohraničující rámečky (pokud je někdy budete potřebovat pro pokročilou analýzu rozvržení).

```csharp
    // Perform OCR on the loaded image
    OcrResult ocrResult = ocrEngine.Recognize(inputImage);
    string extractedText = ocrResult.Text;

    // Quick sanity check: print the first 200 characters to the console
    Console.WriteLine("Extracted Arabic text (preview):");
    Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Proč si ponechat náhled?**  
Zobrazení úryvku extrahovaného textu vám pomůže ověřit, že jazykový balíček byl načten správně, než ztratíte čas generováním PDF.

## Krok 4 – Vytvoření nového PDF dokumentu a přidání prázdné stránky

S textem v ruce můžeme začít sestavovat PDF. Aspose PDF nám poskytuje objekt `Document`, který představuje celý soubor. Přidání stránky nám poskytne plátno, kam umístit jak původní obrázek, tak skrytou textovou vrstvu.

```csharp
    // Initialize a new PDF document
    var pdfDocument = new Aspose.Pdf.Document();

    // Add a blank page – this will become the background for our image
    var pdfPage = pdfDocument.Pages.Add();
```

**Poznámka:**  
Můžete přidat více stránek, pokud zpracováváte vícestránkový TIFF nebo PDF, ale pro scénář s jedním obrázkem stačí jedna stránka.

## Krok 5 – Vložení původního obrázku jako pozadí

Chceme, aby konečné PDF vypadalo přesně jako skenovaná faktura, takže vložíme obrázek jako viditelné pozadí. Třída `Image` z Aspose PDF očekává stream, takže soubor načteme do `MemoryStream`.

```csharp
    // Load the same image bytes for the PDF background
    var backgroundImage = new Aspose.Pdf.Image
    {
        ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
    };

    // Add the image to the page's paragraph collection
    pdfPage.Paragraphs.Add(backgroundImage);
```

**Proč použít obrázek jako pozadí?**  
Umístění obrázku přímo na stránku zachová původní rozvržení, barvy a případné razítka nebo loga, která by OCR engine jinak ignoroval.

## Krok 6 – Přidání OCR textu jako skryté vrstvy

Tajnou ingrediencí pro **prohledávatelné PDF** je skrytá textová vrstva, která leží nad obrázkem. Nastavením velikosti písma na `0` učiníme text neviditelným pro lidské oko, ale stále výběratelným a prohledávatelným.

```csharp
    // Create a TextFragment with the extracted Arabic text
    var searchableText = new Aspose.Pdf.Text.TextFragment(extractedText)
    {
        // Hide the visible text; only the text layer remains searchable
        TextState = { FontSize = 0 }
    };

    // Add the hidden text fragment to the same page
    pdfPage.Paragraphs.Add(searchableText);
```

**Důležitý detail:**  
Pokud potřebujete, aby skrytý text byl dokonale zarovnán s obrázkem (např. když OCR vrací souřadnice), můžete použít `TextFragmentAbsorber` a umístit každý fragment ručně. Pro většinu faktur stačí jednoduchý překrytí celé stránky.

## Krok 7 – Uložení prohledávatelného PDF

Nakonec zapíšeme PDF na disk. Výstupní soubor bude obsahovat jak vizuální obrázek, tak skrytý arabský text, což umožní plné prohledávání v Adobe Reader, Google Drive nebo jakémkoli pro OCR připraveném prohlížeči.

```csharp
    // Define the output path
    string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";

    // Save the document
    pdfDocument.Save(outputPath);

    Console.WriteLine($"Searchable PDF created at: {outputPath}");
}
```

### Kompletní funkční příklad

Sestavením všech částí dohromady získáte kompletní, připravený k spuštění program:

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR for Arabic
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Arabic,
            AutomaticResourceDownload = true
        };

        // 2️⃣ Load the source image
        string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";
        using (var inputImage = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR and get the text
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);
            string extractedText = ocrResult.Text;

            // Optional preview
            Console.WriteLine("Extracted Arabic text (preview):");
            Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));

            // 4️⃣ Create PDF document
            var pdfDocument = new Document();
            var pdfPage = pdfDocument.Pages.Add();

            // 5️⃣ Add original image as background
            var backgroundImage = new Aspose.Pdf.Image
            {
                ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
            };
            pdfPage.Paragraphs.Add(backgroundImage);

            // 6️⃣ Add hidden searchable text
            var searchableText = new TextFragment(extractedText)
            {
                TextState = { FontSize = 0 }
            };
            pdfPage.Paragraphs.Add(searchableText);

            // 7️⃣ Save the searchable PDF
            string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";
            pdfDocument.Save(outputPath);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Očekávaný výsledek:**  
Otevřete vygenerovaný `arabic_invoice_searchable.pdf` v libovolném PDF prohlížeči, stiskněte **Ctrl + F** a zadejte arabské slovo, které se nachází na původní faktuře. Prohlížeč by měl slovo najít, i když nevidíte žádnou textovou vrstvu.

## Časté otázky a úskalí

- **Funguje to i s jinými jazyky?**  
  Naprosto. Stačí změnit `Language = OcrLanguage.YourLanguage` a ujistit se, že jazykový balíček je k dispozici. Zbytek pipeline zůstává stejný.

- **Co když je spolehlivost OCR nízká?**  
  Můžete zkontrolovat `ocrResult.Confidence` (hodnota mezi 0 a 1). Pokud klesne pod prahovou hodnotu (např. 0,75), zvažte předzpracování obrázku – vyrovnání, zvýšení kontrastu nebo převod na odstíny šedi – před předáním enginu.

- **Mohu přidat více obrázků do jednoho PDF?**  
  Ano. Projděte kolekci cest k obrázkům, přidejte novou stránku pro každý obrázek a opakujte kroky 5‑6. Jen nezapomeňte zachovat `using` blok pro každý obrázek, aby se uvolnily GDI zdroje.

- **Je skrytý text skutečně neviditelný?**  
  Nastavení `FontSize = 0` dělá text neviditelným ve většině prohlížečů. Pokud některý prohlížeč stále zobrazuje slabý znak, můžete také nastavit barvu textu na plně průhlednou (`TextState.FillColor = Color.Transparent`).

## Další kroky

Nyní, když víte, jak **vytvořit prohledávatelné PDF** z arabského obrázku, můžete zkoumat:

- **Dávkové zpracování** – načíst všechny obrázky ve složce a vygenerovat jedno prohledávatelné PDF pro každý soubor.  
- **Přidání OCR souřadnic** – použijte `OcrResult.Regions` k umístění každého textového fragmentu přesně tam, kde se nachází, což zlepšuje přesnost vyhledávání u složitých rozvržení.  
- **Šifrování PDF** – Aspose PDF vám umožní přidat hesla nebo digitální podpisy, pokud potřebujete vyšší zabezpečení.  
- **Integrace s Azure Blob Storage** – ukládejte vygenerovaná PDF přímo do cloudu pro následné pracovní postupy.

Každé z těchto témat přirozeně zahrnuje sekundární klíčová slova **convert image to pdf**, **extract**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}