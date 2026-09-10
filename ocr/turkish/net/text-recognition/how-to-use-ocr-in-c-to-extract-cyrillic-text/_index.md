---
category: general
date: 2026-09-10
description: C#'ta OCR kullanarak Kiril alfabesi metnini çıkarmak, görüntüleri ön
  işleme tabi tutmak ve tek bir çalıştırılabilir örnekle PDF veya HTML dosyalarına
  dönüştürmek.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- preprocess image for OCR
- convert image to PDF
- convert image to HTML
- extract Cyrillic text
language: tr
lastmod: 2026-09-10
og_description: C#'ta OCR'ı kullanarak Kiril alfabesi metnini çıkarmak, görüntüleri
  ön işleme tabi tutmak ve sonuçları PDF ya da HTML olarak dışa aktarmak. Bu adım
  adım rehberi izleyin.
og_image_alt: Diagram illustrating how to use OCR to extract Cyrillic text and convert
  images
og_title: C#'ta OCR Nasıl Kullanılır – Kiril Metni Çıkar ve Görüntüleri Dönüştür
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: How to use OCR in C# to extract Cyrillic text, preprocess images, and
    convert them to PDF or HTML files in a single, runnable example.
  headline: How to use OCR in C# to extract Cyrillic text
  type: TechArticle
tags:
- OCR
- C#
- Cyrillic
- Image processing
- PDF conversion
title: C#'ta OCR kullanarak Kiril metnini nasıl çıkarabilirsiniz
url: /tr/net/text-recognition/how-to-use-ocr-in-c-to-extract-cyrillic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR Kullanarak Kiril Metni Çıkarma

If you need to **how to use OCR** in C# for extracting Cyrillic text from scanned documents, this guide shows you a complete, ready‑to‑run solution. You’ll also learn how to **preprocess image for OCR**, and how to **convert image to PDF** or **convert image to HTML** once the text has been recognized.

Document digitization projects often stumble on two problems: low‑quality scans and the need to store results in multiple formats. This tutorial solves both by using the Aspose.OCR library, which automatically downloads missing language packs, offers built‑in image‑processing helpers, and can export the OCR result to PDF or HTML with a single call.

## Önkoşullar

* .NET 6.0 SDK veya daha yenisi (kod .NET Framework 4.7+ ile de çalışır).
* Visual Studio 2022 veya C# projelerini destekleyen herhangi bir editör.
* The **Aspose.OCR** NuGet package. Install it with:

```bash
dotnet add package Aspose.OCR
```

* Kiril karakterleri içeren bir görüntü dosyası (ör. `sample_cyrillic.jpg`).  
  Dosyayı `YOUR_DIRECTORY` olarak referans verebileceğiniz bir klasöre yerleştirin.

The library will download the Cyrillic language pack the first time you set `ocrEngine.Language = Language.Cyrillic;`, so no manual download is required.

## Adım 1 – OCR motorunu başlatma (how to use OCR)

Creating an `OcrEngine` instance prepares the engine for all subsequent operations.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine – the first step in how to use OCR with Aspose
        var ocrEngine = new OcrEngine();
```

**Neden önemli:** The engine holds configuration such as language, image‑processing settings, and output options. Initializing it once keeps the rest of the code clean and thread‑safe.

## Adım 2 – Kiril dilini seçme (extract Cyrillic text)

```csharp
        // Select Cyrillic language; the pack is fetched automatically if missing
        ocrEngine.Language = Language.Cyrillic;
```

**Neden önemli:** OCR accuracy depends heavily on the correct language model. By explicitly selecting `Language.Cyrillic`, the engine applies character‑frequency tables suited for Russian, Ukrainian, Bulgarian, etc.

## Adım 3 – Görüntüyü OCR için ön işleme

Low‑quality scans contain skew, speckles, or uneven lighting. The built‑in `ImageProcessor` can improve recognition rates with just two calls.

```csharp
        // Optional but strongly recommended: deskew and despeckle the image
        ocrEngine.ImageProcessor.Deskew();      // Aligns rotated text
        ocrEngine.ImageProcessor.Despeckle();  // Removes isolated noise pixels
```

**Neden önemli:** Pre‑processing reduces false characters and boosts the confidence score. Skewed text often yields garbled output; deskewing straightens it. Despeckling eliminates tiny artifacts that the OCR engine might otherwise interpret as letters.

> **Pro ipucu:** If your source images are already clean, you can skip these calls. For heavily degraded scans, consider additional steps such as `Binarize()` or `ContrastStretch()`.

## Adım 4 – Giriş görüntüsü üzerinde OCR gerçekleştirme

```csharp
        // The image path can be absolute or relative to the executable
        string inputPath = Path.Combine("YOUR_DIRECTORY", "sample_cyrillic.jpg");
        ocrEngine.Process(inputPath);
```

**Neden önemli:** `Process` runs the recognition pipeline on the supplied bitmap. It returns `void`; the recognized text becomes available through the `Text` property.

## Adım 5 – Tanınan metni al ve bir dosyaya kaydet

```csharp
        // Access the recognized string
        string recognizedText = ocrEngine.Text;

        // Save the plain‑text result
        string txtOutput = Path.Combine("YOUR_DIRECTORY", "result.txt");
        File.WriteAllText(txtOutput, recognizedText);
        Console.WriteLine("Text saved to: " + txtOutput);
```

**Neden önemli:** Storing the raw text enables downstream processing such as searching, indexing, or feeding into translation services.

## Adım 6 – OCR sonucunu diğer formatlara dışa aktarma (convert image to PDF & convert image to HTML)

```csharp
        // Export as PDF – useful for archival or sharing with non‑technical users
        string pdfOutput = Path.Combine("YOUR_DIRECTORY", "result.pdf");
        ocrEngine.SaveResultAsPdf(pdfOutput);
        Console.WriteLine("PDF saved to: " + pdfOutput);

        // Export as HTML – retains basic layout and can be displayed in browsers
        string htmlOutput = Path.Combine("YOUR_DIRECTORY", "result.html");
        ocrEngine.SaveResultAsHtml(htmlOutput);
        Console.WriteLine("HTML saved to: " + htmlOutput);
    }
}
```

**Neden önemli:** Converting the OCR result to PDF or HTML lets you keep the visual context of the original image while providing searchable text. This is especially valuable for legal or archival workflows.

### Beklenen çıktı

Running the program with a clear Cyrillic scan produces three files:

* `result.txt` – düz Unicode metin, ör. `Пример текста на кириллице`.
* `result.pdf` – görüntüyü içinde barındıran ve aranabilir görünmez bir metin katmanı olan PDF.
* `result.html` – görüntüyü ve seçilebilir metni gösteren bir HTML sayfası.

Open any of the files to verify that the Cyrillic characters have been correctly extracted.

## Yaygın sorular ve uç durumlar

| Question | Answer |
|----------|--------|
| **Dil paketi indirilmezse ne olur?** | Ensure the machine has internet access. You can also pre‑download the pack from Aspose’s site and place it in the `bin` folder. |
| **Aynı çalışmada başka alfabeleri tanıyabilir miyim?** | Yes. Call `ocrEngine.Language = Language.English;` (or any supported enum) before `Process`. You may need to run `Process` separately for each language if the image mixes scripts. |
| **Görselim çok sayfalı TIFF – bu çalışır mı?** | `OcrEngine` processes one bitmap at a time. Load each page into a `Bitmap` and call `Process` in a loop, concatenating the results. |
| **Büyük toplular için performansı nasıl artırabilirim?** | Reuse a single `OcrEngine` instance and set `ocrEngine.OptimizeMemory = true;`. Also, consider parallel processing with separate engine instances per thread. |

## Sonuç

You now know **how to use OCR** in C# to **extract Cyrillic text**, **preprocess image for OCR**, and **convert image to PDF** or **convert image to HTML** in a few concise steps. The complete example demonstrates a production‑

## Sonra Ne Öğrenmelisiniz?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [AspOCR Nasıl Kullanılır: .NET için Görüntü OCR Filtrelerini Ön İşleme](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [C#’ta OCR Metni Nasıl Çıkarılır – Tam Adım Adım Kılavuz](/ocr/english/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/)
- [Aspose OCR JSON Sonucu Görüntü Tanıma İçin Nasıl Kullanılır](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}