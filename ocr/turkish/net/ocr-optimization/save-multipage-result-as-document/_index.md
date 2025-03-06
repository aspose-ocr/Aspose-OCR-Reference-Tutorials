---
title: OCR Görüntü Tanıma'da Çok Sayfalı Sonucu Belge Olarak Kaydet
linktitle: OCR Görüntü Tanıma'da Çok Sayfalı Sonucu Belge Olarak Kaydet
second_title: Aspose.OCR .NET API'si
description: Aspose.OCR for .NET'in potansiyelini ortaya çıkarın. Bu kapsamlı, adım adım kılavuzla çok sayfalı OCR sonuçlarını zahmetsizce belge olarak kaydedin.
weight: 14
url: /tr/net/ocr-optimization/save-multipage-result-as-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Görüntü Tanıma'da Çok Sayfalı Sonucu Belge Olarak Kaydet

## giriiş

Aspose.OCR for .NET kullanarak optik karakter tanımanın (OCR) büyüleyici dünyasına hoş geldiniz! Bu eğitimde, çok sayfalı OCR sonuçlarını belge olarak kaydetmek için Aspose.OCR'ın özelliklerinden nasıl yararlanacağımızı keşfedeceğiz. İster deneyimli bir geliştirici olun ister OCR'a yeni başlıyor olun, bu kılavuz size her adımda yol gösterecek ve bu güçlü araçtan en iyi şekilde yararlanmanızı sağlayacaktır.

## Önkoşullar

Eğiticiye dalmadan önce her şeyin ayarlandığından emin olalım:

1.  Aspose.OCR for .NET'i yükleyin: Aspose.OCR for .NET'i indirip yükleyerek başlayın. Gerekli dosyaları bulabilirsiniz[Burada](https://releases.aspose.com/ocr/net/).

2.  Ücretsiz Denemenizi veya Lisansınızı Alın: Henüz yapmadıysanız, ücretsiz deneme sürümünü edinebilirsiniz[Burada](https://releases.aspose.com/) veya bir lisans satın alın[Burada](https://purchase.aspose.com/buy).

3.  Belgeleri Keşfedin: Kendinizi tanıyın[dokümantasyon](https://reference.aspose.com/ocr/net/)Aspose.OCR for .NET için. Ayrıntılı bilgi için başvurulacak kaynağınızdır.

4.  Destek Forumlarına Erişim: Herhangi bir sorunla karşılaşırsanız veya sorularınız varsa,[destek forumları](https://forum.aspose.com/c/ocr/16) değerli bir topluluk kaynağıdır.

Artık hazır olduğunuza göre adım adım kılavuza geçelim.

## Ad Alanlarını İçe Aktar

Gerekli ad alanlarını içe aktararak projenize başlayın:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

## 1. Adım: Belge Dizininizi Ayarlayın

```csharp
// Belgeler dizininin yolu.
string dataDir = "Your Document Directory";
```

 Değiştirildiğinden emin olun`"Your Document Directory"` belge dizininizin gerçek yolu ile.

## Adım 2: Aspose.OCR'ı başlatın

```csharp
// AsposeOcr örneğini başlat
AsposeOcr api = new AsposeOcr();
```

 Bir örneğini oluşturun`AsposeOcr` OCR işlevlerine erişmek için.

## 3. Adım: Görüntüleri Tanıma

```csharp
// Resmi tanı
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

Birden fazla görüntüdeki metni tanımak için Aspose.OCR'ı kullanın. Dosya yollarını görüntü dosyalarınıza göre ayarlayın.

## 4. Adım: Sonuçları Tercih Edilen Formatlarda Kaydedin

```csharp
// Sonucu tercih ettiğiniz formatta kaydedin
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

İstediğiniz formatı seçin (Docx, Text, Pdf veya Xlsx) ve OCR sonuçlarını çok sayfalı bir belge olarak kaydedin.

## Çözüm

Tebrikler! Aspose.OCR for .NET kullanarak çok sayfalı OCR sonuçlarını belge olarak nasıl kaydedeceğinizi başarıyla öğrendiniz. Bu çok yönlü araç, projelerinizde metin tanıma için bir olasılıklar dünyasının kapılarını açar.

## SSS'ler

### S1: Test amaçlı olarak geçici bir lisans mevcut mu?

 Cevap1: Evet, geçici lisans alabilirsiniz[Burada](https://purchase.aspose.com/temporary-license/) Aspose.OCR'yi test etmek için.

### S2: Farklı formatlardaki görsellerdeki metinleri tanıyabilir miyim?

A2: Kesinlikle! Aspose.OCR çeşitli görüntü formatlarını destekleyerek OCR görevlerinizde esneklik sağlar.

### S3: Tanıma için resim sayısında herhangi bir sınırlama var mı?

C3: İşleyebileceğiniz görsellerin sayısı lisansınıza bağlıdır. Ayrıntılar için belgelere bakın.

### S4: OCR tanıma sırasındaki hataları nasıl halledebilirim?

Cevap 4: Hata gidermeye yönelik en iyi uygulamalar için belgelere bakın veya destek forumlarından yardım isteyin.

### S5: Aspose.OCR İngilizce dışındaki dilleri destekliyor mu?

Cevap5: Evet, Aspose.OCR birden fazla dili destekler. Dil desteği ayrıntıları için belgeleri inceleyin.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
