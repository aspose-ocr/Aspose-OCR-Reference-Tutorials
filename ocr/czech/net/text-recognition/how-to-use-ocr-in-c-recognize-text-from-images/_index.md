---
category: general
date: 2026-02-09
description: Jak použít OCR v C# k rozpoznání textu z obrázku, extrahování textu a
  převodu obrázku na text pomocí Aspose OCR. Kompletní krok‑za‑krokem návod.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- load image stream
language: cs
og_description: Jak použít OCR v C# k rozpoznání textu z obrázku, extrahování textu
  a převodu obrázku na text pomocí Aspose OCR. Kompletní průvodce s kódem.
og_title: Jak použít OCR v C# – Rozpoznávejte text z obrázků
tags:
- C#
- Aspose OCR
- Image Processing
title: Jak použít OCR v C# – Rozpoznat text z obrázků
url: /cs/net/text-recognition/how-to-use-ocr-in-c-recognize-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR v C# – Rozpoznávat text z obrázků

Už jste se někdy zamysleli **jak používat OCR** k převodu snímku obrazovky na editovatelný text? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují *rozpoznat text z obrázku* souborů, ale postrádají jasný, připravený k běhu příklad.  

V tomto tutoriálu projdeme celý proces – načtení licence, vytvoření enginu, předání proudu obrázku a nakonec získání čistého textu. Na konci budete schopni **extrahovat text z obrázku**, **převést obrázek na text** a dokonce pochopit nuance manipulace s **load image stream**.

> **Co získáte:** kompletní, spustitelný C# program používající Aspose.OCR, vysvětlení každého kroku a tipy, jak se vyhnout běžným úskalím.

---

## Požadavky

- .NET 6.0 nebo novější (API funguje také s .NET Framework 4.6+)  
- NuGet balíček Aspose.OCR pro .NET (`Aspose.OCR`) nainstalován  
- Platný licenční soubor Aspose OCR (`Aspose.OCR.lic`) – zkušební verze funguje, ale přidává vodoznak.  
- Obrázek (`sample.jpg`) obsahující jasný, strojově čitelný text.

> **Tip:** Pokud používáte Visual Studio, příkaz v NuGet konzoli je  
> `Install-Package Aspose.OCR -Version 23.10` (nahraďte nejnovější verzí).

## Jak používat OCR: Načtení licence a inicializace enginu

První věc, kterou musíte udělat, je informovat Aspose, že vlastníte licenci. Přeskočení tohoto kroku stále umožní spuštění, ale ve výstupu se objeví vodoznak a zbytečně ztratíte čas kontrolou zkušebního režimu.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // Step 1 – Load the Aspose OCR license (replace with your .lic file path)
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Step 2 – Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the steps follow...
    }
}
```

**Proč je to důležité:** Objekt `License` vypíná zkušební vodoznak a odemyká plnou sadu funkcí, která zahrnuje modely s vyšší přesností a podporu více jazyků.  

> **Pro tip:** Uchovávejte licenční soubor mimo repozitář se zdrojovým kódem. Použijte proměnné prostředí nebo bezpečný trezor k vložení cesty za běhu.

## Krok 2 – Načtení proudu obrázku (a proč je lepší než cesta k souboru)

Když *načtete image stream* místo předání surové cesty k souboru, získáte flexibilitu: obrázek může pocházet z databáze, webového požadavku nebo z paměťového pole bajtů.  

```csharp
// Step 3 – Load the image you want to recognize
// Using ImageStream.FromFile is the simplest way for local files.
ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

// Alternative: load from a byte array (e.g., when the image is uploaded via HTTP)
// byte[] imageBytes = ... // get from request
// ImageStream imageStream = ImageStream.FromBytes(imageBytes);
```

**Vysvětlení:** `ImageStream` abstrahuje podkladový zdroj, což umožňuje OCR enginu zacházet se vším jednotně. Pokud později přejdete na úložiště v cloudu, stačí změnit způsob vytvoření `ImageStream`; zbytek kódu zůstane nedotčen.

## Krok 3 – Rozpoznat text z obrázku

Nyní přichází jádro věci: **rozpoznat text z obrázku**. Metoda `OcrEngine.Recognize` spouští neuronové modely dodávané s Aspose a vrací objekt `OcrResult` obsahující několik užitečných vlastností.

```csharp
// Step 4 – Run the OCR process on the image
OcrResult ocrResult = ocrEngine.Recognize(imageStream);
```

**Co je uvnitř `OcrResult`?**  
- `PlainText` – jediný řetězec se všemi detekovanými znaky.  
- `Words` – kolekce objektů slov s ohraničujícími rámečky (užitečné pro zvýraznění).  
- `Lines` – seskupení na úrovni řádků, praktické pro zachování odstavcových zalomení.

Pokud potřebujete jen surový text, `PlainText` je nejrychlejší cesta. Pro pokročilejší scénáře (např. překrytí výsledků na původní obrázek) prozkoumejte `Words` a `Lines`.

## Krok 4 – Zobrazit nebo uložit extrahovaný text

Nakonec vypíšeme rozpoznaný text do konzole. Ve skutečné aplikaci můžete zapisovat do databáze, souboru nebo jej posílat přes API.

```csharp
// Step 5 – Display the recognized plain text (watermark omitted with a full license)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.PlainText);
Console.WriteLine("==================");

// Optional: Save to a .txt file
System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
```

**Očekávaný výstup:**  
Pokud `sample.jpg` obsahuje větu *„Hello World!“*, uvidíte:

```
=== OCR Output ===
Hello World!
==================
```

Při použití zkušební licence bude výstup obsahovat malý vodoznak „Aspose OCR Demo“ na konci textu. S plnou licencí zmizí úplně.

## Kompletní funkční příklad (připravený ke kopírování a vložení)

Níže je celý program, připravený ke kompilaci. Nahraďte cesty vlastními umístěními a můžete spustit.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // 1️⃣ Load license – required for production use
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // 2️⃣ Create OCR engine – the core processing object
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Load image – you can also use ImageStream.FromBytes for in‑memory data
        ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

        // 4️⃣ Recognize text – this is where the magic happens
        OcrResult ocrResult = ocrEngine.Recognize(imageStream);

        // 5️⃣ Output the plain text – perfect for further processing
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.PlainText);
        Console.WriteLine("==================");

        // Optional: persist the result
        System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
    }
}
```

> **Pamatujte:** Výše uvedený kód **extrahuje text z obrázku** a **převádí obrázek na text** jedním voláním. Žádné další smyčky, žádná ruční manipulace s pixely – Aspose dělá těžkou práci.

## Časté otázky a okrajové případy

### Co když je můj obrázek rozmazaný nebo má nízký kontrast?

Aspose OCR obsahuje možnosti předzpracování (např. `ocrEngine.ImagePreprocessor`). Můžete povolit binarizaci nebo korekci sklonu před rozpoznáním:

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Binarization = true,
    Deskew = true
};
```

### Jak zvládnout více jazyků?

Nastavte vlastnost `Language` na engine:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Engine se pak pokusí automaticky detekovat oba jazyky.

### Mohu zpracovávat PDF místo JPEG?

Ano – Aspose OCR může číst PDF přímo, ale budete potřebovat knihovnu Aspose.PDF k extrakci každé stránky jako obrázku a poté předat proud obrázku OCR enginu.

### Co s velkými dávkami?

Zabalte logiku rozpoznání do smyčky a znovu použijte stejnou instanci `OcrEngine`. Vytváření nového enginu pro každý obrázek přidává zbytečnou zátěž.

## Pro tipy pro produkčně připravené OCR

- **Uložte objekt licence do cache**: Načtěte jej jednou při startu aplikace, ne při každém požadavku.  
- **Znovu použijte `OcrEngine`**: Engine drží interní buffery; opakované použití snižuje zatížení GC.  
- **Omezte velikost obrázku**: Velmi velké obrázky (>5 MP) dramaticky zvyšují dobu zpracování. Zmenšete na 150‑300 DPI, pokud není vyžadována vysoká rozlišení.  
- **Ověřte výstup**: OCR není dokonalé; implementujte jednoduchou kontrolu důvěry (`ocrResult.Words.Average(w => w.Confidence)`) a označte výsledky s nízkou důvěrou k ručnímu přezkoumání.  
- **Bezpečnost vláken**: `OcrEngine` není thread‑safe. Vytvořte samostatné instance pro každé vlákno nebo použijte vzor poolu.

## Závěr

Probrali jsme **jak používat OCR** v C# od načtení licence po extrahování čistého, prohledávatelného textu. Dodržením výše uvedených kroků můžete **rozpoznat text z obrázku**, **extrahovat text z obrázku** a snadno **převést obrázek na text**, přičemž ovládáte vzor **load image stream**, který činí váš kód flexibilním pro budoucí zdroje dat.

Jste připraveni na další výzvu? Zkuste přidat ořezání oblasti zájmu, integraci s Azure Blob storage, nebo předat výstup OCR do pipeline pro zpracování přirozeného jazyka. Obloha je limit a nyní máte pevný základ, na kterém můžete stavět.

![Diagram ukazující tok OCR: load license → create engine → load image stream → recognize → output text](image-placeholder.png "jak používat OCR k rozpoznání textu z obrázku")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}