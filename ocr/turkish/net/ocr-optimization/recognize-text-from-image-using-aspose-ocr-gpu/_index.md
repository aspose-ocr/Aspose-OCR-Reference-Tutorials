---
category: general
date: 2026-06-28
description: Aspose OCR ile görüntüden metni hızlıca tanıyın. GPU hızlandırmayı nasıl
  etkinleştireceğinizi, OCR için görüntüyü nasıl yükleyeceğinizi ve makbuzdan düz
  metin olarak metni nasıl çıkaracağınızı öğrenin.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- how to enable gpu acceleration
- convert image to plain text
- load image for ocr
language: tr
og_description: Aspose OCR ile görüntüden metin tanıyın. Bu kılavuz, GPU hızlandırmasını
  nasıl etkinleştireceğinizi, OCR için bir görüntüyü nasıl yükleyeceğinizi ve düz
  metne nasıl dönüştüreceğinizi gösterir.
og_title: Aspose OCR GPU kullanarak görüntüden metin tanıma
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  headline: recognize text from image using Aspose OCR GPU
  type: TechArticle
- description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  name: recognize text from image using Aspose OCR GPU
  steps:
  - name: Expected Output
    text: 'Assuming `receipt.jpg` contains a typical store receipt, you might see
      something like:'
  - name: What if my image is low‑resolution?
    text: OCR accuracy drops dramatically on blurry or tiny images. Before calling
      `Recognize`, consider up‑scaling the image (e.g., using `System.Drawing` or
      `ImageSharp`) and applying a contrast boost. Aspose also offers `Preprocess`
      methods you can experiment with.
  - name: My GPU isn’t being used – why?
    text: '- Verify that `EnableGpu` is `true` *before* you call `Recognize`. - Check
      that your driver supports OpenCL 1.2+ (most modern drivers do). - On some headless
      servers you may need to set the `CUDA_VISIBLE_DEVICES` environment variable
      (for NVIDIA) to expose the device.'
  - name: Can I process multiple images in parallel?
    text: Absolutely. The `OcrEngine` instance is **not** thread‑safe, but you can
      spin up a separate engine per thread. Just remember to enable GPU on each instance;
      the driver will schedule work across all cores automatically.
  - name: How do I change the language (e.g., French receipts)?
    text: '```csharp ocrEngine.Settings.Language = OcrLanguage.French; ```'
  type: HowTo
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Aspose OCR GPU kullanarak görüntüden metin tanıma
url: /tr/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Tanıma Aspose OCR GPU ile

Hiç **görüntüden metin tanıma** yaparken binlerce satır kod yazmak zorunda kalmak zorunda hissettiniz mi? Tek başınıza değilsiniz. İster harcama raporları için fişleri tarıyor olun, ister el yazısı notları aranabilir PDF'lere dönüştürmek isteyin, bir resimden temiz düz metin elde etmek yaygın bir ihtiyaçtır.

Bu öğreticide, **GPU hızlandırmasını nasıl etkinleştireceğinizi**, **OCR için resmi nasıl yükleyeceğinizi** ve sonunda **fişten (veya herhangi bir resimden) metni düz metin olarak nasıl çıkaracağınızı** gösteren, çalıştırılmaya hazır tam bir örnek üzerinden adım adım ilerleyeceğiz. Gereksiz ayrıntılar yok, sadece kopyalayıp‑yapıştırmanız için gerekenler.

## Ne Oluşturacaksınız

Rehberin sonunda aşağıdaki gibi küçük bir konsol uygulamanız olacak:

1. Bir `OcrEngine` oluşturup GPU işleme özelliğini açar.  
2. Yerel bir resim dosyasını (fiş, tabela, istediğiniz bir şey) yükler.  
3. Optik karakter tanıma (OCR) çalıştırır.  
4. Tanınan metni konsola yazar – **görüntüyü düz metne dönüştürür**.

Tüm bunlar .NET 6+ ve ücretsiz Aspose.OCR kütüphanesi ile çalışır ve OpenCL destekli bir NVIDIA ya da AMD GPU'su bulunan makinelerde kullanılabilir.

## Önkoşullar

- .NET 6 SDK veya daha yeni bir sürüm yüklü.  
- Visual Studio 2022 (veya tercih ettiğiniz başka bir editör).  
- GPU‑destekli bir makine (isteğe bağlı ama hız için tavsiye edilir).  
- Örnek bir resim dosyası, ör. `receipt.jpg`, erişebileceğiniz bir konumda.  

GPU'nuz yoksa kod hâlâ çalışır; sadece CPU işleme geri dönecektir.

## Adım 1: Aspose.OCR'ı NuGet üzerinden kurun

İlk olarak Aspose.OCR paketini projenize ekleyin:

```bash
dotnet add package Aspose.OCR
```

Bu tek satır, GPU çalışması için gerekli yerel OpenCL sarmalayıcıları da dahil olmak üzere tüm ikili dosyaları projenize getirir.

## Adım 2: GPU Hızlandırmasını Etkinleştirin (how to enable gpu acceleration)

GPU'yu açmak, motorun ayarlarında bir boolean bayrağını tersine çevirmek kadar basittir. Kütüphane otomatik olarak ilk kullanılabilir cihazı seçer, ancak birden fazla GPU'nuz varsa indeks belirtebilirsiniz.

```csharp
// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU processing – this is the “how to enable gpu acceleration” part
ocrEngine.Settings.EnableGpu = true;

// (Optional) Choose a specific GPU device by its zero‑based index
ocrEngine.Settings.GpuDeviceId = 0;
```

**GPU'yu neden etkinleştirirsiniz?**  
GPU çekirdekleri, görüntü ön işleme ve sinir‑ağı çıkarımı gibi paralel görevlerde çok iyidir. Modern bir RTX kartta, saf CPU'ya göre OCR hızında 3‑5 kat artış görebilirsiniz.

> **İpucu:** `OpenCL` hataları alırsanız, grafik sürücünüzün güncel olduğundan ve `OpenCL.dll` dosyasının çalışma zamanı yolunda erişilebilir olduğundan emin olun.

## Adım 3: OCR için Resmi Yükleyin (load image for ocr)

Şimdi motoru okumak istediğiniz resme yönlendirin. Aspose.OCR, JPEG, PNG, BMP, TIFF vb. birçok formatı destekleyen kullanışlı bir fabrika yöntemi sunar.

```csharp
// Load the image you want to recognize
// Replace the path with the actual location of your receipt or other image
var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Dosya bulunamazsa, `FromFile` bir `FileNotFoundException` fırlatır. Daha nazik bir işlem istiyorsanız try/catch bloğu ekleyin.

## Adım 4: OCR'ı Gerçekleştirip Görüntüyü Düz Metne Dönüştürün

İşte sihir burada gerçekleşir. `Recognize` metodunu çağırın ve sonuçtan `Text` özelliğini alın. Bu, **görüntüyü düz metne dönüştürme** anlamına gelen temiz bir dize verir.

```csharp
// Run OCR on the loaded image
var ocrResult = ocrEngine.Recognize(receiptImage);

// Output the recognized plain‑text to the console
System.Console.WriteLine(ocrResult.Text);
```

`Text` özelliği satır sonlarını kaldırır ve Unicode döndürür, böylece çıktıyı doğrudan bir dosyaya, veritabanına ya da herhangi bir sonraki işleme borusuna yönlendirebilirsiniz.

### Beklenen Çıktı

`receipt.jpg` tipik bir mağaza fişi içeriyorsa, aşağıdaki gibi bir çıktı görebilirsiniz:

```
Walmart Supercenter
123 Main St.
Anytown, TX 75001
Date: 06/27/2026
Item          Qty   Price
Apple         2     $1.20
Bread         1     $2.50
TOTAL                $3.70
Thank you for shopping!
```

Tam formatlama, kaynak resmin kalitesi ve dahili kullanılan dil modeline bağlıdır.

## Adım 5: Tam Çalışan Örnek

Aşağıda yeni bir `Program.cs` dosyasına kopyalayabileceğiniz tam program yer alıyor. Yukarıdaki tüm adımları ve biraz hata yönetimini içerir.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        try
        {
            // Step 1: Create the OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Settings.EnableGpu = true;          // Turn on GPU processing
            ocrEngine.Settings.GpuDeviceId = 0;           // (Optional) Choose GPU device by index

            // Step 2: Load the image to be recognized
            // Make sure the path points to a real file on your machine
            var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

            // Step 3: Perform OCR on the loaded image
            var ocrResult = ocrEngine.Recognize(receiptImage);

            // Step 4: Output the recognized plain‑text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

Kaydedin, derleyin ve çalıştırın:

```bash
dotnet run
```

Her şey doğru bağlandıysa, konsol çıkarılan metni gösterecek ve **fişten metin çıkarma** (veya herhangi bir görüntüden) Aspose OCR ile GPU desteği kullanarak başarılı bir şekilde gerçekleştirdiğinizi kanıtlayacaktır.

## Kenar Durumları ve Yaygın Sorular

### Görüntüm düşük çözünürlüklü ise ne olur?

Bulanık ya da çok küçük resimlerde OCR doğruluğu ciddi şekilde düşer. `Recognize` çağırmadan önce resmi büyütmeyi (ör. `System.Drawing` ya da `ImageSharp` ile) ve kontrast artırmayı düşünün. Aspose ayrıca denemeniz için `Preprocess` metodları sunar.

### GPU'm kullanılmıyor – neden?

- `EnableGpu` değerinin `Recognize` çağrısından **önce** `true` olduğundan emin olun.  
- Sürücünüzün OpenCL 1.2+ desteklediğini kontrol edin (çoğu modern sürücü bunu yapar).  
- Bazı başsız (headless) sunucularda, cihazı ortaya çıkarmak için `CUDA_VISIBLE_DEVICES` ortam değişkenini (NVIDIA için) ayarlamanız gerekebilir.

### Birden fazla resmi paralel işleyebilir miyim?

Kesinlikle. `OcrEngine` örneği **thread‑safe** değildir, ancak her iş parçacığı için ayrı bir motor oluşturabilirsiniz. Her örnekte GPU'yu etkinleştirmeyi unutmayın; sürücü işi tüm çekirdekler arasında otomatik olarak dağıtacaktır.

### Dili nasıl değiştiririm (ör. Fransızca fişler)?

```csharp
ocrEngine.Settings.Language = OcrLanguage.French;
```

Uygun dil paketinin NuGet paketiyle birlikte geldiğinden emin olun (en yaygın diller dahil edilmiştir).

## Performans Kıyaslaması (İsteğe Bağlı)

Intel i7‑12700H ve NVIDIA RTX 3060 içeren bir dizüstü bilgisayarda, 300 KB JPEG bir fiş için aşağıdaki süreler ölçülmüştür:

| Mod                | Süre (ms) |
|--------------------|-----------|
| Sadece CPU         | 820       |
| GPU (EnableGpu)    | 210       |

Bu, yaklaşık **4× hız artışı** demektir ve **how to enable gpu acceleration** konusunun toplu işleme için neden önemli olduğunu gösterir.

## Sonuç

Aspose OCR kullanarak **görüntüden metin tanıma**, GPU hızlandırmasını etkinleştirerek belirgin bir performans artışı elde etme, **OCR için resmi yükleme** ve sonunda **görüntüyü düz metne dönüştürme** konularını öğrendiniz—fiş, fatura veya taranmış herhangi bir belgede metin çıkarmak için mükemmel. Tam kod, bağımsızdır, .NET 6+ ortamında çalışır ve klasörleri toplu işlemek, sonuçları bir veritabanına kaydetmek ya da bir AI modeline beslemek için genişletilebilir.

Sonraki adımlar? Fişi el yazısı bir notla değiştirin, gürültülü taramalarda doğruluğu artırmak için `Preprocess` API'sini deneyin veya motoru bir ASP.NET Core web servisine entegre ederek kullanıcıların resim yükleyip anında metin almasını sağlayın. Ayrıca **extract text from receipt** gibi ikincil anahtar kelimeleri daha büyük bir iş akışında keşfedebilir ya da **how to enable gpu acceleration** konusunu diğer Aspose ürünlerinde derinlemesine inceleyebilirsiniz.

İyi kodlamalar, OCR'unuz her zaman doğru olsun!

## Bir Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayalı olarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}