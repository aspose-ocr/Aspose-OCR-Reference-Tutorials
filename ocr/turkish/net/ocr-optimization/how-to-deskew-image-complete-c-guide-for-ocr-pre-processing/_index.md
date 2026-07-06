---
category: general
date: 2026-03-20
description: Aspose OCR ile görüntünün eğriliğini düzeltmeyi ve görüntü gürültüsünü
  kaldırmayı öğrenin. Bu adım adım kılavuz, ayrıca OCR için görüntüyü ön işlemeyi
  ve OCR doğruluğunu artırmayı gösterir.
draft: false
keywords:
- how to deskew image
- remove image noise
- preprocess image for OCR
- recognize text from image
- improve OCR accuracy
language: tr
og_description: Aspose OCR ile görüntüyü düzeltmeyi ve gürültüyü temizlemeyi öğrenin.
  Dakikalar içinde OCR doğruluğunuzu artırın.
og_title: Görüntüyü Nasıl Düzeltiriz – OCR Ön İşleme için Tam C# Rehberi
tags:
- OCR
- C#
- Image Processing
title: Görüntüyü Eğrilikten Düzeltme – OCR Ön İşleme İçin Tam C# Rehberi
url: /tr/net/ocr-optimization/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü Nasıl Düzeltiriz – OCR Ön İşleme için Tam C# Kılavuzu

Bir tarayıcıdan garip bir açıyla çıkan **görüntüyü nasıl düzeltiriz** diye hiç merak ettiniz mi? Tek başınıza değilsiniz; birçok geliştirici bir fotoğrafı OCR motoruna beslemeye çalışırken aynı sorunu yaşıyor. İyi haber şu ki, birkaç satır C# ve Aspose OCR ile bir temiz pipeline içinde görüntüyü düzleştirebilir, gürültüyü azaltabilir ve kontrastı artırabilirsiniz—Photoshop’a gerek yok.

Bu öğreticide, bilmeniz gereken her şeyi adım adım inceleyeceğiz: eğimli bir resmi yüklemekten, **görüntü gürültüsünü kaldırmaya**, **OCR için görüntüyü ön işlemeye**, ve nihayet **görüntüden metin tanımaya** kadar, yüksek bir **OCR doğruluğunu artırma** puanı elde etmeye. Sonunda, dağınık bir taramayı temiz, aranabilir metne dönüştüren, çalıştırmaya hazır bir konsol uygulamanız olacak.

## Gereksinimler

- .NET 6 ve üzeri (kod `using var` sözdizimini kullanır, bu C# 8’den itibaren desteklenir)
- Aspose OCR NuGet paketi (`Aspose.OCR`) – `dotnet add package Aspose.OCR` komutuyla kurun
- Eğimli ve gürültülü bir örnek resim (ör. `skewed_noisy.png`)
- Tercih ettiğiniz bir IDE veya editör (Visual Studio, VS Code, Rider… seçiminiz)

> **Pro ipucu:** Eğer bir örnek dosyanız yoksa, net bir ekran görüntüsünü birkaç derece döndürüp bir görüntü düzenleyiciyle biraz “tuz‑ve‑karabiber” gürültüsü ekleyin. Pipeline aynı şekilde çalışır.

## Adım 1: Deskew Filter ile Görüntüyü Düzeltme

İlk yaptığımız şey dönüşü düzeltmektir. Aspose, yapılandırılabilir bir `MaxAngle` değerine kadar açıları otomatik olarak algılayabilen bir `DeskewFilter` sağlar. Çoğu taranmış belge için güvenli bir varsayılan olan **5°** değerine ayarlamak yeterlidir.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image class

// Initialize the OCR engine – English is the most common language
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};

// Build the preprocessing pipeline
var preprocessPipeline = new PreprocessPipeline()
    .Add(new DeskewFilter { MaxAngle = 5 })          // This is where we answer “how to deskew image”
    .Add(new DespeckleFilter { Strength = 2 })      // Next we’ll remove image noise
    .Add(new ContrastFilter { Level = 1.5 });        // Finally we boost contrast for OCR
```

**Neden önemli:**  
Metin eğimli ise OCR algoritması karakterleri yanlış yorumlayabilir—örneğin “l” harfi “i”ye dönüşebilir. Önce **görüntüyü düzeltmek**, motorun üzerinde çalışacağı düz bir tuval sağlar.

## Adım 2: Despeckle ile Görüntü Gürültüsünü Kaldırma

Ucuz telefonlar veya eski tarayıcılardan gelen taramalar genellikle rastgele noktalara benzeyen lekeler içerir. Bu lekeler karakter tanıyıcıyı karıştırır. `DespeckleFilter`, kenarları koruyarak görüntüyü yumuşatır.

```csharp
// The DespeckleFilter is already part of the pipeline (see Step 1)
// Strength = 2 is a balanced setting; increase for very noisy pics
```

Eğer **görüntü gürültüsünü** daha agresif bir şekilde kaldırmanız gerekiyorsa, `Strength` değerini 3 veya 4'e yükseltin—ancak ince çizgilerin kaybolmasına dikkat edin.

## Adım 3: OCR için Görüntüyü Ön İşleme – Kontrast Artırma

Düşük kontrastlı taramalar (beyaz kağıt üzerinde açık gri) OCR'ın soluk harfleri kaçırmasına neden olabilir. `ContrastFilter`, ton aralığını genişleterek koyu pikselleri daha koyu, açık pikselleri daha açık hale getirir.

```csharp
// Contrast level of 1.5 is a good starting point.
// You can experiment with values between 1.0 (no change) and 2.0 (strong boost).
```

**Köşe durumu:** Kaynak görüntünüz zaten yüksek kontrastlıysa, bu filtreyi uygulamak detayları silkeleyebilir. Bu durumda `Level` değerini `1.0` olarak ayarlayın (pratikte devre dışı bırakır).

## Adım 4: Kaynak Görüntüyü Yükleme ve Temizleme

Şimdi resmi gerçekten yüklüyor ve az önce oluşturduğumuz pipeline’dan geçiriyoruz.

```csharp
// Load the source image – replace the path with your own file location
var sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_noisy.png");

// Apply the entire preprocessing pipeline
var cleanedImage = preprocessPipeline.Apply(sourceImage);
```

> **Not:** `Apply` yöntemi yeni bir `Image` nesnesi döndürür; orijinali dokunulmaz kalır. Bu, süreci hata ayıklamak isterseniz “önce” ve “sonra” karşılaştırmasını kolaylaştırır.

## Adım 5: Aspose OCR Kullanarak Görüntüden Metin Tanıma

Düz, gürültüsüz ve yüksek kontrastlı bir resim elinizde olduğunda, nihayet onu OCR motoruna teslim ediyoruz.

```csharp
// Perform OCR on the cleaned image
var ocrResult = ocrEngine.Recognize(cleanedImage);

// Output the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**Görmeniz gereken:** Konsol, orijinal taramanın metin içeriğini yazdırır; genellikle ham dosyayı doğrudan beslemiş olsanıza göre çok daha az yanlış tanıma olur.

## Adım 6: OCR Doğruluğunu Doğrulama ve İyileştirme

Sağlam bir pipeline olsa bile, bazı karakterler hâlâ hatalı olabilir—özellikle orijinal font alışılmadık ise. İşte **OCR doğruluğunu artırmak** için birkaç hızlı ipucu:

| Sorun | Hızlı Çözüm |
|-------|------------|
| Küçük noktalama işaretleri eksik | Kontrast adımından önce bir `BinaryThresholdFilter` ekleyin |
| Karışık dil (ör. İngilizce + İspanyolca) | `ocrEngine.Language = Language.English \| Language.Spanish;` olarak ayarlayın |
| Çok koyu arka plan | Deskew öncesinde görüntüyü ters çevirin (`new InvertFilter()`) |
| Büyük belgeler | Sayfaları paralel işleyin (`Parallel.ForEach`) hızlandırmak için |

Filtrelerin sırasıyla denemeler yapın; bazen **kontrast**ı **despeckle** öncesinde uygulamak düşük kaliteli taramalarda daha iyi sonuç verir.

## Tam Çalışan Örnek

Aşağıda, yeni bir konsol projesine kopyalayıp yapıştırabileceğiniz tam program bulunmaktadır. Tartıştığımız tüm parçaları ve birkaç güvenlik kontrolünü içerir.

```csharp
// File: Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine (English language)
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // -------------------------------------------------
        // 2️⃣ Build preprocessing pipeline:
        //    Deskew → Despeckle → Contrast Boost
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
            .Add(new DeskewFilter { MaxAngle = 5 })          // how to deskew image
            .Add(new DespeckleFilter { Strength = 2 })      // remove image noise
            .Add(new ContrastFilter { Level = 1.5 });        // preprocess image for OCR

        // -------------------------------------------------
        // 3️⃣ Load the source image (adjust path as needed)
        // -------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/skewed_noisy.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ File not found: {imagePath}");
            return;
        }

        var sourceImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // 4️⃣ Apply the pipeline → cleaned image
        // -------------------------------------------------
        var cleanedImage = preprocessPipeline.Apply(sourceImage);

        // -------------------------------------------------
        // 5️⃣ Recognize text (this is the “recognize text from image” step)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(cleanedImage);

        // -------------------------------------------------
        // 6️⃣ Output the result
        // -------------------------------------------------
        Console.WriteLine("\n=== OCR Output ===\n");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Beklenen çıktı** (örnek görüntünün “Hello World!” içerdiğini varsayarsak):

```
=== OCR Output ===

Hello World!
```

Eğer karışık karakterler görürseniz, pipeline sırasını tekrar kontrol edin ya da `DespeckleFilter.Strength` değerini artırın.

## Sonuç

**Görüntüyü nasıl düzeltiriz**, **görüntü gürültüsünü nasıl kaldırırız**, **OCR için görüntüyü nasıl ön işleriz** ve sonunda Aspose OCR kullanarak **görüntüden metin tanımayı** ele aldık—hepsi de **OCR doğruluğunu artırma** üzerine odaklanarak. Tam, çalıştırılabilir örnek her adımı bağlam içinde gösterir, böylece herhangi bir .NET projesine ekleyip hemen metin çıkarmaya başlayabilirsiniz.

Bir sonraki meydan okumaya hazır mısınız? Pipeline’ı çok sayfalı PDF’leri işlemek için genişletmeyi deneyin ya da çok dilli belgeler için dil paketleriyle deney yapın. Aynı kavramlar geçerli—sadece `Language` bayrağını değiştirin ve belki de ters sayfalar için bir `RotateFilter` ekleyin.

Sorularınız mı var ya da hâlâ işbirliği yapmayan zor bir görüntünüz mü var? Aşağıya bir yorum bırakın, birlikte sorun giderelim. İyi kodlamalar!

![görüntüyü düzeltme örneği](/images/deskew-example.png "Aspose OCR kullanarak görüntüyü nasıl düzeltileceğinin illüstrasyonu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}