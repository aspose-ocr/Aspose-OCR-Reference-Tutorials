---
category: general
date: 2026-04-29
description: Aspose OCR ile görüntünün eğriliğini düzeltme ve OCR doğruluğunu artırma
  – gürültüyü kaldırmayı, görüntü kontrastını artırmayı ve görüntülerden metin çıkarmayı
  öğrenin.
draft: false
keywords:
- how to deskew image
- remove noise from image
- boost image contrast
- extract text from image
- improve ocr accuracy
language: tr
og_description: görüntüyü eğriltmeyi düzeltme ve OCR doğruluğunu artırma. Bu öğreticide,
  görüntüden gürültüyü nasıl kaldıracağınızı, kontrastı nasıl artıracağınızı ve Aspose
  OCR kullanarak görüntüden metni nasıl çıkaracağınızı gösterir.
og_title: Görüntünün eğriliğini düzeltme – Tam Aspose OCR Rehberi
tags:
- Aspose OCR
- C#
- Image preprocessing
title: görüntüyü eğriltmeyi düzeltme – Aspose OCR ön işleme rehberi
url: /tr/net/ocr-optimization/how-to-deskew-image-aspose-ocr-preprocessing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# nasıl görüntüyü düzeltiriz – Tam Aspose OCR Rehberi

Bir OCR motoruna göndermeden önce **how to deskew image** dosyalarının nasıl düzeltileceğini hiç merak ettiniz mi? Tek başınıza değilsiniz. Eğri bir tarama ya da açıyla çekilmiş bir fotoğraf, metin tanımayı bozabilir ve size karışık bir çıktı bırakabilir.  

Bu öğreticide, sadece **how to deskew image** değil, aynı zamanda **remove noise from image**, **boost image contrast** ve nihayetinde Aspose OCR ile **extract text from image** yapan eksiksiz, uçtan uca bir çözümü adım adım inceleyeceğiz. Sonunda **improve OCR accuracy** nasıl artırabileceğinizi belge içinde gezinmeden göreceksiniz.

> **What you’ll get:** hazır‑çalıştırılabilir bir C# konsol uygulaması, her ön işleme adımının net açıklaması ve kendi projelerinize kopyalayıp‑yapıştırabileceğiniz bir dizi pratik ipucu.

## Önkoşullar

- .NET 6.0 veya daha yeni (kod .NET Core ve .NET Framework ile de çalışır)  
- Aspose.OCR NuGet paketi (`Install-Package Aspose.OCR`)  
- Eğik, gürültülü veya düşük kontrastlı bir örnek görüntü (ör. `skewed_noisy.jpg`)  
- Visual Studio, VS Code veya tercih ettiğiniz herhangi bir C# editörü  

Ek yerel kütüphanelere gerek yok – Aspose her şeyi işlem içinde yönetir.

---

## Aspose OCR ile Görüntüyü Nasıl Düzeltiriz

İlk ihtiyacımız, dönüş açısını düzelten bir düzeltme filtresidir. Aspose OCR, metin taban çizgilerini analiz edip bitmap'i buna göre döndüren `FilterDeskew` ile birlikte gelir.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that will later recognize text.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Build an image‑processing pipeline.
        //    The order matters: deskew → denoise → contrast boost.
        ImageProcessingPipeline processingPipeline = new ImageProcessingPipeline();
        processingPipeline.Add(new FilterDeskew());          // ✅ how to deskew image
        processingPipeline.Add(new FilterDenoise());         // ✅ remove noise from image
        processingPipeline.Add(new FilterContrastBoost());   // ✅ boost image contrast

        // 3️⃣ Load your source picture.
        var sourceImage = OcrEngine.LoadImage(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Apply the pipeline – the image is now straight, cleaner, and sharper.
        var processedImage = processingPipeline.Apply(sourceImage);

        // 5️⃣ Run OCR on the cleaned‑up bitmap.
        var ocrResult = ocrEngine.Recognize(processedImage);

        // 6️⃣ Print the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Neden düzeltme ile başlıyoruz:**  
Metin satırları yatay değilse, OCR motoru eğik karakterleri farklı glifler olarak yorumlamaya çalışır ve bu da **improve OCR accuracy**'yi büyük ölçüde düşürür. Düzeltme, taban çizgilerini hizalar ve tanıyıcıya temiz bir tuval sunar.

> *Pro tip:* Dönüş açısını önceden biliyorsanız (ör. tüm taramalar 90° yanlıysa), filtreyi atlayıp manuel olarak döndürebilirsiniz – bu küçük bir performans kazancı sağlar.

---

## Görüntüden Gürültüyü Kaldırma – Tarama Temizliği

Gürültü, rastgele siyah veya beyaz lekeler (klasik “tuz‑ve‑karabiber” deseni) şeklinde ortaya çıkar ve karakter segmentasyonunu karıştırabilir. `FilterDenoise`, kenarları korurken bunları yumuşatan bir medyan filtre uygular.

```csharp
// Inside the pipeline we already added FilterDenoise.
// If you need a custom strength, you can instantiate it like:
var denoise = new FilterDenoise { Strength = 2 }; // 1‑3 are typical values
processingPipeline.Add(denoise);
```

**Gücü ne zaman ayarlamalısınız:**  
- **Strength = 1** – Hafif taneli, hızlı işleme.  
- **Strength = 3** – Çok gürültülü taramalar (ör. faks belgeleri).  

Gücü çok artırmak ince çizgileri bulanıklaştırabilir ve bu da *zarar* **improve OCR accuracy**'ye yol açabilir. Temsilci bir örnek üzerinde birkaç değer test edin.

---

## Görüntü Kontrastını Artırma – Soluk Karakterleri Vurgulama

Düşük kontrastlı görüntüler (solmuş fişler gibi) genellikle OCR motorunun hafif glifleri kaçırmasına neden olur. `FilterContrastBoost`, histogramı genişleterek koyu pikselleri daha koyu, açık pikselleri daha açık hale getirir.

```csharp
var contrast = new FilterContrastBoost { ContrastLevel = 1.5f }; // 1.0 = no change
processingPipeline.Add(contrast);
```

**Neden kontrast önemlidir:**  
Daha yüksek kontrast, sinyal‑gürültü oranını artırır ve Aspose'un sinirsel tanıyıcısının “I” ile “l” arasını ayırt etmesini kolaylaştırır. Ancak, aşırı artırma görüntüyü doygunlaştırabilir, yumuşak geçişleri yapay kenarlara dönüştürebilir. Dengeyi hedefleyin; 1.5‑2.0 iyi bir başlangıç noktasıdır.

---

## Görüntüden Metin Çıkarma – Son OCR Adımı

Şimdi görüntü düz, temiz ve canlı olduğuna göre OCR motoru işini yapabilir. `Recognize` metodu, ham metin, güven skorları ve gerekirse sınırlama kutuları içeren bir `OcrResult` nesnesi döndürür.

```csharp
var ocrResult = ocrEngine.Recognize(processedImage);
Console.WriteLine(ocrResult.Text);
```

**Örnek çıktı** (kaynak görüntünün “Invoice #12345” içerdiğini varsayarsak):

```
=== OCR Output ===
Invoice #12345
Date: 04/28/2026
Total: $1,234.56
```

Eksik karakterler görürseniz, ön işleme hattını tekrar kontrol edin – belki görüntü hâlâ daha güçlü bir gürültü azaltma veya farklı bir kontrast seviyesine ihtiyaç duyuyordur.

*Common question:* “İngilizce dışındaki bir dili tanımam gerekirse ne olur?”  
> `ocrEngine.Language = Language.English;` satırını başka bir desteklenen dile (ör. `Language.French`) ayarlamanız yeterlidir. Ön işleme adımları aynı kalır.

---

## OCR Doğruluğunu Artırma – Ek Ayarlamalar

Mükemmel bir hat bile olsa, birkaç ekstra ayar **improve OCR accuracy**'yi daha da artırabilir:

| İpucu | Ne Zaman Kullanılır | Nasıl |
|-----|--------------|-----|
| **Binary Thresholding** | Çok karanlık veya çok açık taramalar | `processingPipeline.Add(new FilterBinarize());` |
| **Resize Image** | Küçük fontlar (<10 pt) | `processedImage = OcrEngine.Resize(processedImage, 2.0);` |
| **Specify Character Set** | Bilinen alfabe (sadece rakamlar vb.) | `ocrEngine.Characters = "0123456789";` |
| **Multi‑page PDFs** | Toplu işleme | Her sayfayı döngüye alıp aynı hattı yeniden kullanın. |

Unutmayın: her ekstra filtre işleme süresini artırır, bu yüzden sadece gerçekten ihtiyaç duyduğunuzu etkinleştirin.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, derlemeye hazır tüm program yer alıyor. `YOUR_DIRECTORY` ifadesini `skewed_noisy.jpg` dosyasını içeren klasörle değiştirin.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Build preprocessing pipeline
        ImageProcessingPipeline pipeline = new ImageProcessingPipeline();
        pipeline.Add(new FilterDeskew());                     // how to deskew image
        pipeline.Add(new FilterDenoise { Strength = 2 });    // remove noise from image
        pipeline.Add(new FilterContrastBoost { ContrastLevel = 1.8f }); // boost image contrast

        // Load source image
        var sourcePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        var sourceImage = OcrEngine.LoadImage(sourcePath);

        // Apply pipeline
        var cleanImage = pipeline.Apply(sourceImage);

        // Perform OCR
        var result = ocrEngine.Recognize(cleanImage);

        // Output
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

**Beklenen sonuç:** Konsola temiz, düzeltilmiş metin yazdırılır; ham dosyayı doğrudan `ocrEngine.Recognize` ile beslemekten çok daha az tanıma hatası olur.

---

## Sonuç

**how to deskew image**, **remove noise from image**, **boost image contrast** ve sonunda Aspose OCR kullanarak **extract text from image** konularını ele aldık. Bu filtreleri zincirleme uyguladığınızda, özellikle düşük kaliteli taramalarda **improve OCR accuracy**'de belirgin bir artış göreceksiniz.

Bir sonraki meydan okumaya hazır mısınız? Aynı hattı çok sayfalı bir PDF ile deneyin ya da ikilileştirme için özel eşiklerle deney yapın. Aynı prensipler geçerlidir – düzelt, temizle, aydınlat, ardından tanı.

Sorularınız veya tuhaf bir uç durumunuz mu var? Yorum bırakın, birlikte sorun giderelim. Kodlamanın tadını çıkarın!  

![görüntüyü düzeltme örneği](deskew-example.png "görüntüyü düzeltme örneği")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}