---
date: 2025-12-21
description: Aspose.OCR for .NET ile birden çok görüntüde OCR nasıl yapılır, görüntülerden
  metin nasıl çıkarılır ve JPEG metni nasıl verimli bir şekilde okunur öğrenin.
linktitle: Multiple Image OCR with List in Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: Aspose.OCR for .NET'te Liste Kullanarak Çoklu Görüntü OCR
url: /tr/net/ocr-configuration/ocr-operation-with-list/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bir Liste ile Çoklu Görüntü OCR’u Aspose.OCR for .NET ile

## Giriş

Aspose.OCR for .NET kullanarak **çoklu görüntü ocr** üzerine kapsamlı öğreticimize hoş geldiniz. Optik Karakter Tanıma (OCR), taranmış kağıt belgelerini, PDF’leri veya görüntü dosyalarını düzenlenebilir, aranabilir metne dönüştürür. Bu rehberde görüntülerden metin çıkarma, JPEG metnini okuma ve tek bir çağrıda birden fazla dosyayı işleme konularını öğreneceksiniz—**belgeyi metne tarama** ihtiyacınız olduğunda hızlı ve güvenilir bir çözüm.

## Hızlı Yanıtlar
- **“çoklu görüntü ocr” ne yapar?** Tek bir API çağrısında bir görüntü dosyası listesinde metin tanıması yapmanızı sağlar.  
- **Hangi formatlar desteklenir?** JPEG, PNG, BMP, TIFF, GIF ve daha birçok format.  
- **Lisans gerekli mi?** Üretim için geçici bir lisans gerekir; değerlendirme için ücretsiz deneme sürümü yeterlidir.  
- **Tanıma ayarlarını özelleştirebilir miyim?** Evet—`RecognitionSettings` ile dil, çözünürlük ve ön işleme ayarlarını değiştirebilirsiniz.  
- **Bir kerede kaç görüntü işleyebilirim?** Pratikte sınırsız; API her dosyayı akış olarak işler, böylece bellek kullanımı düşük kalır.

## Çoklu görüntü ocr nedir?
**çoklu görüntü ocr**, Aspose.OCR’a bir dizi görüntü yolu gönderip her görüntü için tanınan metni tek bir işlemde almanızı sağlayan özelliktir. Bu, geliştirme süresini kısaltır ve toplu taranmış belgelerle çalışırken ağ isteklerini azaltır.

## Aspose.OCR’u çoklu görüntü işleme için neden kullanmalısınız?
- **Gürültülü taramalar ve düşük çözünürlüklü JPEG’lerde yüksek doğruluk**.  
- **Çok dilli belgeler için yerleşik dil algılama**.  
- **Tam .NET desteği** – .NET Framework, .NET Core ve .NET 5/6+ ile çalışır.  
- **Harici bağımlılık yok**—kütüphane görüntü yükleme, ön işleme ve metin çıkarma işlemlerini dahili olarak yönetir.

## Önkoşullar

Kodlamaya başlamadan önce aşağıdaki önkoşulları yerine getirdiğinizden emin olun:

1. Aspose.OCR for .NET Kütüphanesi: Aspose.OCR kütüphanesinin kurulu olduğundan emin olun. İndirmek için [Aspose.OCR for .NET indirme sayfası](https://releases.aspose.com/ocr/net/) adresini ziyaret edebilirsiniz.

2. Belge Dizini: OCR tanıması için belgelerinizin ve görüntülerinizin bulunduğu bir dizin oluşturun.

Gerekli temellere sahip olduğunuza göre, adım adım rehbere başlayalım.

## Ad Alanlarını İçe Aktarma

C# projenizde Aspose.OCR for .NET’i kullanmak için gerekli ad alanlarını ekleyin:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Adım 1: Belge Dizinini Ayarlama

Belge dizininizin yolunu başlatın:

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Adım 2: Görüntü Yollarını Belirtme

Tanımadan önce işlemek istediğiniz görüntülerin yollarını tanımlayın. Örneğin, JPEG ve PNG dosyalarından **metin görüntülerini çıkarabilirsiniz**:

```csharp
List<string> imagePaths = new List<string>
{
    dataDir + "0001460985.Jpeg",
    dataDir + "sample.png"
};
```

## Adım 3: OCR Görüntü Tanımasını Gerçekleştirme

Belirtilen görüntülerle OCR tanıma sürecini başlatın. Bu adım **ocr birden fazla dosya** işleme örneğini gösterir:

```csharp
RecognitionResult[] result = api.RecognizeMultipleImages(imagePaths, new RecognitionSettings
{
   //default or custom settings
});
```

## Adım 4: Tanıma Sonuçlarını Görüntüleme

Her görüntü için tanıma sonuçlarını yazdırın. Burada her dosyadan çıkarılan metni göreceksiniz; bu da **JPEG metnini okuma** ve diğer formatları kapsar:

```csharp
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
```

## Yaygın Sorunlar ve Çözümler

| Sorun | Neden | Çözüm |
|-------|-------|-------|
| Metin döndürülmüyor | Görüntü kalitesi çok düşük | DPI artırın veya `RecognitionSettings` ile görüntü ön işleme etkinleştirin |
| Yanlış dil algılandı | Varsayılan dil İngilizce | `RecognitionSettings.Language` değerini uygun dil koduna ayarlayın |
| Büyük partilerde bellek yetersizliği | Birçok yüksek çözünürlüklü görüntü aynı anda yükleniyor | Görüntüleri daha küçük partilerde işleyin veya `RecognizeMultipleImages` zaten akış yönetimi yaptığı için bunu kullanın |

## Sık Sorulan Sorular

**S: Belirli görüntüler için tanıma ayarlarını özelleştirebilir miyim?**  
C: Evet, `RecognitionSettings` sınıfı OCR parametrelerini (dil, çözünürlük, ön işleme vb.) her toplu işlem için özelleştirmenize olanak tanır.

**S: Aspose.OCR for .NET çeşitli görüntü formatlarıyla uyumlu mu?**  
C: Kesinlikle. Aspose.OCR JPEG, PNG, BMP, TIFF, GIF ve birçok diğer formatı destekler, böylece farklı belge tipleriyle çalışabilirsiniz.

**S: Aspose.OCR for .NET için geçici bir lisans nasıl alınır?**  
C: Değerlendirme amaçlı geçici lisans almak için [bu linki](https://purchase.aspose.com/temporary-license/) ziyaret edin.

**S: Aspose.OCR for .NET için ayrıntılı belgeleri nerede bulabilirim?**  
C: Kapsamlı bilgi ve kullanım kılavuzları için [belgelendirme](https://reference.aspose.com/ocr/net/) sayfasına bakın.

**S: Uygulama sırasında sorunlarla karşılaşırsam ya da özel sorularım olursa ne yapmalıyım?**  
C: Topluluk ve uzmanlardan hızlı destek almak için [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) adresine başvurabilirsiniz.

## Sonuç

Tebrikler! Aspose.OCR for .NET kullanarak bir liste ile **çoklu görüntü ocr** işlemini başarıyla gerçekleştirdiniz. Bu güçlü özellik sayesinde **belgeyi metne tarama**, **metin görüntülerini çıkarma** ve **JPEG metnini toplu okuma** gibi işlemleri kolayca yapabilir, veri çıkarma, arşivleme ve otomatik iş akışları için yeni fırsatlar yaratabilirsiniz.

---

**Son Güncelleme:** 2025-12-21  
**Test Edilen:** Aspose.OCR 24.11 for .NET  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}