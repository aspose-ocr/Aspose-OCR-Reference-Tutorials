---
category: general
date: 2026-01-13
description: C#'ta görüntüyü eğriltmeyi düzeltme ve görüntü gürültüsünü kaldırma –
  görüntü kontrastını artırmayı, OCR ön işleme yapmayı ve birden fazla görüntü filtresi
  uygulamayı öğrenin.
draft: false
keywords:
- how to deskew image
- remove image noise
- increase image contrast
- preprocess image ocr
- multiple image filters
language: tr
og_description: C#'ta görüntüyü eğriltmeyi düzeltme ve görüntü gürültüsünü kaldırma
  – görüntü kontrastını artırmayı, OCR ön işleme yapmayı ve birden fazla görüntü filtresi
  uygulamayı öğrenin.
og_title: görüntüyü eğrilikten düzeltme – OCR için Tam C# Ön İşleme Rehberi
tags:
- OCR
- C#
- Image Processing
title: Görüntüyü Eğri Düzeltme – OCR için Tam C# Ön İşleme Rehberi
url: /tr/net/skew-angle-calculation/how-to-deskew-image-complete-c-pre-processing-guide-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to deskew image – Complete C# Pre‑processing Guide for OCR

Hiç **görüntüyü eğik (deskew) nasıl düzelteceğinizi** bir OCR motoruna beslemeden önce merak ettiniz mi? Tek başınıza değilsiniz. Gerçek dünyada—taratılmış sözleşmeler, makbuzlar veya eski fotokopiler—metin hafif bir açıyla durur, resim grenli görünür ve kontrast dengesiz olur. İyi haber? Birkaç satır C# kodu bu eğimi düzeltebilir, görüntü gürültüsünü kaldırabilir ve kontrastı artırabilir, böylece OCR’unuz sağlam bir temele sahip olur.

Bu öğreticide **tam, çalıştırılabilir bir örnek** üzerinden bir görüntüyü nasıl eğik (deskew) düzelteceğinizi, görüntü gürültüsünü nasıl kaldıracağınızı, kontrastı nasıl artıracağınızı ve ardından Aspose.OCR ile OCR çalıştıracağınızı adım adım göstereceğiz. Sonunda, **birden fazla görüntü filtresini** tek bir akıcı çağrıda uygulayan yeniden kullanılabilir bir pipeline’a sahip olacaksınız—tahmin yürütmeye gerek kalmayacak.

## What You’ll Need

- **.NET 6+** (veya herhangi bir yeni .NET sürümü; API aynı şekilde çalışır)
- **Aspose.OCR for .NET** NuGet paketi (`Aspose.OCR` ve `Aspose.OCR.Filters`)
- Eğik, gürültülü ve düşük kontrastlı bir örnek taranmış görüntü (ör. `skewed_noisy.png`)
- Sevdiğiniz IDE (Visual Studio, Rider, VS Code—hangisi rahat geliyorsa)

Eğer zaten bir projeniz varsa, sadece NuGet referansını ekleyin:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Filters
```

> **Pro ipucu:** Aspose, sınırlı sayfa sayısı ile ücretsiz bir deneme sunar—aşağıdaki kodu denemek için mükemmeldir.

## Step 1: Create the OCR Engine Instance

İlk yaptığımız şey bir `OcrEngine` oluşturmak. Bunu, daha sonra metni okuyacak beyin olarak düşünebilirsiniz. Burada karmaşık bir şey yok, ama sonraki tüm adımların temeli budur.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

> **Neden önemli:** Motoru bir kez başlatıp birçok görüntüde yeniden kullanmak, dil verilerini tekrar tekrar yükleme yükünden kaçınmanızı sağlar.

## Step 2: Load the Raw Scanned Image

Şimdi görüntüyü diskteki dosyadan yüklüyoruz. `OcrImage.FromFile` yöntemi dosyayı Aspose’un işleyebileceği bir formata okur.

```csharp
        // Step 2: Load the raw scanned image (skewed, noisy, low‑contrast)
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");
```

> **Köşe durumu:** Görüntünüz standart dışı bir formatta (TIFF, BMP) ise, Aspose yine de bunu işleyebilir, ancak tutarlılık için önce PNG’ye dönüştürmek isteyebilirsiniz.

## Step 3: Build a Pre‑processing Pipeline (Deskew → Denoise → Contrast)

İşte **görüntüyü eğik (deskew) nasıl düzelteceğiniz**, aynı zamanda **görüntü gürültüsünü nasıl kaldıracağınız** ve **görüntü kontrastını nasıl artıracağınız** sorusunun cevabını bulduğumuz yer. Aspose’un akıcı API’si filtreleri zincirlemenize izin verir, böylece kod bir cümle gibi okunur.

```csharp
        // Step 3: Apply Deskew, Denoise, and Contrast filters in one pipeline
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())      // Corrects rotation
            .ApplyFilter(new DenoiseFilter())     // Reduces grainy artifacts
            .ApplyFilter(new ContrastFilter());   // Boosts foreground/background separation
```

### What Each Filter Does

| Filter | Purpose | Typical Impact |
|--------|---------|----------------|
| **DeskewFilter** | Metin satırlarının açısını tespit eder ve görüntüyü yatay hâle getirecek şekilde döndürür. | OCR’ı şaşırtan eğimi ortadan kaldırır, hata oranlarını genellikle %30‑50 azaltır. |
| **DenoiseFilter** | Kenarları korurken rastgele piksel gürültüsünü yok eden bir yumuşatma algoritması uygular. | Tarama makbuzları veya düşük ışıklı fotoğrafları temizler, karakterleri daha net hâle getirir. |
| **ContrastFilter** | Histogramı genişleterek koyu bölgeleri daha koyu, açık bölgeleri daha açık hâle getirir. | Metin ile arka plan arasındaki farkı artırır, özellikle soluk belgelerde faydalıdır. |

> **Neden zincirleme?** Önce eğikliği düzeltmek, denoise filtresinin doğru yönlendirilmiş bir görüntüde çalışmasını sağlar; kontrastı sonradan artırmak ise temizlenmiş metnin OCR motoru için daha belirgin olmasını sağlar.

## Step 4: Perform OCR on the Processed Image

Şimdi görüntü düz, temiz ve yüksek kontrastlı olduğuna göre OCR motoruna veriyoruz. İngilizce dil verisini kullanacağız, ancak Aspose 150’den fazla dili destekler.

```csharp
        // Step 4: Recognize text using the English language pack
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);
```

Başka bir dil gerekiyorsa, sadece `OcrLanguage.English` ifadesini uygun enum değeriyle değiştirin (ör. `OcrLanguage.Spanish`).

## Step 5: Output the Recognized Text

Son olarak sonucu konsola yazdırıyoruz. Gerçek bir uygulamada bir dosyaya, veritabanına ya da sonraki NLP pipeline’larına aktarabilirsiniz.

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Expected Output

Tipik bir eğik makbuz üzerinde tam programı çalıştırdığınızda aşağıdakine benzer bir çıktı alırsınız:

```
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
Thank you for your business!
```

Çıktı bozuk görünüyorsa, orijinal görüntüyü tekrar kontrol edin—aşırı bulanıklık ya da aşırı karanlık ek ön işleme (ör. SharpenFilter) gerektirebilir.

![görüntüyü eğik (deskew) nasıl düzeltebilirsiniz örnek](images/deskewed_example.png "görüntüyü eğik (deskew) nasıl düzeltebilirsiniz – işleme öncesi ve sonrası")

*Yukarıdaki görsel, sol tarafta orijinal eğik taramayı, sağ tarafta ise düzeltilmiş, gürültüsü alınmış ve yüksek kontrastlı hâlini gösterir.*

## Additional Tips & Common Pitfalls

### 1. When the Skew Angle Is Extreme

Belge 30°’den fazla eğilmişse, `DeskewFilter` zorlanabilir. Bu durumda görüntüyü manuel olarak önceden döndürün:

```csharp
var manuallyRotated = rawImage.Rotate(45); // rotates 45 degrees clockwise
var processed = manuallyRotated.ApplyFilter(new DeskewFilter());
```

### 2. Handling Color Images

Filtreler içsel olarak gri tonlamada çalışır, ancak zorla dönüşüm yapabilirsiniz:

```csharp
var grayImage = rawImage.ConvertToGrayscale();
var processed = grayImage.ApplyFilter(new DeskewFilter());
```

### 3. Tuning the Denoise Strength

`DenoiseFilter` isteğe bağlı bir `strength` parametresi alır (0‑100). Daha yüksek değerler daha fazla gürültüyü kaldırır ancak ince detayları da bulanıklaştırabilir.

```csharp
.ApplyFilter(new DenoiseFilter(strength: 70))
```

### 4. Using Multiple Image Filters Beyond the Basics

Aspose, `SharpenFilter`, `BinarizeFilter`, `ResizeFilter` gibi birçok ek filtre sunar. Belirli belge tipinize uygun özel bir pipeline oluşturmak için bunları karıştırıp eşleştirebilirsiniz.

```csharp
var processed = rawImage
    .ApplyFilter(new DeskewFilter())
    .ApplyFilter(new DenoiseFilter())
    .ApplyFilter(new BinarizeFilter())
    .ApplyFilter(new SharpenFilter());
```

## Full Working Example (Copy‑Paste Ready)

Aşağıda, bir konsol projesine yapıştırmaya hazır, tüm program yer alıyor.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Load the original scanned image
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // Build preprocessing pipeline: Deskew → Denoise → Contrast
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())
            .ApplyFilter(new DenoiseFilter())
            .ApplyFilter(new ContrastFilter());

        // Run OCR using English language
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);

        // Output recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

Programı `dotnet run` ile çalıştırın. Her şey doğru kurulduysa, konsol orijinal eğik ve gürültülü görüntünüzden temiz, okunabilir metni gösterecek.

## Conclusion

**Görüntüyü eğik (deskew) nasıl düzelteceğinizi**, aynı zamanda **görüntü gürültüsünü nasıl kaldıracağınızı**, **kontrastı nasıl artıracağınızı** ve **birden fazla görüntü filtresi zinciriyle OCR ön işleme** nasıl yapacağınızı C# ile ele aldık. Temel çıkarım, iyi düzenlenmiş bir ön işleme pipeline’ının OCR doğruluğunu büyük ölçüde artırmasıdır—neredeyse okunamaz bir taramayı tamamen okunabilir metne dönüştürebilir.

Bir sonraki adım için hazır mısınız? `ContrastFilter` yerine `BinarizeFilter` deneyerek ikili (siyah‑beyaz) dönüşümün sonuçlarını görebilir, ya da `ResizeFilter` ile motorun daha yüksek çözünürlüklü bir görüntü almasını sağlayabilirsiniz. Hangi filtreyi seçerseniz seçin aynı desen geçerli, böylece gelecekteki tüm OCR projeleriniz için esnek bir temeliniz olmuş olur.

PDF’lerle, çok‑dilli OCR’la ya da bunu bir ASP.NET API’ye entegre etmekle ilgili sorularınız mı var? Aşağıya yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}