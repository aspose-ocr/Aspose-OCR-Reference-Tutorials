---
category: general
date: 2026-03-13
description: Jak provést OCR v C# a extrahovat text z obrázku pomocí OcrEngine. Naučte
  se rychle převádět obrázek na text s kompletním krok‑za‑krokem průvodcem.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- read text from picture
- how to extract text
language: cs
og_description: Jak provést OCR v C#? Tento průvodce vám ukáže, jak extrahovat text
  z obrázku, převést obrázek na text a číst text z obrázku pomocí OcrEngine.
og_title: Jak provést OCR v C# – extrahovat text z obrázku
tags:
- OCR
- C#
- Image Processing
title: Jak provést OCR v C# – Extrahovat text z obrázku
url: /cs/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR v C# – Extrahovat text z obrázku

Jak provést OCR v C# je častá otázka pro vývojáře, kteří potřebují **číst text z obrázku** souborů. V tomto průvodci vás provedeme extrahováním textu z obrázku pomocí knihovny `OcrEngine`, která převádí obrázky na prohledávatelné řetězce pomocí několika řádků kódu.  

Pokud jste někdy zírali na naskenovanou fakturu, ručně psanou poznámku nebo snímek obrazovky a přemýšleli *„jak extrahovat text?“*, jste na správném místě. Také se dotkneme převodu obrázku na text pro dávkové zpracování, abyste mohli automatizovat celý pracovní postup.

---

## Co budete potřebovat

- **.NET 6.0 nebo novější** (API, které používáme, funguje s .NET Standard 2.0+)
- **OcrEngine** NuGet balíček (nebo jakákoli kompatibilní OCR knihovna, která poskytuje vlastnosti `Language`, `Image`, `Recognize` a `Text`)
- Vzorek souboru obrázku, např. `hindi_page.jpg`, umístěný ve složce, na kterou můžete odkazovat z kódu
- Základní znalost syntaxe C# – žádné pokročilé triky nejsou potřeba

To je vše. Žádné externí služby, žádné API klíče, jen místní knihovna, která provádí těžkou práci.

---

## Implementace krok za krokem

Níže rozdělíme proces do logických částí. Každá sekce má jasný nadpis, krátký úryvek kódu a vysvětlení **proč** je krok důležitý – ne jen **co** dělá.

### Jak provést OCR – Základní kroky

Celkový tok lze shrnout do pěti akcí:

1. **Vytvořit** instanci OCR enginu
2. **Vybrat** jazyk, který chcete rozpoznat
3. **Načíst** obrázek obsahující text
4. **Spustit** algoritmus rozpoznávání
5. **Přečíst** extrahovaný text

To je kostra; následující sekce ji doplní.

---

### Extrahovat text z obrázku – Vytvořit engine

Nejprve potřebujeme objekt, který umí komunikovat s OCR enginem.

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

*Proč je to důležité:* Instanciace `OcrEngine` alokuje všechny vnitřní buffery a načte potřebné nativní DLL knihovny pro analýzu obrazu. Přeskočení tohoto kroku by vás nechalo bez rozpoznávače, který byste mohli později volat.

> **Tip:** Pokud plánujete zpracovávat mnoho obrázků po sobě, udržujte stejnou instanci `ocrEngine` aktivní. Znovu používá jazykové modely a urychluje následné volání.

---

### Převést obrázek na text – Vybrat jazyk

OCR přesnost silně závisí na jazykovém modelu, který mu poskytnete. Pro hindštinu, tamilštinu nebo jakýkoli jiný skript nastavte vlastnost `Language` odpovídajícím způsobem.

```csharp
// Step 2: Select the language of the text to recognize (e.g., Hindi)
ocrEngine.Language = Language.Hindi;   // You can also use Language.Tamil, Language.English, etc.
```

*Proč je to důležité:* Engine používá jazykově specifické znakové sady a statistické modely. Poskytnutí špatného jazyka často vede k nečitelnému výstupu, zejména u ne‑latinských skriptů.

> **Hraniční případ:** Pokud potřebujete podporu více jazyků, některé knihovny vám umožní nastavit seznam náhrad, např. `ocrEngine.Language = Language.Multilingual;`.

---

### Číst text z obrázku – Načíst zdrojový obrázek

Nyní nasměrujeme engine na soubor, který obsahuje vizuální text.

```csharp
// Step 3: Load the image that contains the text
ocrEngine.Image = ImageStream.FromFile(@"C:\OCR\Samples\hindi_page.jpg");
```

*Proč je to důležité:* `ImageStream.FromFile` převádí surový soubor do bitmapového formátu, který OCR jádro dokáže pochopit. Poskytnutí poškozeného nebo nepodporovaného formátu (např. SVG) způsobí výjimku.

> **Pozor:** Velké obrázky mohou spotřebovat hodně paměti. Pokud zpracováváte skeny s vysokým rozlišením, zvažte zmenšení pomocí `Image.Resize` před předáním engine.

---

### Převést obrázek na text – Spustit rozpoznávání

S připraveným enginem a načteným obrázkem nakonec spustíme proces OCR.

```csharp
// Step 4: Perform the OCR operation
ocrEngine.Recognize();
```

*Proč je to důležité:* `Recognize` spouští sérii vnitřních kroků – předzpracování, segmentaci, klasifikaci znaků a následné zpracování. Volání je blokující, což znamená, že vlákno čeká, dokud není text připraven.

> **Poznámka o výkonu:** Na typickém desktopu rozpoznání stránky s 300 dpi trvá < 1 sekundu. Na serveru můžete chtít spustit toto v úkolu na pozadí, aby nedocházelo k zamrznutí UI.

---

### Jak extrahovat text – Získat výsledek

Jakmile rozpoznání skončí, engine ukládá výstup prostého textu do vlastnosti `Text`.

```csharp
// Step 5: Output the recognized text
Console.WriteLine(ocrEngine.Text);
```

*Proč je to důležité:* Vlastnost `Text` vám poskytuje čistý řetězec UTF‑8, který můžete zapsat do souboru, vložit do databáze nebo předat do následných NLP pipeline.

> **Očekávaný výstup:** Pro ukázkovou hindskou stránku můžete vidět něco jako  
> `यह एक उदाहरण पाठ है जो OCR द्वारा पहचाना गया है।`  
> (Přesný výstup závisí na kvalitě obrázku a jazykovém modelu.)

---

## Další úvahy pro reálné projekty

Níže jsou některé scénáře „co‑když“, se kterými se pravděpodobně setkáte, když v produkci **extrahujete text z obrázku**.

### Zpracování více obrázků ve smyčce

Pokud potřebujete **převést obrázek na text** pro desítky souborů, zabalte kroky do smyčky `foreach` a znovu použijte stejný `ocrEngine`:

```csharp
string[] files = Directory.GetFiles(@"C:\OCR\Batch\", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), ocrEngine.Text);
}
```

### Práce s nízkokvalitními skeny

- **Předzpracovat** binarizací (`Image.Binarize()`), odstraněním šumu nebo korekcí sklonu.
- **Zvýšit DPI** při skenování (300 dpi je bezpečný výchozí bod).
- **Vybrat jazykový model**, který podporuje ligatury skriptu (např. Devanagari pro hindštinu).

### Čtení textu z obrázku na webu

Když obrázek pochází z URL, nejprve jej stáhněte do paměťového proudu:

```csharp
using (HttpClient client = new())
{
    byte[] data = await client.GetByteArrayAsync(imageUrl);
    using var ms = new MemoryStream(data);
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
    Console.WriteLine(ocrEngine.Text);
}
```

### Bezpečnost vláken a paralelismus

Většina OCR knihoven **není** zcela bezpečná pro více vláken. Pokud plánujete **číst text z obrázku** souběžně, vytvořte samostatné instance `OcrEngine` pro každé vlákno, nebo použijte frontu producent‑spotřebitel k serializaci přístupu.

---

## Kompletní funkční příklad

Spojením všeho dohromady zde máte připravenou konzolovou aplikaci, která demonstruje **jak provést OCR**, **extrahovat text z obrázku** a **číst text z obrázku** v jednom koherentním programu.

```csharp
using System;
using OcrLibrary;               // Adjust to your OCR library's namespace
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Choose the language (Hindi in this case)
        ocrEngine.Language = Language.Hindi;

        // Load the image file
        string imagePath = @"C:\OCR\Samples\hindi_page.jpg";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // Run the recognition process
        ocrEngine.Recognize();

        // Output the extracted text
        string result = ocrEngine.Text;
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(result);

        // Optional: Save to a .txt file
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, result);
        Console.WriteLine($"Text saved to {txtPath}");
    }
}
```

**Co byste měli vidět:** Konzole vypíše hindskou větu extrahovanou z `hindi_page.jpg`, následovanou potvrzením, že textový soubor byl vytvořen. Pokud je obrázek čistý, výstup bude prakticky identický s originálním tištěným textem.

---

## Závěr

Nyní víte **jak provést OCR** v C# od začátku až do konce, jak **extrahovat text z obrázku**, **převést obrázek na text** a **číst text z obrázku** pomocí jednoduchého pracovního postupu `OcrEngine`. Pětikrokový vzor – vytvořit, nastavit jazyk, načíst, rozpoznat, přečíst – pokrývá většinu případů použití a další tipy vám pomohou zvládnout dávkové úlohy, nízkokvalitní skeny a zdroje z webu.

Jste připraveni na další výzvu? Zkuste změnit jazyk na angličtinu, předat stránku PDF převedenou na obrázek, nebo propojit výstup OCR do pipeline pro vyhledávací index. Možnosti jsou neomezené, jakmile ovládnete základy OCR v C#.

Máte otázky nebo obtížný obrázek, který nespolupracuje? Zanechte komentář níže a pojďme to společně vyřešit. Šťastné kódování!  

![jak provést OCR příklad](images/ocr-example.png "jak provést OCR příklad")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}