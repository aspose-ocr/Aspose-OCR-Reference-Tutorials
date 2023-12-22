---
title: OCR Görüntü Tanıma'da Paragraflar için Dikdörtgenler Alma
linktitle: OCR Görüntü Tanıma'da Paragraflar için Dikdörtgenler Alma
second_title: Aspose.OCR .NET API'si
description: Aspose.OCR for .NET ile gelişmiş OCR özelliklerinin kilidini açın. Paragraf dikdörtgenlerini zahmetsizce çıkarın.
type: docs
weight: 11
url: /tr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
---
## giriiş

OCR görüntü tanımada paragraf dikdörtgenlerini çıkarmak için Aspose.OCR for .NET'ten yararlanmaya ilişkin kapsamlı kılavuzumuza hoş geldiniz. Belge işleme yeteneklerinizi geliştirmek ve .NET uygulamalarınızda Optik Karakter Tanıma'nın (OCR) gücünden yararlanmak istiyorsanız doğru yerdesiniz.

## Önkoşullar

Eğiticiye dalmadan önce aşağıdaki önkoşulların mevcut olduğundan emin olun:

- C# ve .NET geliştirme konusunda temel bilgiler.
-  Aspose.OCR for .NET ile oluşturulmuş bir geliştirme ortamı. Henüz yapmadıysanız indirebilirsiniz[Burada](https://releases.aspose.com/ocr/net/).
- Görüntü işleme kavramlarının anlaşılması ve görüntülerden metin çıkarmada OCR'nin önemi.

## Ad Alanlarını İçe Aktar

Aspose.OCR'ı verimli bir şekilde kullanmak için C# kodunuzda gerekli ad alanlarının içe aktarıldığından emin olun. Dosyanızın en üstüne aşağıdakileri ekleyin:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 1. Adım: Belge Dizininizi Kurun

OCR işleme için görüntülerin saklandığı belge dizininizin yolunu başlatarak başlayın:

```csharp
string dataDir = "Your Document Directory";
```

## Adım 2: AsposeOcr Örneğini Başlatın

OCR işlevlerine erişim kazanmak için AsposeOcr sınıfının bir örneğini oluşturun:

```csharp
AsposeOcr api = new AsposeOcr();
```

## 3. Adım: Görüntü Yolunu Belirleyin

İşlemek istediğiniz görüntünün tam yolunu tanımlayın:

```csharp
string fullPath = dataDir + "sample.png";
```

## Adım 4: Görüntüyü Tanıyın ve Paragraf Dikdörtgenlerini Alın

 Çağır`GetRectangles` OCR görüntüsündeki paragraflar için dikdörtgenler elde etme yöntemi. Ayarlamak`detect_areas` ile`true` paragrafları çıkarmak istiyorsanız:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Adım 5: Sonuçları Yazdır

Tanımlanan alanların koordinatlarını yazdırın:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Adım 6: Sonuç

Tebrikler! Aspose.OCR for .NET kullanarak paragraflar için dikdörtgenler elde etmek amacıyla OCR görüntü tanıma işlemini başarıyla gerçekleştirdiniz.

## Çözüm

Bu eğitimde Aspose.OCR for .NET'i uygulamalarınıza entegre etmenin ve OCR ile işlenmiş görüntülerden paragraf dikdörtgenleri çıkarmanızı sağlayacak temel adımları inceledik. Aspose.OCR, OCR'nin uygulanmasını basitleştirerek onu belge işleme ve metin çıkarma için değerli bir araç haline getirir.

## SSS'ler

### S1: Aspose.OCR farklı görüntü formatlarıyla uyumlu mudur?

Cevap1: Evet, Aspose.OCR PNG, JPEG ve TIFF dahil olmak üzere çeşitli görüntü formatlarını destekler.

### S2: Aspose.OCR'ı birden fazla görüntünün toplu işlenmesi için kullanabilir miyim?

A2: Kesinlikle! Aspose.OCR, birden fazla görüntüyü sorunsuz bir şekilde işlemek için toplu işlemeyi kolaylaştırır.

### S3: Aspose.OCR for .NET'in ücretsiz deneme sürümü mevcut mu?

 C3: Evet, ücretsiz deneme sürümünü keşfedebilirsiniz[Burada](https://releases.aspose.com/).

### S4: Aspose.OCR için nasıl geçici lisans alabilirim?

 Cevap4: Geçici bir lisans alabilirsiniz[Burada](https://purchase.aspose.com/temporary-license/).

### S5: Aspose.OCR ile ilgili ek destek ve tartışmaları nerede bulabilirim?

 A5: Şuraya gidin:[Aspose.OCR forumu](https://forum.aspose.com/c/ocr/16) topluluk desteği ve tartışmalar için.