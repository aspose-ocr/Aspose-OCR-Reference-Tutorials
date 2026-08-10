---
category: general
date: 2026-03-20
description: 'Rychle vytvořte prohledávatelný PDF: převod obrázku na PDF, extrakce
  textu z obrázku a přidání skryté textové vrstvy pro plnou prohledatelnost.'
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- pdf with hidden text
- scan image to pdf
language: cs
og_description: Vytvořte prohledávatelný PDF v C# převodem obrázku na PDF, extrakcí
  textu a vložením skryté vrstvy pro okamžité vyhledávání.
og_title: Vytvořte prohledávatelný PDF z obrázku – kompletní C# tutoriál
tags:
- Aspose
- C#
- OCR
- PDF generation
title: Vytvořte prohledávatelný PDF z obrázku v C# – krok za krokem
url: /cs/net/text-recognition/create-searchable-pdf-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF z obrázku v C# – Kompletní průvodce

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** ze skenované faktury, ale nechtěli jste vše přepisovat ručně? Nejste v tom sami. V mnoha kancelářských pracovních postupech je převod bitmapového skenu na PDF, které lze skutečně prohledávat, každodenní bolestivý bod. Dobrá zpráva? S několika řádky C# a knihovnami OCR a PDF od Aspose můžete celý proces automatizovat – bez ručního kopírování a vkládání.

V tomto tutoriálu si projdeme, jak **převést obrázek na PDF**, získat text z tohoto obrázku a poté text vrstvit neviditelně, aby finální soubor fungoval jako nativní PDF. Na konci budete mít připravenou metodu pro vytvoření **pdf s skrytým textem**, která funguje pro jakýkoli skenovaný dokument, ať už jde o fakturu, smlouvu nebo účtenku.

## Co budete potřebovat

- .NET 6.0 nebo novější (kód používá `using var` příkazy, takže aktuální SDK usnadňuje práci)
- NuGet balíčky Aspose.OCR a Aspose.Pdf (`Install-Package Aspose.OCR` a `Install-Package Aspose.Pdf`)
- Ukázkový soubor obrázku (PNG, JPG nebo TIFF), který obsahuje text, který chcete indexovat
- Visual Studio 2022 nebo jakékoli IDE, které preferujete

> **Tip:** Pokud pracujete s vícestránkovými skeny, stačí provést smyčku přes každý obrázek a opakovat kroky – stejná logika platí.

---

## Krok 1 – Inicializace OCR enginu (extrakce textu z obrázku)

Než můžeme vložit prohledávatelný text, musíme skutečně přečíst znaky z obrázku. `OcrEngine` od Aspose odvádí těžkou práci.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine and tell it which language to look for.
// English works for most invoices, but you can set Language.French, etc.
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Proč je to důležité:** Inicializace enginu se správným jazykem dramaticky zvyšuje přesnost. Pokud to přeskočíte, OCR může špatně rozpoznat čísla – něco, čemu rozhodně chcete v finančních dokumentech předejít.

---

## Krok 2 – Načtení vašeho skenovaného obrázku (převod obrázku na PDF)

Nyní načteme bitmapu do paměti. Aspose pracuje přímo s `System.Drawing.Image`, takže jakýkoli formát podporovaný .NET bude vyhovovat.

```csharp
using System.Drawing;

// Replace the path with the location of your scanned file.
var inputImage = Image.FromFile(@"C:\Docs\invoice.png");
```

Pokud máte workflow **scan image to PDF**, který již vytváří vícestránkový TIFF, stačí změnit příponu souboru a opakovat krok načítání pro každou stránku.

---

## Krok 3 – Spuštění OCR a zachycení rozpoznaného textu

S připraveným obrázkem požádáme OCR engine, aby udělal své kouzlo.

```csharp
// Perform OCR – the result contains the raw text and confidence scores.
var ocrResult = ocrEngine.Recognize(inputImage);

// For debugging, you might want to see what was read.
Console.WriteLine("OCR Output:");
Console.WriteLine(ocrResult.Text);
```

**Hraniční případ:** Pokud je obrázek nízkého rozlišení (< 300 dpi), klesá jistota. Zvažte zvětšení nebo opětovný sken s vyšším DPI před předáním enginu.

---

## Krok 4 – Vytvoření PDF a umístění původního obrázku jako pozadí

**pdf s skrytým textem** stále potřebuje vizuální reprezentaci skenu. Přidáme obrázek jako pozadí stránky.

```csharp
using Aspose.Pdf;

// Start a fresh PDF document.
var pdfDocument = new Document();

// Add a new page.
var pdfPage = pdfDocument.Pages.Add();

// Insert the image; it will fill the page by default.
pdfPage.Paragraphs.Add(new Aspose.Pdf.Image
{
    ImageInfo = new ImageInfo(@"C:\Docs\invoice.png")
});
```

**Proč používáme obrázek jako pozadí:** Uživatelé stále vidí přesný originální sken, zachovávají se podpisy a razítka, zatímco vrstva skrytého textu poskytuje možnost vyhledávání.

---

## Krok 5 – Překrytí OCR textu neviditelnou vrstvou (PDF s skrytým textem)

Zde je klíčová část: přidáme `TextFragment`, který leží nad obrázkem, ale je nastaven jako neviditelný. Aspose.Pdf to dělá jednoduchým.

```csharp
using Aspose.Pdf.Text;

// Create a text fragment from the OCR result.
var searchableText = new TextFragment(ocrResult.Text)
{
    // Position (0,0) aligns with the bottom‑left of the page.
    Position = new Position(0, 0),

    // Make the text invisible – it still participates in search.
    TextState = { Font = FontRepository.FindFont("Arial"), FontSize = 0.1f, IsHidden = true }
};

// Add the invisible text to the same page.
pdfPage.Paragraphs.Add(searchableText);
```

**Vysvětlení:** Nastavení velmi malé velikosti písma a označení fragmentu jako skrytého udržuje vizuální výstup čistý a zároveň zajišťuje, že textová vrstva PDF obsahuje výstup OCR. Vyhledávače a PDF čtečky jej indexují.

---

## Krok 6 – Uložení prohledávatelného PDF

Nakonec zapíšeme dokument na disk.

```csharp
// Choose a destination path.
string outputPath = @"C:\Docs\invoice_searchable.pdf";

// Save the PDF. The file now contains both the image and searchable text.
pdfDocument.Save(outputPath);

Console.WriteLine($"Searchable PDF created at: {outputPath}");
```

Otevřete výsledný soubor v Adobe Reader, stiskněte **Ctrl + F**, zadejte slovo, které jste viděli na faktuře, a uvidíte zvýrazněný výsledek – i když text nikdy nebyl viditelný.

---

## Kompletní funkční příklad (všechny kroky dohromady)

Níže je kompletní program, který můžete zkopírovat a vložit do konzolové aplikace. Překládá se a spouští tak, jak je, za předpokladu, že jsou nainstalovány NuGet balíčky a cesty k souborům jsou správné.

```csharp
// ------------------------------------------------------------
// Create Searchable PDF from Image – Complete C# Example
// ------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load scanned image
        var inputImagePath = @"C:\Docs\invoice.png";
        var inputImage = Image.FromFile(inputImagePath);

        // 3️⃣ Perform OCR
        var ocrResult = ocrEngine.Recognize(inputImage);
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);

        // 4️⃣ Create PDF and add image as background
        var pdfDocument = new Document();
        var pdfPage = pdfDocument.Pages.Add();
        pdfPage.Paragraphs.Add(new Aspose.Pdf.Image
        {
            ImageInfo = new ImageInfo(inputImagePath)
        });

        // 5️⃣ Add invisible searchable text layer
        var searchableText = new TextFragment(ocrResult.Text)
        {
            Position = new Position(0, 0),
            TextState = { Font = FontRepository.FindFont("Arial"), FontSize = 0.1f, IsHidden = true }
        };
        pdfPage.Paragraphs.Add(searchableText);

        // 6️⃣ Save the searchable PDF
        var outputPath = @"C:\Docs\invoice_searchable.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"✅ Searchable PDF saved to: {outputPath}");
    }
}
```

**Expected outcome:**  
- `invoice_searchable.pdf` vypadá identicky jako `invoice.png`.  
- Vyhledávání textu funguje pro jakékoli slovo, které se objevilo v originálním skenu.  
- Velikost souboru roste jen mírně (skrytý text přidá několik kilobajtů).

---

## Často kladené otázky a hraniční případy

### Můžu zpracovat více stránek v jednom PDF?
Ano. Zabalte logiku OCR‑a‑PDF do smyčky `foreach (string imagePath in imageFiles)`, vytvářející novou `Page` pro každou iteraci. Vrstva skrytého textu se přidává pro každou stránku, takže vyhledávání funguje v celém dokumentu.

### Co když můj dokument obsahuje více jazyků?
Nastavte `ocrEngine.Language` na `Language.Multilingual` nebo vytvořte samostatné enginy pro každý jazykový segment. Aspose vrátí výsledky v mixu jazyků, které můžete následně vložit do stejné PDF stránky.

### Jak mohu řídit DPI nebo škálování obrázku?
Před přidáním obrázku do PDF jej můžete změnit velikost pomocí `System.Drawing`:

```csharp
var resized = new Bitmap(inputImage, new Size(1240, 1754)); // A4 at 150 dpi
```

### Je skrytý text skutečně neviditelný ve všech prohlížečích?
Většina moderních prohlížečů respektuje příznak `IsHidden`. Pokud narazíte na prohlížeč, který stále zobrazuje drobný text, snižte velikost písma ještě více (např. `0.01f`) nebo nastavte barvu textu na plně transparentní pomocí `TextState.FillColor = Color.Transparent`.

### Co bezpečnost – mohu PDF chránit heslem?
Ano. Po dokončení přidávání obsahu zavolejte:

```csharp
pdfDocument.Encrypt("ownerPwd", "userPwd", EncryptionAlgorithms.AES256);
```

Nyní prohledávatelné PDF také respektuje zásady důvěrnosti vaší organizace.

---

## Tipy pro produkčně připravené implementace

- **Dávkové zpracování:** Použijte `Parallel.ForEach` pro velké sady obrázků, ale dejte pozor na nevláknově bezpečné instance `OcrEngine` – vytvořte jednu pro každé vlákno.
- **Zpracování chyb:** Zabalte volání OCR do try/catch; zkontrolujte `ocrResult.IsRecognized`, abyste přeskočili neúspěšné stránky.
- **Logování:** Ukládejte hodnoty `ocrResult.Confidence`; nízká jistota může naznačovat potřebu předzpracování obrázku (odklonění, odstranění šumu).
- **Výkon:** Znovu použijte stejný objekt `Document` pro všechny stránky, abyste se vyhnuli opakovanému otevírání/zavírání souborů.
- **Testování:** Porovnejte extrahovaný text z prohledávatelného PDF (`pdfDocument.Pages[1].ExtractText()`) s výstupem OCR, abyste zajistili, že nedošlo k oříznutí.

---

## Závěr

Právě jsme vám ukázali, jak **vytvořit prohledávatelné PDF** soubory z běžných obrázků pomocí C#. Extrahováním textu pomocí Aspose.OCR, vrstvením neviditelně na stránku PDF a uložením výsledku získáte dokument, který vypadá přesně jako originální sken, ale chová se jako nativní PDF. Tato technika pokrývá klasický workflow **convert image to PDF**, přidává **pdf s skrytým textem** a řeší každodenní potřebu **scan image to PDF**, kterou můžete skutečně prohledávat.

Jste připraveni na další krok? Zkuste rozšířit kód tak, aby dávkově zpracovával složku s účtenkami, nebo jej integrovat do webového API, které vrací prohledávatelná PDF za běhu. Můžete také experimentovat s různými fonty, přidat metadata nebo dokonce vložit skóre důvěry OCR jako PDF anotace pro auditní stopy.

Pokud se vám tento průvodce líbil, dejte mu hvězdičku, sdílejte ho s kolegy nebo zanechte komentář s vašimi úpravami. Šťastné kódování a ať jsou vaše PDF vždy prohledávatelná!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}