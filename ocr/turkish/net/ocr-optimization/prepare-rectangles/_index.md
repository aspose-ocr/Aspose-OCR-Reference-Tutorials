---
date: 2026-02-25
description: Aspose.OCR for .NET kullanarak görüntüden metin çıkarmayı öğrenin. Bu
  kılavuz, OCR görüntü tanıması için dikdörtgenleri hazırlamayı ve doğruluğu artırmayı
  adım adım gösterir.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: OCR'de Dikdörtgenler Hazırlayarak Görüntüden Metin Nasıl Çıkarılır
url: /tr/net/ocr-optimization/prepare-rectangles/
weight: 11
---

 with same formatting.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Görüntü Tanıma İçin Dikdörtgenler Hazırlama

## Giriş

Optik Karakter Tanıma (OCR), görsel içeriği aranabilir, düzenlenebilir metne dönüştürmek için gereklidir. Bu öğreticide **görüntüden metin çıkarma** işlemini, OCR motorunu belirli bölgelere odaklayan özel dikdörtgenler hazırlayarak yapacaksınız. Aspose.OCR for .NET kullanarak, projenizi kurmaktan tanınan metni almaya kadar her adımı göstereceğiz; böylece .NET uygulamalarınıza güçlü görüntü‑metin işlevselliği entegre edebilirsiniz.

## Hızlı Yanıtlar
- **“görüntüden metin çıkarma” ne anlama geliyor?** Bir resimdeki görsel karakterleri makine‑okunabilir dizelere dönüştürmek anlamına gelir.  
- **.NET'te bu konuda hangi kütüphane yardımcı olur?** Aspose.OCR for .NET.  
- **Geliştirme için lisansa ihtiyacım var mı?** Test için ücretsiz deneme çalışır; üretim için lisans gereklidir.  
- **Belirli alanları hedefleyebilir miyim?** Evet, OCR kapsamını sınırlayan dikdörtgenler tanımlayarak.  
- **Hangi .NET sürümleri destekleniyor?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Dikdörtgenlerle “görüntüden metin çıkarma” nedir?
Bir görüntüde dikdörtgen bölgeler tanımladığınızda, OCR motoru yalnızca bu bölgeleri işler. Bu, doğruluğu artırır, işleme süresini azaltır ve gürültülü arka planları ya da alakasız bölümleri görmezden gelmenizi sağlar.

## OCR'den önce neden dikdörtgenler hazırlamalısınız?
- **İlgili içeriğe odaklanın:** Başlıkları, altbilgileri veya süsleyici grafikleri atlayın.  
- **Performansı artırın:** Daha küçük bölgeler daha hızlı tanıma demektir.  
- **Doğruluğu artırın:** Daha az görsel gürültü daha temiz sonuçlar verir.

## Gerçek dünyadaki projeler için bunun önemi
Birçok iş belgesi—makbuzlar, faturalar, kimlik kartları—karışık düzenlere sahiptir ve sadece belirli bölümler değerli metin içerir. Dikdörtgenler kullanarak sadece gereken alanları çıkarabilir, son‑işlem çalışmalarını büyük ölçüde azaltabilir ve otomasyon hattınızın genel güvenilirliğini artırabilirsiniz.

## Yaygın kullanım senaryoları
- **Veri girişi otomasyonu:** Tarama formlarından belirli alanları çekin.  
- **Uyumluluk kontrolleri:** Hukuki metin bloklarını izole edip doğrulayın.  
- **İçerik indeksleme:** Görüntünün yalnızca başlığını veya alt yazısını arama motorları için indeksleyin.

## Önkoşullar

- C# ve .NET geliştirme konusunda aşinalık.  
- Aspose.OCR for .NET kütüphanesi yüklü – **[buradan](https://releases.aspose.com/ocr/net/)** indirebilirsiniz.  
- Çıkarılacak metni içeren bir örnek görüntü (ör. `sample.png`).

## Ad Alanlarını İçe Aktarın

İlk olarak, gerekli ad alanlarını kapsam içine getirin:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Adım 1: Belge Dizinini Ayarlayın

Görüntü dosyalarınızın bulunduğu yeri belirtin ve OCR motorunun bir örneğini oluşturun.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Birden fazla dikdörtgen kullanarak görüntüden metin çıkarma

### Adım 2: Görüntüyü Birden Fazla Dikdörtgenle Tanıma

#### 2.1 Dikdörtgenleri Tanımlayın

`Rectangle` nesnelerinin bir listesini oluşturun; bu nesneler OCR motorunun taramasını istediğiniz alanları çizer.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 OCR tanımasını gerçekleştirin

Görüntü yolunu ve dikdörtgen listesini `RecognizeImage` metoduna aktarın. Metot, her bir dikdörtgene karşılık gelen bir dizi string döndürür.

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

`RecognitionSettings` kullanmayı tercih ederseniz, biraz farklı bir API çağrısıyla aynı sonuca ulaşabilirsiniz.

#### 3.1 Tanıma ayarlarını tanımlayın

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Tanınan metni gösterin

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Yaygın Sorunlar ve İpuçları

- **Yanlış dikdörtgen koordinatları:** `X`, `Y`, `Width` ve `Height` değerlerinin istediğiniz bölgeye doğru eşlendiğinden emin olun.  
- **Görüntü kalitesi:** Düşük çözünürlüklü görüntüler kötü OCR sonuçları verebilir; ön işleme (ör. ikilileştirme) düşünün.  
- **Boş sonuçlar:** Dikdörtgenlerin gerçekten metin içerdiğini doğrulayın; aksi takdirde motor boş string döndürür.

## Sorun Giderme ve En İyi Uygulamalar

| Semptom | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| Çıktı yok veya boş stringler | Dikdörtgenler görüntü sınırlarının dışında | Görüntü boyutlarını ve dikdörtgen koordinatlarını tekrar kontrol edin |
| Bozuk karakterler | Düşük kontrast veya gürültü | OCR'den önce görüntü temizleme (gri tonlama, eşikleme) uygulayın |
| Büyük dosyalarda yavaş performans | Çok fazla dikdörtgen veya çok büyük görüntü | Mümkün olduğunca görüntüyü bölün veya dikdörtgen sayısını azaltın |

## Sonuç

Artık Aspose.OCR for .NET ile özel dikdörtgenler hazırlayarak **görüntüden metin çıkarma** yöntemini öğrendiniz. Bu teknik, OCR işleme üzerinde ayrıntılı kontrol sağlar ve uygulamalarınızda daha hızlı, daha doğru metin çıkarma özellikleri oluşturmanıza yardımcı olur.

## Sık Sorulan Sorular

**S:** Aspose.OCR for .NET'i diğer .NET framework'leriyle kullanabilir miyim?  
**C:** Evet, Aspose.OCR for .NET çeşitli .NET framework'leriyle uyumludur.

**S:** Aspose.OCR for .NET için ücretsiz deneme mevcut mu?  
**C:** Kesinlikle! Ücretsiz denemeye **[buradan](https://releases.aspose.com/)** ulaşabilirsiniz.

**S:** Aspose.OCR for .NET için desteği nasıl alabilirim?  
**C:** Ayrı destek için **[Aspose.OCR forumunu](https://forum.aspose.com/c/ocr/16)** ziyaret edin.

**S:** Test amaçlı geçici bir lisans alabilir miyim?  
**C:** Evet, geçici lisansı **[buradan](https://purchase.aspose.com/temporary-license/)** edinebilirsiniz.

**S:** Aspose.OCR for .NET dokümantasyonunu nerede bulabilirim?  
**C:** Dokümantasyon **[burada](https://reference.aspose.com/ocr/net/)** mevcuttur.

---

**Son Güncelleme:** 2026-02-25  
**Test Edilen Sürüm:** Aspose.OCR 24.11 for .NET  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}