---
category: general
date: 2026-04-06
description: Aspose OCR GPU kullanarak C#'ta görüntüden metin çıkarın. Bu adım adım
  rehberde dosyadan görüntü yüklemeyi ve GPU bellek sınırını ayarlamayı öğrenin.
draft: false
keywords:
- extract text from image
- load image from file
- set gpu memory limit
- aspose ocr example
- aspose ocr gpu
language: tr
og_description: C#'ta Aspose OCR GPU kullanarak görüntüden metin çıkarın. Bu adım
  adım rehberde dosyadan görüntü yüklemeyi ve GPU bellek sınırını ayarlamayı öğrenin.
og_title: Aspose OCR GPU ile Görüntüden Metin Çıkarma – Tam C# Rehberi
tags:
- Aspose OCR
- C#
- GPU
- OCR
title: Aspose OCR GPU ile Görüntüden Metin Çıkarma – Tam C# Rehberi
url: /tr/net/ocr-configuration/extract-text-from-image-with-aspose-ocr-gpu-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU ile Görüntüden Metin Çıkarma – Tam C# Kılavuzu

Hiç **görüntüden metin çıkarma** ihtiyacı duydunuz mu ama performansın kritik olduğu noktada takıldınız mı? Yalnız değilsiniz—birçok geliştirici OCR bir darboğaz haline geldiğinde aynı duvara çarpar. Bu öğreticide, Aspose OCR'ın GPU çalışma zamanını kullanarak görüntüden metin nasıl çıkarılır, dosyadan nasıl yüklenir ve daha sıkı kaynak kontrolü için GPU bellek sınırı nasıl ayarlanır, adım adım göstereceğiz.

Tam çalışır bir C# örneği üzerinden ilerleyecek, her satırın neden önemli olduğunu açıklayacak ve karşılaşabileceğiniz yaygın tuzakları işaretleyeceğiz. Sonunda, GPU üzerinde çalışan hızlı ve ölçeklenebilir OCR boru hatları oluşturmak için sağlam bir temele sahip olacaksınız.

## Bu Kılavuzda Neler Ele Alınıyor

- **Önkoşullar**: .NET 6+ (veya .NET Framework 4.6+), Aspose.OCR NuGet paketi, uyumlu bir GPU sürücüsü.
- **Adım‑adım kod**: dosyadan bir görüntü yükler, Aspose OCR GPU motorunu yapılandırır ve metni çıkarır.
- **Neden** GPU bellek sınırı belirlemek isteyebileceğinizi ve bunu güvenli bir şekilde nasıl yapacağınızı.
- **Köşe‑durum yönetimi**: düşük çözünürlüklü görüntüler, eksik GPU ve güven skorlarını sorun giderme.
- **Sonraki adımlar**: toplu işleme, ASP.NET Core entegrasyonu ve gerekirse CPU’ya geri dönme.

> **Pro ipucu:** GPU’nuzun kullanılıp kullanılmadığından emin değilseniz, OCR çalışırken GPU aktivite izleyicisini (ör. NVIDIA‑SMI) kontrol edin. Ayarladığınız sınıra uyan bir bellek kullanım artışı göreceksiniz.

---

![Aspose OCR GPU motoru kullanarak görüntüden metin çıkarma akışını gösteren diyagram](extract-text-from-image-aspose-ocr-gpu.png "Aspose OCR GPU kullanarak görüntüden metin çıkarma")

## Adım 1: GPU İşleme için Aspose OCR Motorunu Başlatma

İlk olarak, GPU’da çalışması gerektiğini bilen bir `OcrEngine` örneğine ihtiyacınız var. Aspose, çalışma zamanını belirtebileceğiniz temiz bir `OcrEngineSettings` nesnesi sunar.

```csharp
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

// Create the OCR engine and tell it to use the GPU runtime
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
});
```

**Neden önemli:** Varsayılan olarak Aspose OCR CPU’ya geri döner; bu küçük görüntüler için yeterli olabilir ancak yüksek çözünürlüklü fotoğraflar için acı verici derecede yavaştır. `Runtime = OcrRuntime.Gpu` ayarını açıkça belirlemek, ağır işi grafik kartına devrederek belirgin bir hız artışı sağlar.

## Adım 2: (İsteğe Bağlı) GPU Bellek Sınırı Belirleme

Paylaşımlı bir iş istasyonu ya da sınırlı GPU kaynaklarına sahip bir konteyner üzerinde çalışıyorsanız, OCR motorunun tükettiği bellek miktarını sınırlayabilirsiniz. Bu, bellek dışı hataları önler ve diğer süreçlerin mutlu çalışmasını sağlar.

```csharp
// Limit the GPU memory usage to 1024 MB (1 GB)
ocrEngine.Settings.GpuMemoryLimit = 1024;
```

**Ne zaman kullanılmalı:**  
- **Çok kiracılı ortamlar** where several services share the same GPU.  
- **CI/CD boru hatları** that allocate a fixed amount of GPU memory per job.  

Bu satırı atladığınızda, Aspose ihtiyacı olduğu kadar bellek kullanır; bu, ayrılmış bir iş istasyonunda sorun yaratmaz.

## Adım 3: Dosyadan Görüntü Yükleme

Şimdi resmi belleğe getirmemiz gerekiyor. Aspose OCR `System.Drawing.Image` ile çalışır, bu yüzden `Image.FromFile` kullanacağız. Yolun gerçek bir dosyaya işaret ettiğinden emin olun; aksi takdirde bir istisna fırlatılır.

```csharp
// Replace with the actual path to your high‑resolution image
string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

using (var image = Image.FromFile(imagePath))
{
    // The image is now ready for OCR processing
    // (the next step will happen inside this using block)
}
```

**Dosyadan yüklemenin önemi:** Birçok geliştirici doğrudan bir bayt dizisi beslemeye çalışır; bu çalışır ama gereksiz bir dönüşüm adımı ekler. `Image.FromFile` kullanmak basittir ve `using` ifadesi dosya tutamacının hızlıca serbest bırakılmasını garanti eder.

## Adım 4: OCR’ı Çalıştırma ve Sonucu Alma

Motor yapılandırıldı ve görüntü yüklendi, artık metni çıkarabiliriz. `Recognize` yöntemi, ham metin ve bir güven skoru içeren bir `OcrResult` döndürür.

```csharp
using (var image = Image.FromFile(imagePath))
{
    // Perform OCR on the loaded image
    var ocrResult = ocrEngine.Recognize(image);

    // Display the confidence and the extracted text
    Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Çıktıyı anlama:**  
- `Confidence` 0 ile 1 arasında bir değerdir. 0.95 (veya %95) genellikle OCR’ın %100 doğru olduğu anlamına gelir.  
- `Text` görüntüde göründüğü gibi satır sonları içerir; bu, sonraki işlemler için kullanışlıdır.

## Adım 5: Çıktıyı Doğrulama ve Köşe Durumlarını Ele Alma

### Güven Seviyelerini Kontrol Etme

Güven %80’in altına düşerse, CPU işleme geri dönmeyi ya da görüntü ön işleme (ör. ikilileştirme) uygulamayı düşünebilirsiniz.

```csharp
if (ocrResult.Confidence < 0.80)
{
    Console.WriteLine("Low confidence detected – consider preprocessing or CPU fallback.");
    // Example fallback: switch to CPU runtime temporarily
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
    Console.WriteLine(cpuResult.Text);
}
```

### Eksik GPU ile Baş Etme

Her makinede uyumlu bir GPU bulunmaz. Aspose, GPU çalışma zamanını başlatamazsa bir `OcrException` fırlatır.

```csharp
try
{
    var ocrResult = ocrEngine.Recognize(image);
    // Normal processing...
}
catch (OcrException ex) when (ex.Message.Contains("GPU"))
{
    Console.WriteLine("GPU not available – falling back to CPU.");
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine(cpuResult.Text);
}
```

### Yüksek Çözünürlüklü Görüntüler

Çok büyük görüntüler (ör. genişliği 4000 px’den fazla) çok fazla GPU belleği tüketebilir. Önceden belirlediğiniz sınırı aşarsanız, Aspose işleme kesilir. Bu durumda görüntüyü önce küçültün:

```csharp
using (var original = Image.FromFile(imagePath))
{
    int maxWidth = 2000;
    var resized = new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width));
    var ocrResult = ocrEngine.Recognize(resized);
    // Continue as before
}
```

## Tam Çalışan Örnek

Aşağıda yeni bir konsol projesine kopyalayıp yapıştırabileceğiniz tam program yer alıyor. Tüm adımları, hata yönetimini ve isteğe bağlı geri dönüş mantığını içerir.

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Initialize OCR engine to use GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
        });

        // Step 2: (Optional) Limit GPU memory usage to 1 GB
        ocrEngine.Settings.GpuMemoryLimit = 1024;

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

        // Step 3: Load image from file
        using (var image = Image.FromFile(imagePath))
        {
            try
            {
                // Step 4: Run OCR on the image
                var ocrResult = ocrEngine.Recognize(image);

                // Step 5: Output confidence and extracted text
                Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
                Console.WriteLine("Extracted text:");
                Console.WriteLine(ocrResult.Text);

                // Edge‑case: low confidence handling
                if (ocrResult.Confidence < 0.80)
                {
                    Console.WriteLine("\nLow confidence detected – trying CPU fallback...");
                    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                    var cpuResult = ocrEngine.Recognize(image);
                    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                    Console.WriteLine(cpuResult.Text);
                }
            }
            catch (OcrException ex) when (ex.Message.Contains("GPU"))
            {
                Console.WriteLine("GPU not available – falling back to CPU runtime.");
                ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                var cpuResult = ocrEngine.Recognize(image);
                Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                Console.WriteLine(cpuResult.Text);
            }
        }
    }
}
```

### Beklenen Çıktı

```
GPU OCR confidence: 96.45%
Extracted text:
This is the text that was
found in the high‑resolution
image you supplied.

```

Güven eşik değerinin altına düşerse, ek CPU geri dönüş mesajlarını göreceksiniz.

---

## Sonuç

Artık **görüntüden metin çıkarma** işlemini Aspose OCR’ın GPU motoru ile nasıl yapacağınızı, **dosyadan görüntü yükleme** adımını ve üretim ortamları için **GPU bellek sınırı** belirlemenin neden gerekli olduğunu biliyorsunuz. Yukarıdaki örnek, herhangi bir .NET projesine ekleyebileceğiniz tam işlevsel, referans alınabilir bir çözümdür.

Sırada ne var? Şunları düşünün:

- **Toplu işleme**: bir klasördeki tüm görüntüler üzerinde döngü kurup sonuçları bir CSV’ye yazın.  
- **ASP.NET Core entegrasyonu**: yüklenen bir görüntüyü kabul eden ve OCR metnini dönen bir API uç noktası oluşturun.  
- **Performans ayarı**: farklı `GpuMemoryLimit` değerleri deneyin ve optimum noktayı bulmak için GPU kullanımını izleyin.

Kodu kendi senaryonuza uyarlamaktan çekinmeyin—belge dijitalleştirme boru hattı, gerçek‑zamanlı çeviri uygulaması ya da fiş tarama servisi olsun. Temel adımlar aynı kalır: GPU motorunu başlatın, belleği akıllıca yönetin ve her zaman güven skorunu doğrulayın.

Sorularınız mı var ya da bir sorunla mı karşılaştınız? Aşağıya yorum bırakın, birlikte sorun giderelim. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}