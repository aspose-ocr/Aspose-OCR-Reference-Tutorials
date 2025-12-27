---
category: general
date: 2025-12-27
description: Vytvořte konzolový logger v C# a povolte automatické stahování do správných
  tabulek pomocí AsposeAI. Naučte se, jak zobrazit výstup opravených tabulek během
  několika kroků.
draft: false
keywords:
- create console logger
- enable auto download
- how to correct tables
- setup console logger
- display corrected table
language: cs
og_description: Vytvořte konzolový logger v C# a povolte automatické stahování do
  správných tabulek pomocí AsposeAI. Postupujte podle tohoto návodu, abyste rychle
  zobrazili výstup opravených tabulek.
og_title: Vytvořte konzolový logger a opravte tabulky pomocí AsposeAI
tags:
- AsposeAI
- C#
- OCR
- Table processing
title: Vytvořte konzolový logger a opravte tabulky pomocí AsposeAI
url: /cs/net/ocr-optimization/create-console-logger-and-correct-tables-with-asposeai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte konzolový logger a opravte tabulky pomocí AsposeAI

Už jste někdy potřebovali **vytvořit konzolový logger** pro C# AI pipeline, ale nevedeli jste, kde začít? V tomto průvodci projdeme celý proces – jak vytvořit konzolový logger, povolit automatické stahování modelových souborů a nakonec **jak opravit tabulky**, které vznikly po OCR. Na konci budete schopni **zobrazit opravené tabulky** ve své konzoli pomocí několika řádků kódu.

Probereme vše od počátečního nastavení loggeru až po finální úklid, takže nebudete muset prohledávat roztříštěnou dokumentaci. Předchozí zkušenost s AsposeAI není vyžadována; stačí základní znalost C# a .NET. Po cestě vám naservírujeme tipy na **nastavení konzolového loggeru**, zmíníme okrajové případy a ukážeme, jak by měl výstup vypadat.

---

## Požadavky

Než se pustíme do práce, ujistěte se, že máte po ruce následující:

- .NET 6.0 nebo novější (kód používá moderní jazykové funkce)
- Visual Studio 2022 nebo jakékoli IDE podporující C# projekty
- **Aspose.AI** NuGet balíček nainstalovaný (`Install-Package Aspose.AI`)
- **Aspose.OCR** NuGet balíček nainstalovaný (`Install-Package Aspose.OCR`)
- Vzorek objektu OCR výsledku (`ocrResult`) získaný z předchozího volání Aspose.OCR

Pokud vám něco chybí, zastavte se nyní a doplňte to – později vám to usnadní práci.

---

## Krok 1: Vytvořte konzolový logger a inicializujte AsposeAI

První věc, kterou potřebujeme, je logger zapisující přímo do konzole. To usnadňuje ladění a poskytuje okamžitou zpětnou vazbu během běhu AI enginu.

```csharp
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

// Step 1: Create a logger that writes to the console
ILogger consoleLogger = new ConsoleLogger();

// Step 2: Initialise the AsposeAI engine with the logger
AsposeAI asposeAI = new AsposeAI(consoleLogger);
```

**Proč je to důležité:**  
`ConsoleLogger` implementuje rozhraní `ILogger`, takže všechny interní zprávy z AsposeAI (načítání modelu, stav post‑processoru, chyby) se okamžitě objeví ve vašem terminálu. Je to nejjednodušší způsob, jak **nastavit konzolový logger** bez nutnosti přidávat externí logging frameworky.

> **Tip:** Pokud později budete potřebovat logování do souboru, stačí vyměnit `ConsoleLogger` za vlastní logger implementující `ILogger` – zbytek kódu zůstane nedotčen.

---

## Krok 2: Povolit automatické stahování AI modelů

AsposeAI dokáže načíst potřebné modelové soubory za běhu. Zapnutí této funkce vám ušetří ruční stahování velkých binárních souborů.

```csharp
// Step 3: (Optional) Configure automatic model download and set the model directory
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,               // <‑‑ enable auto download
    DirectoryModelPath = "YOUR_DIRECTORY"   // change to a writable folder
};
```

**Co může selhat?**  
Pokud `DirectoryModelPath` ukazuje na umístění jen pro čtení, automatické stažení selže a v konzoli se zobrazí výjimka. Ujistěte se, že složka existuje a aplikace má práva zápisu.

---

## Krok 3: Vytvořte post‑processor tabulek (jak opravit tabulky)

Tabulky extrahované z OCR jsou často nepořádné – sloučené buňky, chybějící okraje nebo nesprávně zarovnaný text. `TableAIProcessor` z AsposeAI je dokáže automaticky vyčistit.

```csharp
// Step 4: Create a table post‑processor that lets the engine decide when to run correction
TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);
```

**Proč režim AUTO?**  
`AITableDetectionMode.AUTO` nechá engine prozkoumat OCR výstup a rozhodnout, zda je korekce potřeba. Pokud dáváte přednost manuální kontrole, můžete použít `MANUAL` a volat `RunCorrection()` sami.

---

## Krok 4: Připojte post‑processor a jeho konfiguraci

Nyní vše spojíme – logger, konfiguraci modelu a tabulkový processor.

```csharp
// Step 5: Attach the post‑processor and its configuration to the AI engine
asposeAI.SetPostProcessor(tableProcessor, modelConfig);
```

V tomto okamžiku AI engine ví, *kde* ukládat modely, *jak* logovat a *co* provádět při post‑processingu. Jedná se o čisté oddělení odpovědností, které usnadňuje budoucí změny.

---

## Krok 5: Spusťte post‑processor na vašem OCR výsledku

Předpokládáme, že již máte `ocrResult` z Aspose.OCR, stačí jej předat engine.

```csharp
// Step 6: Run the post‑processor on the OCR result returned by Aspose.OCR
asposeAI.RunPostprocessor(ocrResult);
```

**Upozornění na okrajové případy:**  
Pokud `ocrResult` neobsahuje žádné tabulky, processor korekci tiše přeskočí. Po zpracování můžete ověřit `tableProcessor.GetResult().Count`, abyste zjistili, zda něco bylo skutečně zpracováno.

---

## Krok 6: Získejte a **zobrazte opravený výstup tabulky**

Nakonec si načteme vyčištěný text tabulky a vypíšeme jej do konzole.

```csharp
// Step 7: Retrieve and display the corrected table text
Console.WriteLine("Corrected table output:");
Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
```

Výstup bude vypadat zhruba takto (v závislosti na zdrojovém obrázku):

```
Corrected table output:
| Item   | Quantity | Price |
|--------|----------|-------|
| Apple  | 10       | $1.20 |
| Banana | 5        | $0.80 |
```

Pokud uvidíte prázdný řetězec, zkontrolujte, že OCR skutečně detekovalo tabulku a že `AllowAutoDownload` proběhlo úspěšně.

---

## Krok 7: Uvolněte prostředky

Dobré chování zahrnuje uvolnění těžkých objektů po dokončení práce.

```csharp
// Step 8: Release resources used by the AI engine
asposeAI.Dispose();
```

Vynechání tohoto kroku může nechat otevřené souborové handle, zejména ve Windows, kde jsou modelové soubory uzamčeny.

---

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat do nového konzolového projektu. Nahraďte `"YOUR_DIRECTORY"` skutečnou cestou a ujistěte se, že `ocrResult` je naplněn před voláním `RunPostprocessor`.

```csharp
using System;
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

namespace AsposeAITableCorrection
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a console logger
            ILogger consoleLogger = new ConsoleLogger();

            // 2️⃣ Initialise AsposeAI with the logger
            AsposeAI asposeAI = new AsposeAI(consoleLogger);

            // 3️⃣ Configure auto‑download (optional but recommended)
            AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
            {
                AllowAutoDownload = true,
                DirectoryModelPath = @"C:\AsposeModels" // <-- change this
            };

            // 4️⃣ Create the table processor (auto‑detect mode)
            TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);

            // 5️⃣ Attach processor and config
            asposeAI.SetPostProcessor(tableProcessor, modelConfig);

            // 6️⃣ Obtain OCR result (replace with your own OCR call)
            // Example placeholder – you should have this from Aspose.OCR already
            OcrResult ocrResult = GetOcrResultSomehow();

            // 7️⃣ Run post‑processor on the OCR output
            asposeAI.RunPostprocessor(ocrResult);

            // 8️⃣ Display corrected table
            Console.WriteLine("Corrected table output:");
            if (tableProcessor.GetResult().Count > 0)
            {
                Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
            }
            else
            {
                Console.WriteLine("No tables were detected or corrected.");
            }

            // 9️⃣ Clean up
            asposeAI.Dispose();
        }

        // Dummy method – replace with your actual OCR logic
        static OcrResult GetOcrResultSomehow()
        {
            // For illustration only
            OcrEngine engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample-table.png");
            return engine.Recognize();
        }
    }
}
```

**Očekávaný výstup v konzoli** (při jednoduchém obrázku tabulky):

```
Corrected table output:
| Name   | Age | City      |
|--------|-----|-----------|
| Alice  | 30  | New York  |
| Bob    | 25  | Seattle   |
```

---

## Často kladené otázky

- **Potřebuji internetové připojení pro automatické stažení?**  
  Ano. Při první žádosti o model se AsposeAI připojí k CDN. Po uložení souboru do `DirectoryModelPath` jsou další běhy offline.

- **Co když má moje tabulka sloučené buňky?**  
  AI model se pokusí sloučené buňky rozdělit podle vizuálních vodítek. Pokud výsledek vypadá špatně, zvažte předzpracování obrázku (zvýšení kontrastu, narovnání rotace) před OCR.

- **Mohu zpracovávat více tabulek najednou?**  
  Určitě. `tableProcessor.GetResult()` vrací seznam; můžete jej iterovat a vytisknout každou tabulku.

- **Je `ConsoleLogger` thread‑safe?**  
  Píše přímo do `System.Console`, což je thread‑safe pro jednoduché zápisy. V náročných multithreadových scénářích může být vhodnější vlastní logger se synchronizací.

---

## Další kroky a související témata

Nyní, když víte **jak opravit tabulky**, můžete:

- **Povolit automatické stahování** i pro jiné AsposeAI modely (např. překlad jazyků).
- **Nastavit konzolový logger** s různými úrovněmi logování (Info, Warning, Error) pro jemnější kontrolu.
- Prozkoumat **zobrazení opravených tabulek** v GUI (WinForms nebo WPF) místo konzole.
- Kombinovat opravu tabulek s **extrakcí dat** a přímo je ukládat do databáze.

Každý z těchto kroků staví na základech, které jsme právě položili, takže klidně experimentujte.

---

## Závěr

Prošli jsme celým životním cyklem **vytvoření konzolového loggeru**, povolení automatického stahování a **opravy tabulek** pomocí AsposeAI, a ukázali jsme čistý způsob, jak **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}