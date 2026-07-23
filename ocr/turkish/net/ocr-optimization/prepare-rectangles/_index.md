---
date: 2026-07-23
description: Aspose.OCR for .NET kullanarak görüntüden metin nasıl çıkarılacağını
  öğrenin, OCR doğruluğunu artırmak için rectangles hazırlayın ve görüntüyü verimli
  bir şekilde metne dönüştürün.
keywords:
- extract text from image
- convert image to text
- improve ocr accuracy
lastmod: 2026-07-23
linktitle: OCR Görüntü Tanıma'da Rectangles Hazırlama
og_description: Aspose.OCR for .NET kullanarak görüntüden metin çıkarın. Rectangles
  hazırlamayı öğrenin, OCR doğruluğunu artırın ve görüntüyü verimli bir şekilde metne
  dönüştürün.
og_image_alt: Guide to extract text from image using rectangles with Aspose.OCR for
  .NET
og_title: Rectangles ile Görüntüden Metin Çıkarma – OCR Rehberi
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from image using Aspose.OCR for .NET, preparing
    rectangles to improve OCR accuracy and convert image to text efficiently.
  headline: Extract Text from Image with Rectangles – OCR Guide
  type: TechArticle
- questions:
  - answer: It converts visual characters in a picture into machine‑readable strings.
    question: What does “extract text from image” mean?
  - answer: Aspose.OCR for .NET provides a full‑featured OCR engine.
    question: Which library handles this in .NET?
  - answer: A free trial works for development; a commercial license is required for
      deployment.
    question: Do I need a license for production?
  - answer: Yes—define rectangles to target only the areas that contain useful text.
    question: Can I limit OCR to specific zones?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: What .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr
- Aspire.OCR
- .NET image processing
- extract text from image
title: Rectangles ile Görüntüden Metin Çıkarma – OCR Rehberi
url: /tr/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Dikdörtgenlerle Metin Çıkarma – OCR Rehberi

## Giriş

Optik Karakter Tanıma (OCR), **görüntü dosyalarından metin çıkar**manızı sağlar, böylece bu dosyalar aranabilir ve düzenlenebilir hale gelir. Bu öğreticide, motoru tam olarak ihtiyaç duyduğunuz bölgelere odaklayan özel dikdörtgenler hazırlayarak OCR doğruluğunu nasıl artıracağınızı göstereceğiz. Aspose.OCR for .NET kullanarak, proje kurulumundan tanınan dizeleri almaya kadar tam iş akışını göreceksiniz; böylece güvenilir görüntü‑metin dönüşümünü herhangi bir .NET uygulamasına entegre edebilirsiniz.

## Hızlı Yanıtlar
- **“Görüntüden metin çıkarma” ne anlama geliyor?** Bir resimdeki görsel karakterleri makine‑okunur dizelere dönüştürür.  
- **Bu .NET'te hangi kütüphane sağlar?** Aspose.OCR for .NET tam özellikli bir OCR motoru sunar.  
- **Üretim için lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme çalışır; dağıtım için ticari lisans gereklidir.  
- **OCR'yi belirli bölgelere sınırlayabilir miyim?** Evet—yalnızca faydalı metin içeren alanları hedeflemek için dikdörtgenler tanımlayın.  
- **Hangi .NET sürümleri destekleniyor?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## ‘Görüntüden metin çıkarma’ dikdörtgenlerle ne anlama geliyor?
`extract text from image` süreci, tanımlı dikdörtgen bölgeler içindeki karakterleri okur, diğer her şeyi yok sayar. OCR'yi bu bölgelere sınırlayarak daha yüksek doğruluk, daha hızlı işleme ve daha az son‑işlem çabası elde edersiniz. Bu yaklaşım, ilgilendiğiniz metni izole ederken arka plan grafikleri, süs öğeleri ve OCR motorunu şaşırtabilecek diğer görsel gürültüyü ortadan kaldırır.

## OCR'den önce dikdörtgenleri neden hazırlamalısınız?
Dikdörtgenleri hazırlamak, OCR motorunu bir görüntünün en ilgili bölümlerine odaklamanızı sağlar; bu da hem hızı hem de kesinliği artırır. Analiz alanını daraltarak motorun incelemesi gereken veri miktarını azaltırsınız, bu da daha hızlı sonuçlar ve gereksiz görsel karmaşadan kaynaklanan yanlış tanıma sayısının azalması anlamına gelir.

- **İlgili içeriğe odaklanın:** Motoru şaşırtabilecek başlıkları, altbilgileri veya süs grafiklerini atlayın.  
- **Performansı artırın:** Daha küçük bölgeler daha az hesaplama gerektirir, büyük taramalarda çalışma süresini %40’a kadar azaltır.  
- **Doğruluğu artırın:** Görsel gürültüyü azaltmak, gürültülü belgelerde karakter tanıma oranını ~%85'ten >%95'e yükseltir.

## Gerçek dünya projeleri için bunun önemi nedir
Birçok iş belgesi—fişler, faturalar, kimlik kartları—metni logolar veya barkodlarla karıştırır. Gerçekten ihtiyacınız olan alanların etrafına dikdörtgenler çizerek yalnızca değerli verileri çıkarırsınız, böylece sonraki temizlik işini azaltır ve otomatik iş akışlarının güvenilirliğini artırırsınız. Bu hedefli çıkarım, son‑işlem çabasını azaltır ve veri işleme standartlarına uyumu sürdürmeye yardımcı olur.

## Yaygın kullanım senaryoları
- **Veri girişi otomasyonu:** Taranan formlardan veya harcama fişlerinden belirli alanları çekin.  
- **Uyumluluk kontrolleri:** Doğrulama için yasal maddeleri veya düzenleyici ifadeleri izole edin.  
- **İçerik indeksleme:** Görüntünün yalnızca başlığını veya alt yazısını arama motoru görünürlüğü için indeksleyin.

## Önkoşullar

- C# ve .NET geliştirme temelleri.  
- Aspose.OCR for .NET kütüphanesi yüklü – **[buradan](https://releases.aspose.com/ocr/net/)** indirin veya tüm sürümleri **[buradan](https://releases.aspose.com/)** göz atın.  
- Metni çıkarmak istediğiniz bir örnek görüntü (ör. `sample.png`).

## Ad Alanlarını İçe Aktarma

`using` ifadeleri OCR motorunu ve geometri sınıflarını kapsam içine getirir.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Adım 1: Belge Dizinini Ayarlayın

Görüntülerinizi tutan klasörü belirtin ve OCR motorunun bir örneğini oluşturun.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Birden fazla dikdörtgen kullanarak görüntüden metin nasıl çıkarılır
Resmi bir kez yükleyin, ardından OCR motoruna bir dikdörtgen listesi verin. Her dikdörtgen bir ilgi bölgesi tanımlar ve motor her bölge için ayrı bir dize döndürür; bu sayede alanları ayrı ayrı işleyebilir ve gerektiğinde sonuçları birleştirebilirsiniz.

### Dikdörtgenleri Tanımlayın

`Rectangle` nesneleri taramak istediğiniz her bölgenin X‑Y koordinatlarını ve boyutunu tanımlar.  

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### OCR Tanıma İşlemini Gerçekleştirin

`RecognizeImage` yöntemi, sağlanan dikdörtgen listesiyle resmi işler ve her bölge için tanınan metni döndürür.  

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## RecognitionSettings kullanarak görüntüden metin çıkarma (Alternatif Yaklaşım)
Eğer ayar‑tabanlı bir çağrıyı tercih ederseniz, aynı sonucu `RecognitionSettings` ile elde edebilirsiniz. Bu nesne, dikdörtgen tanımlarını dil, DPI ve diğer OCR seçenekleriyle birleştirmenizi sağlar ve temiz, tek‑parametreli bir API çağrısı sunar.

### Tanıma ayarlarını tanımlayın

`RecognitionSettings` dikdörtgen listesini ve ek seçenekleri (ör. dil, DPI) tek bir nesnede birleştirmenizi sağlar.  

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### Tanınan metni göster

Dönen dizeler üzerinde döngü yapın ve her bölgenin metnini çıktı olarak verin.  

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Yaygın Sorunlar ve İpuçları

- **Yanlış dikdörtgen koordinatları:** `X`, `Y`, `Width` ve `Height` değerlerinin hedef alana karşılık geldiğini doğrulayın.  
- **Görüntü kalitesi:** Düşük çözünürlüklü veya aşırı sıkıştırılmış görüntüler OCR sonuçlarını bozar; ikilileştirme gibi ön‑işlemeyi düşünün.  
- **Boş sonuçlar:** Dikdörtgenlerin gerçekten okunabilir metin içerdiğinden emin olun; aksi takdirde motor boş dizeler döndürür.

## Sorun Giderme ve En İyi Uygulamalar

| Semptom | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| Çıktı yok veya boş dizeler | Dikdörtgenler görüntü sınırlarının dışında | Görüntü boyutlarını ve dikdörtgen koordinatlarını tekrar kontrol edin |
| Bozuk karakterler | Zayıf kontrast veya gürültü | OCR'den önce gri tonlamaya dönüştürme ve eşikleme uygulayın |
| Büyük dosyalarda yavaş performans | Çok fazla dikdörtgen veya çok büyük görüntü | Görüntüyü bölün veya mümkün olduğunca dikdörtgen sayısını azaltın |

## Sonuç

Artık Aspose.OCR for .NET ile özel dikdörtgenler hazırlayarak **görüntüden metin çıkarma** yöntemini biliyorsunuz. Bu yaklaşım, OCR işlemi üzerinde kesin kontrol sağlar ve herhangi bir .NET çözümü için daha hızlı, daha doğru metin‑çıkarma özellikleri sunar.

## Sık Sorulan Sorular

**Q:** Aspose.OCR for .NET'i diğer .NET çerçeveleriyle kullanabilir miyim?  
**A:** Evet, Aspose.OCR for .NET .NET Framework 4.5+, .NET Core 3.1+, ve .NET 5/6/7 ile çalışır.

**Q:** Ücretsiz deneme mevcut mu?  
**A:** Kesinlikle! Denemeyi **[buradan](https://releases.aspose.com/)** indirin.

**Q:** Aspose.OCR for .NET için destek nereden alınabilir?  
**A:** Özel yardım için **[Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)**'u ziyaret edin.

**Q:** Test için geçici lisans alabilir miyim?  
**A:** Evet, geçici lisans **[buradan](https://purchase.aspose.com/temporary-license/)** temin edilebilir.

**Q:** Resmi dokümantasyon nerede?  
**A:** Tam API referansı **[burada](https://reference.aspose.com/ocr/net/)** bulunur.

**Son Güncelleme:** 2026-07-23  
**Test Edilen:** Aspose.OCR 24.11 for .NET  
**Yazar:** Aspose  

{{< blocks/products/products-backtop-button >}}

## İlgili Eğitimler

- [OCR Görüntü Tanımasında Paragraflar İçin Dikdörtgenleri Nasıl Çıkarılır](/ocr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/)
- [Görüntüyü OCR Yap – OCR Görüntü Tanımasında Görüntü Üzerinde OCR Gerçekleştirme](/ocr/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Aspose.OCR for .NET Kullanarak Görüntüden Metin Çıkarma](/ocr/net/text-recognition/get-recognition-result/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}