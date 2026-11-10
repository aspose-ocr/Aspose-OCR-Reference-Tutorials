---
category: general
date: 2026-02-09
description: Aspose OCR kullanarak görüntü OCR ön işleme ve metin görüntüsü tanıma
  yöntemlerini öğrenin. Görüntü gürültüsünü azaltın, filtreler ekleyin ve dakikalar
  içinde düz metni çıkarın.
draft: false
keywords:
- preprocess image OCR
- recognize text image
- extract plain text
- reduce image noise
- how to add filters
language: tr
og_description: Görüntü OCR'sini hızlıca ön işleme tabi tutun. Bu kılavuz, filtre
  eklemeyi, görüntü gürültüsünü azaltmayı ve herhangi bir resimden düz metin çıkarmayı
  gösterir.
og_title: C# ile Görüntü OCR Ön İşleme – Adım Adım Öğretici
tags:
- OCR
- C#
- Image Processing
title: C#'ta Görüntü OCR Ön İşleme – Filtrelerle Tam Kılavuz
url: /tr/net/ocr-optimization/preprocess-image-ocr-in-c-complete-guide-with-filters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Görüntü OCR Ön İşleme – Filtrelerle Tam Kılavuz

Tarama dosyalarınız eğri, grenli ya da okunması çok zor olduğu için **görüntü OCR ön işleme** yapmakta zorlandınız mı? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede, bir makbuzun titrek fotoğrafı ya da gürültülü taranmış bir form, OCR motorunun faydalı veri yerine anlamsız karakterler üretmesine neden olabilir.

İyi haber? Bu resimleri motorun içine vermeden önce temizleyebilirsiniz ve **metin görüntüsü tanıma** sırasında sonuç çok daha yüksek bir doğruluk olur. Bu öğreticide **filtrelerin nasıl ekleneceğini**, gürültünün nasıl azaltılacağını ve sonunda Aspose.OCR ile C#'ta **düz metin çıkarma** işlemini adım adım göstereceğiz.

İhtiyacınız olan her şeyi kapsayacağız—kütüphaneyi kurmaktan kodu çalıştırmaya ve çıktıyı doğrulamaya kadar—böylece çalışan bir çözümü hemen kopyalayıp yapıştırabilirsiniz.

---

## İhtiyacınız Olanlar

- **.NET 6+** (veya herhangi bir yeni .NET çalışma zamanı; API aynı şekilde çalışır)
- **Aspose.OCR for .NET** NuGet paketi  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Dönme, gürültü veya düşük kontrast sorunu olan bir örnek görüntü (ör. `skewed_noisy.jpg`)
- Sevdiğiniz bir IDE veya editör (Visual Studio, VS Code, Rider—hangisini tercih ederseniz)

Hepsi bu. Ek yerel kütüphaneler yok, ağır görüntü işleme çerçeveleri yok. Aspose ihtiyacımız olan filtrelerle birlikte gelir.

---

## Adım 1 – OCR Motoru Örneğini Oluşturma  

İlk yaptığınız şey bir `OcrEngine` başlatmaktır. Bunu, resmi temizledikten sonra karakterleri okuyacak beyin olarak düşünün.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;

class FilterExample
{
    static void Main()
    {
        // Initialize the OCR engine – this object will hold our filters and settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Neden önemli?** Motor bir **ön işleme hattı** tutar. Daha sonra filtre eklemek, `Recognize` çağırdığınız her seferde otomatik olarak uygulanır.

## Adım 2 – Görüntü Gürültüsünü Azaltmak ve Okunabilirliği Artırmak İçin Filtreler Ekleme  

Şimdi **filtreler ekliyoruz**. Her bir filtre belirli bir sorunu çözer:

| Filter | Ne Düzeltir | Kullanılan Tipik Değerler |
|--------|-------------|---------------------------|
| `DeskewFilter` | Döndürülmüş metin (eğim) | `MaxAngle = 12` (derece) |
| `DenoiseFilter` | Rastgele lekeler, gren | `Strength = 0.6` (0‑1) |
| `ContrastBoostFilter` | Soluk harfler | `Level = 1.3` (1‑2) |
| `BinarizeAdaptiveFilter` | Düzensiz aydınlatma | varsayılanlar iyi çalışır |

```csharp
        // Step 2: Add preprocessing filters to improve image quality
        //   • Deskew to correct rotation (max 12°)
        //   • Denoise to reduce noise (strength 0.6)
        //   • Contrast boost to enhance visibility (level 1.3)
        //   • Adaptive binarization for better binarization
        ocrEngine.Preprocessing.Add(new DeskewFilter { MaxAngle = 12 });
        ocrEngine.Preprocessing.Add(new DenoiseFilter { Strength = 0.6 });
        ocrEngine.Preprocessing.Add(new ContrastBoostFilter { Level = 1.3 });
        ocrEngine.Preprocessing.Add(new BinarizeAdaptiveFilter());
```

> **İpucu:** Görüntüleriniz zaten dik ise, deskew adımını atlayabilirsiniz. Gereksiz filtreleri kaldırmak işleme süresini hızlandırır.

## Adım 3 – İşlemek İstediğiniz Görüntüyü Yükleyin  

Sonra, motorun temizleyeceği resmi belirtiriz. `ImageStream.FromFile` dosyayı OCR motorunun anlayacağı bir formata okur.

```csharp
        // Step 3: Load the image that needs OCR processing
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **Köşe durum:** Web API'den gelen akışlarla çalışırken, dosya sistemine dokunmamak için `FromFile` yerine `FromStream` kullanın.

## Adım 4 – OCR Motorunu Çalıştırın ve Metin Görüntüsünü Tanıyın  

Şimdi sihir gerçekleşir. Motor eklediğimiz tüm filtreleri uygular, ardından karakter tanıma işlemini yapar.

```csharp
        // Step 4: Run the OCR engine on the prepared image
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Neden işe yarıyor:** Ön işleme hattı, tanıyıcıya verilen görüntünün mümkün olduğunca temiz olmasını sağlar; bu da doğrudan **metin görüntüsü tanıma** doğruluğunu artırır.

## Adım 5 – Düz Metni Çıkarın ve Görüntüleyin  

Son olarak, düz metin sonucunu alır ve konsola yazdırırız. Bu, iş akışının **düz metin çıkarma** kısmıdır.

```csharp
        // Step 5: Output the recognized plain text
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

### Beklenen Çıktı

`skewed_noisy.jpg` basit bir fatura satırı içeriyorsa, örneğin `Total: $123.45`, şu çıktıyı görmelisiniz:

```
Total: $123.45
```

Orijinal dosya 10° döndürülmüş, lekeli ve düşük kontrastlı olsa bile, filtreler OCR motorunun doğru bir şekilde okuması için yeterince temizlemeli.

## Görsel Genel Bakış  

Aşağıda ön işleme hattının hızlı bir illüstrasyonu yer alıyor. Diyagram kodun çalışması için gerekli değildir, ancak akışı görselleştirmeye yardımcı olur.

![ön işleme görüntü OCR diyagramı](https://example.com/ocr-pipeline.png "ön işleme görüntü OCR boru hattı")

*Alt metin: deskew, denoise, contrast boost ve adaptive binarization adımlarını gösteren ön işleme görüntü OCR boru hattı.*

## Sık Sorulan Sorular & Dikkat Edilmesi Gerekenler  

- **OCR sonucu hâlâ karışık çıkarsa ne olur?**  
  `DenoiseFilter.Strength` değerini `0.8`'e yükseltmeyi ya da `ContrastBoostFilter.Level` değerini `1.1`'e düşürmeyi deneyin. Kontrastı aşırı artırmak bazen tanıyıcıyı şaşırtan halo'lar oluşturabilir.

- **Kendi özel filtremi ekleyebilir miyim?**  
  Evet. Aspose.OCR, `IFilter` arayüzünü uygulamanıza ve `ocrEngine.Preprocessing` içine enjekte etmenize izin verir. Bu ileri düzey bir konudur, ancak alan‑spesifik ön işleme ihtiyaçlarınız olduğunda faydalıdır.

- **Bu PDF'lerle çalışır mı?**  
  Sadece her PDF sayfasını önce bir görüntüye (ör. Aspose.PDF kullanarak) dönüştürürseniz çalışır. Bitmap elde ettiğinizde aynı filtre zinciri uygulanır.

- **Kütüphane çoklu iş parçacığı (thread) güvenli mi?**  
  `OcrEngine` örneği **thread‑safe** değildir. Her iş parçacığı için ayrı bir motor oluşturun ya da çağrıları bir kilit (lock) içinde sarın.

## Örneği Genişletme  

Artık sağlam bir temeliniz olduğuna göre, aşağıdaki adımları düşünün:

1. **Toplu işleme** – Bir klasördeki görüntüler üzerinde döngü yapın, aynı filtre zincirini uygulayın ve her sonucu bir `.txt` dosyasına yazın.  
2. **Dil paketleri** – Fransızca veya Almanca tanımanız gerekiyorsa, uygun dil verisini `ocrEngine.Language = "fra"` (veya `"deu"`) ile yükleyin.  
3. **İlgi Bölgesi (ROI)** – Belirli bir alana odaklanmak için `ocrEngine.Recognize(image, new Rectangle(x, y, width, height))` kullanın; bu, büyük taramaları hızlandırabilir.

## Sonuç  

Bu rehberde, bir dizi yerleşik filtre ekleyerek **görüntü OCR ön işleme** yapıyoruz, ardından **metin görüntüsü tanıma** ve sonunda gürültülü, eğik bir resimden **düz metin çıkarma** gerçekleştiriyoruz. Tam ve çalıştırılabilir kod yukarıdadır ve güvenilir OCR sonuçları gerektiren herhangi bir C# projesine uyarlayabilirsiniz.

Unutmayın, iyi bir OCR için anahtar sadece güçlü bir motor değil—temiz bir girdi. Görüntü gürültüsünü azaltarak ve metni doğru hizalayarak tanıyıcıya başarılı olma şansını en üst düzeye çıkarırsınız.

Filtre değerleriyle denemeler yapmaktan, farklı görüntü formatlarını denemekten veya bu yaklaşımı diğer Aspose kütüphaneleriyle birleştirmekten çekinmeyin. Bir sorunla karşılaşırsanız, aşağıya yorum bırakın ya da her bir filtre sınıfı hakkında daha derin bilgi için Aspose'un resmi belgelerine bakın. Kodlamanın tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}