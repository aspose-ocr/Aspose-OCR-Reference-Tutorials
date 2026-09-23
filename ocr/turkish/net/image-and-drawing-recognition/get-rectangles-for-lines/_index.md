---
date: 2026-02-22
description: Aspose.OCR for .NET kullanarak bir görüntüdeki metin satırlarını tanıyarak
  ve satır dikdörtgenlerini çıkararak yerleşim analizi OCR nasıl yapılır öğrenin.
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: Düzen Analizi OCR – Görüntülerden Satır Dikdörtgenlerini Al
url: /tr/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Düzen Analizi OCR – Görüntülerden Satır Dikdörtgenlerini Al

## Giriş

Bu öğreticide Aspose.OCR for .NET ile **OCR satır dikdörtgenlerini nasıl alacağınızı** keşfedeceksiniz. Kılavuzun sonunda **bir görüntüdeki metin satırlarını tanıyabilecek** ve **her algılanan satır için satır koordinatlarını çıkarabilecek** olacaksınız—bu, **düzen analizi OCR**, veri çıkarma veya özel renderleme gibi sonraki işlemler için mükemmeldir.

## Hızlı Yanıtlar
- **“OCR satır dikdörtgenlerini al” ne anlama geliyor?** Görüntüde algılanan her metin satırının sınırlayıcı kutularını döndürür.  
- **Hangi API yöntemi kullanılıyor?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Lisans gerekli mi?** Geliştirme için ücretsiz deneme çalışır; üretim için ticari lisans gerekir.  
- **Desteklenen görüntü formatları?** PNG, JPEG, BMP, TIFF ve daha fazlası.  
- **Bunu .NET Core’da çalıştırabilir miyim?** Evet, Aspose.OCR .NET Core ve .NET 5/6’yı tam olarak destekler.

## Önkoşullar

Öğreticiye başlamadan önce aşağıdaki önkoşulların yerine getirildiğinden emin olun:

- C# ve .NET geliştirme hakkında temel bilgi.  
- Visual Studio gibi bir bütünleşik geliştirme ortamı (IDE).  
- Aspose.OCR for .NET kütüphanesi yüklü. Bunu [buradan](https://releases.aspose.com/ocr/net/) indirebilirsiniz.  
- OCR tanıması için metin içeren bir örnek görüntü.

## Ad Alanlarını İçe Aktarın

Projenize gerekli ad alanlarını eklediğinizden emin olun. C# dosyanızın en üstüne aşağıdaki satırları ekleyin:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Şimdi OCR görüntü tanımasında satırlar için dikdörtgenleri elde etme sürecini adım adım inceleyelim.

## Düzen Analizi OCR – Adım Adım Kılavuz

### Adım 1: Belge Dizinini Ayarlayın

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

`"Your Document Directory"` ifadesini örnek görüntünüzün bulunduğu klasörün gerçek yolu ile değiştirin.

### Adım 2: Aspose.OCR’ı Başlatın

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

OCR işlevselliğine erişmek için `AsposeOcr` sınıfının bir örneğini oluşturun.

### Adım 3: Görüntü Yolunu Belirtin

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

OCR uygulamak istediğiniz görüntünün tam yolunu tanımlayın.

### Adım 4: Görüntüyü Tanıyın ve Dikdörtgenleri Alın

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

`GetRectangles` yöntemi, algılanan bir metin satırının koordinatlarını temsil eden `Rectangle` nesnelerinin bir listesini döndürür. Bu, **OCR satır dikdörtgenlerini almanın** temelidir ve **düzen analizi OCR**’a olanak tanır.

### Adım 5: Sonucu Yazdırın

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Algılanan alanların koordinatlarını konsola yazdırın. Daha sonra **satır koordinatlarını çıkarmak** için özel işleme kullanabileceğiniz değerleri göreceksiniz.

## Neden Aspose.OCR Satır Dikdörtgenleri İçin Kullanılmalı?

- **Yüksek doğruluk** – Gelişmiş algoritmalar, gürültülü veya eğik görüntülerde bile satırları algılar.  
- **Çapraz platform** – .NET Framework, .NET Core ve .NET 5/6 üzerinde çalışır.  
- **Harici bağımlılık yok** – Saf .NET kütüphanesi, gönderilecek yerel DLL bulunmaz.  
- **Zengin çıktı** – Satır dikdörtgenlerinin yanı sıra kelimeler, karakterler ve güven skorlarını da alabilirsiniz.

## Yaygın Sorunlar ve Çözümler

| Sorun | Çözüm |
|-------|----------|
| **Dikdörtgen döndürülmüyor** | Görüntünün net, yatay metin içerdiğinden ve `AreasType.LINES` belirtildiğinden emin olun. |
| **Koordinatlar hatalı** | Görüntünün DPI değerini kontrol edin; düşük çözünürlüklü görüntüler hatalı sınırlara yol açabilir. |
| **Büyük görüntülerde performans sorunu** | `GetRectangles` çağırmadan önce görüntüyü makul bir çözünürlüğe yeniden boyutlandırın. |
| **Lisans istisnası** | Test için deneme lisansı kullanın; üretimde değerlendirme sınırlamalarını önlemek için tam lisans uygulayın. |

## Sık Sorulan Sorular

**S: Tüm satırlar yerine tek tek kelimeleri çıkarabilir miyim?**  
C: Evet, aynı `GetRectangles` yöntemiyle `AreasType.WORDS` kullanarak kelime‑düzeyinde sınırlayıcı kutular elde edebilirsiniz.

**S: API çok sayfalı PDF’leri destekliyor mu?**  
C: Önce her PDF sayfasını bir görüntüye dönüştürün, ardından her görüntüde `GetRectangles` çağırın.

**S: Döndürülmüş metni nasıl ele alırım?**  
C: OCR ayarlarında otomatik döndürme seçeneğini etkinleştirin veya işlemden önce görüntüyü önceden döndürün.

**S: Her satır için güven skorlarını almak mümkün mü?**  
C: Dikdörtgenleri aldıktan sonra `api.RecognizeImage(...).Lines` çağırarak güven değeri içeren satır nesnelerine erişebilirsiniz.

**S: Hangi .NET sürümleri uyumlu?**  
C: Kütüphane .NET Framework 4.5+, .NET Core 3.1+ ve .NET 5/6 ile çalışır.

## Gerçek Dünya Kullanım Senaryoları

- **Belge düzen analizi OCR** – Satır dikdörtgenlerini bir düzen motoruna besleyerek sütun yapılarını yeniden oluşturun.  
- **Otomatik veri çıkarma** – Koordinatları, sonraki NLP boru hatları için bireysel satırları kırpmak amacıyla kullanın.  
- **Özel renderleme** – Görsel doğrulama veya UI bindirmeleri için orijinal görüntünün üzerine sınırlama kutuları yerleştirin.  

## Sonuç

Tebrikler! Aspose.OCR for .NET kullanarak bir görüntü için **OCR satır dikdörtgenlerini** başarıyla elde ettiniz. Sınırlayıcı kutular elinizde olduğuna göre, artık satır koordinatlarını özel renderleme, veri çıkarma veya **düzen analizi OCR** gibi sonraki iş akışlarına besleyebilirsiniz.

---

**Son Güncelleme:** 2026-02-22  
**Test Edilen Versiyon:** Aspose.OCR 24.11 for .NET  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}