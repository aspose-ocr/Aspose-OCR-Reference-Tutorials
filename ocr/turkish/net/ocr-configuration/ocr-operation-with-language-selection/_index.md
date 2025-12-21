---
date: 2025-12-21
description: Aspose.OCR for .NET kullanarak OCR nasıl yapılır ve görüntüden metin
  nasıl çıkarılır öğrenin. Bu adım adım kılavuz, çok dilli metin tanıma ve dil seçimini
  gösterir.
linktitle: How to Perform OCR with Language Selection in Aspose.OCR
second_title: Aspose.OCR .NET API
title: Aspose.OCR'de Dil Seçimiyle OCR Nasıl Yapılır
url: /tr/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR'da Dil Seçimi ile OCR Nasıl Yapılır

## Giriş

Bir .NET uygulamasında **OCR nasıl yapılır** ve görüntü dosyalarından metin çıkarılır sorusuna yanıt arıyorsanız, Aspose.OCR for .NET hızlı, doğru ve dil‑bilinçli bir çözüm sunar. Bu öğreticide, dil seçimiyle OCR görüntü tanımasını gösteren gerçek bir örnek üzerinden ilerleyecek ve sadece birkaç satır kodla resimlerden çok dilli metin çekebileceksiniz.

## Hızlı Yanıtlar
- **Aspose.OCR ne yapar?** Görüntülerdeki basılı ve el yazısı metinleri tanır ve çıkarılan metni döndürür.  
- **Dili seçebilir miyim?** Evet – İngilizce, Almanca, İspanyolca, Çince vb. desteklenen herhangi bir dili belirtebilirsiniz.  
- **Geliştirme için lisansa ihtiyacım var mı?** Değerlendirme için ücretsiz deneme sürümü yeterlidir; üretim kullanımı için lisans gereklidir.  
- **Hangi .NET sürümleri destekleniyor?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Eğim düzeltme otomatik mi?** `AutoSkew` özelliğini etkinleştirerek `SkewAngle` ayarını ince ayar yapabilirsiniz.

## Neden OCR Görevleri İçin Aspose.OCR Seçilmeli?

- **Birden çok font ve görüntü kalitesinde yüksek doğruluk**.  
- **Yerleşik dil seçimi** dış dil paketlerine ihtiyaç duymaz.  
- **Basit API** mevcut C# projeleriyle sorunsuz entegrasyon.  
- **Harici bağımlılık yok** – tüm işlemler yerel olarak gerçekleşir, verileriniz güvende kalır.

## Önkoşullar

Koda geçmeden önce aşağıdaki önkoşulların sağlandığından emin olun:

- Aspose.OCR for .NET: Aspose.OCR kütüphanesinin kurulu olduğundan emin olun. İndirmek için [Aspose.OCR for .NET indirme sayfasını](https://releases.aspose.com/ocr/net/) ziyaret edin.

- Geliştirme Ortamı: .NET uygulamasıyla çalışacak bir ortam kurun. Henüz yapmadıysanız, ayrıntılı talimatlar için [belgelere](https://reference.aspose.com/ocr/net/) bakın.

## Namespace'leri İçe Aktarma

.NET uygulamanızda gerekli namespace'leri içe aktararak başlayın:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Adım 1: Aspose.OCR'ı Başlatma

Aspose.OCR sınıfının bir örneğini başlatarak OCR yeteneklerini uygulamanıza dahil edin.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Adım 2: Görüntü Yolunu Belirtme

OCR uygulanacak görüntünün yolunu tanımlayın. Görüntünün uygulamanızdan erişilebilir olduğundan emin olun.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Adım 3: Dil Seçimiyle Görüntüyü Tanıma

Şimdi temel OCR işlemi gerçekleşiyor. Belirtilen görüntüden metin tanımak için Aspose.OCR kütüphanesini kullanın. Dil seçimi dahil olmak üzere tanıma ayarlarını düzenleyin.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Adım 4: Sonuçları Yazdırma ve Görüntüleme

OCR işleminden sonra, tanınan metin, alanlar, uyarılar ve JSON temsili dahil sonuçları yazdırın ve gösterin.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## Yaygın Sorunlar ve İpuçları

- **Yanlış dil seçimi** – Çıktı bozuk görünüyorsa, `Language` özelliğinin kaynak görüntünün diliyle eşleştiğinden emin olun.  
- **Eğimli görüntüler** – Daha iyi doğruluk için `AutoSkew`'i etkinleştirin veya `SkewAngle`'ı manuel ayarlayın.  
- **Büyük dosyalar** – Belleği korumak için büyük görüntüleri parçalara bölerek işleyin veya `RecognizeImage`'a vermeden önce çözünürlüğü düşürün.

## Sonuç

Tebrikler! Aspose.OCR for .NET kullanarak dil seçimiyle **OCR nasıl yapılır** öğrendiniz. Bu öğreticide, görüntü dosyalarından metin çıkarma, tanıma ayarlarını özelleştirme ve çok dilli içeriği sorunsuz şekilde yönetme konularını gördünüz.

## SSS

### S1: Aspose.OCR çok dilli metin tanıma için uygun mu?

C1: Evet, Aspose.OCR çeşitli dilleri destekler ve çok dilli OCR görevleri için esneklik sağlar.

### S2: Belirli görüntü özellikleri için OCR ayarlarını ince ayar yapabilir miyim?

C2: Kesinlikle! Eğim açısı, satır tanıma ve alan tespiti gibi parametreleri farklı senaryolar için optimize edebilirsiniz.

### S3: Ek destek veya topluluk tartışmalarını nereden bulabilirim?

C3: Topluluk desteği ve tartışmalar için [Aspose.OCR forumunu](https://forum.aspose.com/c/ocr/16) ziyaret edin.

### S4: Ücretsiz bir deneme sürümü var mı?

C4: Evet, Aspose.OCR'un yeteneklerini deneyimlemek için [ücretsiz deneme sürümünü](https://releases.aspose.com/) keşfedin.

### S5: Aspose.OCR for .NET nasıl satın alınır?

C5: Satın almak için [satın alma sayfasını](https://purchase.aspose.com/buy) ziyaret edin.

---

**Son Güncelleme:** 2025-12-21  
**Test Edilen Versiyon:** Aspose.OCR 24.11 for .NET  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}