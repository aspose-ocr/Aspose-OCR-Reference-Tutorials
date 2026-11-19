---
category: general
date: 2026-05-06
description: Aspose OCR kullanarak görüntüyü düzeltmeyi ve görüntüden metin çıkarmayı
  öğrenin – OCR doğruluğunu artırmak ve görüntüyü gürültüden arındırmak için adım
  adım rehber.
draft: false
keywords:
- how to deskew image
- extract text from image
- how to use OCR
- improve OCR accuracy
- how to denoise image
language: tr
og_description: Aspose OCR ile görüntüyü düzeltmeyi ve görüntüden metin çıkarmayı
  öğrenin. Bu öğreticide, görüntüyü gürültüden arındırmayı ve OCR doğruluğunu artırmayı
  gösterir.
og_title: C# ile Görüntüyü Düzeltme – Tam OCR Rehberi
tags:
- OCR
- C#
- Image Processing
title: C#'ta Görüntüyü Eğikliği Düzeltme – Tam OCR Rehberi
url: /tr/net/ocr-optimization/how-to-deskew-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Görüntüyü Düzeltme – Tam OCR Rehberi

OCR çalıştırmadan önce **görüntüyü nasıl düzeltiriz** gerektiğinde hiç zorlandınız mı, ancak hangi filtreleri uygulayacağınızdan emin değildiniz? Yalnız değilsiniz—birçok geliştirici, kaynak fotoğraf biraz yamuk veya gürültülü olduğunda aynı sorunu yaşıyor. İyi haber? Birkaç C# satırı ve Aspose.OCR ile görüntüyü düzeltebilir, temizleyebilir ve sonunda metni etkileyici bir doğrulukla çıkarabilirsiniz.

Bu öğreticide ihtiyacınız olan her şeyi adım adım göstereceğiz: eğimli bir resmi yükleme, düzeltme ve gürültü giderme filtrelerini uygulama, kontrastı artırma ve sonunda metni çıkarma. Sonunda **OCR nasıl kullanılır** anlayacak, **OCR doğruluğunu nasıl artırılır** görecek ve herhangi bir .NET projesine ekleyebileceğiniz hazır‑çalıştırılabilir bir kod örneğine sahip olacaksınız.

## Gereksinimler

- .NET 6 veya daha yeni (API .NET Core ve .NET Framework ile çalışır)
- Aspose.OCR for .NET (ücretsiz deneme veya lisanslı sürüm) – NuGet üzerinden `Install-Package Aspose.OCR` komutuyla edinebilirsiniz
- Eğik ve biraz gürültülü bir örnek resim (örnek: `skewed_noisy.jpg`)
- Visual Studio, VS Code veya tercih ettiğiniz herhangi bir editör

Ek native kütüphanelere ihtiyaç yok; Aspose her şeyi dahili olarak yönetir.

## Adım 1: Projeyi Kurun ve Aspose.OCR'ı Yükleyin

### Yeni bir konsol uygulaması oluşturun

```bash
dotnet new console -n DeskewOcrDemo
cd DeskewOcrDemo
```

### Aspose.OCR paketini ekleyin

```bash
dotnet add package Aspose.OCR
```

Hepsi bu—projeniz artık OCR motoruna ve ihtiyacımız olan yerleşik filtrelere referans veriyor.

## Adım 2: İşlemek İstediğiniz Görüntüyü Yükleyin

`OcrEngine` örneği oluşturarak ve temizlemek istediğimiz dosyayı işaret ederek başlayacağız.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Step 2: Load the image you want to process
        var ocrEngine = new OcrEngine();
        ocrEngine.SetImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // The rest of the pipeline will be added next…
    }
}
```

> **Neden önemli:** Görüntüyü yüklemek, sonraki tüm filtreler için ilk adımdır. Yol yanlışsa, tüm işlem hattı sessizce başarısız olur, bu yüzden konumu iki kez kontrol edin.

## Adım 3: İşleme Boru Hattı Oluşturun – Düzeltme, Gürültü Giderme, Ardından Kontrastı Artırma

İşte sihrin gerçekleştiği yer. En iyi OCR sonuçlarını veren tam sıralamayla üç filtre ekleyeceğiz:

1. **DeskewFilter** – görüntüyü düzeltir.
2. **MedianDenoiseFilter** – kenarları bulanıklaştırmadan rastgele lekeleri kaldırır.
3. **ContrastStretchFilter** – metin ile arka plan arasındaki farkı artırır.

```csharp
        // Step 3: Build a processing pipeline – deskew, denoise, then enhance contrast
        ocrEngine.Filters.Add(new DeskewFilter());               // how to deskew image
        ocrEngine.Filters.Add(new MedianDenoiseFilter());        // how to denoise image
        ocrEngine.Filters.Add(new ContrastStretchFilter());      // improve OCR accuracy
```

> **Pro ipucu:** Sıra çok önemlidir. İlk olarak düzeltme yapılmalı, çünkü eğik bir görüntü gürültü gidericiyi şaşırtabilir. Görüntü dikleştikten sonra, medyan filtresi tanecikleri temizler ve sonunda kontrast artırma harfleri belirginleştirir.

## Adım 4: OCR Tanıma İşlemini Çalıştırın

Şimdi Aspose'un işi halletmesine izin veriyoruz. `Recognize` metodu, çıkarılan dizeyi ve bazı güven ölçütlerini içeren bir `OcrResult` nesnesi döndürür.

```csharp
        // Step 4: Run the OCR recognition
        var ocrResult = ocrEngine.Recognize();

        // Optional: check confidence (0‑100). Higher means more reliable.
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
```

> **OCR nasıl kullanılır:** `Recognize` çağrısı, eklediğimiz tüm filtreleri dahili olarak uygular, ardından OCR motorunu çalıştırır. Her filtreyi manuel olarak çağırmanıza gerek yok; boru hattı sizin yerinize yapar.

## Adım 5: Tanınan Metni Çıktılayın

Son olarak, metni konsola yazdırıyoruz. Gerçek uygulamalarda muhtemelen bir dosyaya, veritabanına yazdırır veya başka bir servise gönderirsiniz.

```csharp
        // Step 5: Output the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Tam, Çalıştırılabilir Örnek

Hepsini bir araya getirerek, `Program.cs` dosyasına kopyalayıp yapıştırabileceğiniz tam program burada:

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to process
        ocrEngine.SetImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 3️⃣ Build a processing pipeline – deskew, denoise, then enhance contrast
        ocrEngine.Filters.Add(new DeskewFilter());               // how to deskew image
        ocrEngine.Filters.Add(new MedianDenoiseFilter());        // how to denoise image
        ocrEngine.Filters.Add(new ContrastStretchFilter());      // improve OCR accuracy

        // 4️⃣ Run the OCR recognition
        var ocrResult = ocrEngine.Recognize();

        // 5️⃣ Show confidence and extracted text
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Şu komutla çalıştırın:

```bash
dotnet run
```

Orijinal fotoğrafınızdaki içeriğin güven skorunu ve ardından düz metin sürümünü görmelisiniz.

## Sonucu Doğrulama – Ne Beklenir

Kaynak görüntü, örneğin, basılı bir fatura satırı içeriyorsa:

```
Invoice #12345
Total: $1,250.00
Date: 2024‑04‑30
```

Boru hattı çalıştıktan sonra, konsol şu şekilde bir çıktı verir:

```
Confidence: 96%
=== Extracted Text ===
Invoice #12345
Total: $1,250.00
Date: 2024-04-30
```

Yüksek bir güven değeri (genellikle %90’ın üzeri) **görüntüyü nasıl düzeltiriz** ve **görüntüyü nasıl gürültüsüzleştiririz** adımlarının OCR motorunun karakterleri net görmesine yardımcı olduğunu gösterir.

## Yaygın Sorular & Özel Durumlar

### Görüntü 45 dereceden fazla döndürülmüşse ne olur?

`DeskewFilter` açıları otomatik olarak ±45°'e kadar algılar. Daha büyük dönüşler için, düzeltmeden önce `ocrEngine.Filters.Add(new RotateFilter(angle))` kullanarak görüntüyü önceden döndürün.

### Güven değerim düşük—başka ne deneyebilirim?

- **BinarizationFilter** ekleyerek siyah‑beyaz dönüşümünü zorlayın.
- **MedianDenoiseFilter** yarıçapını artırın: `new MedianDenoiseFilter(3)`.
- Daha yüksek çözünürlüklü bir kaynak görüntü kullanın (300 dpi veya daha fazla).

### Bir döngüde birden fazla görüntüyü işleyebilir miyim?

Kesinlikle. Motor oluşturmayı döngünün dışına taşıyın, her dosya için `SetImage` çağırın ve aynı filtre koleksiyonunu yeniden kullanın.

```csharp
foreach (var file in Directory.GetFiles("images", "*.jpg"))
{
    ocrEngine.SetImage(file);
    var result = ocrEngine.Recognize();
    // handle result...
}
```

### Bu PDF'lerde çalışır mı?

Aspose.OCR PDF sayfalarını görüntü olarak okuyabilir, ancak her sayfayı bitmap olarak çıkarmak için Aspose.PDF kütüphanesine ihtiyacınız olacak.

## OCR Doğruluğunu Azamiye Çıkarma İpuçları

1. **Gereksiz kenarları kırpın** – fazla boşluk OCR motorunu şaşırtabilir.
2. **Tekdüzen bir arka plan kullanın** – düz beyaz veya açık gri en iyisidir.
3. **Aşırı aydınlatmadan kaçının** – gölgeler, gürültü giderme filtresinin tam olarak kaldıramayabileceği sahte kenarlar oluşturur.
4. **Gerçek dünyadan örneklerle test edin** – sentetik veriler temiz görünür; üretim görüntüleri genellikle artefaktlar içerir.

## Sonuç

Şimdi **görüntüyü nasıl düzeltiriz**, **görüntüyü nasıl gürültüsüzleştiririz** ve Aspose ile **OCR nasıl kullanılır** akışını **görüntüden metin çıkarma** ve **OCR doğruluğunu artırma** konularını ele aldık. Örnek kod eksiksiz, çalıştırılabilir ve toplu işleme, UI entegrasyonu veya bulut hizmetlerine uyarlamaya hazır.

Sonraki adımlar? `MedianDenoiseFilter` yerine `GaussianDenoiseFilter` kullanarak güven skorlarını karşılaştırın veya çıkarılan metni doğal dil ayrıştırıcısına besleyerek formları otomatik doldurun. Ön işleme boru hattını ustalaştıktan sonra sınır yoktur.

Kodlamaktan keyif alın, ve OCR sonuçlarınız kristal gibi net olsun!

--- 

![görüntüyü nasıl düzeltiriz örneği](/images/deskew-example.png "görüntüyü nasıl düzeltiriz")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}