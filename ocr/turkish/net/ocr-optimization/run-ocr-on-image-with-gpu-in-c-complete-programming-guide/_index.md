---
category: general
date: 2026-03-26
description: C#'ta Aspose OCR GPU desteğiyle görüntüde OCR çalıştırın. OCR için görüntüyü
  nasıl yükleyeceğinizi, GPU cihaz kimliğini nasıl ayarlayacağınızı ve görüntüden
  hızlı bir şekilde metin çıkartacağınızı öğrenin.
draft: false
keywords:
- run OCR on image
- extract text from image
- load image for OCR
- recognize text from document
- set GPU device ID
language: tr
og_description: C#'ta Aspose OCR GPU kullanarak görüntüde OCR çalıştırın. Bu kılavuz,
  OCR için görüntünün nasıl yükleneceğini, GPU cihaz kimliğinin nasıl ayarlanacağını
  ve görüntüden metnin verimli bir şekilde nasıl çıkarılacağını gösterir.
og_title: C#'ta GPU ile Görüntüde OCR Çalıştırma – Tam Kılavuz
tags:
- C#
- OCR
- GPU
- Aspose
title: C#'ta GPU ile Görüntü Üzerinde OCR Çalıştırma – Tam Programlama Rehberi
url: /tr/net/ocr-optimization/run-ocr-on-image-with-gpu-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU ile Görüntü Üzerinde OCR Çalıştırma C# – Tam Programlama Rehberi

Hiç **run OCR on image** dosyalarını çalıştırmanız gerekti ve CPU sürümünün acı verici derecede yavaş olduğunu mu düşündünüz? Yalnız değilsiniz. Gerçek dünyadaki birçok uygulamada—örneğin fatura tarayıcıları veya büyük ölçekli belge arşivleri—darboğaz OCR motorudur.  

Bu öğreticide **tam, çalıştırılabilir bir örnek** üzerinden **load image for OCR** nasıl yapılır, isteğe bağlı olarak **set GPU device ID** nasıl ayarlanır ve sonunda Aspose OCR’un GPU‑hızlandırmalı API’si kullanılarak **extract text from image** nasıl elde edilir adım adım göstereceğiz. Sonunda, saf‑CPU yaklaşımının alacağı sürenin bir kısmında **recognize text from document** görüntülerinden metin tanıyabileceksiniz.

## Neler Öğreneceksiniz

- Aspose.OCR ve Aspose.OCR.Gpu paketlerini nasıl kurup referans göstereceğinizi.  
- GPU hızlandırmasıyla **run OCR on image** için tam adımlar.  
- Çoklu GPU makinelerde doğru **GPU device ID** seçiminin neden önemli olduğunu.  
- Büyük dosyalarla başa çıkma, geri dönüş stratejileri ve yaygın tuzaklar için ipuçları.  

### Önkoşullar

| Gereksinim | Sebep |
|-------------|--------|
| .NET 6.0 veya üzeri | Modern dil özellikleri ve daha iyi performans |
| Visual Studio 2022 (veya herhangi bir C# IDE) | Kolay proje kurulumu için |
| CUDA desteği olan NVIDIA GPU (isteğe bağlı) | Yalnızca GPU hızlandırması istiyorsanız gereklidir |
| Aspose.OCR & Aspose.OCR.Gpu NuGet paketleri | `GpuOcrEngine` sınıfını sağlar |

GPU'nuz yoksa panik yapmayın—kod, daha sonra ele alacağımız CPU motoruna sorunsuz bir şekilde geri döner.

---

## Adım 1: Aspose OCR Paketlerini Kurun

**run OCR on image** yapabilmeniz için önce kütüphanelere ihtiyacınız var. Terminalinizi (veya Package Manager Console) açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Bu iki paket, temel OCR motorunu ve GPU‑özel uzantılarını getirir. Kurulumdan sonra `.csproj` dosyanızda aşağıdaki referansları göreceksiniz:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
  <PackageReference Include="Aspose.OCR.Gpu" Version="23.10.0" />
</ItemGroup>
```

> **Pro ipucu:** Paket sürümlerini senkronize tutun; uyumsuz sürümler çalışma zamanı hatalarına neden olabilir.

---

## Adım 2: GPU‑Destekli OCR Motoru Oluşturun

Kütüphaneler yerinde olduğuna göre, GPU kullanarak **run OCR on image** yapalım. `GpuOcrEngine` sınıfı, hızlandırılmış işleme için giriş noktasıdır.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Instantiate the GPU OCR engine
        var gpuEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Choose which GPU to use – 0 = first GPU
        // This is where the "set GPU device ID" keyword comes into play.
        gpuEngine.DeviceId = 0;

        // The rest of the workflow continues in the following steps...
```

**Neden GPU?**  
GPU çekirdekleri paralel piksel işlemlerinde mükemmeldir; bu da yüksek çözünürlüklü taramalarda OCR’un tam olarak ihtiyaç duyduğu şeydir. `DeviceId` ayarlanarak, birden fazla GPU’ya sahip iş istasyonlarında hangi fiziksel kartın kullanılacağını belirtebilirsiniz.

---

## Adım 3: OCR İçin Görüntüyü Yükleyin

Tanıma başlamadan önce **load image for OCR** yapmanız gerekir. Aspose, JPEG, PNG, TIFF vb. birçok formatı destekleyen kullanışlı bir statik fabrika yöntemi sunar.

```csharp
        // Step 3: Load the image you want to recognize
        // Replace the path with your actual file location.
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");

        // Quick sanity check – ensure the image was loaded.
        if (ocrImage == null)
        {
            Console.WriteLine("Failed to load image. Check the file path.");
            return;
        }
```

> **Edge case:** Görüntü 10 MB’dan büyükse, GPU bellek tükenmesini önlemek için önce down‑sampling yapmayı düşünün. Tanımadan önce `ocrImage.Resize(width, height)` ile bunu yapabilirsiniz.

---

## Adım 4: Belgeden Metin Tanıma

Motor hazır ve görüntü yüklendiğine göre, **recognize text from document** zamanı geldi. `Recognize` metodu, düz metin çıktısını ve ek meta verileri içeren bir `OcrResult` nesnesi döndürür.

```csharp
        // Step 4: Run the OCR process on the image
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);

        // Verify that OCR succeeded
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR failed or returned empty result.");
            return;
        }
```

**Altında ne oluyor?**  
GPU motoru piksel verilerini CUDA çekirdeklerine gönderir; bu çekirdekler ikilileştirme, karakter segmentasyonu ve sinir‑ağları çıkarımı gibi işlemleri paralel olarak gerçekleştirir. Bu yüzden CPU’da saniyeler süren **run OCR on image** dosyalarını GPU ile çok daha hızlı işleyebilirsiniz.

---

## Adım 5: Görüntüden Metin Çıkarma ve Çıktı

Son olarak **extract text from image** yapıp ekrana gösteriyoruz. Sonucu bir dosyaya, veritabanına yazabilir ya da sonraki NLP boru hatlarına besleyebilirsiniz.

```csharp
        // Step 5: Output the recognized plain‑text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);

        // Optional: Save to a .txt file for later processing
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }
}
```

**Beklenen çıktı** (kısaltılmıştır):

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

Programı çalıştırıp benzer bir blok görürseniz, tebrikler—GPU hızlandırmasıyla **run OCR on image** başarıyla gerçekleştirdiniz!

---

## GPU Olmadan Durumları Yönetme (Geri Dönüş)

Dağıtım yaptığınız makinede uyumlu bir GPU yoksa ne olur? `GpuOcrEngine` yapıcı, bir `GpuNotSupportedException` fırlatır. Başlatmayı try‑catch içinde sarın ve şu şekilde `OcrEngine` (CPU)’a geri dönün:

```csharp
        try
        {
            var gpuEngine = new GpuOcrEngine { DeviceId = 0 };
            // Continue with GPU workflow...
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not available – switching to CPU OCR.");
            var cpuEngine = new OcrEngine();
            OcrResult result = cpuEngine.Recognize(ocrImage);
            Console.WriteLine(result.Text);
        }
```

Bu desen, donanımdan bağımsız olarak uygulamanızın işlevsel kalmasını sağlar; bulut dağıtımları için kritik bir husustur.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda **entire program** yer alıyor—eksik parça yok, sadece dosya yollarını kendi ortamınıza göre değiştirin.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Create a GPU‑enabled OCR engine
        GpuOcrEngine gpuEngine;
        try
        {
            gpuEngine = new GpuOcrEngine { DeviceId = 0 }; // set GPU device ID
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not detected. Falling back to CPU engine.");
            var cpuEngine = new OcrEngine();
            RunCpuOcr(cpuEngine);
            return;
        }

        // 2️⃣ Load image for OCR
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        if (ocrImage == null)
        {
            Console.WriteLine("Unable to load image – check the path.");
            return;
        }

        // 3️⃣ Recognize text from document
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR returned no text.");
            return;
        }

        // 4️⃣ Extract text from image and output
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }

    // Helper for CPU fallback
    static void RunCpuOcr(OcrEngine cpuEngine)
    {
        var img = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        var result = cpuEngine.Recognize(img);
        Console.WriteLine("=== CPU OCR Result ===");
        Console.WriteLine(result.Text);
    }
}
```

> **Not:** Yukarıdaki kod otomatik olarak **extracts text from image** yapar ve `ocr_result.txt` dosyasına yazar. Gerekirse yolları ayarlayın.

---

## Sık Sorulan Sorular & İpuçları

| Soru | Cevap |
|----------|--------|
| *Belirli bir NVIDIA sürücüsüne ihtiyacım var mı?* | Evet—CUDA 11.x veya daha yenisi önerilir. Tam uyumluluk için Aspose'un sürüm notlarını kontrol edin. |
| *Birden fazla görüntüyü aynı anda işleyebilir miyim?* | Kesinlikle. OCR çağrısını bir `Parallel.ForEach` döngüsü içinde sarın, ancak GPU bellek sınırlarına dikkat edin. |
| *OCR sonucu bozuk karakterler içeriyorsa ne yapmalıyım?* | Görüntü ön işleme ayarlarını değiştirin: tanıma öncesinde `ocrImage.Binarize()` veya `ocrImage.Deskew()` kullanın. |
| *Dil modelini sınırlamanın bir yolu var mı?* | Yalnızca İngilizceye ihtiyacınız varsa işleme hızını artırmak için `gpuEngine.Language = OcrLanguage.English;` ayarlayın. |

---

## Sonuç

Artık **tam, uçtan uca bir çözüm** elde ettiniz **run OCR on image** 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}