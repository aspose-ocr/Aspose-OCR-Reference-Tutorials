---
category: general
date: 2026-06-16
description: C#'da Aspose OCR kullanarak OCR için görüntüyü ön işleme tabi tutun.
  Tarama görüntüsünün kontrastını artırmayı ve gürültüyü kaldırmayı öğrenerek doğru
  metin çıkarımı sağlayın.
draft: false
keywords:
- preprocess image for OCR
- enhance image contrast
- remove noise from scanned image
language: tr
og_description: Aspose OCR ile OCR için görüntüyü ön işleyin. Tarama görüntüsünün
  kontrastını artırarak ve gürültüyü gidererek doğruluğu yükseltin.
og_title: C#'ta OCR için Görüntüyü Ön İşleme – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Preprocess image for OCR using Aspose OCR in C#. Learn to enhance image
    contrast and remove noise from scanned image for accurate text extraction.
  headline: Preprocess Image for OCR in C# – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR using Aspose OCR in C#. Learn to enhance image
    contrast and remove noise from scanned image for accurate text extraction.
  name: Preprocess Image for OCR in C# – Complete Guide
  steps:
  - name: '**Heavy Salt‑and‑Pepper Noise** – Increase the aggressiveness of `DenoiseFilter`
      by passing a custom `DenoiseOptions` object (e.g., `new DenoiseFilter(new DenoiseOptions
      { Strength = 2 })`).'
    text: '**Heavy Salt‑and‑Pepper Noise** – Increase the aggressiveness of `DenoiseFilter`
      by passing a custom `DenoiseOptions` object (e.g., `new DenoiseFilter(new DenoiseOptions
      { Strength = 2 })`).'
  - name: '**Faded Ink on Yellow Paper** – Pair `ContrastEnhanceFilter` with a `BrightnessAdjustFilter`
      to lift the background tone before boosting contrast.'
    text: '**Faded Ink on Yellow Paper** – Pair `ContrastEnhanceFilter` with a `BrightnessAdjustFilter`
      to lift the background tone before boosting contrast.'
  - name: '**Colored Text** – Convert the image to grayscale first (`new GrayscaleFilter()`)
      because most OCR engines, including Aspose, work best on single‑channel data.'
    text: '**Colored Text** – Convert the image to grayscale first (`new GrayscaleFilter()`)
      because most OCR engines, including Aspose, work best on single‑channel data.'
  - name: '**Build** the console project (`dotnet build`).'
    text: '**Build** the console project (`dotnet build`).'
  - name: '**Run** (`dotnet run`). You should see something like:'
    text: '**Run** (`dotnet run`). You should see something like:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
title: C#'ta OCR için Görüntü Ön İşleme – Tam Kılavuz
url: /tr/net/ocr-optimization/preprocess-image-for-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR için Görüntüyü Ön İşleme – Tam Kılavuz

Kaynak fotoğraf oldukça net olmasına rağmen OCR sonuçlarınızın karışık bir karmaşa gibi görünmesinin nedenini hiç merak ettiniz mi? Gerçek şu ki, çoğu OCR motoru—Aspose OCR dahil—temiz, iyi hizalanmış bir görüntü bekler. **OCR için görüntüyü ön işleme**, titrek, düşük kontrastlı bir taramayı net, makine tarafından okunabilir metne dönüştürmenin ilk adımıdır.

Bu öğreticide, **OCR için görüntüyü ön işleme** yapmanın yanı sıra Aspose’un yerleşik filtrelerini kullanarak **görüntü kontrastını artırma** ve **tarama görüntüsünden gürültüyü kaldırma** nasıl yapılır gösteren pratik, uçtan uca bir örnek üzerinden ilerleyeceğiz. Sonunda, çok daha güvenilir tanıma sonuçları veren hazır bir C# konsol uygulamanız olacak.

---

## What You’ll Need

- **.NET 6.0 veya üzeri** (kod .NET Framework 4.6+ ile de çalışır)  
- **Aspose.OCR for .NET** – `Aspose.OCR` NuGet paketini edinebilirsiniz  
- Gürültü, eğim veya düşük kontrast sorunu yaşayan bir örnek görüntü (demo için `skewed-photo.jpg` kullanacağız)  
- İstediğiniz IDE – Visual Studio, Rider veya VS Code fark etmez  

Ek native kütüphaneler ya da karmaşık kurulumlar gerekmez; her şey Aspose paketinin içinde yer alır.

---

## ## Preprocess Image for OCR – Step‑by‑Step Implementation

Aşağıda derleyeceğiniz tam kaynak dosyası yer alıyor. Yeni bir konsol projesine kopyalayıp **F5** tuşuna basmanız yeterli.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2: Add preprocessing filters to improve recognition.
        // 2a – Remove noise from scanned image.
        ocrEngine.Settings.Filters.Add(new DenoiseFilter()); // Reduces random speckles.
        // 2b – Correct skew (deskew) that often appears in photographed documents.
        ocrEngine.Settings.Filters.Add(new DeskewFilter()); // Straightens the baseline.
        // 2c – Enhance image contrast for better character separation.
        ocrEngine.Settings.Filters.Add(new ContrastEnhanceFilter()); // Boosts contrast.

        // Step 3: (Optional) Rotate the image if it was captured at an angle.
        // Negative values rotate clockwise, positive counter‑clockwise.
        ocrEngine.Settings.Filters.Add(new RotateFilter(-3)); // Small correction.

        // Step 4: Perform OCR on the image file.
        // Replace the path with the actual location of your test image.
        string extractedText = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed-photo.jpg");

        // Step 5: Display the recognized text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

### Why Each Filter Matters

| Filtre | Ne işe yarar | Neden OCR'a yardımcı olur |
|--------|--------------|----------------------------|
| **DenoiseFilter** | Düşük ışık taramalarında sıkça görülen rastgele piksel gürültüsünü ortadan kaldırır. | Gürültü, karakter parçacıkları olarak algılanabilir ve karakter şekillerini bozar. |
| **DeskewFilter** | Baskın metin satırı açısını tespit eder ve görüntüyü 0°'ye döndürür. | Eğik satırlar, OCR motorunun karakterleri eğik algılamasına ve hatalı tanıma yapmasına neden olur. |
| **ContrastEnhanceFilter** | Koyu metin ile açık arka plan arasındaki farkı genişletir. | Yüksek kontrast, çoğu OCR boru hattındaki ikili eşikleme adımını iyileştirir. |
| **RotateFilter** (isteğe bağlı) | Belirttiğiniz manuel dönüşü uygular. | Otomatik eğim düzeltme yeterli olmadığında (örneğin hafif bir açıyla çekilmiş fotoğraf) kullanışlıdır. |

> **Pro tip:** Kaynağınız taranmış bir PDF ise, önce sayfayı bir görüntü olarak dışa aktarın (ör. `PdfRenderer` kullanarak) ve ardından aynı filtre zincirine besleyin. Aynı ön işleme mantığı geçerlidir.

---

## ## Enhance Image Contrast Before OCR – Visual Confirmation

Bir filtre eklemek bir şey, etkisini görmek başka bir şey. Aşağıda basit bir önce‑ve‑son illüstrasyonu (kendi ekran görüntülerinizi ekleyin) yer alıyor.

![OCR için görüntü ön işleme hattının diyagramı](image.png){alt="OCR için görüntü ön işleme hattının diyagramı"}

Sol tarafta ham, gürültülü tarama, sağ tarafta ise **görüntü kontrastını artırma**, **tarama görüntüsünden gürültüyü kaldırma** ve eğim düzeltme sonrası aynı görüntü gösteriliyor. Karakterlerin net ve izole hâle geldiğine dikkat edin—tam da OCR motorunun ihtiyaç duyduğu durum.

---

## ## Remove Noise from Scanned Image – Edge Cases & Tips

Her belge aynı tür gürültüye sahip değildir. Karşılaşabileceğiniz birkaç senaryo ve boru hattını nasıl ayarlayacağınız aşağıda:

1. **Yoğun Tuz‑ve‑Karabiber Gürültüsü** – `DenoiseFilter`’ın agresifliğini, özel bir `DenoiseOptions` nesnesi geçirerek artırın (ör. `new DenoiseFilter(new DenoiseOptions { Strength = 2 })`).  
2. **Sarı Kağıtta Soluk Mürekkep** – Arka plan tonunu yükseltmek için `ContrastEnhanceFilter` ile birlikte bir `BrightnessAdjustFilter` ekleyin, ardından kontrastı artırın.  
3. **Renkli Metin** – Görüntüyü önce gri tonlamaya çevirin (`new GrayscaleFilter()`) çünkü çoğu OCR motoru, Aspose dahil, tek kanal verilerde daha iyi çalışır.  

Filtre sırasının da önemi olabilir. Pratikte, `DenoiseFilter`’ı **DeskewFilter**’dan **önce** koyarım; daha temiz bir görüntü, eğim algılama algoritmasına daha güvenilir kenar verisi sağlar.

---

## ## Running the Demo & Verifying Output

1. **Projeyi derleyin** (`dotnet build`).  
2. **Çalıştırın** (`dotnet run`). Aşağıdakine benzer bir çıktı görmelisiniz:

```
=== OCR RESULT ===
The quick brown fox jumps over the lazy dog.
```

Çıktı hâlâ bozuk karakterler içeriyorsa, görüntü yolunun doğru olduğundan ve kaynak dosyanın çok düşük çözünürlükte (çoğu OCR görevi için minimum 300 dpi önerilir) olmadığından emin olun.

---

## Conclusion

Artık C#’ta **OCR için görüntüyü ön işleme** için sağlam, üretim‑hazır bir deseniniz var. Aspose’un `DenoiseFilter`, `DeskewFilter` ve `ContrastEnhanceFilter`—ve isteğe bağlı olarak `RotateFilter`—zincirini birleştirerek **görüntü kontrastını artırma**, **tarama görüntüsünden gürültüyü kaldırma** ve sonraki metin çıkarma adımının doğruluğunu büyük ölçüde yükseltebilirsiniz.

Sırada ne var? Temizlenmiş görüntüyü imla kontrolü, dil algılama gibi diğer sonrası‑işleme adımlarına besleyin ya da ham metni bir doğal dil işleme boru hattına yönlendirin. Ayrıca ikili‑sadece iş akışları için Aspose’un `BinarizationFilter`’ını keşfedebilir ya da aynı ön işleme zincirini kullanarak farklı bir OCR motoru (Tesseract, Microsoft OCR) deneyebilirsiniz.

Zor bir görüntünüz hâlâ işbirliği yapmıyorsa, yorum bırakın; birlikte sorun giderelim. İyi kodlamalar, OCR sonuçlarınız daima kristal‑temiz olsun!

## What Should You Learn Next?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [AspOCR Nasıl Kullanılır: .NET için Görüntü OCR Filtrelerini Ön İşleme](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Görüntüden Metin Çıkarma – Aspose.OCR for .NET ile OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)
- [Aspose.OCR for .NET Kullanarak Görüntüden Metin Nasıl Çıkarılır](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}