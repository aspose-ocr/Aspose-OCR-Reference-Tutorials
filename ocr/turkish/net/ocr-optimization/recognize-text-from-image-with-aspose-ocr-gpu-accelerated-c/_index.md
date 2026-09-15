---
category: general
date: 2026-01-13
description: Aspose OCR kullanarak görüntüden metin tanıma ve makbuzdan metni hızlı
  bir şekilde çıkarma yöntemini öğrenin. OCR için görüntü yükleme ve GPU cihaz kimliğini
  ayarlama adımlarını içerir.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for ocr
- set gpu device id
language: tr
og_description: Aspose OCR ile görüntüden metni anında tanıyın. OCR için görüntüyü
  yüklemek, GPU cihaz kimliğini ayarlamak ve makbuzdan metin çıkarmak için bu adım
  adım kılavuzu izleyin.
og_title: görüntüden metin tanıma – Tam GPU Hızlandırmalı C# Rehberi
tags:
- Aspose OCR
- C#
- GPU computing
title: Aspose OCR ile görüntüden metin tanıma – GPU Hızlandırmalı C# Öğreticisi
url: /tr/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# görüntüden metin tanıma – Tam GPU‑Hızlandırmalı C# Rehberi

Hiç **görüntüden metin tanıma** yapmanız gerekti, ancak CPU sürümünün ağrılı derecede yavaş olduğunu mu fark ettiniz? Belki **fişlerden metin çıkarma** dosyalarıyla uğraşıyorsunuz ve gecikme kullanıcı deneyiminizi öldürüyor. İyi haber şu ki, yavaş performansa razı olmak zorunda değilsiniz—Aspose OCR’un GPU paketi süreci turbo‑şarj edebilir ve kod sadece birkaç satır uzunluğunda.

Bu öğreticide, **OCR için görüntü yükleme**, **GPU cihaz kimliğini ayarlama** ve son olarak düz‑metin sonucunu alma adımlarını gösteren tam, çalıştırılabilir bir örnek üzerinden geçeceğiz. Sonuna geldiğinizde, desteklenen bir NVIDIA kartı bulunan modern bir Windows ya da Linux makinesinde çalışacak, doğrudan kopyalayıp yapıştırabileceğiniz bir snippet elde edeceksiniz.

---

## Gereksinimler

- **.NET 6+** (veya .NET Framework 4.7.2+) – API her iki ortamda da çalışır.
- **Aspose.OCR** NuGet paketi **ve** **Aspose.OCR.Gpu** eklentisi.
- En az 2 GB VRAM’e sahip bir NVIDIA GPU (demo kullanımını 1 GB ile sınırlar).
- Örnek bir görüntü, ör. taranmış bir fiş (`receipt.jpg`).

Eğer zaten bir projeniz varsa, sadece `dotnet add package Aspose.OCR` ve `dotnet add package Aspose.OCR.Gpu` komutlarını çalıştırın. Ek native kütüphanelere ihtiyaç yok; SDK gerekli CUDA ikili dosyalarını içerir.

---

## Adım‑Adım Uygulama

### ## Aspose OCR ve GPU kullanarak görüntüden metin tanıma

Aşağıda **tam, bağımsız program** yer alıyor. Yeni bir console projesine kopyalayıp `Ctrl+F5` ile çalıştırın.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑accelerated namespace

class GpuOcrDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize a GPU‑enabled OCR engine
        // -------------------------------------------------
        var ocrEngine = new GpuOcrEngine();

        // -------------------------------------------------
        // Step 2: (Optional) Select the GPU device and limit memory usage
        // -------------------------------------------------
        ocrEngine.DeviceId = 0;        // set GPU device ID – first GPU in the system
        ocrEngine.MaxMemoryMb = 1024;  // cap at 1 GB to avoid OOM on shared machines

        // -------------------------------------------------
        // Step 3: Load the image you want to recognize
        // -------------------------------------------------
        var receiptImage = OcrImage.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

        // -------------------------------------------------
        // Step 4: Perform OCR – here we extract text from receipt (English)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);

        // -------------------------------------------------
        // Step 5: Output the recognized plain text
        // -------------------------------------------------
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **İpucu:** Makinenizde birden fazla GPU varsa, `DeviceId` değerini `1`, `2` vb. olarak değiştirerek daha az meşgul kartı seçebilirsiniz. SDK, kimlik aralık dışındaysa net bir `GpuDeviceNotFoundException` fırlatır.

### ### Adım 1: OCR için görüntü yükleme

`OcrImage.FromFile` çağrısı sadece bir bitmap okumaktan daha fazlasını yapar—görüntüyü (düzeltme, ikilileştirme) dahili heuristiklere göre ön‑işlemden geçirir. Bu yüzden **OCR için görüntü yükleme** ayrı bir adımdır: görüntünüz bir veritabanında ise `MemoryStream` ile değiştirebilirsiniz.

```csharp
var receiptImage = OcrImage.FromFile(@"C:\Invoices\receipt.jpg");
```

Bellekte zaten bulunan bir görüntüden **görüntüden metin tanıma** yapmak isterseniz:

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes(@"receipt.jpg")))
{
    var receiptImage = OcrImage.FromStream(ms);
}
```

### ### Adım 2: GPU cihaz kimliğini ve bellek limitlerini ayarlama

GPU kaynakları sınırlıdır. `DeviceId` ve `MaxMemoryMb` özelliklerini açığa çıkararak Aspose, **GPU cihaz kimliğini ayarlama**nı güvenli bir şekilde yapmanıza izin verir; böylece bir süreç tüm kartı tek başına tüketmez.

```csharp
ocrEngine.DeviceId = 0;        // first GPU
ocrEngine.MaxMemoryMb = 1024; // 1 GB ceiling
```

Bellek sınırını aşarsanız, motor otomatik olarak sistem RAM’ine dökülür; bu daha yavaştır ama çökme riskini önler.

### ### Adım 3: Fișten metin çıkarma (görüntüden metin tanıma)

`Recognize` metodu ağır işi yapar. Aspose OCR tarafından desteklenen herhangi bir dili geçebilirsiniz; fişler için genellikle İngilizce yeterlidir, ancak `OcrLanguage.Spanish` ya da özel bir dil paketi de ekleyebilirsiniz.

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);
Console.WriteLine(ocrResult.Text);
```

**Beklenen çıktı** (örnek):

```
Store: QuickMart
Date: 2025-12-01
Total: $23.45
Thank you for shopping!
```

---

## Yaygın Varyasyonlar & Kenar Durumları

| Durum | Değiştirilecek | Neden |
|-----------|----------------|-----|
| **Tek bir görüntüde birden fazla fiş** | Her kırpılmış bölge için `ocrEngine.Recognize` çağırın (`OcrImage.Crop` kullanın) | Motor daha küçük, temiz bir alan gördüğü için doğruluk artar. |
| **Düşük çözünürlüklü taramalar (<150 dpi)** | Tanımadan önce `receiptImage.Resize(2.0)` ile ölçeklendirin | Daha yüksek piksel yoğunluğu GPU’ya daha fazla veri sağlar. |
| **İngilizce dışı fişler** | `OcrLanguage.French` (veya özel bir `.traineddata`) geçin | Dil‑özel modeller yanlış pozitifleri azaltır. |
| **GPU bulunamadığında** | `try‑catch` bloğu içinde `OcrEngine` (CPU) fallback’i yapın | Başsız sunucularda uygulamanın hâlâ çalışmasını garantiler. |

```csharp
try
{
    var gpuEngine = new GpuOcrEngine();
    // configure GPU as shown earlier …
    var result = gpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
catch (GpuDeviceNotFoundException)
{
    // Graceful fallback
    var cpuEngine = new OcrEngine();
    var result = cpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
```

---

## Üretim‑Hazır OCR İçin İpuçları

- **Batch işleme:** Tanıma döngüsünü `Parallel.ForEach` içinde sarın, ancak paralellik derecesini kart başına tahsis edebileceğiniz GPU akışı sayısına (genellikle 1‑2) sınırlayın.
- **Bellek hijyeni:** `OcrImage` nesnelerini hemen `Dispose()` edin (`receiptImage.Dispose()`), özellikle binlerce fiş işliyorsanız.
- **Loglama:** Her satır için `ocrResult.Confidence` değerini yakalayın; düşük güvenilirlik manuel inceleme akışını tetikleyebilir.
- **Güvenlik:** Hassas fişlerle çalışırken görüntü dosyalarının şifreli geçici klasörlerde saklandığından ve işlem sonrası temizlendiğinden emin olun.

---

## Sonuç

Artık **görüntüden metin tanıma** için Aspose OCR’un GPU hızlandırmasıyla **tam, çalıştırılabilir bir örnek** elde ettiniz; **OCR için görüntü yükleme**, **GPU cihaz kimliğini ayarlama** ve son olarak **fişten metin çıkarma** adımlarını birkaç özlü satırda gerçekleştirdiniz. Kod kopyala‑yapıştır için hazır ve açıklamalar, çok‑dilli, çok‑GPU ya da yüksek‑verim senaryolarına uyarlamanız için yeterli bağlamı sağlıyor.

Bir sonraki meydan okumaya hazır mısınız? `GpuOcrEngine` ile canlı video akışı besleyerek gerçek‑zamanlı fiş taraması yapın ya da sonucu bir muhasebe API’sine entegre edin. Hızlı GPU OCR ile temiz C# tasarımını birleştirdiğinizde sınır yoktur.

*İyi kodlamalar, OCR’unuz daima hızlı olsun!*

![recognize text from image demo screenshot](placeholder-image.png "recognize text from image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}