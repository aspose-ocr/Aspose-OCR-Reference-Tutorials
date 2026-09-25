---
category: general
date: 2026-01-15
description: c# ocr öğreticisi, görüntüden metin tanıma, faturadan metin çıkarma ve
  GPU üzerinde Aspose OCR kullanarak görüntüyü metne dönüştürmeyi gösterir.
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- extract text from invoice
- convert image to text
- load image for ocr
language: tr
og_description: c# ocr öğreticisi, görüntüden metin tanımayı, faturadan metin çıkarmayı
  ve GPU'da Aspose OCR ile görüntüyü metne dönüştürmeyi öğretir.
og_title: c# ocr öğretici – Hızlı GPU Destekli Metin Tanıma
tags:
- OCR
- C#
- Aspose
- GPU
title: c# ocr öğreticisi – GPU hızlandırmasıyla görüntüden metin tanıma
url: /tr/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Görüntüden Metin Tanıma GPU Hızlandırmasıyla

Ever needed a **c# ocr tutorial** that actually gets the job done without endless trial‑and‑error? Maybe you’re staring at a high‑resolution invoice and wondering how to **extract text from invoice** files in a matter of seconds. The good news is you don’t have to reinvent the wheel—Aspose.OCR gives you a clean, GPU‑accelerated API that does the heavy lifting for you.

In this guide we’ll walk through a complete, runnable example that shows how to **recognize text from**, **convert image to text**, and handle the most common pitfalls. By the end you’ll have a self‑contained program that can read any picture of a document, from receipts to scanned contracts, and output clean, searchable text.

## Öğrenecekleriniz

- Aspose.OCR NuGet paketini nasıl kurup referans vereceğinizi.
- OCR motorunu GPU üzerinde çalışacak şekilde nasıl yapılandıracağınızı, yanıp sönen hızlı performans için.
- `OcrImage.FromFile` kullanarak **load image for ocr**'un doğru yolu.
- `Recognize` metodunu istenen dil ile nasıl çağırıp sonucu alacağınızı.
- Çok sayfalı PDF'lerle, düşük kontrast taramalarıyla ve hata yönetimiyle başa çıkma ipuçları.

Aspose ile önceden bir deneyime ihtiyacınız yok; sadece çalışan bir .NET geliştirme ortamı (Visual Studio 2022 veya VS Code) ve mütevazı bir GPU (entegre bir Intel GPU bile yeterli) yeterlidir.

## Adım 1 – Aspose.OCR'yi Kurun ve Projenizi Hazırlayın

İlk olarak, Aspose.OCR kütüphanesine ihtiyacınız var. En kolay yol NuGet üzerinden.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** .NET 6 veya daha yeni bir sürümü hedefliyorsanız, paket Windows, Linux ve macOS için yerel GPU ikili dosyalarını otomatik olarak çeker. Kopyalanacak ekstra DLL yok.

Paket eklendikten sonra, proje dosyanızı (`*.csproj`) açın ve referansı doğrulayın:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.12.0" />
</ItemGroup>
```

Artık kodlamaya başlamak için ihtiyacınız olan her şeye sahipsiniz.

## Adım 2 – GPU‑Destekli OCR Motoru Oluşturun (c# ocr tutorial)

**c# ocr tutorial**'nin kalbi `OcrEngine`'dir. `Engine = Engine.Gpu` ayarlayarak Aspose'a CPU yerine grafik kartını kullanmasını söylüyoruz.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine with GPU acceleration.
            var ocrEngine = new OcrEngine
            {
                Engine = Engine.Gpu // GPU acceleration is selected; the library auto‑detects the device.
            };

            // The rest of the steps are broken out into separate methods for clarity.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            PerformOcr(ocrEngine, imagePath);
        }
    }
}
```

> **Neden GPU?** GPU, binlerce pikseli paralel olarak işleyebilir, büyük, yüksek DPI'lı görüntülerde OCR süresini saniyelerden saniyenin kesirlerine düşürür.

## Adım 3 – OCR için Görüntü Yükleme (load image for ocr)

Görüntüyü doğru yüklemek düşündüğünüzden daha önemlidir. `OcrImage.FromFile` PNG, JPEG, BMP, TIFF ve hatta PDF sayfalarını destekler. Ayrıca görüntünün DPI'sını okur, bu da doğruluğu etkiler.

```csharp
static void PerformOcr(OcrEngine engine, string filePath)
{
    // Step 3: Load the image you want to recognize.
    // The FromFile method automatically detects the format.
    var image = OcrImage.FromFile(filePath);

    // Optional: Pre‑process the image for better results.
    // For example, you can increase contrast or convert to grayscale.
    image = ImagePreprocessor.AdjustContrast(image, 1.2);
    image = ImagePreprocessor.ConvertToGrayscale(image);
    
    // Continue to recognition...
    RecognizeAndDisplay(engine, image);
}
```

**Not:** Bir PDF ile çalışıyorsanız, her sayfayı bir `OcrImage` olarak çıkarabilir ve tek tek besleyebilirsiniz.

## Adım 4 – Görüntüden Metin Tanıma (recognize text from image)

Şimdi sihir gerçekleşiyor. Motoru İngilizce metin tanıması için istiyoruz, ancak Aspose tarafından desteklenen herhangi bir dili (İspanyolca, Almanca, Çince vb.) geçebilirsiniz.

```csharp
static void RecognizeAndDisplay(OcrEngine engine, OcrImage image)
{
    // Step 4: Perform OCR on the image using the desired language.
    var result = engine.Recognize(image, Language.English);

    // Step 5: Output the recognized text.
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(result.Text);
}
```

`result.Text` özelliği düz metni içerir. Her kelime için güven skoruna ihtiyacınız varsa, `result.Regions`'ı inceleyebilirsiniz.

### Beklenen Çıktı

```
=== OCR RESULT ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,234.56
Thank you for your business!
```

Görüntü bulanıksa, bozuk karakterler görebilirsiniz—bu, Adım 3'teki ön işleme burada devreye girer.

## Adım 5 – Faturadan Metin Çıkarma – Gerçek Dünya Örneği

Diyelim ki taranmış faturalarla dolu bir klasörünüz var ve toplam tutarı çıkarmak istiyorsunuz. Aşağıda, basit bir düzenli ifade kullanan önceki kodun hızlı bir uzantısı var.

```csharp
using System.Text.RegularExpressions;

static void ExtractTotalAmount(string ocrText)
{
    // Look for a pattern like "$1,234.56"
    var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
    if (match.Success)
        Console.WriteLine($"Detected total: {match.Value}");
    else
        Console.WriteLine("Total amount not found.");
}
```

OCR sonucunu yazdırdıktan hemen sonra `ExtractTotalAmount(result.Text);` çağırırsınız. Bu, ham dizeyi elde ettikten sonra **extract text from invoice** dosyalarından metin çıkarmanın ne kadar kolay olduğunu gösterir.

## Adım 6 – Toplu Olarak Görüntüyü Metne Dönüştürme (convert image to text)

Tek bir dosyayı işlemek bir demo için yeterli, ancak üretim kodu genellikle onlarca ya da yüzlerce görüntüyü işlemek zorundadır. İşte tüm bir dizini işleyen kısa bir döngü:

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    foreach (var file in Directory.EnumerateFiles(folderPath, "*.*", SearchOption.TopDirectoryOnly)
                                 .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
    {
        Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
        var img = OcrImage.FromFile(file);
        var res = engine.Recognize(img, Language.English);
        Console.WriteLine(res.Text);
        ExtractTotalAmount(res.Text); // optional invoice extraction
    }
}
```

`ProcessFolder(ocrEngine, @"C:\Invoices")` çalıştırmak, klasördeki her desteklenen dosya için **convert image to text** yapacak ve hızı artırmak için GPU'yu kullanacaktır.

## Kenar Durumları ve Yaygın Tuzaklar

| Situation | Why It Happens | Quick Fix |
|-----------|----------------|-----------|
| **Low‑contrast scan** | OCR, ön planı arka plandan ayırt etmekte zorlanır. | Kontrastı artır (`ImagePreprocessor.AdjustContrast`) veya adaptif eşikleme uygulayın. |
| **Multi‑page PDF** | `OcrImage.FromFile` sadece ilk sayfayı okur. | `PdfDocument` kullanarak her sayfayı bir `OcrImage` olarak çıkarın ve döngüye alın. |
| **Unsupported language** | Varsayılan dil İngilizce olarak ayarlanmıştır. | `Language.Spanish` veya desteklenen herhangi bir enum değerini geçin. |
| **GPU not detected** | Yerel ikili dosyalar eksik veya sürücü güncel değil. | GPU sürücüsünün güncel olduğunu doğrulayın; `-runtime` bayrağıyla NuGet paketini yeniden yükleyin. |
| **Out‑of‑memory on huge images** | GPU belleği sınırlıdır. | Görüntüyü küçültün (`image = ImagePreprocessor.Resize(image, 2000, 0)`). |

## Tam Çalışan Örnek

Aşağıda, yeni bir konsol uygulamasına kopyalayıp yapıştırabileceğiniz tam program bulunmaktadır. Yukarıda tartışılan tüm yardımcı metodları içerir.

```csharp
using System;
using System.IO;
using System.Linq;
using System.Text.RegularExpressions;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize GPU‑accelerated OCR engine.
            var ocrEngine = new OcrEngine { Engine = Engine.Gpu };

            // 2️⃣ Define the path to a single image or a folder.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            // string folderPath = @"C:\Invoices";

            // Uncomment one of the following lines:
            PerformOcr(ocrEngine, imagePath);
            // ProcessFolder(ocrEngine, folderPath);
        }

        // -------------------------------------------------
        // Load image, preprocess, recognize, and display.
        // -------------------------------------------------
        static void PerformOcr(OcrEngine engine, string filePath)
        {
            var image = OcrImage.FromFile(filePath);
            image = ImagePreprocessor.AdjustContrast(image, 1.2);
            image = ImagePreprocessor.ConvertToGrayscale(image);

            var result = engine.Recognize(image, Language.English);
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(result.Text);

            ExtractTotalAmount(result.Text);
        }

        // -------------------------------------------------
        // Bulk processing of a folder.
        // -------------------------------------------------
        static void ProcessFolder(OcrEngine engine, string folderPath)
        {
            foreach (var file in Directory.EnumerateFiles(folderPath, "*.*")
                                          .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
            {
                Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
                var img = OcrImage.FromFile(file);
                var res = engine.Recognize(img, Language.English);
                Console.WriteLine(res.Text);
                ExtractTotalAmount(res.Text);
            }
        }

        // -------------------------------------------------
        // Simple regex to pull the total amount from an invoice.
        // -------------------------------------------------
        static void ExtractTotalAmount(string ocrText)
        {
            var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
            if (match.Success)
                Console.WriteLine($"Detected total: {match.Value}");
            else
                Console.WriteLine("Total amount not found.");
        }
    }
}
```

**Run it** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}