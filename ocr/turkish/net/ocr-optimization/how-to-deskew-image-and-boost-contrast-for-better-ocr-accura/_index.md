---
category: general
date: 2025-12-30
description: Görüntüyü hızlı bir şekilde eğriltmeyi düzeltmeyi ve OCR doğruluğunu
  artırmak için görüntüden metin çıkarırken kontrastı nasıl artıracağınızı öğrenin.
draft: false
keywords:
- how to deskew image
- how to boost contrast
- extract text from image
- recognize text image
- improve ocr accuracy
language: tr
og_description: Görüntüyü hızlıca eğriltmeyi düzeltme ve görüntüden metin çıkarırken
  kontrastı artırmayı öğrenerek OCR doğruluğunu artırma.
og_title: Görüntüyü Düzeltme ve Kontrastı Artırma ile Daha İyi OCR Doğruluğu
tags:
- OCR
- C#
- Image Processing
title: Görüntüyü Düzleştirip Kontrastı Artırarak OCR Doğruluğunu Nasıl Artırırsınız
url: /tr/net/ocr-optimization/how-to-deskew-image-and-boost-contrast-for-better-ocr-accura/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü Düzleştirme ve Kontrastı Artırma ile Daha İyi OCR Doğruluğu

Bir tarayıcı ya da akıllı telefondan gelen **how to deskew image** dosyalarını merak ettiniz mi?  
Yalnız değilsiniz—çoğu geliştirici, kaynak resim biraz eğik ya da gürültülü olduğunda bu soruna takılır ve OCR çıktısı karışık bir karmaşa hâline gelir.  

İyi haber şu ki, birkaç C# satırıyla resmi düzleştirebilir, arka planı temizleyebilir ve hatta kontrastı artırarak motorun metni bir profesyonel gibi okumasını sağlayabilirsiniz. Bu rehberde ayrıca **extract text from image** dosyalarını ve **recognize text image** içeriğini Aspose.OCR ile nasıl kullanacağınızı göstereceğiz, tüm bunları **improve OCR accuracy** hedefiyle yapacağız.

## İhtiyacınız Olanlar

- **.NET 6.0** veya daha yeni (kod .NET Framework 4.7+ üzerinde de derlenir)  
- **Aspose.OCR** NuGet paketi (versiyon 23.12 veya daha yeni) – `dotnet add package Aspose.OCR` komutuyla kurun  
- Döndürülmüş ve gürültülü bir örnek resim (ör. `noisy_rotated.jpg`)  
- Visual Studio, VS Code veya tercih ettiğiniz herhangi bir IDE  

Bu kadar—ekstra yerel kütüphane yok, ağır OpenCV bağlamaları yok. Sadece saf yönetilen kod.

---

## Adım 1: Projeyi Kurun ve Ad Alanlarını İçe Aktarın

İlk olarak, yeni bir konsol uygulaması oluşturun ve gerekli ad alanlarını kapsam içine alın. Bu adım, sonraki tüm işlemlerin temelini oluşturur.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later
        }
    }
}
```

**Neden Bu Önemli:**  
`Aspose.OCR` size `OcrEngine` sınıfını verir, `Aspose.OCR.Filters` ise `DeskewFilter` ve `ContrastBoostFilter` gibi kullanışlı ön‑işleme filtreleri sağlar. Bunları önceden içe aktarmak kodu düzenli tutar ve derleyiciye neyi kullanmak istediğimizi bildirir.

---

## Adım 2: OCR Motorunu Başlatın ve Deskew Filter Ekleyin

Şimdi gerçekten **how to deskew image** yapıyoruz. `DeskewFilter` döndürme açısını otomatik olarak algılar (belirlediğiniz maksimuma kadar) ve bitmap'i yatay konuma geri döndürür.

```csharp
// Inside Main()
var ocrEngine = new OcrEngine();

// Deskew: correct up to 15 degrees of rotation
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
```

**Arka Planda Ne Oluyor?**  
Filtre, görüntüyü en uzun yatay metin satırı için tarar, eğimi tahmin eder ve ters bir dönüşüm uygular. `MaxAngle` değerini 15° ile sınırlayarak zaten düz olan görüntüleri aşırı düzeltmekten kaçınırız.

> **Pro tip:** Kaynak görüntüleriniz ters olabilir, `MaxAngle` değerini 180°'ye çıkarın—filtre hâlâ doğru yönelimi bulacaktır.

---

## Adım 3: Denoise Filter ile Gürültüyü Azaltın

Gürültülü bir tarama, en akıllı OCR motorunu bile yanıltabilir. `DenoiseFilter` eklemek, ince detayları silmeden lekeleri yumuşatır.

```csharp
// Denoise: strength ranges from 0 (off) to 1 (max)
ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });
```

**Neden İhtiyacınız Var:**  
Gürültü, OCR algoritmasının karakter olarak yorumladığı sahte kenarlar oluşturur. `0.7` gücü, çoğu taranmış belge için ideal bir noktadır; çok temiz ya da çok kirli girdiler için serbestçe ayarlayabilirsiniz.

---

## Adım 4: Kontrastı Artırma – “How to Boost Contrast” Uygulaması

Burada ikincil anahtar kelime **how to boost contrast**'a yanıt veriyoruz. `ContrastBoostFilter`, koyu metin ile açık arka plan arasındaki farkı artırarak harfleri öne çıkarır.

```csharp
// Contrast boost: level > 1 increases contrast
ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });
```

**Mantık:**  
Daha yüksek kontrast, hafif çizgilerin kaçırılma ihtimalini azaltır. `1.3` seviyesi tipik siyah‑beyaz belgeler için iyi çalışır; renkli fotoğraflar için `1.5` veya daha fazlasına ihtiyaç duyabilirsiniz.

---

## Adım 5: OCR'ı Çalıştırın ve Metni Çıkarın

Görüntü ön‑işlemden geçirildikten sonra, `Recognize` metodunu kullanarak nihayet **extract text from image** yapıyoruz. Metot, ham dize ve güven skorlarını içeren bir `OcrResult` nesnesi döndürür.

```csharp
// Perform OCR on the prepared image
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/noisy_rotated.jpg");

// Output the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**Elde Ettikleriniz:**  
`ocrResult.Text`, motorun okuyabildiği her şeyin düz metin temsilini tutar. Kelime‑düzeyinde güven ihtiyacınız varsa, `ocrResult.Regions`'ı inceleyin—her bölge bir `Confidence` özelliği içerir.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, `Program.cs` dosyasına ekleyebileceğiniz tam program yer alıyor. Görüntü yolunun makinenizdeki gerçek bir dosyaya işaret ettiğinden emin olun.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Deskew – correct up to 15° rotation
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

            // 3️⃣ Denoise – smooth out speckles (strength 0.7)
            ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });

            // 4️⃣ Contrast boost – make text pop (level 1.3)
            ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });

            // 5️⃣ Recognize the image
            var imagePath = @"YOUR_DIRECTORY\noisy_rotated.jpg";
            var ocrResult = ocrEngine.Recognize(imagePath);

            // 6️⃣ Show the result
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Beklenen çıktı (örnek):**

```
=== OCR Output ===
Invoice #12345
Date: 2024-09-30
Total Amount: $1,250.00
Thank you for your business!
```

Sonuç karışık görünüyorsa, görüntü kalitesini tekrar kontrol edin, `Strength` veya `Level` değerlerini ayarlayın, ya da daha agresif bir düzleştirme için `MaxAngle`'ı artırın.

---

## Sık Sorulan Sorular & Kenar Durumları

### Görüntü ters olursa ne olur?

`DeskewFilter` içinde `MaxAngle = 180` olarak ayarlayın. Filtre 180° dönüşümünü algılayıp doğru şekilde döndürecektir.

### Belgem renkli (ör. mavi vurgulu taranmış bir form).

Kontrast artırmadan önce bir `ColorFilter` eklemeyi deneyin, ya da görüntüyü manuel olarak gri tonlamaya dönüştürün:

```csharp
ocrEngine.Filters.Add(new GrayscaleFilter());
```

### Birçok dosyayı toplu olarak işlemek istiyorum.

OCR mantığını bir dizinde dolaşan `foreach` döngüsüyle sarın:

```csharp
foreach (var file in Directory.GetFiles(@"C:\Scans", "*.jpg"))
{
    var result = ocrEngine.Recognize(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
}
```

### OCR güvenini nasıl öğrenebilirim?

`ocrResult.Regions`'ı inceleyin:

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"Text: {region.Text} – Confidence: {region.Confidence:P2}");
}
```

Daha yüksek güven değerleri (100% yakın) genellikle ön‑işleme adımlarının başarılı olduğunu gösterir.

---

## OCR Doğruluğunu Azamiye Çıkarmak İçin İpuçları

| İpucu | Neden Yardımcı Olur |
|-----|--------------|
| **Lossless görüntü formatları kullanın** (PNG, TIFF) | JPEG sıkıştırması kenarları bulanıklaştırabilir, tanıma zarar verir. |
| **DPI'yi 300+ tutun** | Karakter başına daha fazla piksel, motorun daha fazla veri elde etmesini sağlar. |
| **Alakasız kenar boşluklarını kırpın** | Gürültüyü azaltır ve işleme hızını artırır. |
| **Kontrast artırdıktan sonra ikili eşik uygulayın** (siyah/beyaz) saf metin belgeleri için | Görüntüyü iki renge sadeleştirir, çoğu OCR motoru bunu sever. |
| **Önce küçük bir örnekle test edin** | `Strength` ve `Level`'ı ölçeklendirmeden önce ince ayar yapmanızı sağlar. |

---

## Sonuç

Aspose.OCR kullanarak **how to deskew image** dosyalarını, **how to boost contrast**'i ve **extract text from image** tam sürecini ele aldık. `Recognize` metodundan önce bir `DeskewFilter`, `DenoiseFilter` ve `ContrastBoostFilter` zinciri ekleyerek, çoğu gerçek dünya taramasında **improve OCR accuracy**'de belirgin bir artış fark edeceksiniz.  

Kodu çalıştırın, filtre parametrelerini kendi belge özelliklerinize göre ayarlayın ve en dağınık fotoğraflardan bile temiz metin elde edin. Daha ileri gitmek mi istiyorsunuz? Dil‑spesifik sözlükler ekleyin ya da çıktıyı bir yazım denetleyicisine besleyerek son işleme yapın.  

İyi kodlamalar, ve OCR sonuçlarınız her zaman kristal gibi net olsun!  

--- 

![how to deskew image example](deskew_example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}