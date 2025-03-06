---
title: OCR Görüntü Tanıma'da Çizgiler için Dikdörtgenler Alma
linktitle: OCR Görüntü Tanıma'da Çizgiler için Dikdörtgenler Alma
second_title: Aspose.OCR .NET API'si
description: Hassas OCR görüntü tanıma anahtarınız olan Aspose.OCR for .NET'i keşfedin. Metin çıkarmanın gücünü zahmetsizce ortaya çıkarın.
weight: 10
url: /tr/net/image-and-drawing-recognition/get-rectangles-for-lines/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Görüntü Tanıma'da Çizgiler için Dikdörtgenler Alma

## giriiş

.NET uygulamalarınızda Optik Karakter Tanıma'nın (OCR) potansiyelinden yararlanmanıza olanak tanıyan güçlü bir araç olan Aspose.OCR for .NET dünyasına hoş geldiniz. İster deneyimli bir geliştirici olun ister meraklı bir meraklı olun, bu kılavuz Aspose.OCR kullanarak OCR görüntü tanımada çizgiler için dikdörtgenler alma sürecinde size yol gösterecektir.

## Önkoşullar

Eğiticiye dalmadan önce aşağıdaki önkoşulların yerine getirildiğinden emin olun:

- C# ve .NET geliştirme konusunda temel bilgiler.
- Visual Studio gibi entegre bir geliştirme ortamı (IDE).
-  Aspose.OCR for .NET kütüphanesi kuruldu. İndirebilirsin[Burada](https://releases.aspose.com/ocr/net/).
- OCR tanıma için metin içeren örnek bir resim.

## Ad Alanlarını İçe Aktar

Projenize aktarılan gerekli ad alanlarına sahip olduğunuzdan emin olun. C# dosyanızın en üstüne aşağıdaki satırları ekleyin:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Şimdi OCR görüntü tanımada çizgiler için dikdörtgenler elde etme sürecini takip edilmesi kolay adımlara ayıralım.

## 1. Adım: Belge Dizininizi Kurun

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

 Yer değiştirmek`"Your Document Directory"` belge dizininizin gerçek yolu ile.

## Adım 2: Aspose.OCR'ı başlatın

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExBitiş:4
```

 Bir örneğini oluşturun`AsposeOcr` OCR işlevselliğine erişmek için sınıf.

## 3. Adım: Görüntü Yolunu Belirleyin

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExBitiş:5
```

OCR gerçekleştirmek istediğiniz görüntünün tam yolunu tanımlayın.

## Adım 4: Görüntüyü Tanıyın ve Dikdörtgenler Alın

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExBitiş:6
```

 Kullanın`GetRectangles` Belirtilen görüntüdeki çizgiler için dikdörtgenleri alma yöntemi.

## Adım 5: Sonucu Yazdır

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExBitiş:7
```

Tespit edilen alanların koordinatlarını konsola yazdırın.

## Çözüm

Tebrikler! Aspose.OCR for .NET'i kullanarak OCR görüntü tanımada çizgiler için dikdörtgenleri başarıyla elde ettiniz. Bu çok yönlü araç, uygulamalarınızda metin çıkarma için bir dünya olasılıklar dünyasının kapılarını açar.

## SSS'ler

### S1: Aspose.OCR for .NET'i herhangi bir görüntü türüyle kullanabilir miyim?

Cevap1: Aspose.OCR çok çeşitli görüntü formatlarını destekleyerek OCR uygulamalarınızda esneklik sağlar.

### S2: OCR tanıma ne kadar doğrudur?

Cevap2: Aspose.OCR, yüksek doğruluk için gelişmiş algoritmalardan yararlanır ve bu da onu çeşitli metin tanıma senaryolarına uygun hale getirir.

### S3: Deneme sürümü mevcut mu?

 C3: Evet, Aspose.OCR for .NET'in özelliklerini şu adresle keşfedebilirsiniz:[ücretsiz deneme](https://releases.aspose.com/).

### S4: Kapsamlı belgeleri nerede bulabilirim?

 A4: Bkz.[dokümantasyon](https://reference.aspose.com/ocr/net/) Detaylı bilgi ve kullanım kılavuzu için.

### S5: Yardıma mı ihtiyacınız var veya özel sorularınız mı var?

 A5: ziyaret edin[Aspose.OCR forumu](https://forum.aspose.com/c/ocr/16) topluluk desteği ve tartışmalar için.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
