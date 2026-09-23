---
category: general
date: 2026-01-10
description: Aspose.OCR ile görüntüyü düzleştirerek OCR sonuçlarını nasıl iyileştireceğinizi
  öğrenin. OCR için görüntüyü ön işleme, taramadan gürültüyü kaldırma ve taramadan
  metni tanıma.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from scan
- how to use ocr
- remove noise from scan
language: tr
og_description: Görüntüyü nasıl eğriltme düzeltir ve OCR doğruluğunu artırır. Bu kılavuz,
  OCR için görüntüyü ön işleme, taramadan gürültüyü kaldırma ve Aspose.OCR kullanarak
  taramadan metni tanıma yöntemlerini gösterir.
og_title: C#'ta Görüntüyü Düzeltme – Tam OCR Ön İşleme Rehberi
tags:
- OCR
- C#
- Image Processing
title: C#'ta Görüntüyü Düzleştirme – Tam OCR Ön İşleme Rehberi
url: /tr/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Görüntüyü Nasıl Düzeltiriz – Tam OCR Ön İşleme Kılavuzu

Bir OCR motoruna vermeden önce **how to deskew image** dosyalarını nasıl düzelteceğinizi hiç merak ettiniz mi? Tek başınıza değilsiniz. Tarama belgeleri genellikle eğik, gürültülü veya düşük‑kontrastlıdır ve bu, herhangi bir metin‑tanıma girişimini bozar.  

Bu öğreticide, Aspose.OCR kütüphanesini kullanarak **preprocesses image for OCR** yapan, taramadan gürültüyü kaldıran ve sonunda **recognize text from scan** yapan tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, C#'ta **how to use OCR** konusunda net bir anlayışa sahip olacak ve kodu kısa ve öz tutacaksınız.

> **Pro ipucu:** Küçük bir dönüş (5‑10°) bile OCR doğruluğunu %30 'dan fazla düşürebilir. Deskewing, asla atlamamanız gereken ilk adımdır.

---

## Gereksinimler

- **.NET 6+** (kod .NET Framework'te de çalışır, ancak .NET 6 şu anki LTS'dir)
- **Aspose.OCR for .NET** – NuGet'ten alabilirsiniz (`Install-Package Aspose.OCR`)
- Döndürülmüş veya gürültülü bir örnek TIFF/PNG/JPEG (örnekte `noisy_rotated.tif` dosyasını kullanacağız)
- İstediğiniz herhangi bir IDE – Visual Studio, Rider veya VS Code işinizi görecektir

Hepsi bu. Başka kütüphane yok, dış hizmet yok.

## Adım 1 – Kaynak Görüntüyü Yükle (Neden Önemli?)

**deskew image** yapmadan önce, Aspose `ImageStream` içine okumamız gerekir. Bu nesne dosya I/O'yu soyutlar ve OCR motoruna tutarlı bir arayüz sağlar.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the original scan – replace the path with your own file
var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");

// Quick sanity check – make sure the image loaded
if (sourceImage == null)
{
    Console.WriteLine("Failed to load the image. Check the path and file permissions.");
    return;
}
```

*Neden önce yükleyelim?* Çünkü sonraki tüm filtreler bellek içi bir görüntü üzerinde çalışır. Dosya okunamazsa, tüm işlem hattı çöküşe uğrar.

## Adım 2 – Ön‑İşleme Boru Hattı Oluştur (Deskew + Denoise + Contrast)

Sağlam bir OCR iş akışı genellikle birkaç filtreyi zincirler. Burada **preprocesses image for OCR** ve daha da önemlisi **how to deskew image** otomatik olarak gerçekleştiriyoruz.

```csharp
// Create a pipeline that will run three filters in order
var preprocessPipeline = new PreprocessPipeline()
{
    // 1️⃣ DeskewFilter – detects rotation up to 30° and corrects it
    new DeskewFilter { MaxAngle = 30 },

    // 2️⃣ DenoiseFilter – smooths out speckles while keeping edges
    new DenoiseFilter { Strength = 0.8 },

    // 3️⃣ ContrastBoostFilter – makes faint characters pop
    new ContrastBoostFilter { Level = 1.3 }
};
```

**Neden bu üç?**  
- **DeskewFilter**, “how to deskew image” sorununu otomatik olarak çözer; açı tahmin etmenize gerek yoktur.  
- **DenoiseFilter**, “remove noise from scan” gereksinimini ele alır, aksi takdirde hayalet karakterler oluşur.  
- **ContrastBoostFilter**, OCR motorunun koyu metni açık bir arka plandan ayırmasına yardımcı olur; bu, *preprocess image for OCR* yaparken klasik bir sorundur.

## Adım 3 – Boru Hattını Uygula (Dönüşümü Görmek)

Şimdi filtreleri gerçekten çalıştırıyoruz. Dönen `processedImage`, OCR motoruna vereceğimiz şeydir.

```csharp
// Apply all filters – the result is a cleaned‑up bitmap
var processedImage = preprocessPipeline.Apply(sourceImage);

// Optional: Save the cleaned image for visual verification
processedImage.Save("cleaned_output.tif");
Console.WriteLine("Image preprocessing complete – cleaned_output.tif saved.");
```

`cleaned_output.tif` dosyasını açarsanız, metnin düz, daha az grenli ve daha yüksek kontrastlı olduğunu fark edeceksiniz. Bu görsel kontrol, *remove noise from scan* yaptığınızda ve deskew'in çalıştığını doğrulamak istediğinizde kullanışlıdır.

## Adım 4 – OCR Motorunu Oluştur ve Yapılandır (How to Use OCR)

Düzenli bir görüntü elde ettiğimizde, `OcrEngine`'i örnekliyoruz. Bu, Aspose ile **how to use OCR**'un çekirdeğidir.

```csharp
// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    // Assign the pre‑processed image
    Image = processedImage,

    // Optional: Set language (English is default)
    // Language = Language.English,
    
    // Enable automatic page segmentation (helps with multi‑column scans)
    AutoPageSegmentation = true
};
```

*Neden `AutoPageSegmentation` ayarlıyoruz?* Çünkü birçok tarama tablo veya birden çok sütun içerir. Açık tutmak, motorun sayfayı akıllıca bölmesini sağlar ve son **recognize text from scan** sonucunu iyileştirir.

## Adım 5 – Tanıma İşlemini Çalıştır (Sonunda Metni Tanı)

Şimdi gerçek an: motoru metni okumaya istiyoruz.

```csharp
// Kick off the OCR process
ocrEngine.Recognize();

// Retrieve the plain‑text result
string recognizedText = ocrEngine.Text;

// Show the output in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

Eğer her şey sorunsuz ilerlediyse, orijinal belgeyle eşleşen temiz bir metin bloğu göreceksiniz. Bu, doğru şekilde **deskewing image**, **removing noise** ve **preprocessing image for OCR** yapmanın karşılığıdır.

## Adım 6 – Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, derlenmeye hazır tam program yer alıyor. Sadece dosya yolunu değiştirin ve hazırsınız.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");
        if (sourceImage == null)
        {
            Console.WriteLine("Unable to load image. Check the path.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Build the preprocessing pipeline
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
        {
            new DeskewFilter { MaxAngle = 30 },          // how to deskew image
            new DenoiseFilter { Strength = 0.8 },       // remove noise from scan
            new ContrastBoostFilter { Level = 1.3 }      // improves OCR accuracy
        };

        // -------------------------------------------------
        // 3️⃣ Apply the pipeline
        // -------------------------------------------------
        var processedImage = preprocessPipeline.Apply(sourceImage);
        processedImage.Save("cleaned_output.tif");
        Console.WriteLine("Preprocessing finished – cleaned_output.tif saved.");

        // -------------------------------------------------
        // 4️⃣ Configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Image = processedImage,
            AutoPageSegmentation = true   // how to use OCR effectively
        };

        // -------------------------------------------------
        // 5️⃣ Recognize text from scan
        // -------------------------------------------------
        ocrEngine.Recognize();
        string result = ocrEngine.Text;

        Console.WriteLine("\n=== Recognized Text ===");
        Console.WriteLine(result);
    }
}
```

**Beklenen çıktı** (kısaltılmış olarak):

```
=== Recognized Text ===
This is a sample scanned document.
It contains several lines of text,
and the OCR engine has correctly read them.
```

Eğer çıktı bozuk görünüyorsa, kaynak görüntünün 30°'den fazla döndürülmediğini iki kez kontrol edin veya `DeskewFilter.MaxAngle` değerini artırın.

## Sıkça Sorulan Sorular (Köşe Durumları & Varyasyonlar)

| Question | Answer |
|----------|--------|
| **Tarama 45° döndürülmüş olsaydı ne olur?** | `DeskewFilter` `MaxAngle` ile sınırlıdır. Bunu artırın (ör. `MaxAngle = 60`) veya boru hattına vermeden önce bir grafik kütüphanesi ile görüntüyü önceden döndürün. |
| **PDF'leri sayfa‑sayfa işleyebilir miyim?** | Evet. Her PDF sayfasını bir görüntüye dönüştürün (ör. `Aspose.Pdf` kullanarak) ve aynı boru hattını her bitmap üzerinde çalıştırın. |
| **Belgem Fransızca – bir şey değiştirmem gerekir mi?** | `ocrEngine.Language = Language.French;` olarak ayarlayın veya özel bir dil paketi yükleyin. Boru hattının geri kalanı aynı kalır. |
| **Orijinal çözünürlüğü korumanın bir yolu var mı?** | `PreprocessPipeline` orijinal bitmap üzerinde çalışır, DPI'yi korur. Performans için küçültme ihtiyacınız olmadıkça `ImageStream.Resize` çağrısından kaçının. |
| **Kontrast artırma renkli taramaları nasıl etkiler?** | `ContrastBoostFilter` her kanalda çalışır; gri tonlamalı veya renkli görüntüler için güvenlidir, ancak `new GrayscaleFilter()` ile önce gri tonlamaya da dönüştürebilirsiniz. |

## Görsel Örnek (Görsel Yardım)

![how to deskew image örneği](/images/deskew-example.png)

*Resim, 12° döndürülmüş, gürültülü bir taramanın deskew ve temizlenmiş öncesi/sonrası görüntüsünü gösterir.*

## Sonuç

Aspose.OCR kullanarak **how to deskew image** konusunu ele aldık, tam bir **preprocess image for OCR** boru hattını gösterdik, **remove noise from scan** nasıl yapılır gösterdik ve sonunda birkaç C# satırıyla **recognize text from scan** yaptık. `DeskewFilter`, `DenoiseFilter` ve `ContrastBoostFilter`'ı zincirleyerek, OCR motorunun artefaktlarla boğulmadan işini yapmasını sağlayan düzenli bir bitmap elde edersiniz.  

Sonraki adımlar? Farklı filtre güçleriyle denemeler yapın, saf siyah‑beyaz çıktı için bir `BinarizationFilter` ekleyin veya temizlenmiş görüntüyü sonraki bir NLP boru hattına besleyin. Aynı desen makbuzlar, pasaportlar ve tarihi belgeler için de işe yarar.  

Diğer dillerde veya çerçevelerde **how to use OCR** hakkında daha fazla sorunuz mu var? Yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}