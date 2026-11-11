---
category: general
date: 2026-02-25
description: GPU hızlandırmalı OCR kullanarak görüntüden metni hızlıca tanıyın. GPU
  modunu ayarlamayı, OCR için görüntüyü yüklemeyi ve TIFF'ten metin çıkarmayı öğrenin.
draft: false
keywords:
- recognize text from image
- set gpu mode
- gpu accelerated ocr
- load image for ocr
- extract text from tiff
language: tr
og_description: GPU hızlandırmalı OCR kullanarak görüntüden metni anında tanıyın.
  GPU modunu ayarlama, OCR için görüntü yükleme ve TIFF'ten metin çıkarma konularını
  kapsayan adım adım C# öğreticisi.
og_title: GPU hızlandırmalı OCR ile görüntüden metin tanıma – C# Rehberi
tags:
- Aspose OCR
- C#
- GPU computing
title: C#'ta GPU hızlandırmalı OCR ile görüntüden metin tanıma
url: /tr/net/ocr-optimization/recognize-text-from-image-using-gpu-accelerated-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU‑hızlandırmalı OCR ile C#'ta görüntüden metin tanıma

Hiç **görüntüden metin tanıma** yapmak istediniz ama CPU yüksek çözünürlüklü bir tarama ile boğuluyordu mu? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede—örneğin fatura dijitalleştirme ya da eski gazetelerin arşivlenmesi—tek bir TIFF dosyası dakikalarca süren bir tıkanıklığa neden olabilir. İyi haber? Aspose.OCR bir anahtarı çevirmenize ve ağır işi GPU'nuza devretmenize olanak tanır; yavaş bir işlemi neredeyse anlık bir hâle getirir.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: **GPU modunu nasıl ayarlarsınız**, **OCR için görüntüyü nasıl yüklersiniz**, ve **TIFF dosyalarından metni nasıl çıkarırsınız**. Sonunda, .NET 6+ herhangi bir projeye ekleyebileceğiniz, bağımsız ve üretim‑hazır bir örnek elde edeceksiniz.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

- .NET 6 SDK (veya daha yeni bir sürüm).
- Visual Studio 2022 ya da tercih ettiğiniz başka bir editör.
- Projenize eklenmiş bir Aspose.OCR NuGet paketi (`Aspose.OCR`).
- DirectX 11 veya daha yeni bir sürümü destekleyen bir GPU (çoğu modern GPU bu şartı karşılar).  
  *GPU'nuz yoksa, `GpuMode.Auto` ile kodu hâlâ çalıştırabilirsiniz—kütüphane otomatik olarak CPU'ya geçer.*

> **İpucu:** GPU sürücünüzün güncel olduğundan emin olun; eski sürücüler gizli başlatma hatalarına yol açabilir.

## Adım 1 – OCR motorunu oluşturun ve GPU modunu ayarlayın

İlk olarak bir `OcrEngine` örneğine ihtiyacınız var. Bu nesne tüm yapılandırmayı tutar, GPU kullanılıp kullanılmayacağını da içerir.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // Step 1: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Enable GPU acceleration.
            // Use GpuMode.Auto if you want the library to pick CPU when a GPU isn’t available.
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled);

            // The rest of the workflow continues below…
        }
    }
}
```

**Neden önemli:** GPU modunu etkinleştirmek, hesaplama açısından yoğun görüntü ön‑işleme (ikiliye çevirme, gürültü giderme vb.) görevlerini grafik kartına taşır. Orta seviye bir RTX 3060'da, saf CPU işlemine kıyasla **3‑5× hız artışı** görebilirsiniz.

## Adım 2 – OCR için görüntüyü yükleyin (TIFF örneği)

Aspose.OCR birçok formatı destekler, ancak TIFF taranmış belgeler için yaygın olarak tercih edilir çünkü kayıpsız kalite sunar. Dosyayı belleğe almak için `ImageStream.FromFile` kullanın.

```csharp
// Step 2: Load the high‑resolution TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"C:\Data\high_res_scan.tif");

// Optional: If you need to work with a stream (e.g., from a web API), use:
// ocrEngine.Image = ImageStream.FromStream(yourInputStream);
```

**Köşe durumu:** Bazı TIFF dosyaları birden fazla sayfa içerir. `ImageStream.FromFile` yalnızca ilk sayfayı okur. Tüm sayfaları işlemek istiyorsanız, `ImageInfo.Pages` üzerinde döngü kurup her birini motorun `Image` özelliğine ayrı ayrı atayın.

## Adım 3 – Tanıma işlemini gerçekleştirin

Motor yapılandırıldı ve görüntü yüklendiğine göre, `Recognize()` metodunu çağırın. Metot, düz metin çıktısını ve ek meta verileri içeren bir `OcrResult` nesnesi döndürür.

```csharp
// Step 3: Run OCR
OcrResult result = ocrEngine.Recognize();

// The result may include confidence scores per line, if you enable them in the config.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

**Metin bozuk çıkarsa ne yapmalı?**  
- Görüntünün okunabilir bir yönlendirmede olduğundan emin olun (gerekirse döndürün).  
- `ocrEngine.Config.DeskewEnabled = true;` gibi ön‑işleme seçeneklerini ayarlayın.  
- Çok dilli belgeler için `ocrEngine.Config.Language = Language.English;` ya da uygun enum değerini kullanın.

## Adım 4 – Çıktıyı doğrulayın ve hataları yönetin

Sağlam bir uygulama, null sonuçları kontrol eder ve olası istisnaları yakalar (ör. eksik GPU sürücüleri).

```csharp
try
{
    OcrResult result = ocrEngine.Recognize();

    if (result?.Text == null)
    {
        Console.WriteLine("No text detected – double‑check the image quality.");
    }
    else
    {
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
catch (Exception ex)
{
    Console.WriteLine($"OCR failed: {ex.Message}");
    // You might want to fallback to CPU mode here:
    // ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
}
```

**Neden try‑catch?** GPU başlatma aşamasında gerekli yerel kütüphaneler bulunmazsa `DllNotFoundException` fırlatılabilir. Catch bloğu, sorunsuz bir gerileme yolu sağlar.

## Tam, çalıştırılabilir örnek

Hepsini bir araya getirdiğimizde, hemen derleyip çalıştırabileceğiniz eksiksiz bir program elde edersiniz. Dosya yolunu kendi makinenizdeki gerçek bir TIFF ile değiştirin.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // 1️⃣ Create OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled); // or GpuMode.Auto for fallback

            // 2️⃣ Load the image you want to process
            string imagePath = @"C:\Data\high_res_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Optional: tweak preprocessing (helps with noisy scans)
            ocrEngine.Config.DeskewEnabled = true;
            ocrEngine.Config.RemoveNoiseEnabled = true;

            // 4️⃣ Run recognition and handle the result
            try
            {
                OcrResult result = ocrEngine.Recognize();

                if (string.IsNullOrWhiteSpace(result?.Text))
                {
                    Console.WriteLine("No text found – consider improving image quality.");
                }
                else
                {
                    Console.WriteLine("=== Recognized Text ===");
                    Console.WriteLine(result.Text);
                }
            }
            catch (Exception e)
            {
                Console.WriteLine($"Error during OCR: {e.Message}");
                // Fallback to CPU if GPU failed
                ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
                // You could retry here…
            }
        }
    }
}
```

**Beklenen çıktı**

TIFF okunabilir İngilizce metin içeriyorsa, aşağıdakine benzer bir çıktı görürsünüz:

```
=== Recognized Text ===
Invoice #12345
Date: 2024‑11‑08
Total Amount: $1,235.00
...
```

Görüntü boş ya da okunamazsa, konsol kaynak dosyayı kontrol etmeniz gerektiğini belirtecektir.

## Sık sorulan sorular & varyasyonlar

| Soru | Cevap |
|----------|--------|
| **TIFF yerine JPEG veya PNG işleyebilir miyim?** | Kesinlikle. `ImageStream.FromFile` Aspose.OCR'un desteklediği (PNG, JPEG, BMP vb.) tüm formatlarla çalışır. |
| **Bir TIFF içinde birden fazla sayfa varsa ne yapmalıyım?** | `ImageInfo.Pages` üzerinden döngü kurup her sayfayı `ocrEngine.Image`'a atayın, ardından `Recognize()` çağırın. |
| **Aspose.OCR için lisansa ihtiyacım var mı?** | Ücretsiz değerlendirme sürümü 100 sayfaya kadar çalışır. Üretim ortamı için değerlendirme filigranını kaldırmak üzere lisans satın alın. |
| **Dil modelini nasıl değiştiririm?** | `ocrEngine.Config.Language = Language.Spanish;` (veya desteklenen herhangi bir enum) şeklinde ayarlayın. |
| **Güven skorlarını alabilir miyim?** | `ocrEngine.Config.EnableConfidence = true;` etkinleştirin ve `result.Confidence` değerini satır bazında inceleyin. |

## Sonuç

Artık **GPU‑hızlandırmalı OCR** boru hattı kullanarak **görüntüden metin tanıma** işlemini C# içinde nasıl yapacağınızı biliyorsunuz. **GPU modunu ayarlayarak**, **görüntüyü OCR için yükleyerek** ve **TIFF dosyalarından metin çıkararak**, gerçek dünya iş yüklerine hazır, hızlı ve ölçeklenebilir bir çözüm inşa ettiniz.

Sonraki adımlar? Bu kodu bir PDF oluşturucu ile zincirleyerek aranabilir PDF'ler üretin ya da çıkarılan metinleri doğal dil işleme (NLP) hattına besleyin. Ayrıca, GPU'suz ortamlara uyum sağlamak için `GpuMode.Auto` ile deneyler yapabilirsiniz.

Keyifli kodlamalar ve OCR işlemlerinizin ışık hızında çalışması dileğiyle!

![görüntüden metin tanıma örneği](https://example.com/ocr-demo.png "GPU‑hızlandırmalı OCR ile görüntüden metin tanıma")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}