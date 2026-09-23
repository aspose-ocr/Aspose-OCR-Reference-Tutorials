---
category: general
date: 2025-12-30
description: Aspose OCR'de toplu OCR işleme ve OCR metin çıkarımı için GPU'yu nasıl
  etkinleştireceğinizi öğrenin. GPU cihazını ayarlamayı ve Aspose'u verimli bir şekilde
  nasıl kullanacağınızı keşfedin.
draft: false
keywords:
- how to enable gpu
- batch ocr processing
- ocr text extraction
- set gpu device
- how to use aspose
language: tr
og_description: Aspose OCR'de GPU'yu nasıl etkinleştirirsiniz. Bu kılavuzu izleyerek
  toplu OCR işleme, OCR metin çıkarma, GPU cihazını ayarlama ve Aspose'u nasıl kullanacağınızı
  öğrenin.
og_title: Aspose OCR için GPU'yu Nasıl Etkinleştirirsiniz – Tam Kılavuz
tags:
- Aspose
- OCR
- GPU
- C#
title: Aspose OCR için GPU'yu Nasıl Etkinleştirirsiniz – Adım Adım Kılavuz
url: /tr/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR için GPU'yu Etkinleştirme – Tam Kılavuz

Aspose OCR kullanırken **GPU'yu nasıl etkinleştirirsiniz** diye hiç merak ettiniz mi? Tek başınıza değilsiniz—devasa belge hacimleriyle uğraşan geliştiriciler, OCR motoru CPU’da takılı kaldığı için performans sınırlarıyla karşılaşıyor. İyi haber? GPU hızlandırmasını açmak oldukça basit ve her sayfada saniyeler kazanmanızı sağlıyor. Bu rehberde **GPU'yu nasıl etkinleştirirsiniz**, **toplu OCR işleme**yi nasıl çalıştırırsınız, tanınan metni nasıl çıkarırsınız ve doğru GPU cihazını nasıl seçersiniz adım adım göstereceğiz. Sonunda **Aspose**'u ışık hızıyla OCR metin çıkarımı için nasıl kullanacağınızı bileceksiniz.

## Bu Kılavuzda Neler Ele Alınıyor

Önce Aspose OCR kütüphanesini kuracağız, ardından GPU desteğini etkinleştireceğiz ve son olarak bir dizi TIFF görüntüsünü motor üzerinden çalıştıracağız. Yol boyunca **GPU cihazını** manuel olarak ayarlamanın neden gerekli olabileceğini, dikkat edilmesi gereken tuzakları ve metin çıkarımının gerçekten çalıştığını nasıl doğrulayacağınızı açıklayacağız. Harici dokümanlara ihtiyaç yok; bugün çalıştırabileceğiniz eksiksiz, kopyala‑yapıştır çözümü.

> **Önkoşullar**  
> - .NET 6.0 veya üzeri (kod modern C# sözdizimini kullanıyor)  
> - Aspose.OCR for .NET NuGet paketi (sürüm 23.10 veya daha yeni)  
> - Uygun sürücü yüklü CUDA‑uyumlu bir GPU  
> - Toplu çalıştırma için birkaç örnek `.tif` dosyasının bulunduğu bir klasör  

Bu temel gereksinimleri karşıladıysanız, başlayalım.

## Aspose OCR'de GPU'yu Nasıl Etkinleştirirsiniz

İlk yapmanız gereken, `OcrEngine`'e GPU'yu kullanmasını söylemek. Bu, iki basit özellik aracılığıyla yapılır: `UseGpu` ve isteğe bağlı olarak `GpuDeviceId`. `UseGpu`'yu `true` olarak ayarlamak motoru GPU moduna geçirir, `GpuDeviceId` ise birden fazla GPU'nuz varsa hangi GPU'nun işi üstleneceğini seçmenizi sağlar.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;
using System.Collections.Generic;

// Step 1: Create the OCR engine and enable GPU acceleration
var ocrEngine = new OcrEngine
{
    // Turn on GPU support – this is the core of “how to enable gpu”
    UseGpu = true,

    // (optional) Choose GPU index 0; change if you have multiple devices
    GpuDeviceId = 0
};
```

> **Neden önemli?** – CPU sürümü her pikseli sırayla işler ve yüksek çözünürlüklü görüntülerde darboğaz oluşturur. GPU sürümü binlerce iş parçacığını paralel çalıştırarak sayfa başına geçen süreyi dramatik şekilde azaltır.

### Görsel Genel Bakış  

![GPU'yu nasıl etkinleştirirseniz OCR motorunun işi GPU'ya nasıl devredildiğini gösteren diyagram](/images/enable-gpu-diagram.png){: .center .responsive alt="gpu nasıl etkinleştirilir"}

*(Görseli göremiyorsanız, OCR motorunun görüntü tamponunu CUDA çekirdeğine verdiği bir akış şeması hayal edin.)*

## Aspose ile Toplu OCR İşleme

Motor GPU'ya hazır olduğuna göre, ona bir dosya listesi verelim. Toplu işleme, `List<string>` içinde bulunan görüntü yolları üzerinde döngü yapmak kadar basittir. GPU kullandığımız için motor her görüntüyü otomatik olarak cihaza kuyruğa alır ve pipeline'ı meşgul tutar.

```csharp
// Step 2: Define the image files you want to process
var imageFiles = new List<string>
{
    @"C:\OCRSamples\page1.tif",
    @"C:\OCRSamples\page2.tif",
    @"C:\OCRSamples\page3.tif"
};

// Step 3: Process each image and report the character count
foreach (var imagePath in imageFiles)
{
    // Recognize the image – the GPU does the heavy lifting behind the scenes
    var ocrResult = ocrEngine.Recognize(imagePath);

    // Show how many characters were extracted – a quick sanity check
    Console.WriteLine($"{imagePath}: {ocrResult.Text.Length} characters");
}
```

> **Pro ipucu** – Gerçekten büyük toplular için `Parallel.ForEach` ile birlikte `ocrEngine.Clone()` kullanmayı düşünün; bu, thread‑safety sorunlarını önler. `Clone` yöntemi, aynı GPU bağlamına işaret eden sığ bir kopya oluşturur.

### Beklenen Çıktı

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

Sayısal değerler makul görünüyorsa, **toplu OCR işleme** çalışıyor ve GPU kullanılmaktadır.

## OCR Metin Çıkarma – Sonuçları Almak

`Recognize` yöntemi, ham metin, güven puanları ve gerekirse sınırlayıcı kutular içeren bir `OcrResult` nesnesi döndürür. Düz metni alıp bir dosyaya yazalım, böylece çıkarımı doğrulayabilirsiniz.

```csharp
foreach (var imagePath in imageFiles)
{
    var ocrResult = ocrEngine.Recognize(imagePath);
    var extractedText = ocrResult.Text;

    // Save the text to a .txt file with the same base name
    var outputPath = System.IO.Path.ChangeExtension(imagePath, ".txt");
    System.IO.File.WriteAllText(outputPath, extractedText);

    Console.WriteLine($"Extracted text saved to {outputPath}");
}
```

> **Neden bir dosyaya çıkarılıyor?** – OCR metnini saklamak, sonraki işlemler (arama indeksleme, veri madenciliği vb.) için motoru yeniden çalıştırmadan kullanılmasını sağlar. Ayrıca hata ayıklama için kalıcı bir kayıt sunar.

## Optimum Performans İçin GPU Cihazını Ayarlama

İş istasyonunuzda birden fazla GPU varsa—örneğin, bir ML için ayrılmış RTX ve bir bütünleşik grafik kartı—doğru olanı kullandığınızdan emin olmalısınız. `GpuDeviceId` özelliği, `CudaDeviceInfo.GetDevices()` tarafından rapor edilen cihaz indeksine karşılık gelen bir tamsayı alır.

```csharp
using Aspose.OCR.Gpu;

// List all available GPU devices
var devices = CudaDeviceInfo.GetDevices();
for (int i = 0; i < devices.Length; i++)
{
    Console.WriteLine($"Device {i}: {devices[i].Name} (Compute Capability {devices[i].ComputeCapability})");
}

// Suppose you want to use the second GPU (index 1)
ocrEngine.GpuDeviceId = 1;
Console.WriteLine($"Switched to GPU device {ocrEngine.GpuDeviceId}");
```

> **Köşe durumu** – Bazı eski GPU'lar gerekli CUDA sürümünü desteklemez. Bu durumda `UseGpu = true` sessizce CPU'ya geri döner, bu yüzden her zaman `ocrEngine.IsGpuEnabled` ile başlatma sonrası kontrol edin.

## Gerçek Dünya Projesinde Aspose OCR Nasıl Kullanılır

Her şeyi bir araya getiren, **GPU'yu nasıl etkinleştirirsiniz**, **toplu OCR işleme**yi çalıştırır, metni çıkarır ve GPU cihazını seçmenizi sağlayan kompakt, çalıştırmaya hazır bir konsol uygulaması aşağıdadır.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine with GPU support
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,
            GpuDeviceId = 0 // change if you have multiple GPUs
        };

        // -------------------------------------------------
        // 2️⃣ (Optional) Show available GPU devices
        // -------------------------------------------------
        var devices = CudaDeviceInfo.GetDevices();
        Console.WriteLine("Available GPU devices:");
        for (int i = 0; i < devices.Length; i++)
        {
            Console.WriteLine($"  [{i}] {devices[i].Name} – Compute {devices[i].ComputeCapability}");
        }

        // -------------------------------------------------
        // 3️⃣ Define the batch of images to process
        // -------------------------------------------------
        var imageFiles = new List<string>
        {
            @"C:\OCRSamples\page1.tif",
            @"C:\OCRSamples\page2.tif",
            @"C:\OCRSamples\page3.tif"
        };

        // -------------------------------------------------
        // 4️⃣ Process each image, extract text, and save it
        // -------------------------------------------------
        foreach (var imagePath in imageFiles)
        {
            var result = ocrEngine.Recognize(imagePath);
            var text = result.Text;

            var txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, text);

            Console.WriteLine($"{Path.GetFileName(imagePath)} → {Path.GetFileName(txtPath)} ({text.Length} chars)");
        }

        Console.WriteLine("All done! GPU‑accelerated OCR batch completed.");
    }
}
```

### Örneği Çalıştırma

1. NuGet paketini kurun: `dotnet add package Aspose.OCR --version 23.10.0`  
2. `imageFiles` içindeki yolları kendi `.tif` dosyalarınızın konumuyla değiştirin.  
3. Derleyin ve çalıştırın: `dotnet run`.  

GPU listesi, ardından her görüntü için karakter sayısı ve oluşturulan `.txt` dosyasının yolu satır satır görüntülenecektir.

## Yaygın Sorular & Dikkat Edilmesi Gerekenler

- **Bu sadece CPU‑only bir makinede çalışır mı?**  
  Evet—`UseGpu` `true` olarak ayarlanmış ama uyumlu bir GPU bulunamazsa Aspose otomatik olarak CPU'ya geçer. Modu `ocrEngine.IsGpuEnabled` ile doğrulayabilirsiniz.

- **“CUDA driver version is insufficient” hatası alırsam ne yapmalıyım?**  
  NVIDIA sürücünüzü, Aspose ile gelen CUDA araç setiyle uyumlu en son sürüme güncelleyin. Kütüphane, son GPU özellikleri için en az CUDA 11.0 gerektirir.

- **PDF'leri doğrudan işleyebilir miyim?**  
  Aspose OCR raster görüntüler üzerinde çalışır. PDF sayfalarını önce görüntülere (ör. Aspose.PDF kullanarak) dönüştürün, ardından OCR motoruna besleyin.

- **Gürültülü taramalarda doğruluğu nasıl artırırım?**  
  `ocrEngine.Preprocess = true` gibi ön işleme seçeneklerini etkinleştirin veya daha yüksek çözünürlüklü (300 dpi ve üzeri) görüntüler kullanın. GPU hızlandırması hâlâ geçerlidir.

## Sonuç

**GPU'yu nasıl etkinleştirirsiniz**, **toplu OCR işleme**, **OCR metin çıkarımı** ve **GPU cihazını ayarlama** konularını ele aldık. Tam kod örneğini izleyerek artık herhangi bir .NET projesine hızlı, GPU‑destekli OCR entegrasyonu yapabilir ve “Aspose nasıl kullanılır” sorusuna güvenle yanıt verebilirsiniz.

Bir sonraki adıma hazır mısınız? Dil algılama ekleyin, çıkarılan metni bir arama indeksine besleyin veya devasa belge arşivleri için çoklu GPU ölçeklendirmesi deneyin. Aspose'un sağlam API'si ile modern GPU'ların ham gücünü birleştirdiğinizde sınır yoktur.

İyi kodlamalar, OCR işleriniz GPU'nuzun hızı kadar çabuk yürüsün!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}