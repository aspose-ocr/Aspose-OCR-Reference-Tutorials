---
category: general
date: 2026-02-16
description: Vytvořte prohledávatelný PDF ze souboru TIFF pomocí Aspose OCR. Naučte
  se, jak převést TIFF na PDF, provést OCR obrázku do PDF a rozpoznat text z obrázku
  v C#.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- ocr image to pdf
- recognize text from image
- convert scanned image pdf
language: cs
og_description: Rychle vytvořte prohledávatelný PDF. Tento tutoriál ukazuje, jak převést
  TIFF na PDF, OCR obrázek na PDF a rozpoznat text z obrázku pomocí Aspose OCR.
og_title: Vytvořte prohledávatelný PDF z TIFF – Průvodce Aspose OCR
tags:
- Aspose OCR
- C#
- PDF/A
- Document Processing
title: Vytvoření prohledávatelného PDF z TIFF – krok za krokem průvodce Aspose OCR
url: /cs/net/text-recognition/create-searchable-pdf-from-tiff-aspose-ocr-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF z TIFF – Aspose OCR krok za krokem

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** ze skenovaného TIFF, ale nebyli jste si jisti, která knihovna to zvládne? Nejste sami. V mnoha projektech kancelářské automatizace končíme s hromadou souborů TIFF, které vypadají jako obrázky, ne jako text. Dobrá zpráva? S Aspose OCR můžete **převést tiff na pdf**, spustit OCR na obrázku a získat PDF/A‑2b, které je plně prohledávatelné.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem v C#, který přesně ukazuje, jak **vytvořit prohledávatelné PDF** soubory, proč je každý krok důležitý a na jaké úskalí si dát pozor. Na konci budete schopni **rozpoznat text z obrázku**, **OCR obrázek do pdf** a dokonce **převést skenovaný obrázek pdf** dokumenty, které splňují archivní standardy.

## Co se naučíte

- Jak nainstalovat a odkazovat na NuGet balíček Aspose OCR.  
- Přesný kód potřebný k **vytvoření prohledávatelného PDF** z TIFF souboru.  
- Proč je načtení správného jazykového modelu klíčové pro přesné OCR.  
- Tipy pro práci s velkými skeny, multi‑page TIFFy a PDF/A kompatibilitou.  
- Kde najít výsledný soubor a jak ověřit, že je text prohledávatelný.

### Předpoklady

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later (any recent .NET runtime) | Aspose OCR dodává binární soubory pro .NET Standard 2.0+, které běží všude od .NET Core po .NET Framework. |
| Visual Studio 2022 (or VS Code with C# extension) | Poskytuje vám IntelliSense a snadnou správu NuGet balíčků. |
| An active Aspose OCR license (or a free evaluation key) | Bezplatná zkušební verze omezuje počet stránek; licence odstraňuje vodoznak a umožňuje výstup PDF/A‑2b. |
| A TIFF file you want to process (e.g., `input.tif`) | Toto je zdrojový obrázek, který převedeme na **prohledávatelné PDF**. |

> **Tip:** Pokud pracujete s multi‑page TIFFy, Aspose OCR automaticky zachází s každou stránkou jako s odděleným obrázkem – není potřeba žádný další kód.

---

## Krok 1: Instalace NuGet balíčku Aspose OCR

Nejprve přidejte knihovnu do svého projektu. Otevřete Package Manager Console a spusťte:

```powershell
Install-Package Aspose.OCR
```

Nebo, pokud dáváte přednost GUI, vyhledejte “Aspose.OCR” v **NuGet Package Manager** a klikněte na **Install**. Tím se stáhnou všechny potřebné DLL, včetně jazykových modelů, které později budeme potřebovat.

> **Proč tento krok?** Bez balíčku třída `OcrEngine` neexistuje a získáte chyby při kompilaci. Přístup přes NuGet zaručuje, že máte správnou verzi (aktuálně 23.12) a automaticky stáhne všechny tranzitivní závislosti.

## Krok 2: Inicializace OCR enginu

Vytvoření instance enginu je první skutečná řádka kódu, kterou napíšete. Představte si `OcrEngine` jako mozek, který provádí veškerou těžkou práci.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine – this object will manage the entire pipeline
OcrEngine ocrEngine = new OcrEngine();
```

> **Co se děje?** Konstruktor nastaví interní buffery a připraví engine na načtení jazykového modelu. Pokud to přeskočíte, pozdější volání jako `LoadLanguage` vyhodí `NullReferenceException`.

## Krok 3: Načtení anglického jazykového modelu (nebo jiného)

Přesnost OCR závisí na načteném jazykovém modelu. Pro většinu západních dokumentů stačí angličtina, ale Aspose podporuje desítky jazyků.

```csharp
// Load English language data – essential for recognizing Latin characters
ocrEngine.LoadLanguage(LanguageModel.English);
```

> **Proč načíst model?** Engine potřebuje statistické vyjádření tvarů znaků. Bez něj získáte nesmysly nebo prázdný výsledek. Pokud potřebujete **rozpoznat text z obrázku** ve francouzštině, nahraďte `LanguageModel.English` za `LanguageModel.French`.

## Krok 4: Poskytnutí TIFF obrázku a generování PDF/A‑2b

Nyní nasměrujeme engine na náš zdrojový soubor. Pomocník `ImageStream.FromFile` načte TIFF (jednostránkový nebo multi‑page) do paměti.

```csharp
// Step 4: Assign the TIFF image to the engine
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.tif");

// Run OCR and produce a PDF/A‑2b document – this is the searchable PDF we want
PdfAResult searchablePdf = ocrEngine.RecognizePdfA(PdfAStandard.PdfA2b);
```

> **Co to dělá?** `RecognizePdfA` provádí tři akce pod kapotou:
> 1️⃣ Spustí OCR na každé stránce TIFF.  
> 2️⃣ Vloží rozpoznaný text jako neviditelnou vrstvu.  
> 3️⃣ Zabalí vše do kontejneru PDF/A‑2b, což je ISO‑standard pro dlouhodobou archivaci.  

Pokud potřebujete jen obyčejné PDF (bez archivní kompatibility), můžete místo toho zavolat `ocrEngine.RecognizePdf()`. Pro většinu podnikového scénáře je však PDF/A‑2b nejbezpečnější volba.

## Krok 5: Uložení prohledávatelného PDF na disk

Nakonec výsledek zapíšete do souboru. Metoda `Save` přijímá cestu a řeší veškerý I/O.

```csharp
// Save the generated searchable PDF to your output folder
searchablePdf.Save("YOUR_DIRECTORY/output.pdf");
```

Když otevřete `output.pdf` v Adobe Readeru, měli byste být schopni zadat slovo do vyhledávacího pole a okamžitě jej najít – i když původní soubor byl jen obrázek. To je kouzlo **vytvoření prohledávatelného PDF** workflow.

## Převod TIFF na PDF – Rychlé shrnutí

Níže je kompletní, připravený program, který spojuje vše dohromady. Klidně jej zkopírujte do konzolové aplikace a stiskněte **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the desired language model (English in this case)
        ocrEngine.LoadLanguage(LanguageModel.English);

        // 3️⃣ Point the engine at the TIFF you want to convert
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.tif");

        // 4️⃣ Recognize the image and produce a PDF/A‑2b (searchable PDF)
        PdfAResult searchablePdf = ocrEngine.RecognizePdfA(PdfAStandard.PdfA2b);

        // 5️⃣ Persist the result to disk
        searchablePdf.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("✅ Searchable PDF created successfully!");
    }
}
```

**Očekávaný výsledek:** `output.pdf` se objeví v `YOUR_DIRECTORY`. Otevřete jej, vyberte nástroj pro text a uvidíte vybratelný, prohledávatelný text překrytý nad původním rastrovým obrázkem.

## OCR obrázek do PDF – Řešení okrajových případů

### Multi‑page TIFFy

Pokud váš zdrojový soubor obsahuje více než jednu stránku, Aspose OCR automaticky zpracuje každou stránku a přidá odpovídající stránku do PDF. Žádné další cyklení není potřeba.

### Velké soubory a správa paměti

Pro skeny v řádu gigabajtů zvažte zapnutí **streaming režimu**:

```csharp
ocrEngine.Image = ImageStream.FromFile("large.tif", useMemoryCache: false);
```

Tím řeknete enginu, aby četl bloky z disku místo načítání celého obrázku do RAM – ideální pro serverové dávkové úlohy.

### Různé výstupní formáty

Někdy nepotřebujete PDF/A‑2b, ale obyčejné PDF. Změňte volání:

```csharp
PdfResult plainPdf = ocrEngine.RecognizePdf();
plainPdf.Save("plain.pdf");
```

Nebo pokud chcete jen čistý text (bez PDF), použijte:

```csharp
string extractedText = ocrEngine.RecognizeText();
System.IO.File.WriteAllText("text.txt", extractedText);
```

Tyto varianty řeší scénář **convert scanned image pdf**, kde následné systémy akceptují jen obyčejná PDF.

## Tipy pro spolehlivé OCR

- **DPI má význam:** Skeny s 300 DPI nebo vyšší poskytují nejlepší rozpoznávací poměr. Pod 200 DPI zaznamenáte pokles přesnosti.  
- **Předzpracování:** Pokud je TIFF šumivý, spusťte jej přes `ocrEngine.Image = ImageProcessor.Deskew(...).Apply(ocrEngine.Image);` před rozpoznáním.  
- **Licencování:** Nezapomeňte nastavit licenci brzy v aplikaci (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`). Bez ní bude výstup obsahovat vodoznak “Evaluation”.  
- **Dávkové zpracování:** Zabalte hlavní logiku do `foreach` smyčky přes adresář TIFF souborů, abyste **convert tiff to pdf** hromadně.

## Často kladené otázky

**Q: Funguje to na Linuxu?**  
A: Naprosto. Aspose OCR cílí na .NET Standard, takže můžete spustit stejný binární soubor na Windows, Linuxu nebo macOS s .NET 6 runtime.

**Q: Co když potřebuji rozpoznat jazyk jiný než angličtinu?**  
A: Stačí nahradit `LanguageModel.English` odpovídajícím enumem, např. `LanguageModel.Spanish`. Můžete také načíst více jazyků najednou pro dokumenty s mixovanými jazyky.

**Q: Mohu vložit vlastní font do PDF/A?**  
A: Ano. Použijte `ocrEngine.Options.PdfOptions.Font = PdfFont.CreateFont("path/to/font.ttf");` před voláním `RecognizePdfA`.

## Závěr

Probrali jsme vše, co potřebujete k **vytvoření prohledávatelného PDF** souborů z TIFF obrázků pomocí Aspose OCR. Od instalace NuGet balíčku, načtení správného jazykového modelu, až po generování PDF/A‑

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}