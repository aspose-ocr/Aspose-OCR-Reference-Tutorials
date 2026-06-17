---
category: general
date: 2026-03-18
description: Tarama dosyalarında görüntüyü düzeltme ve gürültüyü azaltma. Dosyadan
  görüntü yüklemeyi, TIFF'ten metin çıkarmayı ve Aspose OCR ile görüntüden metin tanımayı
  öğrenin.
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: tr
og_description: Aspose OCR kullanarak görüntüyü hızlıca düzeltme. Bu kılavuz, gürültüyü
  azaltmayı, görüntüyü dosyadan yüklemeyi ve C#’ta TIFF’ten metin çıkarmayı gösterir.
og_title: Görüntüyü Düzeltme – Tam C# OCR Eğitimi
tags:
- OCR
- C#
- Image Processing
title: Görüntünün Eğriliğini Düzeltme ve Taramaları Temizleme – Tam C# Rehberi
url: /tr/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü Eğrilikten Düzeltme – Tam C# OCR Öğreticisi

Hiç **görüntüyü eğrilikten düzeltme** dosyalarının, sallanan bir tarayıcıdan çekilmiş gibi göründüğünü merak ettiniz mi? Yalnız değilsiniz. Çoğu geliştirici, kaynak TIFF biraz yamuk olduğunda bu soruna takılır ve OCR sonuçları bir karmaşa hâline gelir. İyi haber? Birkaç C# satırıyla resmi düzeltebilir, grenli arka planı bastırabilir ve dosyadan temiz, aranabilir metni doğrudan çıkarabilirsiniz.

Bu rehberde **gürültüyü azaltma**, **dosyadan resmi yükleme** ve sonunda **resimden metin tanıma** işlemlerini Aspose OCR kullanarak adım adım inceleyeceğiz. Sonuna geldiğinizde **tiff'ten metin çıkarma** işlemini zahmetsizce yapabilecek duruma geleceksiniz.

> **Pro tip:** Zaten başka projelerde Aspose OCR kullanıyorsanız, bu filtreleri ekstra lisans derdi olmadan ekleyebilirsiniz.

---

## Gereksinimler

- .NET 6 veya daha yeni (kod .NET Core’da da çalışır)  
- Aspose.OCR NuGet paketi (`Install-Package Aspose.OCR`)  
- Hafifçe döndürülmüş veya gürültülü bir taranmış TIFF (örnek olarak `skewed_scanned_doc.tif` kullanacağız)  
- Bir metin editörü veya IDE (Visual Studio, VS Code, Rider – tercihinize göre)

Ek bir kütüphane gerekmez; kullanacağımız filtreler Aspose OCR içinde yer alır.

---

## Adım 1 – OCR Motorunu Oluşturma (Görüntüyü Eğrilikten Düzeltme)

İlk yapmanız gereken bir `OcrEngine` başlatmak. Bu, karakterleri sizin için daha sonra okuyacak beyin gibi düşünülebilir.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

Motoru önceden oluşturmak neden? Ön işleme filtrelerini, dil paketlerini ve çıktı seçeneklerini tek bir yerde ekleyebilmenizi sağlar. `OcrEngine.Recognize` metodunu doğrudan çağırırsanız, önce resmi temizleme şansını kaçırırsınız; işte bu yüzden eğrilikten düzeltme (deskew) önemli.

---

## Adım 2 – Eğrilikten Düzeltme ve Gürültü Azaltma Filtrelerini Ekleme (Gürültüyü Azaltma)

Şimdi iki filtre ekliyoruz:

| Filtre | Ne yapar | Neden önemlidir |
|--------|----------|-----------------|
| `AutoDeskewFilter` | Döndürmeyi algılar ve düzeltir | Metin satırlarını düzeltir, böylece OCR motoru doğru okuyabilir |
| `NoiseReductionFilterV2` | Lekeleri ve arka plan grenini kaldırır | Temiz pikseller, hatalı tanıma olasılığını azaltır |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

`NoiseReductionFilterV2` yerine eski sürümü de kullanabilirsiniz, ancak v2 algoritması modern tarayıcılarla daha iyi çalışır. Belgeniz zaten tamamen düzse, eğrilikten düzeltme filtresi resmi değişmeden geçirir—hiçbir zarar vermez.

---

## Adım 3 – Dosyadan Resmi Yükleme (Dosyadan Resmi Yükle)

Aspose, TIFF, JPEG, PNG ve BMP dahil çeşitli formatları okuyabilen kullanışlı bir `ImageStream.FromFile` yardımcı metoduna sahiptir. İşte dosyayı belleğe nasıl alacağımız:

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

`YOUR_DIRECTORY` kısmını makinenizdeki gerçek yol ile değiştirin. Göreli bir yol kullanıyorsanız, dosyanın çalıştırılabilir dosyanızın yanına yerleştirildiğinden veya çalışma dizinini buna göre ayarladığınızdan emin olun.

---

## Adım 4 – Ön İşlem Görmüş Resim Üzerinde OCR Çalıştırma (Resimden Metin Tanıma)

Filtreler yüklendi ve resim belleğe alındıktan sonra, Aspose’dan karakterleri okumasını istiyoruz:

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

Motor, arka planda eğrilikten düzeltme algoritmasını çalıştırır, gürültüyü yumuşatır ve ardından sinir‑ağ‑temelli bir tanıyıcıyı devreye sokar. Sonuç, ham metin, güven skorları ve gerekirse sınırlayıcı kutular gibi bilgileri içeren bir `OcrResult` nesnesi içinde paketlenir.

---

## Adım 5 – Çıkarılan Metni Görüntüleme veya Kaydetme (TIFF'ten Metin Çıkarma)

Hızlı bir demo için metni konsola dökebiliriz, ancak bir dosyaya, veritabanına yazabilir veya sonraki bir iş akışına besleyebilirsiniz.

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Beklenen çıktı** (örnek, belgenize göre değişir):

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

Çıktı hâlâ bozuk karakterler içeriyorsa, orijinal TIFF’in çok düşük çözünürlükte olmadığını (minimum 300 dpi önerilir) ve `ocrEngine.Settings.Language` ayarının doğru yapıldığını kontrol edin.

---

## Tam Çalışan Örnek (Tüm Adımlar Tek Bir Yerde)

Aşağıda, yeni bir konsol projesine kopyalayıp hemen çalıştırabileceğiniz tam program yer alıyor.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Dosyayı `Program.cs` olarak kaydedin, `dotnet run` komutunu çalıştırın ve temizlenmiş metnin terminalinizde göründüğünü izleyin.

---

## Sık Sorulan Sorular & Kenar Durumları

### TIFF'im birden fazla sayfa içeriyorsa ne yapmalıyım?
Aspose OCR, `image.GetPages()` (veya `image.Pages`) üzerinden döngü yaparak çok sayfalı görüntüleri işleyebilir. Her sayfa kendi `OcrResult` nesnesini döndürür. Tek bir metin istiyorsanız, sonuçları `StringBuilder` ile birleştirebilirsiniz.

### Eğrilikten düzeltme filtresi çok fazla döndürülmüş görüntülerde çalışır mı?
Filtre, yaklaşık ±15°'e kadar olan döndürmeleri kaldırabilir. Daha büyük açıları işlemek için resmi önce bir grafik kütüphanesi (ör. `System.Drawing` veya `SkiaSharp`) ile manuel olarak döndürmeniz gerekebilir.

### İngilizce dışı metinlerde doğruluğu nasıl artırabilirim?
Dili açıkça ayarlayın:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

Yerleşik paketler alfabetinizi kapsamazsa, özel dil paketleri de yükleyebilirsiniz.

### Bunu Linux üzerinde çalıştırabilir miyim?
Kesinlikle. Aspose OCR platformlar arasıdır; sadece yerel bağımlılıkların (genellikle saf .NET sürümünde yok) mevcut olduğundan emin olun. Kendine özgü bir ikili oluşturmak için `dotnet publish -r linux-x64` komutunu kullanın.

---

## Bonus: Eğrilikten Düzeltmiş Resmi Görselleştirme

OCR’dan önce düzeltilmiş resmi görmek isterseniz, diske geri kaydedebilirsiniz:

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![görüntüyü eğrilikten düzeltme örneği](https://example.com/deskew-demo.png "görüntüyü eğrilikten düzeltme örneği")

*Resim alt metni:* **görüntüyü eğrilikten düzeltme örneği** – AutoDeskewFilter ile düzeltilmiş döndürülmüş bir TIFF’in önce/sonra görüntüsü.

---

## Sonuç

**Görüntüyü eğrilikten düzeltme**, **gürültüyü azaltma**, **resimden metin tanıma**, **dosyadan resmi yükleme** ve **tiff'ten metin çıkarma** adımlarını Aspose OCR ve C# ile ele aldık. Temel çıkarım? Sadece iki ön işleme filtresi eklemek, sarsıntılı ve grenli bir taramayı temiz, aranabilir bir belgeye dönüştürebilir; ek bir araç gerektirmez.

Bir sonraki adım için ne yapacaksınız? Belgeleriniz baş aşağıysa `AutoDeskewFilter` yerine `AutoRotateFilter` deneyin ya da soluk baskılar için `ContrastEnhancementFilter` ile oynayın. Aynı desen—motor → filtreler → yükleme → tanıma—tüm Aspose OCR senaryoları için geçerlidir; bu iskeleti PDF, PNG veya kamera fotoğrafları için de yeniden kullanabilirsiniz.

Kodlamaktan keyif alın, OCR’unuz her zaman doğru olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}