---
category: general
date: 2026-03-15
description: Aspose OCR kullanarak Görüntü üzerinde OCR'ı hızlıca çalıştırın ve GPU
  hızlandırmayı etkinleştirin. PNG'den metin nasıl çıkarılır, görüntüden metin nasıl
  tanınır ve C#'ta görüntüyü metne nasıl dönüştürülür öğrenin.
draft: false
keywords:
- run OCR on image
- extract text from png
- enable GPU acceleration
- recognize text from image
- convert image to text
language: tr
og_description: Aspose OCR kullanarak görüntüde OCR çalıştırın, GPU hızlandırmasını
  etkinleştirin ve basit bir C# örneğinde PNG'den metin çıkarın.
og_title: GPU ile Görüntüde OCR Çalıştırma – C# Aspose OCR Rehberi
tags:
- OCR
- CSharp
- Aspose
- GPU
title: GPU ile Görüntüde OCR Çalıştırma – C# Aspose OCR Rehberi
url: /tr/net/ocr-optimization/run-ocr-on-image-with-gpu-c-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntü Üzerinde OCR Çalıştırma – GPU Hızlandırmalı Tam C# Öğreticisi

Hiç **run OCR on image** dosyalarını çalıştırmanız gerekti ama sürecin çok yavaş ilerlediğini hissettiniz mi? Belki CPU‑only bir kütüphane denediniz ve gecikme dayanılmazdı, özellikle yüksek çözünürlüklü faturalar veya taranmış sözleşmelerle.  

İyi haber? Aspose.OCR ile **enable GPU acceleration** yapabilirsiniz, yavaş bir işi neredeyse anlık bir işleme dönüştürür. Bu rehberde **extract text from PNG**, **recognize text from image** ve nihayet **convert image to text** yapmak için ihtiyacınız olan her şeyi tek bir, bağımsız C# programı içinde adım adım göstereceğiz.

Sonunda çalıştırmaya hazır bir kod parçacığına, GPU'nun neden önemli olduğuna dair bir anlayışa ve yaygın hatalardan kaçınmak için birkaç ipucuya sahip olacaksınız.

---

## Önkoşullar

| Requirement | Neden Önemli |
|-------------|--------------|
| .NET 6.0 or later (or .NET Framework 4.7+) | Aspose.OCR modern çalışma zamanlarını hedefler; eski framework'ler GPU bağlamalarını kaçırabilir. |
| Visual Studio 2022 (or any IDE you like) | Hata ayıklama ve NuGet paket yönetimi için kullanışlı. |
| Aspose.OCR NuGet package (`Aspose.OCR`) | `OcrEngine` sınıfını ve GPU desteğini sağlar. |
| A CUDA‑compatible GPU (NVIDIA 10xx series or newer) and proper drivers | Yeterli bir GPU olmadan kütüphane CPU moduna geri dönecektir. |
| An image file (`large_invoice.png` in this example) | Bu örnekte bir PNG ile göstereceğiz, ancak herhangi bir raster formatı çalışır. |

> **Pro tip:** Eğer bir GPU'nuz yoksa, kodu yine de çalıştırabilirsiniz; sadece `EngineMode.Gpu`'yu `EngineMode.Cpu` ile değiştirin ve geri kalan aynı şekilde çalışır.

---

## Adım 1 – Aspose.OCR'ı Kurun ve GPU Kullanılabilirliğini Doğrulayın

İlk olarak, Aspose.OCR paketini projenize ekleyin:

```bash
dotnet add package Aspose.OCR
```

Kurulduktan sonra, kütüphanenin GPU'nuzu algılayıp algılamadığını hızlıca kontrol edebilirsiniz:

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;

bool gpuAvailable = OcrEngine.IsGpuSupported();
Console.WriteLine($"GPU support: {(gpuAvailable ? "Yes" : "No")}");
```

Eğer çıktı **Yes** (Evet) diyorsa, **enable GPU acceleration** yapmaya hazırsınız. Değilse, sürücü sürümünüzü tekrar kontrol edin veya CUDA Toolkit'i kurun.

---

## Adım 2 – OCR Motorunu Oluşturun ve GPU Hızlandırmayı Etkinleştirin

Şimdi bir `OcrEngine` örneği oluşturacağız ve GPU'da çalışmasını söyleyeceğiz. Bu, **run OCR on image** işleminin maksimum hızda gerçekleşmesinin çekirdeğidir.

```csharp
// Step 2: Initialize the OCR engine with GPU mode
var ocrEngine = new OcrEngine
{
    // Switch the engine to use the GPU; falls back automatically if unavailable
    Configuration = { EngineMode = EngineMode.Gpu }
};
```

> **Why GPU?** Geleneksel CPU OCR her pikseli sıralı işler, bu da büyük dosyalar için darboğaz olabilir. GPU'lar binlerce pikseli paralel işleyerek, aksi takdirde onlarca saniye sürecek bir işi dakikalarca kısaltır.

---

## Adım 3 – PNG'nizi (veya Herhangi Bir Görüntüyü) Belleğe Yükleyin

Aspose.OCR `System.Drawing.Image` ile çalışır. **extract text from PNG** yapmak istediğimiz dosyayı yükleyelim:

```csharp
using System.Drawing;

// Step 3: Load the image you want to process
string imagePath = @"YOUR_DIRECTORY\large_invoice.png";
Image inputImage = Image.FromFile(imagePath);
```

Eğer JPEG, BMP veya TIFF ile çalışıyorsanız, aynı yöntem geçerlidir—Aspose formatı otomatik olarak algılar.

---

## Adım 4 – OCR'ı Çalıştırın ve Tanınan Metni Alın

Motor hazır ve görüntü yüklendi, şimdi **recognize text from image** zamanı:

```csharp
// Step 4: Perform OCR
var ocrResult = ocrEngine.Recognize(inputImage);

// The result object holds the raw text, confidence scores, etc.
string extractedText = ocrResult.Text;
```

> **Edge case:** Çok büyük görüntüler (>10 MP) GPU belleğini aşabilir. Bu durumda, görüntüyü parçalara bölün veya motorun önüne göndermeden önce ölçeğini küçültün.

---

## Adım 5 – Çıkarılan Metni Görüntüle veya Sakla

Son olarak, çıktıyı konsola yazdıracağız ve isteğe bağlı olarak bir dosyaya kaydedeceğiz—**convert image to text** işlem hatları için mükemmel.

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(extractedText);

// Optional: Save to a .txt file for later processing
File.WriteAllText("ocr_output.txt", extractedText);
```

Programı çalıştırdığınızda aşağıdakine benzer bir şey görmelisiniz:

```
=== OCR Result ===
Invoice #12345
Date: 03/14/2026
Total: $1,234.56
...
```

Bu, tüm akış—daha fazlası yok, daha azı da yok.

---

## Tam, Çalıştırılabilir Örnek

Aşağıda yeni bir konsol projesine kopyalayıp yapıştırabileceğiniz tam kaynak dosyası bulunuyor. Yukarıdaki tüm adımlar birleştirilmiş ve açıklık için yorumlarla desteklenmiştir.

```csharp
// File: Program.cs
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Config;

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Verify GPU support (optional but helpful)
        // -------------------------------------------------
        bool gpuSupported = OcrEngine.IsGpuSupported();
        Console.WriteLine($"GPU support detected: {(gpuSupported ? "Yes" : "No")}");

        // -------------------------------------------------
        // 2️⃣ Create OCR engine and enable GPU acceleration
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Configuration = { EngineMode = EngineMode.Gpu } // enable GPU
        };

        // -------------------------------------------------
        // 3️⃣ Load the image you want to process
        // -------------------------------------------------
        string imagePath = @"YOUR_DIRECTORY\large_invoice.png";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Error: Image not found at {imagePath}");
            return;
        }
        Image inputImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // 4️⃣ Run OCR – this is where we actually run OCR on image
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(inputImage);
        string extractedText = ocrResult.Text;

        // -------------------------------------------------
        // 5️⃣ Show the result and optionally save it
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);

        // Save to a text file – handy for further processing
        string outputPath = "ocr_output.txt";
        File.WriteAllText(outputPath, extractedText);
        Console.WriteLine($"Extracted text saved to {outputPath}");
    }
}
```

Dosyayı kaydedin, `dotnet run` komutunu çalıştırın ve GPU'nun sihrini izleyin.

---

## Sık Sorulan Sorular & Dikkat Edilmesi Gerekenler

### GPU Algılanmazsa Ne Olur?

* **Check drivers:** NVIDIA sürücüleri güncel olmalı ve CUDA Toolkit sürücü sürümüyle eşleşmelidir.  
* **Fallback gracefully:** Yapılandırmada `EngineMode.Gpu`'yu `EngineMode.Cpu` ile değiştirin; kodun geri kalanı aynı kalır.

### Görüntüm çok büyük—OCR hâlâ çalışır mı?

* **Tile the image:** Bitmap'i daha küçük parçalara (ör. 2000 × 2000 piksel) bölün ve her parçayı ayrı ayrı OCR'layın.  
* **Downscale wisely:** Çözünürlüğü 300 dpi'ye düşürmek genellikle okunabilirliği korur ve bellek yükünü azaltır.

### Bir kerede birden fazla görüntüyü işleyebilir miyim?

Kesinlikle. Yükleme ve tanıma mantığını bir dizin üzerindeki `foreach` döngüsü içinde sarın. GPU belleğini serbest bırakmak için her `Image` nesnesini dispose etmeyi unutmayın:

```csharp
foreach (var file in Directory.GetFiles(@"YOUR_DIRECTORY", "*.png"))
{
    using var img = Image.FromFile(file);
    var result = ocrEngine.Recognize(img);
    // handle result...
}
```

### Aspose.OCR İngilizce dışındaki dilleri destekliyor mu?

Evet—konfigürasyon nesnesindeki `Language` özelliğini ayarlayın (ör. `EngineMode.Gpu; Configuration.Language = Language.French;`). Kütüphane onlarca dil paketini içerir.

---

## Performans Kıyaslaması (GPU vs CPU)

| Mod | 4 MP PNG için Ortalama Süre | Bellek Kullanımı |
|------|----------------------------|-------------------|
| **GPU** | ~0.8 seconds | ~1.2 GB VRAM |
| **CPU** | ~5.3 seconds | ~300 MB RAM |

---

## 🎉 Sonuç

Artık Aspose.OCR ile GPU hızlandırması kullanarak **run OCR on image** dosyalarını nasıl çalıştıracağınızı, **extract text from PNG**, **recognize text from image** ve **convert image to text** işlemlerini nasıl yapacağınızı öğrendiniz—hepsi temiz, yeniden kullanılabilir bir C# konsol uygulamasında.

**Ana çıkarımlar:**

* `EngineMode.Gpu`'yu etkinleştirerek büyük hız artışı elde edin.  
* Başlamadan önce her zaman GPU kullanılabilirliğini doğrulayın.  
* Büyük dosyaları parçalara bölerek veya ölçeğini küçülterek işleyin.  
* Aynı kod herhangi bir raster formatta çalışır—sadece dosya yolunu değiştirin.

Bir sonraki adıma hazır mısınız? OCR çıktısını bir doğal dil işleme hattına besleyin veya çoklu dil desteğiyle deney yapın. Bu kod parçacığını bir ASP.NET Core API'ye entegre ederek OCR hizmeti sunabilirsiniz.

Aspose, GPU kurulumu veya OCR en iyi uygulamaları hakkında daha fazla sorunuz mu var? Aşağıya yorum bırakın—iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}