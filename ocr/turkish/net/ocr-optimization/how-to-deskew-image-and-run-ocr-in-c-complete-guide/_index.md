---
category: general
date: 2026-03-07
description: Aspose OCR kullanarak görüntünün eğriliğini düzeltmeyi, kontrastı artırmayı
  ve taramadan metin çıkarmayı öğrenin. Tam bir C# örneğiyle görüntü üzerinde OCR
  gerçekleştirin ve OCR için görüntüyü kolayca yükleyin.
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: tr
og_description: Aspose OCR'i C#'ta kullanarak görüntüyü eğriltmeyi düzeltmeyi, kontrastı
  artırmayı ve taramadan metin çıkarmayı öğrenin. Görüntü üzerinde adım adım kodla
  OCR gerçekleştirin.
og_title: C#'ta Görüntüyü Eğikliği Düzeltme ve OCR Çalıştırma – Tam Kılavuz
tags:
- C#
- OCR
- Image Processing
title: C#'ta Görüntünün Eğikliğini Düzeltme ve OCR Çalıştırma – Tam Rehber
url: /tr/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü Eğriltmeyi Düzeltme ve C#'ta OCR Çalıştırma – Tam Kılavuz

Eğer OCR çalıştırmadan önce **görüntüyü eğriltmeyi düzeltme** hakkında hiç merak ettiyseniz, doğru yerdesiniz. Bu öğreticide kontrast artırma, OCR için bir görüntüyü yükleme ve sonunda Aspose OCR ile **taramadan metin çıkarma** adımlarını göstereceğiz.  

İster eski makbuzları dijitalleştiriyor olun, taranmış sözleşmeleri temizliyor olun, ya da sadece eğri bir fotoğraftan metin okumanın güvenilir bir yoluna ihtiyacınız olsun, aşağıdaki adımlar ihtiyacınız olan her şeyi kapsıyor. Gereksiz ayrıntı yok—sadece Visual Studio'ya kopyalayıp‑yapıştırabileceğiniz çalışan bir örnek.  

## Başaracaklarınız

* Eğriltmeyi 30°'ye kadar düzeltebilme (bu **görüntüyü eğriltmeyi düzeltme** kısmıdır).  
* Daha keskin karakter kenarları için görüntü kontrastını artırma (**kontrastı artırma**).  
* Resminizi OCR motoruna yükleme (**OCR için görüntü yükleme**).  
* Tanıma sürecini çalıştırma ve **taramadan metin çıkarma**.  

Tüm bunlar, yazı zamanı itibarıyla en son Aspose.OCR .NET NuGet paketi (v23.11) ile çalışır.  

---

![Görüntüyü eğriltmeyi düzeltme örneği](/images/deskew-example.png "görüntüyü eğriltmeyi düzeltme")

*Yukarıdaki görüntü, taranmış bir belgenin eğriltme öncesi ve sonrası halini gösterir.*

## Önkoşullar

* .NET 6.0 veya daha yeni bir sürüm (kod ayrıca .NET Framework 4.7+ üzerinde de çalışır).  
* Visual Studio 2022 (veya tercih ettiğiniz herhangi bir C# IDE).  
* Aspose.OCR NuGet paketi – `dotnet add package Aspose.OCR` komutuyla kurun.  

Hepsi bu. Harici hizmet yok, API anahtarı yok.

---

## Aspose OCR ile Görüntüyü Eğriltmeyi Düzeltme

İlk adım olarak bir **ImageProcessingPipeline** oluşturup `DeskewFilter` ekliyoruz. Bu filtre, baskın metin satırı açısını otomatik olarak algılar ve görüntüyü yataya döndürür.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**Neden önemli:**  
Eğri bir tarama, karakterler artık temel çizgiye hizalanmadığı için OCR motorunu şaşırtır. `DeskewFilter` görüntü histogramını analiz eder, açıyı bulur ve döndürür, tanıma doğruluğunu büyük ölçüde artırır.

> **Pro ipucu:** Belgelerinizin 15°'den fazla eğilmediğini biliyorsanız, işleme hızını artırmak için `MaxAngle = 15` ayarlayın.

---

## Daha İyi Tanıma İçin Kontrastı Artırma

Eğriltmeyi düzelttikten sonra, bir sonraki adım metni öne çıkarmaktır. `ContrastBoostFilter`, piksel yoğunluğu aralığını genişletir; bu, solmuş baskılar için özellikle faydalıdır.

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**Neden yardımcı olur:**  
Düşük kontrastlı taramalar, ikilileştiricinin arka plan olarak yorumlayabileceği gri tonlu karakterler üretir. Kontrastı artırmak, koyu pikselleri daha koyu, açık pikselleri daha açık hale getirir ve sonraki `BinarizationFilter` için daha temiz bir tuval sağlar.

---

## Görüntü Üzerinde OCR Çalıştırma – Dosyayı Yükleme

Görüntü ön‑işlemden geçtiğine göre, **OCR için görüntü yükleme** yapmamız gerekiyor. Aspose, kullanışlı bir `ImageStream.FromFile` yardımcı fonksiyonu sunar.

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Görüntünüz bir akışta (ör. bir web API üzerinden yüklenmiş) bulunuyorsa, bunun yerine `ImageStream.FromStream(yourStream)` kullanabilirsiniz. Motor BMP, JPEG, PNG, TIFF ve daha birçok formatı kabul eder.

---

## Tanıma Sürecini Çalıştırma ve Taramadan Metin Çıkarma

Her şey bağlandıktan sonra, `Recognize()` çağrısı işi halleder. Çağrıdan sonra tanınan metin `ocrEngine.Text` üzerinden erişilebilir.

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**Beklenen çıktı** (basit bir fatura örneği):

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

Çıktı bozuk görünüyorsa, pipeline sırasını iki kez kontrol edin—önce eğriltmeyi düzelt, ardından gürültü azaltma, kontrast artırma ve son olarak ikilileştirme. Sıralamayı değiştirmek sonuçları kötüleştirebilir.

---

## Yaygın Tuzaklar ve Kenar Durumları

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|-------|
| **Boş sonuç** | Görüntü, varsayılan ikilileştirme yöntemi için çok karanlık ya da çok aydınlık. | `ContrastBoostFilter.Strength` değerini artırın veya `BinarizationMethod.Otsu`'ya geçin. |
| **Kısmi metin eksik** | Gürültü, gürültü azaltmadan sonra hâlâ kalıyor. | Daha hafif görüntüler için `DenoiseLevel.Medium` kullanın veya ikinci bir `DenoiseFilter` ekleyin. |
| **Yanlış döndürme yönü** | Belge karışık bir yönlendirmeye sahip (ör. döndürülmüş bir sayfanın fotoğrafı). | `DeskewFilter.MaxAngle` değerini daha düşük ayarlayın ve görüntüyü `ImageProcessor.Rotate` ile önceden döndürün. |
| **Performans yavaşlaması** | Yüksek çözünürlüklü büyük bir görüntü topluluğu. | Pipeline'dan önce görüntüleri (`ImageProcessor.Resize`) küçültün veya paralel işleyin (`Parallel.ForEach`). |

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

`Program.cs` olarak kaydedin, `dotnet run` komutunu çalıştırın ve konsolun **taramadan metin çıkarma** sonucunu yazdırmasını izleyin.  

---

## Sonraki Adımlar ve İlgili Konular

* **Toplu işleme** – Yukarıdaki mantığı bir döngüye sararak onlarca dosyayı işleyin.  
* **Özel dil paketleri** – Latin dışı scriptleri okumak gerekiyorsa, `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;` ile bir dil modeli yükleyin.  
* **PDF çıktısı** – Aspose.PDF'yi OCR ile birleştirerek aranabilir metni doğrudan bir PDF dosyasına gömün.  
* **Performans ayarı** – `ImageProcessingPipeline` sırasını deneyin; bazen gürültü azaltma, eğriltmeyi düzeltmeden önce yapıldığında gürültülü fotoğraflarda daha hızlı sonuç verir.  

Bunların tümü, ele aldığımız temel kavramlar üzerine kuruludur: **görüntüyü eğriltmeyi düzeltme**, **kontrastı artırma**, **OCR için görüntü yükleme**, **görüntü üzerinde OCR çalıştırma** ve sonunda **taramadan metin çıkarma**.

---

## Özet

C#'ta **görüntüyü eğriltmeyi düzeltme** ve OCR çalıştırma için eksiksiz, üretime hazır bir yöntemi yeni gösterdik. Bir eğriltme filtresi, bir gürültü azaltma adımı, bir kontrast artırma ve bir ikilileştiriciyi zincirleyerek, Aspose OCR'nin güvenilir bir şekilde **taramadan metin çıkarma** yapmasını sağlayan temiz bir girdi elde edersiniz.  

Kodu çalıştırın, filtre parametrelerini kendi belgeleriniz için ayarlayın ve tanıma doğruluğunun ne kadar hızlı arttığını görün. Sorularınız mı var? Yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}