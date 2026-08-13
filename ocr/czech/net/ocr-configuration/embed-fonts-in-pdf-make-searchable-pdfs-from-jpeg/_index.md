---
category: general
date: 2026-03-05
description: Vkládejte písma do PDF při převodu JPEG na prohledávatelný PDF pomocí
  Aspose OCR. Naučte se, jak rozpoznat text z JPEG a vložit písma pro soulad s PDF/A‑2b.
draft: false
keywords:
- embed fonts in pdf
- recognize text from jpeg
- how to create searchable pdf
- convert image to searchable pdf
- perform ocr on image
language: cs
og_description: Vložte písma do PDF při převodu JPEG na prohledávatelné PDF. Tento
  krok‑za‑krokem průvodce ukazuje, jak rozpoznat text z JPEG a vytvořit soubory kompatibilní
  s PDF/A‑2b.
og_title: Vložit písma do PDF – Vytvořit prohledávatelné PDF z JPEG
tags:
- Aspose OCR
- PDF generation
- C#
- .NET
title: Vložit písma do PDF – Vytvořit prohledávatelné PDF z JPEG
url: /cs/net/ocr-configuration/embed-fonts-in-pdf-make-searchable-pdfs-from-jpeg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vkládání fontů do PDF – Vytvořte prohledávatelné PDF z JPEG

Už jste někdy potřebovali **vložit fonty do PDF** souborů, které byly vytvořeny ze skenovaných obrázků? Nejste v tom sami. Většina vývojářů narazí na problém, kdy výsledné PDF vypadá v pořádku na jejich počítači, ale po otevření jinde chybí text, protože fonty nebyly vloženy.  

Dobrá zpráva? S Aspose OCR můžete **rozpoznat text z JPEG**, vložit potřebné fonty a vygenerovat plně prohledávatelný dokument PDF/A‑2b během několika řádků C#. V tomto tutoriálu projdeme každý krok – proč je každé nastavení důležité, jak se vyhnout běžným úskalím a jak by měl vypadat finální PDF.

Na konci tohoto průvodce budete schopni **převést obrázek na prohledávatelné PDF**, správně vložit fonty a pochopit, jak **provádět OCR na obrázkových** souborech programově.

---

## Co budete potřebovat

- **Aspose.OCR for .NET** (nejnovější verze, např. 23.10) – knihovna, která dělá těžkou práci.
- Platný **licenční soubor Aspose OCR** (`Aspose.OCR.lic`). Bezplatná zkušební verze funguje, ale licencovaná verze odstraňuje vodotisk hodnocení.
- JPEG obrázek (`input.jpg`) obsahující tištěný nebo psaný text.
- Vývojové prostředí .NET (Visual Studio, Rider nebo VS Code s rozšířením C#).

Žádné další NuGet balíčky nejsou potřeba; OCR engine již obsahuje nástroje pro generování PDF.

---

## Krok 1: Nastavte OCR engine a aplikujte licenci *(Embed Fonts in PDF)*

Než spustíte jakékoli rozpoznávání, musíte vytvořit instanci `OcrEngine` a zadat, kterou licenci použít. Přeskočení kroku s licencí způsobí, že engine poběží v evaluačním režimu, který přidává překrytí „Powered by Aspose“ na každou stránku.

```csharp
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;
using Aspose.OCR.Saving;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Apply your license – replace the path with the actual location of your .lic file
ocrEngine.SetLicense("Aspose.OCR.lic");
```

**Proč je to důležité:** Licence nejen odstraňuje vodotisky, ale také odemyká možnosti souladu s PDF/A, které později potřebujeme pro vložení fontů.

---

## Krok 2: Načtěte JPEG obrázek, který chcete zpracovat *(Recognize Text from JPEG)*

OCR engine pracuje s vlastností `Image`, která přijímá `ImageStream`. Nasmerujte ji na JPEG, který chcete převést.

```csharp
// Load the source JPEG image
ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\input.jpg");
```

**Tip:** Pokud je váš obrázek v proudu (např. nahraný přes API), můžete použít `ImageStream.FromStream(yourStream)` místo `FromFile`.

---

## Krok 3: Nakonfigurujte PDF Save Options pro prohledávatelné PDF

Toto je jádro požadavku „embed fonts in PDF“. Použijeme `PdfSaveOptions` k:

1. Cílení na **PDF/A‑2b** (široce akceptovaný archivní standard).
2. **Vložení všech použitých fontů**, aby PDF vypadalo stejně všude.
3. Použití **bezeztrátové Flate komprese** pro udržení rozumné velikosti souboru.
4. Zachování původního JPEG jako pozadí, což zachovává vizuální věrnost.

```csharp
// Set up PDF export options
var pdfSaveOptions = new PdfSaveOptions
{
    // Produce a PDF/A‑2b compliant document
    PdfAStandard = PdfAStandard.PdfA2b,

    // Ensure every font used by the OCR text is embedded
    EmbedFonts = true,

    // Use lossless compression for the text and graphics streams
    Compression = PdfCompression.Flate,

    // Keep the original image behind the OCR layer (makes the PDF searchable)
    RenderOriginalImage = true
};
```

**Proč tato nastavení?**  
- **PdfAStandard.PdfA2b** zajišťuje dlouhodobou archivaci a vynutí vložení fontů.  
- **EmbedFonts = true** je explicitní příznak, který splňuje hlavní klíčové slovo.  
- **Compression.Flate** snižuje velikost bez ztráty kvality.  
- **RenderOriginalImage** zachovává vizuální vzhled naskenované stránky, zatímco skrytá OCR vrstva poskytuje prohledávatelný text.

---

## Krok 4: Spusťte OCR rozpoznání na obrázku *(Perform OCR on Image)*

S veškerou přípravou spusťte rozpoznání. Engine analyzuje JPEG, extrahuje znaky a interně vytvoří textovou vrstvu.

```csharp
// Execute OCR – this populates the internal text layer
ocrEngine.Recognize();
```

**Často kladená otázka:** *Musím specifikovat jazyk nebo slovník?*  
Pokud váš dokument není v angličtině, nastavte `ocrEngine.Language = OcrLanguage.French;` (nebo jakýkoli podporovaný jazyk) před voláním `Recognize()`. Výchozí je angličtina.

---

## Krok 5: Uložte výstup jako prohledávatelné PDF s vloženými fonty

Nakonec výsledek zapíšete na disk. Metoda `Save` přijímá cílovou cestu a `PdfSaveOptions`, které jsme definovali dříve.

```csharp
// Save the searchable PDF with embedded fonts
ocrEngine.Save(@"C:\MyImages\output.pdf", pdfSaveOptions);
```

Když otevřete `output.pdf` v Adobe Acrobat nebo jakémkoli PDF prohlížeči, měli byste být schopni:

- **Vyhledávat** libovolné slovo, které se objevilo v původním JPEG.
- Nevidět **žádná varování o chybějících fontech** (díky `EmbedFonts = true`).
- Ověřit, že soubor splňuje **PDF/A‑2b** (Soubor → Vlastnosti → PDF/A).

---

## Kompletní funkční příklad

Níže je kompletní, připravený program. Zkopírujte jej do nového projektu Console App, upravte cesty k souborům a stiskněte **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;
using Aspose.OCR.Saving;

namespace ImageToSearchablePdf
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine and apply license
            var ocrEngine = new OcrEngine();
            ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

            // 2️⃣ Load JPEG image
            ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\input.jpg");

            // 3️⃣ Configure PDF save options (embed fonts, PDF/A‑2b, etc.)
            var pdfSaveOptions = new PdfSaveOptions
            {
                PdfAStandard = PdfAStandard.PdfA2b,
                EmbedFonts = true,
                Compression = PdfCompression.Flate,
                RenderOriginalImage = true
            };

            // 4️⃣ Run OCR recognition
            ocrEngine.Recognize();

            // 5️⃣ Save searchable PDF with embedded fonts
            string outputPath = @"C:\MyImages\output.pdf";
            ocrEngine.Save(outputPath, pdfSaveOptions);

            Console.WriteLine($"✅ PDF created at: {outputPath}");
            Console.WriteLine("Open it in any PDF viewer and try searching for words from the original JPEG.");
        }
    }
}
```

**Očekávaný výstup:**  
Konzole vypíše zprávu o úspěchu a `output.pdf` se objeví v cílové složce. Otevření PDF a použití vyhledávacího pole prohlížeče by mělo najít jakékoli slovo, které bylo v `input.jpg`.

---

## Často kladené otázky a okrajové případy

### 1. „Co když je můj JPEG multi‑page TIFF?“
Aspose OCR zachází s každou stránkou samostatně. Převěďte TIFF na sérii JPEG (nebo použijte `ImageStream.FromFile` na každou stránku) a v cyklu provádějte OCR, přičemž výsledky přidáváte do stejného PDF opětovným použitím stejné instance `OcrEngine`.

### 2. „Mohu řídit DPI nebo předzpracování obrázku?“
Ano. Před voláním `Recognize()` můžete upravit rozlišení obrázku:

```csharp
ocrEngine.Image.DpiX = 300;
ocrEngine.Image.DpiY = 300;
ocrEngine.Image.AutoRotate = true; // auto‑rotate for landscape scans
```

Vyšší DPI často přináší lepší přesnost rozpoznání, zejména u malých fontů.

### 3. „Moje PDF stále ukazuje chybějící fonty v Adobe Readeru – co je špatně?“
Ujistěte se, že cílíte na **PDF/A‑2b** a že `EmbedFonts` je nastaveno na `true`. Pokud jste ručně změnili `PdfAStandard` na `None`, krok validace PDF/A je přeskočen a některé fonty mohou zůstat nevloženy.

### 4. „Je OCR vrstva prohledávatelná na mobilních zařízeních?“
Rozhodně. Skrytá textová vrstva je součástí PDF specifikace, takže jakýkoli PDF prohlížeč, který podporuje extrakci textu (včetně iOS Files, Android PDF Viewer atd.), umožní uživatelům vyhledávat.

### 5. „Jak zacházet s pravopisnými jazyky zprava doleva, jako je arabština?“
Nastavte jazyk před rozpoznáním:

```csharp
ocrEngine.Language = OcrLanguage.Arabic;
ocrEngine.Recognize();
```

Aspose OCR automaticky přepne směr textu a vloží odpovídající fonty, když je `EmbedFonts` true.

---

## Pro tipy a běžné úskalí

- **Pro tip:** Pokud jsou vaše zdrojové obrázky barevné fotografie, zvažte jejich převod na odstíny šedi (`ocrEngine.Image.ConvertToGrayscale();`). Tím snížíte velikost souboru bez zhoršení přesnosti OCR.
- **Dejte pozor na:** Použití bezplatné zkušební licence s **velkým** obrázkem může způsobit oříznutí OCR textu. Pro produkční zatížení upgradujte na plnou licenci.
- **Tip pro výkon:** Opakované používání stejné instance `OcrEngine` napříč více obrázky eliminuje režii opakovaného načítání OCR DLL.
- **Bezpečnostní poznámka:** PDF/A‑2b soubory jsou **read‑only** ze své podstaty, což pomáhá předcházet nechtěnému vkládání skriptů – pěkný bonus pro prostředí s přísnými požadavky na soulad.

---

## Závěr

Probrali jsme celý proces **vkládání fontů do PDF** při **rozpoznávání textu z JPEG** a vytvoření **prohledávatelného PDF**, které splňuje standard PDF/A‑2b. Celý postup se zjednodušuje na:

1. Inicializujte `OcrEngine` a aplikujte licenci.  
2. Načtěte JPEG obrázek.  
3. Nakonfigurujte `PdfSaveOptions` (vložit fonty, PDF/A‑2b, komprese).  
4. Spusťte `Recognize()`.  
5. Uložte s nastavenými možnostmi.

Nyní můžete tento tok integrovat do webových služeb, desktopových utilit nebo dávkových úloh, které potřebují **převést obrázek na prohledávatelné PDF** za běhu. Dalším krokem může být **vytvoření prohledávatelného PDF** z více stránek PDF nebo PDF generovaných

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}