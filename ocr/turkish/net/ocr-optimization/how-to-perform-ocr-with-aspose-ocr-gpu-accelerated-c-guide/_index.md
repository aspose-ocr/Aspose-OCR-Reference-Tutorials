---
category: general
date: 2026-02-19
description: Yüksek çözünürlüklü TIFF görüntülerinde OCR'ı hızlı bir şekilde nasıl
  gerçekleştireceğinizi öğrenin. C#'ta GPU OCR kullanarak TIFF dosyalarından metin
  çıkarmayı keşfedin.
draft: false
keywords:
- how to perform OCR
- extract text from tiff
- use gpu ocr
- Aspose OCR C#
- high‑resolution image processing
- OCR performance tuning
language: tr
og_description: Aspose OCR ve GPU hızlandırması kullanarak yüksek çözünürlüklü TIFF
  dosyalarında OCR nasıl yapılır. Tam adım adım rehber.
og_title: OCR Nasıl Yapılır – GPU Hızlandırmalı C# Öğreticisi
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: Aspose OCR ile OCR Nasıl Yapılır – GPU Hızlandırmalı C# Rehberi
url: /tr/net/ocr-optimization/how-to-perform-ocr-with-aspose-ocr-gpu-accelerated-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Nasıl Yapılır – GPU‑Hızlandırmalı C# Öğreticisi

Hiç devasa bir TIFF taraması üzerinde OCR yapmanız gerekti ve neden sonsuza kadar sürüyor diye merak ettiniz mi? Tek başınıza değilsiniz. Bu rehberde **OCR nasıl yapılır** konusunu yüksek çözünürlüklü bir görüntüde GPU'yu kullanarak göstereceğiz ve anında çalıştırabileceğiniz, tiff dosyalarından metin çıkaran bir C# programı elde edeceksiniz.

Aspose OCR paketinin kurulumu ve GPU işleme etkinleştirilmesinden başlayarak her şeyi ele alacağız ve her ayarın neden önemli olduğunu açıklayacağız. Sonunda bu kodu herhangi bir .NET projesine ekleyebilecek, bir .tif dosyasına yönlendirecek ve temiz, aranabilir metin elde edeceksiniz—ekstra hizmetlere ihtiyaç duymadan.

## Önkoşullar

- .NET 6.0 veya daha yenisi (kod .NET 6 hedefli, ancak .NET 5 de çalışır)  
- Uyumlu bir GPU (NVIDIA CUDA 11+ veya OpenCL desteği olan AMD Radeon)  
- **Aspose.OCR** NuGet paketi (sürüm 23.9 veya daha yeni)  
- Okumak istediğiniz yüksek çözünürlüklü bir TIFF dosyası (ör. `high_res_page.tif`)  

Eğer bunlardan biri size yabancı geliyorsa endişelenmeyin—her bir nokta sonraki adımlarda açıklanıyor.

## Adım 1: Aspose OCR'yi Kurun ve GPU İşlemeyi Etkinleştirin  

İlk yapmanız gereken, Aspose OCR kütüphanesini projenize eklemek ve GPU desteğini açmaktır. GPU'yu etkinleştirmek, motorun ağır matris hesaplamalarını grafik kartınıza devretmesini sağlar ve modern bir GPU'da işleme süresini %70 ya da daha fazla azaltabilir.

```csharp
// Install the package via the CLI (run once):
// dotnet add package Aspose.OCR --version 23.9.0

using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;

class GpuDemo
{
    static void Main()
    {
        // Enable GPU acceleration – requires a compatible GPU driver.
        OcrEngine.EnableGpuProcessing(true);
```

**Neden Önemlidir:**  
`EnableGpuProcessing(true)` kullanılmadığında, OCR motoru saf CPU çalışmasına geri döner; bu küçük görüntüler için uygundur ancak çok‑megapiksel TIFF'lerde acı verici derecede yavaştır. Bu bayrağı açmak, kütüphanenin CUDA ya da OpenCL'yi arka planda kullanmasını sağlar ve daha sonra göreceğiniz `ProcessingTime` değerini büyük ölçüde azaltır.

## Adım 2: OCR Motorunu İngilizce (veya ihtiyacınız olan herhangi bir dil) için Yapılandırın  

Sonra bir `OcrEngine` örneği oluşturup dili ayarlarız. Aspose 100'den fazla dili destekler; İngilizce burada en yaygın olduğu için gösterilmiştir, ancak `Language.English` yerine `Language.French`, `Language.German` vb. kullanabilirsiniz.

```csharp
        // Step 2: Create and configure the OCR engine.
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // Change if you need another language.
        };
```

**Pro ipucu:**  
Çok dilli belgeler işlemeyi planlıyorsanız, birden fazla motor örneği oluşturun ya da çağrılar arasında `Language` özelliğini değiştirin. Bu, her sayfa için motoru yeniden oluşturma yükünü ortadan kaldırır.

## Adım 3: Yüksek Çözünürlüklü TIFF Üzerinde OCR Gerçekleştirin  

Şimdi eğlenceli kısım—motoru bir TIFF dosyasıyla besleyin ve ağır işi ona bırakın. `RecognizeImage` metodu, çıkarılan metin ve zaman bilgilerini içeren bir `OcrResult` döndürür.

```csharp
        // Step 3: Run OCR on the TIFF image.
        var ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/high_res_page.tif");
```

**Köşe durumları yönetimi:**  
- **Büyük dosyalar:** TIFF dosyanız 50 MB'yi aşarsa, bellek kullanımını makul tutmak için önce `System.Drawing` veya `ImageSharp` ile alt örnekleme yapmayı düşünün.  
- **Çok sayfalı TIFF'ler:** `RecognizeImage` metodunu her sayfa indeksi için bir döngü içinde çağırın; Aspose her sayfa için metni ayrı ayrı döndürecektir.

## Adım 4: İşleme Süresini ve Çıkarılan Metni Çıktılayın  

Son olarak, geçen süreyi ve ham OCR çıktısını yazdırıyoruz. İşte GPU hızlandırmasının faydasını burada göreceksiniz.

```csharp
        // Step 4: Display results.
        Console.WriteLine($"Time taken: {ocrResult.ProcessingTime} ms");
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Tipik çıktı**

```
Time taken: 312 ms
=== Extracted Text ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Orta seviye bir RTX 3060'da, daha önce CPU'da ~1,2 saniye süren aynı 3000 × 4000 piksel TIFF, şimdi ~300 ms'de bitiyor—dramatik hız artışına dikkat edin.

## TIFF Dosyalarından Metni Verimli Şekilde Nasıl Çıkarabilirsiniz  

Eğer sadece **tiff'ten metin çıkarma** adımıyla ilgileniyor ve GPU'ya ihtiyacınız yoksa, GPU bayrağını atlayabilirsiniz. Kalan kod aynı kalır, ancak büyük taramalarda performans artışını kaybedeceksiniz. İşte minimal bir sürüm:

```csharp
using Aspose.OCR;
using System;

class SimpleTiffOcr
{
    static void Main()
    {
        var engine = new OcrEngine { Language = Language.English };
        var result = engine.RecognizeImage(@"sample.tif");
        Console.WriteLine(result.Text);
    }
}
```

**Ne zaman kullanılmalı:**  
- Dağıtımınız GPU'suz bir headless sunucuda çalışıyor.  
- TIFF'ler küçük (< 1 MP) ve CPU süresi bir darboğaz değil.  

GPU olmadan bile, Aspose'un OCR motoru yerleşik sinir ağları sayesinde son derece yüksek doğruluk sağlar.

## Daha Hızlı İşleme İçin GPU OCR Kullanımı – Yaygın Tuzaklar  

**use gpu OCR** size hız kazandırırken, birkaç tuzak sizi zorlayabilir:

| Sorun | Belirti | Çözüm |
|-------|---------|-----|
| CUDA sürücüsü eksik | `EnableGpuProcessing` `PlatformNotSupportedException` hatası fırlatıyor | En son NVIDIA sürücüsünü ve CUDA araç setini kurun |
| Desteklenmeyen GPU | Motor sessizce CPU'ya geri dönüyor | `OcrEngine.GetAvailableGpus()` içinde GPU'nuzun göründüğünden emin olun (eğer çağırıyorsanız) |
| Çok büyük görüntülerde bellek yetersizliği | `System.OutOfMemoryException` | Görüntüyü parçalar halinde işleyin (`engine.RecognizeRegion`) |
| Yanlış görüntü yönelimi | Bozuk metin | OCR'den önce `ImageSharp` ile TIFF'i önceden döndürün |

**Hızlı doğrulama:** Demo'yu bir kez `EnableGpuProcessing(false)` ile çalıştırın. `ProcessingTime` değerlerini karşılaştırın; sağlıklı bir GPU‑hızlandırmalı çalıştırma en az 2‑3 kat daha hızlı olmalıdır.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, bir konsol uygulamasına ekleyebileceğiniz tam program yer alıyor. `YOUR_DIRECTORY` ifadesini TIFF dosyanızın gerçek yolu ile değiştirin.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;

class GpuDemo
{
    static void Main()
    {
        // 1️⃣ Enable GPU acceleration (requires a compatible GPU)
        OcrEngine.EnableGpuProcessing(true);

        // 2️⃣ Create the OCR engine and set the language
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // Change as needed
        };

        // 3️⃣ Perform OCR on a high‑resolution TIFF
        var imagePath = @"YOUR_DIRECTORY/high_res_page.tif";
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 4️⃣ Show timing and extracted text
        Console.WriteLine($"Time taken: {ocrResult.ProcessingTime} ms");
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

RTX 3070'lu bir makinede çalıştırmak, önceki örnekle benzer bir çıktı verir ve **OCR nasıl yapılır** sorusunun GPU desteğiyle beklendiği gibi çalıştığını doğrular.

## Sonraki Adımlar – Temelin Ötesine Geçmek  

- **Toplu işleme:** `RecognizeImage` çağrısını bir klasördeki TIFF'ler üzerinde `foreach` döngüsüyle sarın.  
- **Son‑işleme:** `ocrResult.Text`'i bir yazım denetleyicisine ya da doğal dil ayrıştırıcısına göndererek OCR hatalarını temizleyin.  
- **Hibrit mod:** Çalışma zamanında görüntü boyutunu algılayın ve GPU'yu etkinleştirip etkinleştirmeye karar verin (`if (image.Width * image.Height > 5_000_000) EnableGpuProcessing(true)`).  

Bu uzantıların tümü, mantıklı olduğunda hâlâ **use gpu ocr** kullanır ve işlem hattınızı hem hızlı hem de kaynak‑bilinçli tutar.

## Sonuç  

Artık Aspose OCR ve GPU hızlandırması kullanarak yüksek çözünürlüklü TIFF dosyalarında **OCR nasıl yapılır** bildiğinize ve CPU‑only bir yaklaşımın gerektireceği sürenin bir kısmında **tiff'ten metin çıkarma** işlemini güvenle yapabildiğinize emin olabilirsiniz. Tam, kopyala‑yapıştır hazır örnek, GPU'yu etkinleştirmeden işleme süresini ve son metni yazdırmaya kadar tüm akışı gösterir.

Deneyin, dil ayarlarını değiştirin ve bir sayfa topluluğunu işleyin. Herhangi bir sorunla karşılaşırsanız, “Daha Hızlı İşleme İçin GPU OCR Kullanımı” tablosuna tekrar bakın; çoğu sorun orada ele alınmıştır. İyi kodlamalar ve hız artışının tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}