---
category: general
date: 2026-05-25
description: Jak použít OCR v C# k extrakci textu z obrazových souborů. Naučte se
  rozpoznávat čínské znaky z JPG pomocí Aspose.OCR během několika jednoduchých kroků.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from jpg
- recognize chinese characters
- ocr chinese simplified
language: cs
og_description: Jak použít OCR v C# k extrakci textu z obrazových souborů. Tento průvodce
  vám ukáže, jak rozpoznat čínské znaky z JPG pomocí Aspose.OCR.
og_title: Jak použít OCR v C# – Rozpoznat čínský text z JPG
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  headline: How to Use OCR in C# – Recognize Chinese Text from JPG
  type: TechArticle
- description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  name: How to Use OCR in C# – Recognize Chinese Text from JPG
  steps:
  - name: What’s happening under the hood?
    text: '- **`OcrEngine.Language`** tells Aspose which dictionary to use. By picking
      `ChineseSimplified`, we instruct the engine to look for the Simplified Chinese
      language pack. - **First‑time download**: When `Recognize` runs, the SDK reaches
      out to Aspose’s CDN, pulls the ≈6 MB language file, caches it lo'
  - name: 5.1 Dealing with Low‑Quality Images
    text: 'OCR accuracy drops when the source image is blurry, noisy, or has poor
      lighting. A quick fix is to pre‑process the image:'
  - name: 5.2 Running in a Headless Environment
    text: 'If you’re deploying to a Linux container without a GUI, make sure the `libgdiplus`
      library (required for `System.Drawing`) is installed:'
  - name: 5.3 Caching the Language Pack Manually
    text: You can download the language file once and point Aspose to it via the `License`
      API, which eliminates the one‑time network call. This is handy for offline scenarios.
  - name: Expected Output
    text: 'If the JPG contains the phrase “欢迎光临”, the console will print:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Jak použít OCR v C# – Rozpoznat čínský text z JPG
url: /cs/net/text-recognition/how-to-use-ocr-in-c-recognize-chinese-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR v C# – Rozpoznat čínský text z JPG

Už jste se někdy zamysleli **jak používat OCR** k vytažení slov z obrázku, který jste pořízili telefonem? Nejste v tom sami. V mnoha reálných projektech—například skenery účtenek, překladové aplikace nebo automatizovaný vstup dat—budete potřebovat **extrahovat text z obrázku** souborů rychle a spolehlivě.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který **rozpoznává text z JPG** souborů a dokonce řeší obtížný případ **rozpoznání čínských znaků** pomocí jazykového balíčku **OCR Chinese Simplified**. Na konci budete mít samostatnou konzolovou aplikaci, která vypíše detekovaný řetězec do konzole, bez nutnosti dalších ručních stažení.

> **Rychlá poznámka:** Kód funguje s Aspose.OCR ≥ 23.7, který automaticky stáhne jazykové zdroje při prvním použití. Pokud používáte starší verzi, budete muset jazyk přidat ručně.

## Požadavky

- .NET 6.0 SDK nebo novější (příklad cílí na .NET 6, ale .NET 5 také funguje)
- Nedávná verze Visual Studio 2022 nebo VS Code s rozšířením C#
- Připojení k internetu pro první stažení jazyka
- JPG obrázek, který obsahuje zjednodušený čínský text (nazveme jej `chinese_sign.jpg`)

To je vše—žádné těžkopádné OCR enginy, žádné manipulace s nativními DLL. Pouze pár příkazů NuGet a několik řádků kódu.

## Krok 1: Instalace Aspose.OCR přes NuGet

Nejprve potřebujeme OCR knihovnu. Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.OCR
```

Nebo, pokud dáváte přednost UI ve Visual Studiu, klikněte pravým tlačítkem na **Dependencies → Manage NuGet Packages**, vyhledejte “Aspose.OCR” a klikněte na **Install**.

> **Pro tip:** Udržujte své balíčky aktuální. Nové jazykové balíčky a vylepšení výkonu přicházejí v každém minor release.

## Krok 2: Vytvoření nového konzolového projektu (pokud jste tak ještě neučinili)

Pokud začínáte od nuly, vytvořte nový konzolový aplikaci:

```bash
dotnet new console -n OcrChineseDemo
cd OcrChineseDemo
```

Nyní máte soubor `Program.cs` připravený pro OCR kód.

## Krok 3: Napsání OCR kódu – Rozpoznání zjednodušené čínštiny z JPG

Otevřete `Program.cs` a nahraďte jeho obsah následujícím. Každý řádek je anotován, abyste viděli *proč* děláme každý krok, ne jen *co* děláme.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;   // Required for Image.FromFile

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // --------------------------------------------------------------
            // 1️⃣  Initialise the OCR engine and request the Simplified Chinese
            //     language. This language isn’t bundled in the core package,
            //     so Aspose.OCR will download it the first time you call
            //     Recognize().
            // --------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                // The enum value maps to the language pack name.
                Language = OcrLanguage.ChineseSimplified
            };

            // --------------------------------------------------------------
            // 2️⃣  Load the image you want to process. Replace the path with
            //     the actual location of your JPG file.
            // --------------------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";
            using var image = Image.FromFile(imagePath);

            // --------------------------------------------------------------
            // 3️⃣  Perform the recognition. The first call may take a few
            //     seconds because the language resources are being fetched.
            // --------------------------------------------------------------
            string recognizedText = ocrEngine.Recognize(image);

            // --------------------------------------------------------------
            // 4️⃣  Output the result to the console.
            // --------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### Co se děje pod kapotou?

- **`OcrEngine.Language`** říká Aspose, který slovník použít. Výběrem `ChineseSimplified` instruujeme engine, aby hledal jazykový balíček pro zjednodušenou čínštinu.
- **První stažení**: Když se spustí `Recognize`, SDK se obrátí na CDN Aspose, stáhne ≈6 MB jazykový soubor, uloží jej lokálně do cache a poté pokračuje v OCR. Následující volání jsou okamžité.
- **`Image.FromFile`** funguje s libovolným rastrovým formátem, který .NET dokáže dekódovat—JPG, PNG, BMP—takže můžete **extrahovat text z obrázku** souborů mnoha typů, nejen JPG.

## Krok 4: Spuštění aplikace a ověření výstupu

Sestavte a spusťte:

```bash
dotnet run
```

Měli byste vidět něco jako:

```
=== Recognized Text ===
欢迎光临
```

Pokud konzole vypíše nesmysly nebo prázdný řetězec, zkontrolujte:

1. Obrázek skutečně obsahuje jasné, vysokokontrastní čínské znaky.
2. Cesta k souboru je správná (žádné nadbytečné mezery nebo chybějící přípony).
3. Váš počítač může dosáhnout na `https://download.aspose.com` pro jazykový balíček.

## Krok 5: Řešení okrajových případů a běžných úskalí

### 5.1 Práce s nízkokvalitními obrázky

Přesnost OCR klesá, když je zdrojový obrázek rozmazaný, šumivý nebo má špatné osvětlení. Rychlé řešení je předzpracovat obrázek:

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
var gray = new Bitmap(image.Width, image.Height);
using (var g = Graphics.FromImage(gray))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}
        });
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(image, new Rectangle(0,0,image.Width,image.Height),
                0,0,image.Width,image.Height, GraphicsUnit.Pixel, attributes);
}

// Use the processed bitmap for OCR
string recognizedText = ocrEngine.Recognize(gray);
```

### 5.2 Spuštění v headless prostředí

Pokud nasazujete do Linux kontejneru bez GUI, ujistěte se, že je nainstalována knihovna `libgdiplus` (vyžadovaná pro `System.Drawing`):

```bash
apt-get update && apt-get install -y libgdiplus
```

### 5.3 Ruční cachování jazykového balíčku

Můžete stáhnout jazykový soubor jednou a nasměrovat Aspose na něj pomocí API `License`, což eliminuje jednorázové síťové volání. To je užitečné pro offline scénáře.

```csharp
// Assuming you have the .dat file downloaded to /opt/ocr/langs/
ocrEngine.SetLicense("Aspose.OCR.lic"); // optional if you have a paid license
ocrEngine.LoadLanguage(@" /opt/ocr/langs/ChineseSimplified.dat");
```

## Kompletní funkční příklad (vše v jednom)

Níže je *kompletní* program, který můžete zkopírovat a vložit do `Program.cs`. Žádné skryté části, žádné externí skripty.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialise OCR engine with Simplified Chinese language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified
            };

            // Path to the JPG image containing Chinese text
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";

            // Load the image (ensure the file exists)
            using var image = Image.FromFile(imagePath);

            // Recognize text – first call may download the language pack
            string recognizedText = ocrEngine.Recognize(image);

            // Display the result
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### Očekávaný výstup

Pokud JPG obsahuje frázi “欢迎光临”, konzole vypíše:

```
=== Recognized Text ===
欢迎光临
```

Klidně nahraďte obrázek jakýmkoli jiným zjednodušeným čínským znakem, názvem ulice nebo štítkem produktu—engine udělá, co může.

## Závěr

Právě jsme probrali **jak používat OCR** v C# k **extrahování textu z obrázku** souborů, konkrétně řešení výzvy **rozpoznání čínských znaků** v **JPG**. Využitím on‑the‑fly stažení jazyků od Aspose.OCR můžete udržet nasazení lehké a přitom podporovat **OCR Chinese Simplified** přímo z krabice.

Co dál? Vyzkoušejte tyto nápady:

- **Dávkové zpracování**: Procházet složku s obrázky a zapisovat každý výsledek do CSV.
- **Kombinace s překladovými API**: Poslat rozpoznaný řetězec do Azure Translator pro aplikace v reálném čase s více jazyky.
- **Prozkoumat další jazyky**: Vyměnit `OcrLanguage.ChineseSimplified` za `Japanese` nebo `Arabic` a sledovat, jak se stejný kód přizpůsobí.

Máte otázky ohledně ladění výkonu, licencování nebo integrace OCR do webové služby? Zanechte komentář níže—šťastné kódování!

---

![Snímek obrazovky výstupu konzole ukazující, jak použít OCR v C# k rozpoznání čínského textu z JPG obrázku](ocr-chinese-demo.png "jak použít výstup OCR v konzoli")

## Související tutoriály

- [Extrahovat text z obrázku v C# s výběrem jazyka pomocí Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [rozpoznat text z obrázku s Aspose OCR pro více jazyků](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Jak extrahovat text z obrázku přípravou obdélníků v OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}