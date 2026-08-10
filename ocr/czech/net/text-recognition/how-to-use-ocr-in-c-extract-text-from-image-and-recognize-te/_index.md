---
category: general
date: 2026-02-13
description: Jak použít OCR v C# k extrakci textu z obrázku, rozpoznání textu z fotografie
  nebo JPG a spustit OCR na obrázku bez internetu.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: cs
og_description: Jak použít OCR v C# k extrahování textu z obrázku, rozpoznání textu
  z fotografie a spuštění OCR na obrázku s kompletním, spustitelným příkladem.
og_title: Jak používat OCR v C# – Extrahovat text z obrázku
tags:
- OCR
- C#
- Image Processing
title: Jak použít OCR v C# – Extrahovat text z obrázku a rozpoznat text z fotografie
url: /cs/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

na fotografii". Keep quotes.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR v C# – Extrahovat text z obrázku a rozpoznat text z fotografie

Už jste se někdy zamýšleli **jak použít OCR** k získání slov ze screenshotu, naskenovaného účtenky nebo náhodné fotky, kterou jste pořídili telefonem? Nejste v tom sami. V mnoha reálných aplikacích potřebujeme převést obrázky na prohledávatelný text a dělat to lokálně – bez nespolehlivého internetového připojení – může připomínat hádanku.

Proto tento průvodce ukazuje krok za krokem, jak **extrahovat text z obrázku** pomocí OCR enginu v C#, a také pokrývá, jak **rozpoznat text z fotografie**, **rozpoznat text z JPG** a **spustit OCR na obrázku**, který leží přímo na disku. Na konci budete mít kompletní, připravený program, který funguje hned po stažení.

## Co se naučíte

- Jak nakonfigurovat OCR engine pro zjednodušenou čínštinu (nebo jakýkoli jazyk, který přidáte).  
- Přesný kód potřebný k **načtení zdrojů** z lokální složky – žádné síťové volání.  
- Jak **rozpoznat text z fotografie** souborů jako JPEG, PNG nebo BMP.  
- Tipy pro zvládání běžných okrajových případů, jako chybějící modelové soubory nebo nepodporované formáty obrázků.  
- Kompletní, spustitelný příklad, který můžete vložit do Visual Studia a okamžitě vidět výsledky.

### Předpoklady

- .NET 6.0 nebo novější (API použité zde cílí na .NET Standard 2.0, takže starší verze také fungují).  
- Základní znalost C# a Visual Studia (nebo libovolného IDE, které používáte).  
- OCR knihovna, kterou používáte (ukázka předpokládá fiktivní třídu `OcrEngine`, která je součástí jazykových modelů).  
- Složka obsahující požadované jazykové modelové soubory – považujte ji za „mozek“, který engine používá k čtení čínských znaků.

> **Pro tip:** Pokud ještě nemáte čínské modelové soubory, stáhněte si je jednou z webu dodavatele a umístěte je do složky jako `C:\OcrResources`. Engine už pak nikdy nebude muset jít online.

---

![Diagram ukazující proces OCR na fotografii](path/to/ocr-diagram.png "Diagram ukazující proces OCR na fotografii")

## Jak používat OCR: Nastavení enginu

První věc, kterou potřebujete, je instance OCR enginu nakonfigurovaná pro jazyk, který vás zajímá. V tomto tutoriálu cílíme na **zjednodušenou čínštinu**, ale výměna `OcrLanguage.ChineseSimplified` za `OcrLanguage.English` (nebo jakoukoli jinou hodnotu enumu) je jen jednorázová změna.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**Proč je to důležité:**  
Nastavení vlastnosti `Language` říká engine, jakou znakovou sadu má očekávat. `ResourceFolder` je místo, kde engine hledá váhy neuronových sítí a jazykové slovníky – považujte to za paměťovou banku mozku. Pokud ukážete na špatnou složku, engine vyhodí `FileNotFoundException` a budete uvíznout.

## Extrahovat text z obrázku – Načtení zdrojů

Než engine dokáže něco přečíst, musíte načíst ty modelové soubory do paměti. Tento krok je **kritický**, protože zabraňuje síťovému volání při každém zpracování obrázku.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**Co může jít špatně?**  
Pokud je cesta ke složce špatná nebo jsou soubory poškozené, `LoadResources()` vyvolá výjimku. Blok `try/catch` výše ukazuje, jak elegantně zachytit chybu – něco, co často potřebujete v produkci.

## Rozpoznat text z fotografie – Spuštění OCR

Teď ta zábavná část: předat soubor obrázku engine a získat zpět rozpoznaný text. To je jádro scénářů **spustit OCR na obrázku**, ať už je obrázek JPEG, PNG nebo dokonce BMP.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

Metoda `RecognizeImage` vrací `RecognitionResult` (nebo jakýkoli název, který vaše SDK používá), který typicky obsahuje:

- `Text` – prostý textový přepis.  
- `Confidence` – číselné skóre udávající, jak moc je engine jistý u každého řádku.  
- `BoundingBoxes` – volitelné souřadnice, kde se každé slovo nachází na obrázku.

**Proč by vás mohla zajímat důvěra (confidence):**  
Pokud budujete nástroj pro automatizaci zadávání dat, můžete nastavit práh (např. 0,85) a požádat uživatele o potvrzení řádků s nízkou důvěrou. To dramaticky zvyšuje celkovou přesnost.

## Rozpoznat text z JPG – Práce s různými formáty

Mnoho vývojářů předpokládá, že OCR funguje jen s PNG, ale moderní enginy zvládají **JPG** soubory bez problémů. Jediný háček je, že JPEG komprese může zavést artefakty, které model zmást.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

Pokud nemáte pomocnou funkci `DenoiseAndDeskew`, mnoho knihoven (např. OpenCvSharp) tyto funkce poskytuje. Hlavní myšlenka: **spustit OCR na obrázku** po malém vyčištění, pokud pochází ze skeneru nebo fotoaparátu telefonu.

## Spustit OCR na obrázku – Tipy, okrajové případy a osvědčené postupy

### 1. Správa paměti
Načítání velkých jazykových modelů může spotřebovat stovky megabajtů. Uvolněte engine, až skončíte:

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. Dávkové zpracování
Pokud potřebujete zpracovat desítky fotografií, načtěte zdroje jednou a pak v cyklu:

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. Scénáře s více jazyky
Jazyky můžete měnit za běhu přepsáním `ocrEngine.Language` a znovu zavoláním `LoadResources()`. Jen si dejte pozor na dodatečný čas načítání.

### 4. Zpracování prázdných výsledků
Někdy engine vrátí prázdný řetězec. To obvykle znamená, že obrázek je příliš rozmazaný nebo barva textu splývá s pozadím. Rychlá kontrola:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. Bezpečnostní úvahy
Nikdy nezasílejte soubory nahrané uživatelem přímo do OCR enginu bez validace. Minimálně ověřte příponu souboru a velikost a zvažte skenování na malware.

---

## Kompletní funkční příklad

Níže je samostatný program, který můžete zkopírovat do nového projektu Console App. Ukazuje **jak používat OCR**, **extrahovat text z obrázku**, **rozpoznat text z fotografie**, **rozpoznat text z JPG** a **spustit OCR na obrázku** – vše v jednom.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**Očekávaný výstup (příklad):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

Váš skutečný text se bude lišit podle obsahu obrázku, ale měli byste vidět blok Unicode znaků vytištěný do konzole spolu s procentem důvěry.

---

## Závěr

Prošli jsme **jak používat OCR** v C# od začátku až do konce – konfigurací enginu, načtením jazykových zdrojů a nakonec **rozpoznáním textu z fotografie** nebo **JPG** souborů bez jakéhokoli připojení k internetu. Dodržením výše uvedených kroků můžete **extrahovat text z obrázku**, **spustit OCR na obrázku** a zvládnout nejčastější úskalí, která začátečníky zaskočí.

Jste připraveni na další výzvu? Zkuste předat engine stránku PDF převedenou na obrázek, nebo experimentujte s jiným jazykovým balíčkem a podívejte se, jak se mění skóre důvěry. Můžete

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}