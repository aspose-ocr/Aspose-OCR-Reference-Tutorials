---
category: general
date: 2026-01-10
description: Jak rychle spustit OCR a extrahovat arabský text z obrázku. Naučte se
  převést obrázek na text, číst text z PNG a zjistit, jak extrahovat text pomocí Aspose
  OCR.
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: cs
og_description: Jak spustit OCR v C# a extrahovat arabský text z PNG obrázku. Tento
  průvodce vám ukáže, jak převést obrázek na text a číst text z PNG krok za krokem.
og_title: Jak spustit OCR v C# – Extrahovat arabský text z PNG
tags:
- OCR
- C#
- Aspose
title: Jak spustit OCR v C# – Extrahovat arabský text z PNG
url: /cs/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak spustit OCR v C# – Extrahovat arabský text z PNG

Už jste se někdy zamýšleli **jak spustit OCR** na obrázku, který obsahuje arabské znaky? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují **extrahovat arabský text** z PNG a neví, která knihovna zvládne skripty psané zprava doleva bez zbytečných komplikací.  

V tomto tutoriálu projdeme vše, co potřebujete vědět k **převodu obrázku na text**, **čtení textu z PNG** a nakonec **jak extrahovat text** pomocí Aspose.OCR v čisté C# konzolové aplikaci. Na konci budete mít připravený program, který vypíše arabský řetězec přímo do terminálu.

## Co se naučíte

- Instalovat a odkazovat na NuGet balíček Aspose.OCR.  
- Nakonfigurovat OCR engine pro podporu arabského jazyka.  
- Načíst PNG obrázek a spustit proces rozpoznávání.  
- Získat a zobrazit extrahovaný text.  
- Doladit nastavení pro vyšší přesnost a vyřešit běžné úskalí.

Žádná předchozí zkušenost s OCR není vyžadována, stačí základní znalost C# a .NET vývojového prostředí (Visual Studio, Rider nebo `dotnet` CLI).

---

## Jak spustit OCR – Nastavení Aspose OCR

### Krok 1: Přidat NuGet balíček Aspose.OCR

První věc, kterou potřebujeme, je samotná OCR knihovna. Aspose.OCR je komerční produkt, ale nabízí bezplatnou zkušební verzi, která pro výukové účely funguje perfektně.

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

Alternativně otevřete **NuGet Package Manager** ve Visual Studio, vyhledejte **Aspose.OCR** a klikněte na **Install**.

> **Tip:** Pokud plánujete knihovnu používat v CI pipeline, přidejte přepínač `-v` pro uzamčení verze, např. `dotnet add package Aspose.OCR -v 23.10`.

### Krok 2: Vytvořit nový konzolový projekt (pokud ještě žádný nemáte)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

Nyní máte čerstvý soubor `Program.cs` připravený pro náš kód.

---

## Extrahovat arabský text – Psání OCR kódu

Níže je kompletní, připravený program. Uložte jej jako `Program.cs` (nebo přepište automaticky vygenerovaný soubor).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### Proč je každý řádek důležitý

- **`OcrEngine`**: Hlavní třída, která koordinuje načítání obrázku, výběr jazyka a rozpoznávání.  
- **`Language = OcrLanguage.Arabic`**: Arabština používá skript zprava doleva a unikátní glyfy; nastavení jazyka říká enginu, aby použil správné modely znaků.  
- **`ImageStream.FromFile`**: Podporuje PNG, JPEG, BMP a mnoho dalších formátů. Pokud budete potřebovat číst z `MemoryStream` (např. nahraný soubor), nahraďte toto volání odpovídajícím způsobem.  
- **`Recognize()`**: Provádí těžkou práci – analýzu pixelů, segmentaci a klasifikaci znaků.  
- **`ocrEngine.Text`**: Výsledný Unicode řetězec, připravený k dalšímu zpracování, uložení nebo zobrazení.

### Očekávaný výstup

Pokud `arabic_sample.png` obsahuje frázi “مرحبا بالعالم” (Hello World), konzole vypíše:

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

Pokud výstup vypadá poškozeně, zkontrolujte, že je obrázek čistý, jazyk je nastaven na arabštinu a verze OCR enginu odpovídá dokumentaci.

---

## Převod obrázku na text – Ladění přesnosti

Zatímco výchozí nastavení funguje pro většinu čistých skenů, reálné obrázky často vyžadují trochu více péče.

| Nastavení | Co dělá | Kdy použít |
|-----------|---------|------------|
| `ocrEngine.Config.Preprocess = true` | Aktivuje automatickou binarizaci a odstraňování šumu. | Skenované dokumenty se stíny. |
| `ocrEngine.Config.Deskew = true` | Otočí obrázek pro opravu mírného naklonění. | Fotografie pořízené pod úhlem. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | Považuje celý obrázek za jeden blok textu. | Jednoduché popisky nebo jednorázové řádky. |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | Omezuje rozpoznávání pouze na arabské znaky. | Snižuje falešně pozitivní výsledky na stránkách s více jazyky. |

Tyto řádky můžete přidat hned po vytvoření enginu:

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## Číst text z PNG – Práce s různými zdroji obrázků

Někdy PNG žije v databázi nebo přichází z webového požadavku. Zde je rychlá varianta, která čte z `byte[]`:

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

Zbytek toku zůstává stejný, což znamená, že **jak extrahovat text** zůstává konzistentní bez ohledu na zdroj.

---

## Jak extrahovat text – Pokročilé možnosti a okrajové případy

### 1. Vícestránkové PDF nebo TIFF

Pokud potřebujete OCR pro vícestránkový dokument, projděte každou stránku ve smyčce:

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **Poznámka:** Pro tento úryvek budete potřebovat balíček `Aspose.PDF`.

### 2. Automatické rozpoznání jazyka

Aspose.OCR také nabízí automatické rozpoznání, ale je pomalejší. Pokud si nejste jisti, zda obrázek obsahuje arabštinu nebo jiný skript, povolte jej:

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

Engine vyzkouší každý jazykový model a vybere nejlepší shodu.

### 3. Tipy pro výkon

- **Znovu použijte objekt `OcrEngine`** pro více obrázků; vytváření nové instance pokaždé přidává režii.  
- **Spouštějte paralelně** pouze pokud máte samostatné instance enginu pro každý vlákno – sdílení jedné instance způsobuje závodní podmínky.

---

## Závěr

Probrali jsme **jak spustit OCR** v C# od začátku až do konce, ukázali vám, jak **extrahovat arabský text**, **převést obrázek na text**, **číst text z PNG** a odpověděli na **jak extrahovat text** v různých scénářích. Ukázkový kód je kompletní, samostatný a připravený k vložení do libovolného .NET konzolového projektu.

Další kroky? Vyzkoušejte zaměnit `OcrLanguage.Arabic` za korejštinu nebo srbskou cyrilici a uvidíte vícejazyčnou sílu knihovny. Experimentujte s předzpracovatelskými příznaky pro zvýšení přesnosti u špinavých skenů, nebo integrujte OCR rutinu do webového API, aby uživatelé mohli nahrávat obrázky a okamžitě získávat textové výsledky.

Šťastné kódování a ať jsou vaše OCR výsledky vždy krystalicky čisté!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}