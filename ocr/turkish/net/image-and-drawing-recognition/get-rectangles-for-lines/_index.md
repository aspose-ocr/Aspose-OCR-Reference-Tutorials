---
date: 2025-12-17
description: Aspose.OCR for .NET kullanarak OCR satır dikdörtgenlerini nasıl alacağınızı
  öğrenin, görüntülerdeki metin satırlarını tanıyın ve satır koordinatlarını kolayca
  çıkarın.
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: Görüntü Metin Satırları için OCR Satır Dikdörtgenlerini Al
url: /tr/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntü Metin Satırları için OCR Satır Dikdörtgenlerini Alın

## Giriş

Bu öğreticide Aspose.OCR for .NET ile **OCR satır dikdörtgenlerini nasıl alacağınızı** keşfedeceksiniz. Kılavuzun sonunda **bir görüntüdeki metin satırlarını tanıyabilecek** ve **algılanan her satır için satır koordinatlarını çıkarabilecek** olacaksınız—düzen analizi, veri çıkarma veya özel render gibi sonraki işlemler için mükemmeldir.

## Hızlı Yanıtlar
- **“OCR satır dikdörtgenlerini al” ne anlama geliyor?** Görüntüde algılanan her metin satırının sınırlayıcı kutularını döndürür.  
- **Hangi API yöntemi kullanılıyor?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Lisans gerekli mi?** Geliştirme için ücretsiz deneme çalışır; üretim için ticari lisans gereklidir.  
- **Desteklenenü formatları?** PNG, JPEG, BMP, TIFF ve daha fazlası.  
- **Bunu .NET Core üzerinde çalıştırabilir miyim?** Evet, Aspose.OCR .NET Core ve .NET 5/6'yı tam olarak destekler.

## Önkoşullar

Öğreticiye başlamadan önce, aşağıdaki önkoşulların mevcut olduğundan emin olun:

- C# ve .NET geliştirme konusunda temel bilgi.  
- Visual Studio gibi bir bütünleşik geliştirme ortamı (IDE).  
- Aspose.OCR for .NET kütüphanesi yüklü. Bunu [buradan](https://releases.aspose.com/ocr/net/) indirebilirsiniz.  
- OCR tanıması için metin içeren bir örnek görüntü.

## Ad Alanlarını İçe Aktarın

Projenize gerekli ad alanlarının içe aktarıldığından emin olun. C# dosyanızın en üstüne aşağıdaki satırları ekleyin:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Şimdi, OCR görüntü tanımasında satırlar için dikdörtgenleri almanın sürecini adım adım takip edilebilir adımlara ayıralım.

## Adım 1: Belge Dizinini Ayarlayın

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

`"Your Document Directory"` ifadesini örnek görüntünüzün bulunduğu klasörün gerçek yolu ile değiştirin.

## Adım 2: Aspose.OCR'ı Başlatın

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

OCR işlevine erişmek için `AsposeOcr` sınıfının bir örneğini oluşturun.

## Adım 3: Görüntü Yolunu Belirtin

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

OCR uygulamak istediğiniz görüntünün tam yolunu tanımlayın.

## Adım 4: Görüntüyü Tanıyın ve Dikdörtgenleri Alın

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

`GetRectangles` yöntemi, algılanan her metin satırının koordinatlarını temsil eden `Rectangle` nesnelerinin bir listesini döndürür. Bu, **OCR satır dikdörtgenlerini almanın** temelidir.

## Adım 5: Sonucu Yazdırın

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Algılanan alanların koordinatlarını konsola yazdırın. Daha sonra özel işleme için **satır koordinatlarını çıkarmak** amacıyla kullanabileceğiniz değerleri göreceksiniz.

## Neden Satır Dikdörtgenleri İçin Aspose.OCR Kullanmalısınız?

- **Yüksek doğruluk** – Gelişmiş algoritmalar, gürültülü veya eğik görüntülerde bile satırları algılar.  
- **Çapraz platform** – .NET Framework, .NET Core ve .NET 5/6'da çalışır.  
- **Harici bağımlılık yok** – Saf .NET kütüphanesi, gönderilecek yerel DLL yok.  
- **Zengin çıktı** – Satır dikdörtgenlerinin yanı sıra kelimeler, karakterler ve güven skorlarını da alabilirsiniz.

## Yaygın Sorunlar ve Çözümler

| Sorun | Çözüm |
|-------|----------|
| **Dikdörtgen döndürülmedi** | Görüntünün net, yatay metin içerdiğinden ve `AreasType.LINES` belirtildiğinden emin olun. |
| **Yanlış koordinatlar** | Görüntünün DPI değerini kontrol edin; düşük çözünürlüklü görüntüler hatalı sınırlar oluşturabilir. |
| **Büyük görüntülerde performans darboğazı** | `GetRectangles` çağırmadan önce görüntüyü makul bir çözünürlüğe yeniden boyutlandırın. |
| **Lisans istisnası** | Test için deneme lisansı kullanın; değerlendirme sınırlamalarından kaçınmak için üretimde tam lisans uygulayın. |

## SSS'ler

### S1: Aspose.OCR for .NET'i herhangi bir türde görüntüyle kullanabilir miyim?
**C1:** Aspose.OCR, OCR uygulamalarınızda esneklik sağlayan geniş bir görüntü formatı yelpazesini destekler.

### S2: OCR tanıması ne kadar doğru?
**C2:** Aspose.OCR, yüksek doğruluk için gelişmiş algoritmalar kullanır ve çeşitli metin tanıma senaryoları için uygundur.

### S3: Deneme sürümü mevcut mu?
**C3:** Evet, Aspose.OCR for .NET'in yeteneklerini [ücretsiz deneme](https://releases.aspose.com/) ile keşfedebilirsiniz.

### S4: Kapsamlı belgeleri nerede bulabilirim?
**C4:** Ayrıntılı bilgi ve kullanım kılavuzları için [belgelere](https://reference.aspose.com/ocr/net/) bakın.

### S5: Yardıma mı ihtiyacınız var ya da belirli sorularınız mı var?
**C5:** Topluluk desteği ve tartışmalar için [Aspose.OCR forumunu](https://forum.aspose.com/c/ocr/16) ziyaret edin.

## Sık Sorulan Sorular

**S: Tek satırlar yerine tek tek kelimeleri çıkarabilir miyim?**  
**C:** Evet, aynı `GetRectangles` yöntemiyle `AreasType.WORDS` kullanarak kelime‑düzeyinde sınırlayıcı kutular alabilirsiniz.

**S: API çok sayfalı PDF'leri destekliyor mu?**  
**C:** Önce her PDF sayfasını bir görüntüye dönüştürün, ardından her görüntüde `GetRectangles` çağırın.

**S: Döndürülmüş metni nasıl ele alırım?**  
**C:** OCR ayarlarında otomatik döndürme seçeneğini etkinleştirin veya işleme öncesinde görüntüyü önceden döndürün.

**S: Her satır için güven skorlarını elde etmenin bir yolu var mı?**  
**C:** Dikdörtgenleri aldıktan sonra `api.RecognizeImage(...).Lines` çağırarak güven değerlerini içeren satır nesnelerine erişebilirsiniz.

**S: Hangi .NET sürümleri uyumludur?**  
**C:** Kütüphane .NET Framework 4.5+, .NET Core 3.1+ ve .NET 5/6 ile çalışır.

## Sonuç

Tebrikler! Aspose.OCR for .NET kullanarak bir görüntü için **OCR satır dikdörtgenlerini** başarıyla elde ettiniz. Sınırlayıcı kutulara sahip olarak, satır koordinatlarını artık özel render, veri çıkarma veya düzen analizi gibi sonraki iş akışlarına besleyebilirsiniz.

---

**Son Güncelleme:** 2025-12-17  
**Test Edilen Versiyon:** Aspose.OCR 24.11 for .NET  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}