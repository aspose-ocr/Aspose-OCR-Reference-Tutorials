---
category: general
date: 2026-05-31
description: Aspose OCR ile C#’ta görüntüden metin tanımayı, tiff dosyalarından metin
  çıkarmayı ve OCR için görüntüyü verimli bir şekilde yüklemeyi öğrenin.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: tr
og_description: Aspose OCR ile görüntüden metin tanıma konusunda adım adım rehber;
  tiff dosyasından çıkarma ve OCR için doğru görüntü yüklemeyi kapsar.
og_title: C#'de Aspose OCR kullanarak görüntüden metin tanıma
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: C#'ta Aspose OCR ile görüntüden metin tanıma
url: /tr/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Aspose OCR Kullanarak Görüntüden Metin Tanıma

Görselden metin tanıma** (recognize text from image)** ihtiyacınız oldu mu ama C#'ta nereden başlayacağınızı bilemediniz? Yalnız değilsiniz—birçok geliştirici taranmış belgeler veya çok sayfalı TIFF'lerle çalışırken bu engelle karşılaşıyor. Bu rehberde, Aspose OCR kütüphanesini kullanarak **recognize text from image** yapan eksiksiz, hemen çalıştırılabilir bir örnek üzerinden sizi adım adım yönlendireceğiz ve ayrıca **extract text from tiff** ve **load image for OCR** işlemlerinin en iyi yolunu göstereceğiz, böylece saçınızı yıpratmadan.

NuGet paketinin kurulumundan GPU hızlandırmasını yönetmeye ve gerektiğinde CPU'ya geri dönmeye kadar her şeyi ele alacağız. Bu öğreticinin sonunda, tanınan metni ve işleme süresini konsola yazdıran bir konsol uygulamanız olacak—eksik parça yok, belirsiz referans yok.

## Oluşturacağınız Şey

- Çok sayfalı TIFF dahil olmak üzere bir görüntüyü yükleyen basit bir .NET konsol uygulaması  
- GPU kullanımı için yapılandırılmış bir OCR motoru, sorunsuz CPU geri dönüşü ile  
- Görüntüden düz metin çıkarma, konsola yazdırma  
- GPU vs. CPU performans etkisini görebilmeniz için zamanlama bilgileri  

**Önkoşullar**

- .NET 6 SDK veya daha yeni bir sürüm (kod .NET Core ve .NET Framework ile çalışır)  
- C# ve komut satırı konusunda temel bilgi  
- Aspose.OCR NuGet paketini indirmek için internet erişimi  

Bu koşullara sahipseniz, başlayalım.

![C# code to recognize text from image using Aspose OCR](image.png "C# code to recognize text from image using Aspose OCR")

## 1. Adım – Görüntüden Metin Tanıma: OCR Motorunu Kurma

İlk olarak bir `OcrEngine` örneğine ihtiyacımız var. Aspose OCR, işleme cihazını seçmenize izin verir—hız için GPU, güvenlik ağı olarak CPU. Motor ayrıca bir bellek‑sınırı ipucu kabul eder; bu, paylaşımlı makinelerde kullanışlı olabilir.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**Neden Önemlidir:**  
`OcrDevice.Gpu` seçmek, özellikle çok sayfalı TIFF'lerde büyük görüntüler için tanıma süresinden saniyeler kazandırabilir. `GpuMemoryLimit` ise uygulamanızın paylaşımlı bir iş istasyonunda tüm GPU belleğini tüketmesini önler.

## 2. Adım – OCR için Görüntü Yükleme (TIFF Desteği Dahil)

Şimdi motoru bir görüntüyle besliyoruz. Aspose’un `ImageStream.FromFile` metodu, kütüphanenin desteklediği **any** formatı kabul eder—TIFF, PNG, JPEG, istediğiniz gibi. Bu adım doğrudan **load image for OCR** gereksinimini karşılar.

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**İpucu:** Çok sayfalı bir TIFF ile çalışıyorsanız, Aspose otomatik olarak her sayfayı ayrı bir çerçeve olarak ele alır ve motor bunları sırasıyla işler. Ek bir kod gerekmez.

## 3. Adım – Tanıma İşlemini Çalıştır ve **extract text from tiff**

Motor hazır ve görüntü yüklendiğinde OCR işlemini başlatıyoruz. `Recognize` metodu, düz metin, güven skorları ve zamanlama detaylarını içeren bir `OcrResult` döndürür.

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**Köşe Durumu İşleme:**  
GPU mevcut değilse, `engine.Recognize()` hâlâ çalışır çünkü motor sessizce CPU'ya geçiş yapar. Hangi cihazın gerçekten kullanıldığını kaydetmek isterseniz, tanıma sonrası `engine.Device` değerini kontrol edebilirsiniz.

## 4. Adım – Tanınan Düz Metni Al

Metni çıkarmak oldukça basittir—sadece `Text` özelliğini okuyun. İşte **extract text from tiff** (veya başka bir görüntü) işlemini tamamladığımız ve kullanıcıya sunduğumuz yer.

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

Ham karakterleri, kaynak görüntüdeki satır sonları korunmuş şekilde göreceksiniz. Daha yapılandırılmış bir çıktı (JSON veya CSV gibi) isterseniz `result.Regions` ve `result.Lines` alanlarına bakabilirsiniz, ancak hızlı betikler için düz metin genellikle yeterlidir.

## 5. Adım – İşleme Süresini Ölç ve GPU Geri Dönüşünü Yönet

Performans önemlidir, özellikle onlarca sayfa işliyorsanız. `ProcessingTime` özelliği, OCR'un GPU ya da CPU üzerinde çalışıp çalışmadığına bakılmaksızın ne kadar sürdüğünü tam olarak gösterir.

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Neden Önemli:**  
Süreyi uzayan görürseniz, `GpuMemoryLimit` değerini ayarlamayı ya da açıkça CPU'ya geçmeyi (`Device = OcrDevice.Cpu`) düşünebilirsiniz. Öte yandan, büyük bir TIFF üzerinde bir saniyeden kısa bir sonuç alıyorsanız GPU hızlandırmanız görevini başarıyla yerine getiriyor demektir.

## Tam, Hemen Çalıştırılabilir Örnek

Aşağıdaki kodu yeni bir konsol projesine (`dotnet new console -n OcrDemo`) kopyalayın ve `dotnet add package Aspose.OCR` komutunu çalıştırın. Ardından `YOUR_DIRECTORY/sample_multi_page.tif` yolunu kendi görüntünüzün yolu ile değiştirin.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Beklenen çıktı (kısaltılmış):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

Makinenizde yeterli bir GPU yoksa, geçen süre birkaç saniye daha uzun olabilir, ancak metin hâlâ doğru bir şekilde çıkarılacaktır.

## Yaygın Sorular & Dikkat Edilmesi Gerekenler

- **Görüntü çok büyük (10 MB üzeri) olduğunda ne yapılmalı?**  
  Motoru beslemeden önce çözünürlüğünü düşürün veya yeterli VRAM varsa `GpuMemoryLimit` değerini artırın.  
- **Bir döngü içinde birden fazla görüntüyü işleyebilir miyim?**  
  Kesinlikle. Aynı `OcrEngine` örneğini yeniden kullanın ve her yinelemede yeni bir `ImageStream` atayın.  
- **Herhangi bir şeyi dispose etmem gerekiyor mu?**  
  `OcrEngine` `IDisposable` uygular. Özellikle GPU kaynaklarıyla çalışırken temiz kaynak yönetimi için bir `using` bloğu içinde tutun.  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **İngilizce dışındaki dillerle çalışabilir miyim?**  
  `engine.Language = OcrLanguage.Spanish` (veya desteklenen herhangi bir dil) ayarını `Recognize()` çağrısından önce yapın.  

## Sonuç

Artık Aspose OCR kullanarak C#'ta **recognize text from image** yapan eksiksiz, uçtan uca bir çözümünüz var. Eğitimde **load image for OCR**, **extract text from tiff** nasıl yapılır ve performans ölçümüyle GPU geri dönüşünün sorunsuz yönetimi ele alındı.

Bundan sonra şunları deneyebilirsiniz:

- Farklı görüntü formatları (BMP, PDF) ile deneyerek Aspose'un nasıl davrandığını görün.  
- Düzen‑duyarlı bir çıktı gerekiyorsa `result.Regions` üzerinden sınırlayıcı‑kutu verilerine dalın.  

## Sonraki Öğrenmeniz Gerekenler

- [Aspose ile Akıştan Görüntü Tanıma Nasıl Kullanılır (OCR Görüntü Tanıma)](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Görüntüden Metin Çıkarma – .NET için Aspose.OCR ile OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)
- [Görüntüden Metin Çıkarma – Aspose.OCR ile Satır Tanıma](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}