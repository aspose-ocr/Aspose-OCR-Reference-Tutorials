---
category: general
date: 2026-03-29
description: Extrahujte text z obrázku pomocí Aspose OCR v C#. Naučte se automatické
  otáčení OCR a jak odstranit zkosení skenovaného obrázku pro dokonalé výsledky.
draft: false
keywords:
- extract text from image
- auto rotate ocr
- how to deskew scanned image
- Aspose OCR C#
- image preprocessing OCR
language: cs
og_description: Extrahujte text z obrázku pomocí Aspose OCR. Tento průvodce ukazuje
  automatické otáčení OCR a jak vyrovnat skenovaný obrázek v C#.
og_title: Extrahovat text z obrázku v C# – automatické otočení OCR a vyrovnání
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Extrahovat text z obrázku v C# – Průvodce automatickým otáčením OCR a vyrovnáním
url: /cs/net/ocr-optimization/extract-text-from-image-in-c-auto-rotate-ocr-deskew-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázku v C# – Automatické otáčení OCR a vyrovnání

Už jste někdy potřebovali **extrahovat text z obrázku**, ale soubor přišel v podivném úhlu? Je to častý problém – zejména když pracujete s naskenovanými fakturami, vyfocenými účtenkami nebo šikmými PDF. Dobrou zprávou je, že nemusíte psát vlastní algoritmus pro otáčení. Pomocí vestavěné funkce *auto rotate OCR* v Aspose OCR můžete nechat motor narovnat obrázek a poté **extrahovat text z obrázku** v jednom plynulém kroku.  

V tomto tutoriálu projdeme kompletní, připravený k spuštění C# program, který:

* Inicializuje OCR engine s automatickou orientací a vyrovnáním (deskew).
* Rozpozná otočený nebo zkosený obrázek.
* Vrátí jak detekovaný úhel otočení, tak extrahovaný text.

Žádné externí služby, žádné složité výpočty – jen pár řádků kódu a jasné vysvětlení *jak vyrovnat naskenovaný obrázek* podle potřeby.

## Co budete potřebovat

| Požadavek | Proč je to důležité |
|--------------|----------------|
| .NET 6.0 or later (or .NET Framework 4.6+) | Aspose OCR je distribuován jako NuGet balíček, který cílí na tyto runtime. |
| Visual Studio 2022 (or any C# editor) | Umožňuje snadno přidat NuGet balíčky a spustit konzolovou aplikaci. |
| A sample image (`rotated_document.jpg`) | Soubor by měl být JPEG, PNG, BMP nebo TIFF, který není dokonale svislý. |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | Poskytuje třídy `OcrEngine`, `PreprocessingFilters` a související typy. |

Pokud máte všechny položky zaškrtnuté, můžete začít. V opačném případě si stáhněte nejnovější Aspose OCR z NuGet – instalace jedním kliknutím.

---

## Krok 1 – Inicializace OCR Engine (Primární klíčové slovo v akci)

První, co uděláme, je vytvořit instanci `OcrEngine` a nastavit jí **auto rotate OCR** a **deskew** pro jakýkoli vstupní obrázek. Tyto dva příznaky jsou kombinovány pomocí bitového OR (`|`), protože `PreprocessingFilters` je výčtový typ s atributem `[Flags]`.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine with English language and preprocessing options
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Enable both auto‑rotate and auto‑deskew
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };
```

> **Proč je to důležité:**  
> *Auto‑rotate OCR* prozkoumá základní linii textu na obrázku, odhadne správnou orientaci a interně jej před rozpoznáním otočí. *Auto‑deskew* dělá totéž pro mírné sklonění, které se často objevuje u skenovaných dokumentů. Povolením obou zajistíte nejlepší možné výsledky **extrahování textu z obrázku** bez ruční úpravy obrázku.

---

## Krok 2 – Rozpoznání obrázku a získání výsledku

Nyní předáme motoru cestu k souboru. Metoda `RecognizeImage` vrací objekt `OcrResult`, který obsahuje detekovaný úhel otočení, skóre spolehlivosti a výstup v prostém textu.

```csharp
        // Recognise the image file and obtain the OCR result
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/rotated_document.jpg");
```

> **Tip:** Pokud pracujete se streamem (např. nahraným souborem), použijte místo toho `ocrEngine.RecognizeImage(Stream)`. Stejné příznaky předzpracování se použijí, takže stále získáte výhody **auto rotate OCR**.

---

## Krok 3 – Zobrazení úhlu otočení a extrahovaného textu

Nakonec vytiskneme dvě informace do konzole: úhel, o který podle motoru obrázek potřebuje být otočen, a skutečný text, který byl získán.

```csharp
        // Show the detected rotation and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Očekávaný výstup** (vaše čísla se budou lišit podle vstupního obrázku):

```
Detected rotation: 12.3°
----- Extracted Text -----
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Pokud byl obrázek již svislý, úhel otočení bude `0°` a stále získáte čistý text díky algoritmu *auto‑deskew*.

---

## Krok 4 – Porozumění tomu, jak vyrovnat naskenovaný obrázek (Hlubší ponor do sekundárního klíčového slova)

Možná se ptáte *jak vyrovnat naskenovaný obrázek*, když OCR engine hlásí nenulový úhel. Pod kapotou Aspose OCR používá **Houghovu transformaci** k detekci dominantní orientace řádku textu. Poté otočí bitmapu o inverzní úhel, čímž efektivně narovná text.

**Kdy je to důležité?**  
* Skenery, které podávají papír pod mírným úhlem (běžné v kancelářích).  
* Fotografie pořízené chytnutím smartphonem – horizont zřídka bývá dokonalý.  

**Řešení okrajových případů:**  
Pokud je `RotationAngle` výsledku neobvykle velký (např. > 45°), motor mohl obrázek špatně interpretovat (možná je to logo nebo ne‑textová grafika). V takovém případě můžete:

1. Obrázek ručně otočit pomocí `System.Drawing` před předáním motoru, nebo  
2. Zakázat `AutoRotate` a ponechat jen `AutoDeskew`, pokud víte, že dokument je již svislý.

```csharp
// Example: manually rotate 90° clockwise before OCR
using (var img = Aspose.OCR.Image.Load("rotated_document.jpg"))
{
    img.Rotate(90);
    OcrResult result = ocrEngine.RecognizeImage(img);
    Console.WriteLine(result.Text);
}
```

---

## Krok 5 – Časté úskalí a profesionální tipy (E‑E‑A‑T v akci)

| Úskalí | Proč se to děje | Řešení |
|---------|----------------|-----|
| **Blurry or low‑resolution images** | Přesnost OCR dramaticky klesá; detekce otočení může selhat. | Použijte skeny alespoň 300 dpi; před OCR aplikujte filtr pro zvýšení ostrosti. |
| **Mixed languages** | Engine výchozí jazyk je angličtina; cizí znaky se zkomolí. | Nastavte `Language = Language.English | Language.Spanish` (nebo vhodnou kombinaci). |
| **Large files (> 10 MB)** | Tlak na paměť může způsobit `OutOfMemoryException`. | Nejprve zmenšete obrázek, nebo zpracovávejte po částech pomocí `OcrEngine.RecognizeRegion`. |
| **Incorrect file path** | `FileNotFoundException` zastaví program. | Použijte `Path.Combine(Environment.CurrentDirectory, "rotated_document.jpg")` pro větší robustnost. |

> **Pro tip:** Vždy zaznamenávejte `ocrResult.RotationAngle` a `ocrResult.Confidence` (pokud jsou k dispozici). Tyto metriky vám pomohou rozhodnout, zda stojí za to opakovat s jiným nastavením předzpracování.

---

## Krok 6 – Rozšíření příkladu (Co dál?)

Nyní, když můžete **extrahovat text z obrázku** s automatickým otáčením a vyrovnáním, zvažte následující kroky:

* **Dávkové zpracování** – Procházet složku s obrázky, ukládat každý výsledek do databáze a označit ty s `RotationAngle > 5°` pro ruční kontrolu.  
* **Konverze do PDF** – Kombinovat extrahovaný text s původním obrázkem do prohledávatelného PDF pomocí Aspose.PDF.  
* **Detekce jazyka** – Použít flag `AutoDetectLanguage` z Aspose.OCR, aby motor automaticky vybral nejlepší jazyk.

Každý z nich staví na stejném základním principu: nechte knihovnu řešit orientaci a vy se soustřeďte na obchodní logiku.

---

## Kompletní funkční příklad (připravený ke kopírování a vložení)

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine with auto‑rotate and auto‑deskew
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };

        // 2️⃣ Recognise the image – replace the path with your own file
        string imagePath = "YOUR_DIRECTORY/rotated_document.jpg";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 3️⃣ Output the rotation angle and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Uložte soubor jako `Program.cs`, spusťte `dotnet add package Aspose.OCR` a poté `dotnet run`. Měli byste vidět úhel a čistý text vytištěný do konzole.

---

## Závěr

Právě jsme ukázali, jak **extrahovat text z obrázku** v C# a nechat Aspose OCR postarat se o *auto rotate OCR* a složitý problém *jak vyrovnat naskenovaný obrázek*. Povolením obou příznaků předzpracování motor automaticky narovná šikmé obrázky, detekuje správnou orientaci a poskytne přesný text – bez nutnosti ruční úpravy obrázku.

Neváhejte experimentovat s většími dávkami, různými jazyky nebo dokonce integrovat výstup do prohledávatelného PDF. Možnosti jsou neomezené, jakmile OCR engine převezme těžkou práci.

**Připravení posunout svůj dokumentový tok na vyšší úroveň?** Vezměte kód, nasměrujte ho na své skeny a sledujte, jak úhly otáčení mizí. Pokud narazíte na problémy, zanechte komentář níže – šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}