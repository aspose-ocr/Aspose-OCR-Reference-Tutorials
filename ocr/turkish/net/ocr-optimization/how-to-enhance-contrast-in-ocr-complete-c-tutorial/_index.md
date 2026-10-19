---
category: general
date: 2026-01-04
description: OCR iş akışlarında kontrastı nasıl artıracağınızı ve daha net metin tanıması
  için gürültüyü nasıl kaldıracağınızı öğrenin. Aspose.OCR ile adım adım rehber.
draft: false
keywords:
- how to enhance contrast
- how to create ocr
- how to remove noise
- recognize text image
- preprocess image ocr
language: tr
og_description: OCR boru hatlarında kontrastı nasıl artıracağınızı ve daha net metin
  tanıma için gürültüyü nasıl kaldıracağınızı öğrenin. Aspose.OCR ile adım adım rehber.
og_title: OCR'de Kontrastı Artırma – Tam C# Öğreticisi
tags:
- OCR
- C#
- Image Processing
title: OCR'de Kontrastı Nasıl Artırılır – Tam C# Öğreticisi
url: /tr/net/ocr-optimization/how-to-enhance-contrast-in-ocr-complete-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR'da Kontrastı Artırma – Tam C# Öğreticisi

OCR'da **kontrastı nasıl artıracağınızı** hiç merak ettiniz mi, böylece bulanık bir tarama aniden kristal netliğine kavuşur? Yalnız değilsiniz. Birçok gerçek dünya projesinde, mütevazı bir kontrast artırımı bozuk bir dize ile tamamen okunabilir metin arasındaki fark olabilir.  

Bu rehberde ayrıca **gürültüyü nasıl kaldıracağınızı**, **OCR nasıl oluşturulacağını** ve **metin görüntüsü dosyalarını tanıma** en iyi yollarına değineceğiz. Sonunda, Aspose.OCR kullanarak **görüntü OCR ön işleme** yapan tam, çalıştırılabilir bir örnek elde edeceksiniz ve temiz, yüksek doğruluklu bir sonuç alacaksınız.

## Gereksinimler

- .NET 6+ (or .NET Framework 4.7+)
- Aspose.OCR NuGet paketi (`Aspose.OCR`)
- Eğik, gürültülü veya düşük kontrastlı bir örnek görüntü (örnek: `skewed_noisy.png`)
- Herhangi bir C# IDE (Visual Studio, Rider, VS Code)

Özel bir donanıma gerek yok—sadece birkaç kod satırı ve deneme isteği.

## Adım 1: Aspose.OCR'ı Yükleyin ve Projeyi Kurun

İlk olarak, OCR kütüphanesine ihtiyacımız var. Terminalinizi açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

Bu komut en son sürümü (2026‑01‑04 itibarıyla 23.10) çeker. Yüklendikten sonra, henüz yapmadıysanız yeni bir konsol projesi oluşturun:

```bash
dotnet new console -n OcrContrastDemo
cd OcrContrastDemo
```

Artık kod yazmaya hazırsınız.

## Adım 2: Özel Bir Görüntü İşleme Boru Hattı Oluşturun (Kontrastı Nasıl Artırırsınız)

Gerçek sihir, OCR motoru görüntüyü görmeden önce **kontrastı artırdığımızda** *ve* görüntüyü temizlediğimizde gerçekleşir. Aspose.OCR, bir `ImageProcessingPipeline` içinde filtreleri zincirlemenize izin verir. Aşağıda kullanacağımız tam boru hattı yer alıyor:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;

// 1️⃣ Create a pipeline that deskews, denoises, boosts contrast, and binarizes.
var preprocessingPipeline = new ImageProcessingPipeline()
    // Correct small skew angles (up to 5°)
    .Add(new DeskewFilter { MaxAngle = 5 })
    // Reduce random speckles and grain
    .Add(new DenoiseFilter { Strength = 2 })
    // 🎯 This is the step that **enhances contrast**.
    .Add(new ContrastBoostFilter { Level = 1.5 })
    // Adaptive binarization makes the text pop against the background
    .Add(new AdaptiveBinarizationFilter());
```

**Neden bu sıra?** İlk olarak Deskew, metin satırlarının yatay olmasını sağlar, bu da sonraki kontrast artırımını daha etkili kılar. Kontrasttan önce gürültü giderme, filtrenin gürültüyü artırmasını önler. Son olarak, ikiliye çevirme (binarization), artırılmış görüntüyü OCR'ın sevdiği temiz bir siyah‑beyaz temsile dönüştürür.

> **Pro ipucu:** Kaynak görüntüleriniz zaten iyi hizalanmışsa, `DeskewFilter`'ı atlayarak bir iki milisaniye tasarruf edebilirsiniz.

## Adım 3: OCR Motorunu Boru Hattını Kullanacak Şekilde Yapılandırın (OCR Nasıl Oluşturulur)

Şimdi Aspose.OCR'a bir görüntü yüklediğimizde boru hattımızı otomatik olarak çalıştırmasını söylüyoruz.

```csharp
// 2️⃣ Initialise the OCR engine and attach the pipeline.
var ocrEngine = new OcrEngine();
ocrEngine.Config.ImageProcessingPipeline = preprocessingPipeline;
```

Bu adım **OCR nasıl oluşturulur** sorusuna yanıt verir: sadece `OcrEngine`'i örnekleyip `Config` özelliği aracılığıyla özel boru hattınızı takmanız yeterlidir.

## Adım 4: Görüntüyü Yükleyin ve Tanıma İşlemini Çalıştırın (Metin Görüntüsü Tanıma)

Zorlu bir resmi yükleyelim ve motorun işini yapmasına izin verelim.

```csharp
// 3️⃣ Load the image you want to recognize.
ocrEngine.LoadImage("YOUR_DIRECTORY/skewed_noisy.png");

// 4️⃣ Perform OCR. The pipeline runs automatically.
OcrResult ocrResult = ocrEngine.Recognize();
```

Her şey yolunda giderse, `ocrResult.Text` çıkarılan dizeyi içerecektir.

## Adım 5: Çıkarılan Metni Görüntüleyin

Hızlı bir konsol çıktısı, sonucu doğrulamanızı sağlar:

```csharp
// 5️⃣ Show the result.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

### Beklenen Çıktı

```
=== OCR Output ===
The quick brown fox jumps over the lazy dog.
```

Elbette gerçek metniniz farklı olacaktır, ancak kontrast artırımı ve gürültü giderme adımları olmadan gördüğünüzden çok daha az bozuk karakter görmelisiniz.

## Tam, Çalıştırılabilir Örnek

Aşağıda `Program.cs` dosyasına kopyalayıp yapıştırabileceğiniz **tam program** yer alıyor. Yukarıdaki tüm adımları ve birkaç yararlı yorumu içerir.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;

namespace OcrContrastDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Build a preprocessing pipeline
            // -------------------------------------------------
            var preprocessingPipeline = new ImageProcessingPipeline()
                .Add(new DeskewFilter { MaxAngle = 5 })          // correct small skew angles
                .Add(new DenoiseFilter { Strength = 2 })        // reduce noise (how to remove noise)
                .Add(new ContrastBoostFilter { Level = 1.5 })   // enhance contrast (how to enhance contrast)
                .Add(new AdaptiveBinarizationFilter());         // improve binarization

            // -------------------------------------------------
            // Step 2: Configure the OCR engine (how to create OCR)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                Config = { ImageProcessingPipeline = preprocessingPipeline }
            };

            // -------------------------------------------------
            // Step 3: Load the image you want to recognize
            // -------------------------------------------------
            // Replace with your actual path
            string imagePath = "YOUR_DIRECTORY/skewed_noisy.png";
            ocrEngine.LoadImage(imagePath);

            // -------------------------------------------------
            // Step 4: Run OCR (recognize text image)
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Output the extracted text
            // -------------------------------------------------
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

Dosyayı kaydedin, `dotnet run` komutunu çalıştırın ve sihrin gerçekleşmesini izleyin.

## Yaygın Sorular ve Kenar Durumları

### Görüntü zaten yüksek kontrastlıysa ne olur?

`ContrastBoostFilter`'ın `Level` özelliğini (ör. `0.8`) düşürebilir veya filtreyi tamamen kaldırabilirsiniz. Aşırı artırma beyazları doygunlaştırabilir ve detayları kırpabilir.

### Çok sayfalı PDF'leri nasıl yönetirim?

Aspose.OCR, PDF sayfalarını tek tek yükleyebilir. Her sayfayı döngüye alıp aynı boru hattını uygular ve sonuçları birleştirirsiniz. Bu, **görüntü OCR ön işleme** iş akışının doğal bir uzantısıdır.

### Görüntüm Aspose.OCR'un tanımadığı bir formatta mı?

Önce `System.Drawing` veya `ImageSharp` kullanarak dönüştürün:

```csharp
using SixLabors.ImageSharp;
using SixLabors.ImageSharp.Formats.Png;

// Load any format, then save as PNG for OCR
using var img = Image.Load("input.tiff");
img.Save("temp.png", new PngEncoder());
ocrEngine.LoadImage("temp.png");
```

### Boru hattı çoklu iş parçacığı (thread) güvenli mi?

Her `OcrEngine` örneği bağımsızdır, bu yüzden farklı iş parçacıklarında birden fazla motor başlatabilirsiniz. Tek yapmanız gereken aynı motoru iş parçacıkları arasında paylaşmamaktır.

## Daha İyi Sonuçlar İçin İpuçları (Gürültüyü Etkili Şekilde Nasıl Kaldırılır)

- **Denoise Gücünü Ayarlayın**: `Strength = 1` hafiftir; `Strength = 3` agresiftir. Veri kümenizin bir alt kümesinde test edin.
- **Filtreleri Birleştirin**: Ağır bozulmuş taramalar için `DenoiseFilter`'dan önce bir `MedianFilter` eklemeyi düşünün.
- **OCR'dan Önce Yeniden Boyutlandırın**: Düşük çözünürlüklü bir görüntüyü (ör. 2×) büyütmek bazen karakter şekli algılamasını iyileştirebilir, ancak eklenen artefaktlara dikkat edin.

## Görsel Özet

![OCR ön işleme sırasında kontrastı artırma](/images/ocr-contrast-pipeline.png "Kontrastı artıran, gürültüyü kaldıran ve görüntüyü OCR için hazırlayan görüntü‑işleme boru hattının illüstrasyonu")

*Şema, ham girdi → deskew → denoise → contrast boost → binarization → OCR akışını gösterir.*

## Sonuç

Bir OCR boru hattında **kontrastı nasıl artıracağınızı** adım adım inceledik, **gürültüyü nasıl kaldıracağınızı** gösterdik ve sıfırdan bir **OCR nasıl oluşturulur** çözümü geliştirdik. `DeskewFilter`, `DenoiseFilter`, `ContrastBoostFilter` ve `AdaptiveBinarizationFilter`'ı zincirleyerek, `recognize text image` işlemlerinin doğruluğunu büyük ölçüde artıran sağlam bir **görüntü OCR ön işleme** iş akışı elde edersiniz.

Denemekten çekinmeyin—filtre parametrelerini ayarlayın, diğer Aspose filtreleriyle değiştirin veya bu kodu daha büyük bir belge‑yutma hizmetine entegre edin. Burada öğrendiğiniz kavramlar, makbuz tarama, pasaport işleme veya aranabilir bir arşiv oluşturma gibi herhangi bir .NET OCR senaryosunda taşınabilir.

Daha fazla sorunuz mu var? Bir yorum bırakın, “Aspose ile Toplu OCR” sonraki öğreticisini deneyin veya dil paketleri ve özel sözlükler gibi gelişmiş özellikler için resmi Aspose.OCR belgelerini inceleyin. Kodlamaktan keyif alın ve OCR sonuçlarınızdaki yeni netliğin tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}