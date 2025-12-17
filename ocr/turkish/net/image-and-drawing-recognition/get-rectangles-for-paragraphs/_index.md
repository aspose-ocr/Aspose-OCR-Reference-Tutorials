---
date: 2025-12-17
description: Aspose.OCR for .NET kullanarak OCR görüntülerindeki paragraflar için
  dikdörtgenleri nasıl çıkaracağınızı öğrenin – dikdörtgenleri çıkarmak ve paragraf
  koordinatlarını elde etmek için başvurulacak rehber.
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: OCR Görüntü Tanıma'da Paragraflar İçin Dikdörtgenleri Nasıl Çıkarılır
url: /tr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Görüntü Tanıma'da Paragraflar İçin Dikdörtgenleri Nasıl Çıkarılır

## Introduction

Aspose.OCR for .NET ile OCR görüntü tanıma sürecinde paragraflar için **dikdörtgenleri nasıl çıkaracağınızı** anlatan kapsamlı rehberimize hoş geldiniz. Belge işleme hattınızı geliştirmek, paragraf sınırlarını çıkarmak ve veri çıkarımını otomatikleştirmek istiyorsanız doğru yerdesiniz. Ortamı kurmaktan dikdörtgen koordinatlarını yazdırmaya kadar her adımı adım adım göstereceğiz, böylece OCR sonuçlarını hemen kullanmaya başlayabilirsiniz.

## Quick Answers
- **“extract rectangles” ne anlama geliyor?** Algılanan metin alanlarının sınırlayıcı kutularını (x, y, genişlik, yükseklik) döndürür.  
- **Hangi API yöntemi dikdörtgenleri sağlar?** `AsposeOcr.GetRectangles` ve `AreasType.PARAGRAPHS`.  
- **Geliştirme için lisansa ihtiyacım var mı?** Test için ücretsiz deneme çalışır; üretim için ticari lisans gereklidir.  
- **Birden fazla resmi aynı anda işleyebilir miyim?** Evet—resim listeniz üzerinde döngü kurup her dosya için `GetRectangles` çağırabilirsiniz.  
- **Hangi formatlar destekleniyor?** PNG, JPEG, TIFF, BMP ve daha birçok format.

## What is “how to extract rectangles” in OCR?
OCR terminolojisinde, dikdörtgenleri çıkarmak, bir görüntü içindeki her paragraf veya satır metnin etrafını çevreleyen geometrik sınırları belirlemek anlamına gelir. Bu koordinatlar, taranmış bir belgenin belirli bölümlerini vurgulamanıza, kırpmanıza veya daha ileri analiz yapmanıza olanak tanır.

## Why extract paragraph coordinates?
- **Precise post‑processing** – her dikdörtgeni sonraki iş akışlarına (ör. çeviri, redaksiyon) besleyebilirsiniz.  
- **Improved UI/UX** – orijinal görüntü üzerine sınırlayıcı kutuları yerleştirerek kullanıcılara metnin nerede bulunduğunu gösterebilirsiniz.  
- **Batch automation** – büyük belge setlerinde paragrafları hızlıca bulup izole edebilirsiniz.

## Prerequisites

- C# ve .NET geliştirme konusunda temel bilgi.  
- Aspose.OCR for .NET yüklü bir geliştirme ortamı – bunu [buradan](https://releases.aspose.com/ocr/net/) indirebilirsiniz.  
- Görüntü işleme kavramlarına aşina olmak ve OCR’ın taranmış dosyalardan metin çıkarmadaki önemini anlamak.

## Import Namespaces

C# dosyanızda OCR sınıflarının kullanılabilmesi için gerekli ad alanlarını içe aktarın:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Step 1: Set Up Your Document Directory

Analiz etmek istediğiniz görüntüleri içeren klasörü tanımlayın:

```csharp
string dataDir = "Your Document Directory";
```

## Step 2: Initialize AsposeOcr Instance

Bir `AsposeOcr` nesnesi oluşturun – bu, tüm OCR işlevlerine erişmenizi sağlar:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Step 3: Specify the Image Path

İşlemek istediğiniz tam görüntü dosyasına işaret edin:

```csharp
string fullPath = dataDir + "sample.png";
```

## Step 4: Recognize Image and Get Paragraph Rectangles

`GetRectangles` metodunu çağırın. `detect_areas` parametresini `true` olarak ayarlamak, motorun **paragraf** dikdörtgenlerini döndürmesini sağlar:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Step 5: Print Results

Koordinatları çıktılayarak tespit edilen **paragraf koordinatlarını** görebilirsiniz:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Common Issues and Solutions

| Issue | Reason | Fix |
|-------|--------|-----|
| No rectangles returned | Görüntü kalitesi çok düşük veya yanlış `AreasType` | Görüntünün net olduğundan emin olun ve `AreasType.PARAGRAPHS` kullanın. |
| Coordinates are off‑by‑one | DPI ölçekleme uyumsuzluğu | Görüntüyü yüklerken doğru DPI'yi ayarlayın veya `api.Config.Dpi` kullanın. |
| License exception | Üretimde geçerli bir lisans olmadan çalıştırılıyor | `api.SetLicense` ile geçici veya kalıcı bir lisans uygulayın. |

## Frequently Asked Questions

**Q: Aspose.OCR farklı görüntü formatlarıyla uyumlu mu?**  
A: Evet, Aspose.OCR PNG, JPEG, TIFF, BMP ve birçok yaygın formatı destekler.

**Q: Aspose.OCR'ı birden fazla görüntünün toplu işlenmesi için kullanabilir miyim?**  
A: Kesinlikle! Dosya yolu koleksiyonunu döngüye alıp her görüntü için `GetRectangles` çağırabilirsiniz.

**Q: Aspose.OCR for .NET için ücretsiz bir deneme mevcut mu?**  
A: Evet, ücretsiz denemeyi [buradan](https://releases.aspose.com/) keşfedebilirsiniz.

**Q: Aspose.OCR için geçici bir lisans nasıl alınır?**  
A: Geçici lisansı [buradan](https://purchase.aspose.com/temporary-license/) temin edebilirsiniz.

**Q: Aspose.OCR ile ilgili ek destek ve tartışmalara nereden ulaşabilirim?**  
A: Topluluk desteği ve tartışmalar için [Aspose.OCR forumuna](https://forum.aspose.com/c/ocr/16) göz atabilirsiniz.

## Conclusion

Bu öğreticide, Aspose.OCR for .NET kullanarak paragraflar için **dikdörtgenleri nasıl çıkaracağınızı** gösterdik, her kod parçacığını adım adım inceledik ve döndürülen koordinatların nasıl yorumlanacağını açıkladık. Bu adımları uygulamanıza entegre ederek paragraf sınırlarını güvenilir bir şekilde çıkarabilir, belge iş akışlarını iyileştirebilir ve daha akıllı OCR‑tabanlı çözümler geliştirebilirsiniz.

---

**Last Updated:** 2025-12-17  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}