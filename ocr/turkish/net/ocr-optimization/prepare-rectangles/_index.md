---
date: 2025-12-22
description: Aspose.OCR for .NET kullanarak görüntüden metin çıkarmayı öğrenin. Bu
  kılavuz, OCR görüntü tanıması için dikdörtgenleri hazırlama ve doğruluğu artırma
  sürecinde size rehberlik eder.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: OCR'da Dikdörtgenler Hazırlayarak Görüntüden Metin Nasıl Çıkarılır
url: /tr/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Görüntü Tanıma için Dikdörtgenler Hazırlama

## Giriş

Optical Character Recognition (OCR), görsel içeriği aranabilir ve düzenlenebilir metne dönüştürmek için hayati öneme sahiptir. Bu öğreticide, OCR motorunu belirli bölgelere odaklayan özel dikdörtgenler hazırlayarak **extract text from image** işlemini gerçekleştireceksiniz. Aspose.OCR for .NET kullanarak, projenizi kurmaktan tanınan metni almaya kadar her adımı adım adım göstereceğiz; böylece .NET uygulamalarınıza güçlü bir görüntü‑den‑metin işlevi entegre edebileceksiniz.

## Hızlı Yanıtlar
- **“extract text from image” ne anlama geliyor?** Bir resimdeki görsel karakterleri makine‑okunabilir dizelere dönüştürmek anlamına gelir.  
- **Bu .NET'te hangi kütüphane yardımcı olur?** Aspose.OCR for .NET.  
- **Geliştirme için lisansa ihtiyacım var mı?** Test için ücretsiz deneme sürümü çalışır; üretim için lisans gereklidir.  
- **Belirli alanları hedefleyebilir miyim?** Evet, OCR kapsamını sınırlayan dikdörtgenler tanımlayarak.  
- **Hangi .NET sürümleri destekleniyor?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Dikdörtgenlerle “extract text from image” nedir?
Bir görüntü üzerinde dikdörtgen alanlar tanımladığınızda, OCR motoru yalnızca bu alanları işler. Bu, doğruluğu artırır, işleme süresini azaltır ve gürültülü arka planları veya alakasız bölümleri görmezden gelmenizi sağlar.

## OCR'den önce dikdörtgenleri neden hazırlamalısınız?
- **İlgili içeriğe odaklanma:** Başlıkları, altbilgileri veya süs grafiklerini atlayın.  
- **Performansı artırma:** Daha küçük bölgeler daha hızlı tanıma anlamına gelir.  
- **Doğruluğu artırma:** Daha az görsel gürültü daha temiz sonuçlar verir.

## Önkoşullar

- C# ve .NET geliştirme konusunda aşinalık.  
- Aspose.OCR for .NET kütüphanesi yüklü – **[buradan](https://releases.aspose.com/ocr/net/)** indirebilirsiniz.  
- Çıkarımını yapmak istediğiniz metni içeren örnek bir resim (ör. `sample.png`).

## Ad Alanlarını İçe Aktarma

İlk olarak, gerekli ad alanlarını kapsam içine getirin:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Adım 1: Belge Dizinini Ayarlama

Resim dosyalarınızın bulunduğu yeri belirtin ve OCR motorunun bir örneğini oluşturun.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Birden Çok Dikdörtgen Kullanarak Resimden Metin Çıkarma

### Adım 2: Çoklu Dikdörtgenlerle Görüntüyü Tanıma

#### 2.1 Dikdörtgenleri Tanımlama

OCR motorunun taramasını istediğiniz alanları belirten `Rectangle` nesnelerinin bir listesini oluşturun.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 OCR Tanımasını Gerçekleştirme

`RecognizeImage` metoduna resim yolunu ve dikdörtgen listesini geçirin. Metot, her bir dikdörtgene karşılık gelen bir dizi string döndürür.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### Adım 3: Tanıma Ayarlarıyla Görüntüyü Tanıma (Alternatif Yaklaşım)

`RecognitionSettings` kullanmayı tercih ederseniz, biraz farklı bir API çağrısı ile aynı sonuca ulaşabilirsiniz.

#### 3.1 Tanıma ayarlarını tanımlama

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Tanınan metni gösterme

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Yaygın Sorunlar ve İpuçları

- **Yanlış dikdörtgen koordinatları:** `X`, `Y`, `Width` ve `Height` değerlerinin istediğiniz bölgeye doğru eşlendiğinden emin olun.  
- **Resim kalitesi:** Düşük çözünürlüklü görüntüler kötü OCR sonuçları verebilir; ön işleme (ör. ikilileştirme) düşünün.  
- **Boş sonuçlar:** Dikdörtgenlerin gerçekten metin içerdiğini doğrulayın; aksi takdirde motor boş stringler döndürür.

## Sonuç

Artık Aspose.OCR for .NET ile özel dikdörtgenler hazırlayarak **extract text from image** işlemini nasıl yapacağınızı öğrendiniz. Bu teknik, OCR işleme üzerinde ayrıntılı kontrol sağlar ve uygulamalarınızda daha hızlı, daha doğru metin çıkarma özellikleri oluşturmanıza yardımcı olur.

## Sıkça Sorulan Sorular

**S:** Aspose.OCR for .NET'i diğer .NET framework'leriyle kullanabilir miyim?  
**C:** Evet, Aspose.OCR for .NET çeşitli .NET framework'leriyle uyumludur.

**S:** Aspose.OCR for .NET için ücretsiz bir deneme sürümü mevcut mu?  
**C:** Kesinlikle! Ücretsiz deneme sürümüne **[buradan](https://releases.aspose.com/)** ulaşabilirsiniz.

**S:** Aspose.OCR for .NET için destek nasıl alınır?  
**C:** Ayrıcalıklı destek için **[Aspose.OCR forumunu](https://forum.aspose.com/c/ocr/16)** ziyaret edin.

**S:** Test amaçlı geçici bir lisans alabilir miyim?  
**C:** Evet, geçici lisansı **[buradan](https://purchase.aspose.com/temporary-license/)** edinebilirsiniz.

**S:** Aspose.OCR for .NET dokümantasyonunu nereden bulabilirim?  
**C:** Dokümantasyon **[burada](https://reference.aspose.com/ocr/net/)** mevcuttur.

---

**Last Updated:** 2025-12-22  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}