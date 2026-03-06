---
category: general
date: 2026-03-05
description: Aspose OCR ile C#'ta TIFF'i metne dönüştürün—tarama görüntü dosyalarından
  metni hızlıca çıkarın ve OCR işleme için C#'ta görüntü dosyasını nasıl yükleyeceğinizi
  öğrenin.
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: tr
og_description: Aspose OCR kullanarak C#'de TIFF'i metne dönüştürün. Tarama görüntülerinden
  metin çıkarmak ve görüntü dosyalarını verimli bir şekilde yüklemek için tam iş akışını
  öğrenin.
og_title: TIFF'i C# ile Metne Dönüştür – Tarama Görüntüsü Metnini Çıkar
tags:
- OCR
- C#
- Aspose
title: C# ile TIFF'i Metne Dönüştür – Tarama Görüntüsü Metnini Çıkar
url: /tr/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF'i Metne Dönüştür – C#'ta Tarama Görüntüsü Metnini Çıkarma

C#'ta **TIFF'i metne dönüştürmek** mi istiyorsunuz? Çok sayfalı taranmış görüntülerle, aranabilir metinlere dönüşmeyi reddedenlerle yalnız değilsiniz.  
Bu rehberde, bir TIFF dosyasını alıp Aspose OCR'a besleyen ve düz metin olarak çıktısını veren eksiksiz, çalıştırmaya hazır bir çözümü adım adım göstereceğiz—ekstra hizmetler yok, gizli sihir yok.

> **Pro ipucu:** Yüksek çözünürlüklü taramalarla çalışıyorsanız, GPU işleme etkinleştirmek her sayfada saniyeler kazandırabilir.

Ayrıca **taranmış görüntü dosyalarından metin çıkarma** ve OCR motoruna **C#'ta görüntü dosyası yükleme** en iyi yolunu da göstereceğiz, böylece bu mantığı bugün herhangi bir .NET projesine entegre edebilirsiniz.

---

## Gereksinimler

Başlamadan önce, makinenizde aşağıdakilerin olduğundan emin olun:

| Gereksinim | Sebep |
|-------------|--------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | Modern çalışma zamanı, `Span<T>` ve async I/O'yu destekler |
| Aspose.OCR for .NET (NuGet package `Aspose.OCR`) | Kullanacağımız OCR motoru |
| A valid Aspose OCR license file (`Aspose.OCR.lic`) | Olmadan değerlendirme limitlerine takılırsınız |
| A TIFF file (single‑ or multi‑page) to test | Kullanılan örnek: `scanned_multi_page.tif` |
| GPU with CUDA 11+ (optional) | `EngineMode = Gpu` olduğunda tanıma hızını artırır |

Eğer bunlardan herhangi birine sahip değilseniz, hemen NuGet paketini alın:

```bash
dotnet add package Aspose.OCR
```

## Adım 1: Projeyi Kurun ve Ad Alanlarını İçe Aktarın

Yeni bir konsol uygulaması oluşturun (veya kodu mevcut bir projeye ekleyin). İlk yaptığımız şey, ihtiyacımız olan sınıfları içe aktarmaktır.

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **Neden önemli:** `Aspose.OCR.Image`'i içe aktarmak, diskten veya bir akıştan doğrudan TIFF dosyalarını okuyabilen `ImageStream` fabrikasını sağlar. Bu adımı atlamak derleme zamanı hatasına yol açar.

## Adım 2: OCR Motorunu Başlatın ve İşleme Modunu Seçin

OCR motoru, herhangi bir görüntü atamadan **önce** yapılandırılmalıdır. Burada CPU'da mı yoksa GPU'yu mu kullanacağımıza karar veririz.

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*Eğer grafik kartı olmayan bir headless sunucuda çalışıyorsanız, `Gpu`'yu `Cpu` ya da `Auto` olarak değiştirin.*  
Motor modu, bellek tahsisi ve hız üzerinde etkilidir; GPU modu büyük, yüksek çözünürlüklü TIFF'lerde 2‑3 kat daha hızlı olabilir.

## Adım 3: Aspose OCR Lisansınızı Uygulayın

Lisans olmadan çalışmak, sizi birkaç sayfa ve filigranla sınırlar. Lisansınızı erken yükleyin, böylece sonraki tüm işlemler sınırsız olur.

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **Yaygın tuzak:** `SetLicense`'ı `Recognize()`'den sonra yerleştirmek, motorun o çağrı için deneme moduna geri dönmesine neden olur.

## Adım 4: TIFF Dosyasını Yükleyin – Tek ve Çok Sayfalı Görüntüleri İşleme

Aspose OCR, çok sayfalı TIFF'leri doğrudan okuyabilir, ancak doğru akışı beslemeniz gerekir. İşte her iki senaryo için de çalışan sağlam bir desen.

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### Neden `ImageStream.FromFile` Kullanılır?

- Temel `FileStream`'i soyutlayarak TIFF sayfa numaralandırmasını dahili olarak yönetir.  
- `MemoryStream` ile de çalışır, böylece dosya sistemine dokunmadan bir veritabanı veya web API'sinden görüntüleri yükleyebilirsiniz.

### Kenar Durumu: Çok Büyük TIFF'ler

TIFF dosyanız 200 MB'yi aşıyorsa, bellek dışı istisnalardan kaçınmak için sayfa sayfa yüklemeyi düşünün:

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

## Adım 5: Çıktıyı Doğrulayın

Programı çalıştırdığınızda aşağıdakine benzer bir şey görmelisiniz:

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

Metin bozuk görünüyorsa, şu noktaları kontrol edin:

1. **Çözünürlük** – OCR, 300 dpi veya daha yüksek çözünürlükte en iyi çalışır.  
2. **EngineMode** – GPU sürücüsü eskiyse `Cpu`'ya geçin.  
3. **Lisans** – Lisans dosyası yolunun doğru ve dosyanın okunabilir olduğundan emin olun.

## Sıkça Sorulan Sorular (SSS)

### Bu diğer görüntü formatlarıyla çalışır mı?

Kesinlikle. `ImageStream.FromFile` JPEG, PNG, BMP ve hatta PDF'yi (Aspose.PDF aracılığıyla) destekler. Sadece dosya uzantısını değiştirin.

### Görüntüler bir veritabanında depolanıyorsa ne yapmalıyım?

BLOB'u bir `MemoryStream`'e okuyun ve `ImageStream.FromStream(memoryStream)`'e geçirin. OCR motoru bunu dosya tabanlı bir akış gibi işler.

### Bunu Linux'ta çalıştırabilir miyim?

Evet—Aspose OCR çapraz platformdur. Uygun .NET çalışma zamanını kurun ve GPU (kullanılıyorsa) için gerekli yerel kütüphanelerin mevcut olduğundan emin olun.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, derlemeye hazır tam program yer alıyor. `YOUR_DIRECTORY` ve lisans dosyası yolunu gerçek konumlarınızla değiştirin.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

`Program.cs` olarak kaydedin, `dotnet run` komutunu çalıştırın ve metni izleyin

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}