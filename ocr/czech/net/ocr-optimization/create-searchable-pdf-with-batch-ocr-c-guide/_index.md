---
category: general
date: 2025-12-29
description: Vytvořte prohledávatelný PDF ze skenovaných obrázků pomocí dávkového
  zpracování Aspose OCR. Naučte se převádět obrázky na PDF, předzpracovávat obrázky
  pro OCR a vyrovnávat skenované dokumenty.
draft: false
keywords:
- create searchable pdf
- batch ocr processing
- convert images to pdf
- preprocess images for ocr
- deskew scanned documents
language: cs
og_description: Vytvořte prohledávatelný PDF ze skenovaných obrázků pomocí dávkového
  zpracování OCR od Aspose. Naučte se převádět obrázky na PDF, předzpracovávat je
  pro OCR a vyrovnávat skenované dokumenty.
og_title: Vytvořte prohledávatelný PDF s dávkovým OCR – průvodce C#
tags:
- OCR
- C#
- PDF/A
- Aspose
title: Vytvořte prohledávatelný PDF s dávkovým OCR – průvodce C#
url: /cs/net/ocr-optimization/create-searchable-pdf-with-batch-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF pomocí dávkového OCR – průvodce pro C#  

Už jste někdy potřebovali **create searchable pdf** soubory z hromady naskenovaných obrázků, ale uvízli jste už v prvním kroku? Nejste v tom sami — většina vývojářů narazí na stejnou překážku při práci s nepořádkem ve skenech, nerovnoměrnými stránkami nebo prostým hromadným převodem.  

Dobrá zpráva? S Aspose OCR můžete spustit **batch OCR processing** pipeline, která nejen **convert images to pdf**, ale také **preprocess images for OCR** a dokonce **deskew scanned documents** automaticky. V tomto tutoriálu projdeme celý proces, od nastavení engine až po vylepšení výstupu, abyste jej mohli spustit na složce souborů a získali prohledávatelné PDF/A‑2b klenoty.

> **Co získáte:** jediné spustitelné C# console app, které vezme adresář obrázků (nebo PDF), vyčistí každou stránku,ustí OCR a uloží prohledávatelný PDF/A‑2b soubor vedle zdroje. Žádné fragmenty kódu, jen jedno koherentní řešení.

---

## Požadavky

- .NET 6 SDK nebo novější (kód se také kompiluje s .NET Core).  
- NuGet balíček Aspose OCR (`Aspose.OCR`).  
- Složka naskenovaných obrázků (TIFF, JPEG, PNG) nebo PDF, které chcete převést na prohledávatelné PDF.  
- (Volitelné) Skutečný licenční klíč — jinak režim zkušební verze přidá vodoznak, ale pro testování funguje.

Pokud to máte, pojďme na to.

## Přehled – Jak celý pipeline vytváří prohledávatelné PDF

1. **Activate trial mode** (nebo načtěte svou licenci).  
2. **Configure `OcrBatchProcessor`** – řekněte mu, kde číst soubory, kam zapisovat PDF, který formát použít a kolik vláken spouštět paralelně.  
3. **Pre‑process each image** – deskew, denoise a odstranit pozadí, aby OCR engine viděl čistou stránku.  
4. **Run the batch** – Aspose zpracuje každý soubor, spustí OCR a zapíše prohledávatelný PDF/A‑2b.  
5. **Notify completion** – jednoduchá zpráva v konzoli, ale můžete připojit logger nebo webhook.

To je vysoká úroveň toku. Kód níže implementuje každý krok s množstvím komentářů, takže můžete upravit jakoukoli část, aniž byste rozbili celý proces.

## Krok 1 – Activate trial mode (nebo načtěte svou licenci)

Než můžete volat jakoukoli třídu Aspose, musíte knihovně vědět, že máte licenci. Pro rychlé experimenty stačí režim zkušební verze.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using Aspose.OCR.Batch;

// Activate trial mode – replace with OcrEngine.SetLicense("YourLicenseFile.lic") for production
OcrEngine.EnableTrialMode();
```

> **Pro tip:** udržujte aktivaci licence na úplném začátku `Program.cs`. Pokud zapomenete, engine vyhodí výjimku při první volání `Process()`.

## Krok 2 – Configure the batch OCR processing engine

Zde nastavujeme objekt **batch OCR processing**. Všimněte si, že `InputFolder` a `OutputFolder` jsou v tomto příkladu stejné, ale můžete je rozdělit, pokud chcete.

```csharp
// Define where your source images live and where the searchable PDFs should be saved
var ocrBatch = new OcrBatchProcessor
{
    // Folder that contains the images or PDFs to be processed
    InputFolder = @"C:\Scans\Incoming",

    // Folder where searchable PDF/A‑2b files will be saved
    OutputFolder = @"C:\Scans\Processed",

    // Choose the output format – searchable PDF/A‑2b (perfect for archiving)
    OutputFormat = SaveFormat.SearchablePdf,

    // Limit the number of concurrent OCR operations to avoid CPU spikes
    MaxDegreeOfParallelism = 3,

    // Pre‑process each image: deskew, denoise, and remove background
    Preprocess = img => ImageFilters
                            .Deskew(img)          // fixes rotated pages
                            .Denoise()            // reduces speckles
                            .RemoveBackground()   // clears colored backgrounds
};
```

### Proč jsou tato nastavení důležitá

- **`MaxDegreeOfParallelism`**: Spuštění příliš mnoha OCR vláken může přetížit CPU, zejména na skromném pracovním stanovišti. Tři vlákna jsou optimální pro většinu čtyřjádrových notebooků.  
- **`Preprocess`** pipeline: Tři filtry dohromady dramaticky zlepšují přesnost OCR. Deskew opravuje běžný problém „nakloněného skenu“, denoise odstraňuje náný šum a odstranění pozadí zajišťuje, že engine vidí jen černý text na bílém pozadí.  
- **`SaveFormat.SearchablePdf`**: Vytváří PDF/A‑2b soubory, které jsou jak archivně připravené, tak prohledávatelné — požadavek mnoha standardů compliance.

## Krok 3 – Execute the batch a sledujte, jak se děje magie

Spuštění batch je tak jednoduché jako volání `Process()`. Metoda blokuje, dokud není každý soubor hotov, pak vrátí. Pokud potřebujete hlášení postupu, můžete připojit událost `ProgressChanged` (není zde ukázáno).

```csharp
// Start processing – this will walk through every file in InputFolder
ocrBatch.Process();

// Let the user (or calling script) know we’re finished
Console.WriteLine("All files processed. Searchable PDFs are ready.");
```

Když konzole vytiskne poslední řádek, najdete prohledávatelný PDF pro každý vstupní obrázek v `C:\Scans\Processed`. Otevřete kterýkoli v Adobe Reader, stiskněte **Ctrl+F** a můžete vyhledávat text, který byl právě extrahován ze skenu.

## Krok 4 – Full runnable program (připravený ke kopírování)

Níže je **complete, self‑contained** program, který můžete vložit do nového konzolového projektu (`dotnet new console`). Ujistěte se, že jste nejprve přidali NuGet balíček Aspose.OCR (`dotnet add package Aspose.OCR`).

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using Aspose.OCR.Batch;

namespace CreateSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Activate trial mode (replace with real license for production)
            OcrEngine.EnableTrialMode();

            // 2️⃣ Configure batch OCR processing
            var ocrBatch = new OcrBatchProcessor
            {
                InputFolder = @"C:\Scans\Incoming",   // 👉 change to your source folder
                OutputFolder = @"C:\Scans\Processed", // 👉 change to your target folder
                OutputFormat = SaveFormat.SearchablePdf,
                MaxDegreeOfParallelism = 3,
                Preprocess = img => ImageFilters
                                        .Deskew(img)          // fixes rotated pages
                                        .Denoise()            // cleans up noise
                                        .RemoveBackground()   // strips colored backgrounds
            };

            // 3️⃣ Run the batch
            ocrBatch.Process();

            // 4️⃣ Notify completion
            Console.WriteLine("All files processed. Searchable PDFs are ready.");
        }
    }
}
```

### Očekávaný výstup

```
All files processed. Searchable PDFs are ready.
```

Po spuštění, přechod do `C:\Scans\Processed` odhalí sadu souborů `.pdf` — každý je prohledávatelný, každý splňuje PDF/A‑2b. Otevřete libovolný soubor, napište slovo, o kterém víte, že se v původním skenu vyskytuje, a voilà, text je zvýrazněn.

## Časté otázky a řešení okrajových případů

### Co když můj zdrojový adresář již obsahuje PDF?

Aspose OCR může přímo načíst PDF; rasterizuje každou stránku, použije stejné **preprocess** filtry a vloží OCR vrstvu. Žádný další kód není potřeba.

### Jak změním výstupní formát na obyčejné PDF (neprohledávatelné)?

Vyměňte `SaveFormat.SearchablePdf` za `SaveFormat.Pdf`. Ztratíte vrstvu prohledávatelného textu, ale vizuální věrnost zůstane stejná.

### Mé skeny jsou barevné — ovlivní to odstranění pozadí?

`RemoveBackground()` cílí na ne‑bílá pozadí při zachování hlavního textu. Pokud potřebujete zachovat barevnou grafiku, můžete tento filtr vynechat:

```csharp
.Preprocess = img => ImageFilters.Deskew(img).Denoise()
```

### Běží na serveru s omezenou RAM — mohu snížit počet vláken?

Určitě. Nastavte `MaxDegreeOfParallelism` na `1` nebo `2`. Batch bude trvat déle, ale využití paměti zůstane nízké.

## Vizualizovaný souhrn (volitelné)

Pokud máte rádi rychlý diagram, představte si tento tok:

![Workflow pro vytvoření prohledávatelného PDF – ukazuje vstupní složku → předzpracování → OCR → výstup prohledávatelného PDF](/images/ocr-workflow.png)

*Image alt text:* **Diagram workflowu pro vytvoření prohledávatelného PDF** – ilustruje dávkové zpracování OCR, konverzi a kroky deskew.

## Závěr

Nyní máte **complete, production‑ready** řešení pro **create searchable pdf** soubory z libovolné dávky naskenovaných obrázků. Využitím **batch OCR processing** můžete **convert images to pdf**, **preprocess images for OCR** a automaticky **deskew scanned documents** — vše jen s několika řádky C#.

Další kroky? Zkuste přidat vlastní pojmenovací schéma, připojit logovací framework pro zachycení skóre důvěryhodnosti OCR, nebo experimentovat s dalšími `ImageFilters` jako `Sharpen()` pro slabý text. Aspose OCR API je dostatečně flexibilní, aby rostlo s vašimi potřebami.

Šťastné kódování a ať jsou vaše PDF vždy prohledávatelné!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}