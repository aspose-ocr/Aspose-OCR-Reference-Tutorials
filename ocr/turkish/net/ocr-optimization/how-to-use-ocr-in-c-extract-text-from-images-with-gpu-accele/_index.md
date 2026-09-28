---
category: general
date: 2025-12-29
description: C#'ta OCR'yi kullanarak görüntülerden metin çıkarmak, karakter sayısını
  göstermek ve Aspose OCR kullanarak GPU hızlandırmasıyla performansı artırmak.
draft: false
keywords:
- how to use OCR
- extract text image
- display character count
- gpu acceleration ocr
- c# ocr aspose
language: tr
og_description: C#'ta OCR kullanarak görüntülerden metin çıkarma, karakter sayısını
  gösterme ve Aspose OCR ile GPU kullanarak işleme hızlandırma.
og_title: C#'da OCR Nasıl Kullanılır – GPU ile Hızlı Metin Çıkarma
tags:
- OCR
- C#
- Aspose
- GPU
title: C#'ta OCR Nasıl Kullanılır – GPU Hızlandırmalı Görüntülerden Metin Çıkarma
url: /tr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR Nasıl Kullanılır – Tam Kılavuz

Binlerce satır kod yazmadan bir .NET projesinde **OCR nasıl kullanılır** diye hiç merak ettiniz mi? Belki devasa bir TIFF dosyasını taradınız ve metni hızlıca ihtiyacınız var, ya da sadece raporlama panosu için karakter saymak istiyorsunuz. Hangi durumda olursanız olun, doğru yerdesiniz. Bu öğreticide bir görüntüden metin çıkarma, karakter sayısını gösterme ve **GPU hızlandırmalı OCR** ile süreci süper‑hızlandırma adımlarını **C# Aspose OCR** kütüphanesiyle birlikte ele alacağız.

Ayrıca aradığınız ikincil konuları da serpiştireceğiz: **görüntüden metin çıkarma**, **karakter sayısını göster** ve **c# ocr aspose** ipuçları. Sonunda büyük taramaları anında işleyebilen hazır bir konsol uygulamanız olacak.

---

## Öğrenecekleriniz

- Aspose OCR'ı bir C# projesinde kurun (NuGet gizemi yok).
- Büyük dosyalar için **GPU hızlandırmalı OCR**'ı etkinleştirin.
- Bir görüntüyü yükleyin ve **görüntüden metin çıkarın**.
- **Karakter sayısını göster** ve işleme süresini görüntüleyin.
- Eksik GPU sürücüleri veya desteklenmeyen görüntü formatları gibi yaygın tuzakları yönetin.

> **Önkoşul:** .NET 6+ (veya .NET Framework 4.7.2) ve uyumlu bir GPU. GPU’nuz yoksa kod sorunsuz bir şekilde CPU moduna geri dönecektir.

![C#'ta GPU hızlandırmalı OCR kullanımı](ocr-gpu.png "GPU kullanımını gösteren OCR örneği")

*Image alt text: GPU hızlandırmalı OCR illüstrasyonu*

---

## Adım 1: Aspose OCR'ı Kurun ve Projeyi Hazırlayın

### Neden önemli

OCR **kullanabilmek** için kütüphane referans edilmelidir. Aspose OCR, CPU ve GPU için yerel ikili dosyaları içeren tek bir NuGet paketi olarak gelir, böylece DLL’leri manuel olarak aramanıza gerek kalmaz.

```csharp
// In your terminal or Package Manager Console
dotnet add package Aspose.OCR
```

> **Pro tip:** .NET Framework hedefliyorsanız, sürüm çakışmalarını önlemek için Visual Studio’daki NuGet UI’yı kullanın.

### Tam proje iskeleti

Yeni bir konsol uygulaması oluşturun ve aşağıdaki `Program.cs` dosyasını yapıştırın. Gerekli tüm `using` ifadelerini içerdiği için neyi içe aktarmanız gerektiği konusunda tahmin yürütmek zorunda kalmayacaksınız.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.ImageProcessing; // optional, for advanced pre‑processing

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Call the helper that does the heavy lifting
            RunOcr(@"YOUR_DIRECTORY/large_scanned_page.tif");
        }

        static void RunOcr(string imagePath)
        {
            // Step 2: Create and configure the OCR engine (see next section)
        }
    }
}
```

Dosyayı kaydedin, paketleri geri yükleyin ve bir sonraki adıma hazırsınız.

---

## Adım 2: OCR Motorunu GPU Hızlandırmasıyla Nasıl Kullanılır

### Neden GPU etkinleştirilmeli?

Çok‑megapiksel bir TIFF’i CPU’da işlemek saniyeler ya da dakikalar sürebilir. **GPU hızlandırmalı OCR** yolu, piksel‑bazlı işlemleri grafik kartınıza devrederek zamanı dramatik şekilde kısar—genellikle orijinal sürenin bir kesri kadar.

```csharp
static void RunOcr(string imagePath)
{
    // Create an OCR engine instance
    var ocrEngine = new OcrEngine();

    // Enable GPU acceleration – if a compatible device is found
    ocrEngine.UseGpu = true;
    ocrEngine.GpuDeviceId = 0; // 0 = first GPU; change if you have multiple

    // Optional sanity check – fall back to CPU if GPU init fails
    try
    {
        // This call forces the engine to initialize GPU resources
        ocrEngine.InitializeGpu();
        Console.WriteLine("✅ GPU acceleration enabled.");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"⚠️ GPU init failed ({ex.Message}), switching to CPU.");
        ocrEngine.UseGpu = false;
    }

    // Load the image (this also validates format)
    var inputImage = Image.Load(imagePath);
    
    // Perform OCR – the heavy lifting happens here
    var ocrResult = ocrEngine.Recognize(inputImage);

    // Step 3: Display results (character count & processing time)
    DisplayResult(ocrResult);
}
```

> **Neden bu çalışıyor:** `UseGpu` iç pipeline’ı açar/kapatır. `InitializeGpu()` erken doğrulama yapar, böylece uzun süren `Recognize` çağrısından önce sürücü sorunlarını yakalayabilirsiniz.

---

## Adım 3: Görüntüden Metin Çıkarma ve Karakter Sayısını Gösterme

Motor çalışır durumda olduğuna göre, **görüntüden metin çıkar** ve tanınan karakter sayısını gösterelim. Bu, çoğu geliştiricinin atladığı ama doğrulama ve sonraki analizler için kritik bir adımdır.

```csharp
static void DisplayResult(OcrResult ocrResult)
{
    // The raw OCR text
    string extractedText = ocrResult.Text;

    // Character count – includes spaces and line breaks
    int charCount = extractedText.Length;

    // Processing time in milliseconds (provided by Aspose)
    long processingMs = ocrResult.ProcessingTime;

    // Output to console – easy to pipe to a file or logger
    Console.WriteLine($"🖋️ Extracted {charCount} characters in {processingMs} ms");
    Console.WriteLine("----- Begin OCR Text -----");
    Console.WriteLine(extractedText);
    Console.WriteLine("------ End OCR Text ------");
}
```

**Beklenen çıktı** (2 sayfalık bir tarama örneği):

```
✅ GPU acceleration enabled.
🖋️ Extracted 12,345 characters in 842 ms
----- Begin OCR Text -----
Lorem ipsum dolor sit amet, consectetur...
... (rest of the page) ...
------ End OCR Text ------
```

GPU mevcut değilse bir uyarı görür ve aynı sonucu alırsınız, sadece daha yavaş.

---

## Adım 4: Büyük Dosyalar ve Kenar Durumlarını Yönetme

### Görüntü çok büyük olsaydı ne olur?

Aspose OCR sayfaları akış olarak işleyebilir, ancak yine de yeterli RAM gerekir. Tanıma öncesinde gereksiz DPI’yı düşürmek iyi bir uygulamadır:

```csharp
// Optional pre‑processing: downscale to 300 DPI if original > 600 DPI
if (inputImage.DpiX > 600 || inputImage.DpiY > 600)
{
    inputImage = inputImage.Resize(0.5, 0.5); // 50% reduction
    Console.WriteLine("🔎 Image downscaled for faster OCR.");
}
```

### Eksik GPU sürücüleri?

`InitializeGpu()` etrafındaki `try/catch` çoğu sorunu yakalar, ancak mevcut cihazları sorgulayabilirsiniz:

```csharp
var gpuInfo = GpuDeviceManager.GetDevices();
if (gpuInfo.Count == 0)
{
    Console.WriteLine("⚡ No GPU detected – defaulting to CPU.");
    ocrEngine.UseGpu = false;
}
```

### Desteklenmeyen görüntü formatları?

Aspose TIFF, PNG, JPEG, BMP ve birkaç egzotik formatı destekler. `UnsupportedFormatException` alırsanız, dosyayı önce ImageMagick gibi bir araçla ya da yerleşik `Image.Save` yöntemiyle PNG’ye dönüştürün.

---

## Adım 5: Özet – Tam Çalışan Örnek

Aşağıdaki tüm programı `Program.cs` içine kopyalayıp yapıştırın. Tek dosyalık bir demo olup, yolu değiştirmeniz yeterli (sadece yolu değiştirin).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.ImageProcessing;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust the path to point at your scanned TIFF or JPEG
            RunOcr(@"YOUR_DIRECTORY/large_scanned_page.tif");
        }

        static void RunOcr(string imagePath)
        {
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,
                GpuDeviceId = 0
            };

            try
            {
                ocrEngine.InitializeGpu();
                Console.WriteLine("✅ GPU acceleration enabled.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ GPU init failed ({ex.Message}), switching to CPU.");
                ocrEngine.UseGpu = false;
            }

            var inputImage = Image.Load(imagePath);

            // Optional downscale for gigantic files
            if (inputImage.DpiX > 600 || inputImage.DpiY > 600)
            {
                inputImage = inputImage.Resize(0.5, 0.5);
                Console.WriteLine("🔎 Image downscaled for faster OCR.");
            }

            var ocrResult = ocrEngine.Recognize(inputImage);
            DisplayResult(ocrResult);
        }

        static void DisplayResult(OcrResult ocrResult)
        {
            string extractedText = ocrResult.Text;
            int charCount = extractedText.Length;
            long processingMs = ocrResult.ProcessingTime;

            Console.WriteLine($"🖋️ Extracted {charCount} characters in {processingMs} ms");
            Console.WriteLine("----- Begin OCR Text -----");
            Console.WriteLine(extractedText);
            Console.WriteLine("------ End OCR Text ------");
        }
    }
}
```

`dotnet run` ile çalıştırın ve konsolda **karakter sayısını** ve OCR metnini izleyin. İşte **OCR nasıl kullanılır** döngüsünün baştan sona tamamı.

---

## Sonuç

C#’ta **OCR nasıl kullanılır** konusunu, **görüntülerden metin çıkarma**, **karakter sayısını göster** ve **GPU hızlandırmalı OCR** ile tüm pipeline’ı **c# ocr aspose** kütüphanesi sayesinde nasıl hızlandırabileceğinizi ele aldık. Özetle:

1. Aspose OCR’ı NuGet üzerinden kurun ve doğru namespace’leri referans alın.  
2. GPU’yu açın, ancak her zaman bir CPU geri dönüşü bulundurun.  
3. Görüntünüzü yükleyin, isteğe bağlı olarak DPI’yı düşürün, ardından `Recognize` çağrısını yapın.  
4. `ocrResult.Text` ve `ocrResult.ProcessingTime` değerlerini alarak **karakter sayısını** ve performans metriklerini gösterin.  

Bundan sonra metni bir veritabanına kaydedebilir, bir arama indeksine besleyebilir ya da çıkarılan dize üzerinde dil algılama çalıştırabilirsiniz. PDF işlemek isterseniz, her sayfayı bir görüntü olarak besleyin; aynı kod çalışır.

**İleride keşfedebileceğiniz adımlar:**

- Çok sayfalı PDF’lerden **görüntüden metin çıkarma** için `PdfConverter` kullanmak.  
- Daha iyi doğruluk için OCR ayarlarını (dil paketleri, gürültü azaltma) ince ayarlamak.  
- Çözümü Azure Functions veya AWS Lambda’da GPU‑destekli örneklerle ölçeklendirmek.  

Deneyin, kırın ve geliştirin. Gerçek dünya OCR projeleri böyle inşa edilir. Kodlamanın tadını çıkarın, taramalarınız her daim okunabilir olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}