---
category: general
date: 2026-03-26
description: Aspose OCR kullanarak C#'de görüntüyü nasıl düzeltiriz. OCR için görüntüyü
  ön işleme, gürültüyü azaltma ve görüntüden metni verimli bir şekilde tanıma öğrenin.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from image
- how to reduce noise
- how to use aspose
language: tr
og_description: C#'ta Aspose OCR kullanarak görüntünün eğriltmesini nasıl düzelteceğinizi
  öğrenin. OCR için görüntüyü ön işleme, gürültüyü azaltma ve görüntüden metni verimli
  bir şekilde tanıma.
og_title: Aspose OCR ile Görüntüyü Düzleştirme – Tam C# Rehberi
tags:
- Aspose
- OCR
- C#
- Image Processing
title: Aspose OCR ile Görüntüyü Düzeltme – Tam C# Kılavuzu
url: /tr/net/skew-angle-calculation/how-to-deskew-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR ile Görüntüyü Düzleştirme – Tam C# Kılavuzu

Görüntüyü düzleştirme, eğik bir fotoğraftan metin çıkarmaya çalışırken sıkça karşılaşılan bir engeldir. **OCR için görüntü ön işleme** yaparken zorlanmışsanız, **görüntüyü tanıma** aşamasına geçmeden önce **gürültüyü azaltan** temiz ve düz bir dosyanın ne kadar değerli olduğunu bilirsiniz.  

Bu öğreticide, Aspose OCR ile bir filtre hattı oluşturma adımlarını adım adım gösterecek, her filtrenin neden önemli olduğunu açıklayacak ve çıkarılan metni ekrana yazdıran çalıştırmaya hazır bir C# programını sunacağız. “Belgelere bakın” gibi belirsiz bağlantılar yok – ihtiyacınız olan her şey burada.

## Gereksinimler

- **Aspose.OCR for .NET** (en son NuGet paketi, ör. 23.12).  
- .NET 6 veya üzeri (kod .NET Framework 4.8 üzerinde de derlenebilir).  
- Eğik ve gürültülü bir örnek görüntü (biz `skewed_noisy.png` olarak adlandıracağız).  
- Visual Studio, Rider veya tercih ettiğiniz herhangi bir editör – ekstra bir şey gerekmez.

Hepsi bu. Eğer zaten bir projeniz varsa, sadece NuGet referansını ekleyin:

```bash
dotnet add package Aspose.OCR
```

Şimdi başlayalım.

## Görüntüyü Düzleştirme – Filtre Hattını Oluşturma

Çözümün kalbi bir **filtre hattı**dır. Bunu, her filtrenin belirli bir sorunu çözdüğü bir montaj hattı gibi düşünün. Görüntü OCR motoruna ulaşana kadar neredeyse okunmaya hazır hâle gelir.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣  Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣  Assemble a pipeline: deskew → denoise → optional channel filter
        FilterPipeline filterPipeline = new FilterPipeline();
        filterPipeline.Add(new AdaptiveDeskewFilter());               // auto‑corrects rotation
        filterPipeline.Add(new NoiseReductionFilter());              // AI‑based denoise
        filterPipeline.Add(new ColorChannelFilter(Channel.Red));     // focus on the red channel (optional)

        // 3️⃣  Hook the pipeline to the engine
        ocrEngine.Filters = filterPipeline;

        // 4️⃣  Load the image you want to process
        OcrImage inputImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // 5️⃣  Run OCR – the engine will first apply the pipeline
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // 6️⃣  Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Neden işe yarıyor:**  
- `AdaptiveDeskewFilter` görüntünün temel çizgisini analiz eder ve 0°'ye geri döndürür; bu **görüntüyü düzleştirme** adımıdır.  
- `NoiseReductionFilter` hafif bir AI modeli kullanarak lekeleri karakterleri bulanıklaştırmadan yumuşatır—bu da **gürültüyü azaltma** sorusuna yanıt verir.  
- `ColorChannelFilter` isteğe bağlıdır ancak metin belirli bir kanalda (bu örnekte kırmızı) öne çıktığında kullanışlıdır.  

Filtre hattı, OCR motoru pikselleri incelemeden **önce** çalışır, böylece tanıma için daha temiz bir tuval elde edersiniz.

## OCR için Görüntü Ön İşleme – Gürültü Azaltma ve Renk Kanalı

Gürültü azaltma filtresini atlamanız durumunda, özellikle taranmış fişlerde veya düşük ışıklı fotoğraflarda bozuk karakterler görürsünüz. Deneyebileceğiniz hızlı bir örnek:

```csharp
// Swap the order: denoise first, then deskew
filterPipeline = new FilterPipeline();
filterPipeline.Add(new NoiseReductionFilter());
filterPipeline.Add(new AdaptiveDeskewFilter());
ocrEngine.Filters = filterPipeline;
```

Filtre sırasını değiştirerek çalıştırmak, çok grenli görüntülerde biraz daha keskin bir sonuç verebilir. Neden? Önce gürültünün azaltılması, düzleştirme algoritmasına daha temiz bir kenar haritası sağlar.  

**İpucu:** Kaynak görüntüleriniz siyah‑beyaz ise `ColorChannelFilter`'ı tamamen kaldırın. Bu sadece çok az bir ek yük oluşturur.

## Görüntüden Metin Tanıma – OCR Motorunu Çalıştırma

Filtre hattı eklendikten sonra, `Recognize` çağrısı ağır işi yapar. Aspose OCR arka planda şu adımları gerçekleştirir:

1. İkilileştirme (görüntüyü siyah‑beyaza dönüştürür).  
2. Düzen analizi (satırları, sütunları, tabloları algılar).  
3. Karakter segmentasyonu (her glifi ayırır).  
4. Sinir ağı sınıflandırması (glifleri Unicode’a eşler).  

Tüm bunlar modern bir CPU’da birkaç milisaniye içinde gerçekleşir. `OcrResult.Text` özelliği, kaydedilebilecek, indekslenebilecek veya başka bir sisteme beslenebilecek düz bir dize döndürür.

### Beklenen Çıktı

`skewed_noisy.png` içinde “Invoice #12345 – Total $89.99” ifadesi varsa, konsol şu şekilde yazdırır:

```
Invoice #12345 – Total $89.99
```

Ek satır sonları veya garip semboller görürseniz, gürültü seviyesini tekrar kontrol edin; ikinci bir `NoiseReductionFilter` eklemek genellikle yardımcı olur.

## Gürültüyü Azaltma – İpuçları ve Özel Durumlar

- **Birden fazla geçiş:** `filterPipeline.Add(new NoiseReductionFilter());` ifadesini iki kez eklemek, aşırı grenli taramalarda faydalı olabilir.  
- **Eşik ayarı:** Filtre, `Strength` (0‑100) özelliğiyle gelir. Düşük değerler ince detayları korur; yüksek değerler agresif bir şekilde yumuşatır.  
- **Dosya formatı önemi:** PNG kayıpsız veri tutar, JPEG ise sıkıştırma artefaktları ekler ve bu da gürültü azaltıcıyı zorlayabilir. Ön işleme için PNG tercih edin.

```csharp
var heavyNoiseFilter = new NoiseReductionFilter { Strength = 80 };
filterPipeline.Add(heavyNoiseFilter);
```

## Aspose Kullanımı – Kurulum, Lisans ve Dikkat Edilmesi Gerekenler

Aspose ticari bir kütüphanedir, ancak **30 gün** ücretsiz deneme sürümü sunar. Tam özellikleri açmak için:

```csharp
// Somewhere early in your app (e.g., Main)
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

`.lic` dosyasını çalıştırılabilir dosyanızın yanına koyun veya bir kaynak (resource) olarak ekleyin.  

**Yaygın tuzak:** Lisansı ayarlamayı unutmak, tanınan metne bir filigran eklenmesine neden olur. Motor hâlâ çalışır, ancak çıktı “Aspose OCR” satırları içerir.  

Ayrıca, kütüphane **okuma işlemleri için çok iş parçacıklı (thread‑safe)** olsa da, `OcrEngine` nesnesi birden fazla iş parçacığı arasında paylaşılmamalıdır; her istek için yeni bir örnek oluşturun.

## Tam Çalışan Örnek – Hepsini Bir Araya Getirin

Aşağıda, bir konsol uygulamasına kopyalayıp yapıştırabileceğiniz eksiksiz program yer alıyor:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // OPTIONAL: Apply your Aspose license
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Build filter pipeline
        FilterPipeline pipeline = new FilterPipeline();
        pipeline.Add(new AdaptiveDeskewFilter());               // how to deskew image
        pipeline.Add(new NoiseReductionFilter());              // how to reduce noise
        pipeline.Add(new ColorChannelFilter(Channel.Red));     // optional color focus

        // 3️⃣ Attach pipeline
        ocrEngine.Filters = pipeline;

        // 4️⃣ Load image
        string imagePath = @"YOUR_DIRECTORY/skewed_noisy.png";
        OcrImage img = OcrImage.FromFile(imagePath);

        // 5️⃣ Perform OCR
        OcrResult result = ocrEngine.Recognize(img);

        // 6️⃣ Output result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
```

Programı çalıştırın, temizlenmiş metnin konsola yazdırıldığını görmelisiniz. Çıktıyı bir dosyaya kaydetmek isterseniz:

```csharp
System.IO.File.WriteAllText("output.txt", result.Text);
```

## Görsel Sonuç – Öncesi ve Sonrası

Aşağıda, sol tarafta orijinal eğik görüntüyü, sağ tarafta ise düzleştirilmiş ve gürültüsü azaltılmış versiyonu gösteren bir yer tutucu illüstrasyon bulunuyor.

![How to deskew image – before and after processing](https://example.com/deskew-before-after.png "how to deskew image example")

*Alt metin:* how to deskew image – orijinal ve işlenmiş görüntünün görsel karşılaştırması.

## Sonuç

Aspose OCR kullanarak **görüntüyü düzleştirme**, **OCR için görüntü ön işleme** ile gürültü azaltma ve C#’ta **görüntüden metin tanıma** konularını ele aldık. `AdaptiveDeskewFilter`, `NoiseReductionFilter` ve isteğe bağlı `ColorChannelFilter`’ı zincirleyerek, çoğu gerçek dünya fotoğrafında işe yarayan sağlam bir hat elde edersiniz.

Sırada ne var? Kırmızı kanal filtresini şu şekilde değiştirmeyi deneyin:

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}