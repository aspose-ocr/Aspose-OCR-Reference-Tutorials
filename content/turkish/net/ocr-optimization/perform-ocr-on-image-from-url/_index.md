---
title: OCR Görüntü Tanıma'da URL'den Görüntü üzerinde OCR gerçekleştirin
linktitle: OCR Görüntü Tanıma'da URL'den Görüntü üzerinde OCR gerçekleştirin
second_title: Aspose.OCR .NET API'si
description: Aspose.OCR for .NET ile kusursuz OCR entegrasyonunu keşfedin. Görüntülerdeki metinleri hassasiyetle tanıyın.
type: docs
weight: 10
url: /tr/net/ocr-optimization/perform-ocr-on-image-from-url/
---
## giriiş

Optik Karakter Tanıma (OCR) alanında Aspose.OCR for .NET, geliştiricilerin görüntülerden metin içeriğini hassas bir şekilde ayıklamasına olanak tanıyan güçlü bir araç olarak öne çıkıyor. OCR özelliklerini .NET uygulamanıza entegre etmek ve metin tanımayı zahmetsizce gerçekleştirmek istiyorsanız, bu adım adım kılavuz, bir URL'deki görüntü üzerinde OCR gerçekleştirme sürecinde size yol gösterecektir.

## Önkoşullar

Öğreticiye başlamadan önce aşağıdaki önkoşulların yerine getirildiğinden emin olun:

-  Aspose.OCR for .NET: Aspose.OCR kütüphanesinin .NET projenize entegre olduğundan emin olun. adresinden indirebilirsiniz.[yayın sayfası](https://releases.aspose.com/ocr/net/).

- Geliştirme Ortamı: Makinenizde çalışan bir .NET geliştirme ortamı kurun.

## Ad Alanlarını İçe Aktar

.NET projenize Aspose.OCR işlevlerine erişmek için gerekli ad alanlarını ekleyin. Aşağıdaki kod parçacığını projenize ekleyin:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## 1. Adım: Belge Dizininizi Kurun

 Belgelerinizin saklandığı dizini belirterek başlayın. Yer değiştirmek`"Your Document Directory"` belgelerinizin gerçek yolu ile.

```csharp
string dataDir = "Your Document Directory";
```

## Adım 2: Tanınacak Resmi Alın

OCR gerçekleştirmek istediğiniz görüntünün URL'sini sağlayın. Resmin herkese açık olduğundan emin olun.

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

## 3. Adım: AsposeOcr'u başlatın

OCR işlevlerine erişmek için AsposeOcr sınıfının bir örneğini oluşturun.

```csharp
AsposeOcr api = new AsposeOcr();
```

## Adım 4: Görüntüyü Tanıyın

Belirtilen resim URL'sindeki metni tanımak için Aspose.OCR kitaplığını kullanın. Tanıma ayarlarını gereksinimlerinize göre ayarlayın.

```csharp
RecognitionResult result = api.RecognizeImageFromUri(uri, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    RecognitionAreas = new List<Rectangle>()
    {
        new Rectangle(1,3,390,70),
        new Rectangle(1,72,390,70)
    }
});
```

## Adım 5: Sonucu Yazdır

Tanınan metin, alanlar ve uyarılar dahil olmak üzere tanıma sonucunu görüntüleyin.

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

## Adım 6: Çalıştırın ve Doğrulayın

Uygulamanızı çalıştırın; her şey doğru ayarlanmışsa OCR işleminin başarıyla yürütüldüğünü görmelisiniz.

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## Çözüm

Aspose.OCR for .NET ile OCR yeteneklerini .NET uygulamalarınıza entegre etmek kusursuz bir deneyime dönüşür. Bu eğitim, projelerinizde metin tanımanın gücünden yararlanmanız için bir temel sağlayarak, bir URL'deki bir görüntü üzerinde OCR gerçekleştirme sürecinde size rehberlik etmiştir.

## SSS'ler

### S1: Aspose.OCR birden fazla dili işlemeye uygun mudur?

C1: Evet, Aspose.OCR çeşitli dillerdeki metinlerin tanınmasını destekleyerek uluslararası uygulamalar için çok yönlü olmasını sağlar.

### S2: Aspose.OCR'ı hem tek satırlı hem de çok satırlı metin tanıma için kullanabilir miyim?

A2: Kesinlikle! Aspose.OCR, özel kullanım durumunuza uyum sağlayarak hem tek satırlı hem de çok satırlı metinleri tanıma konusunda esneklik sağlar.

### S3: Aspose.OCR için herhangi bir lisanslama seçeneği mevcut mu?

 C3: Evet, lisanslama seçeneklerini keşfedebilir ve satın alma işlemlerini[Aspose mağaza](https://purchase.aspose.com/buy).

### S4: Aspose.OCR için ücretsiz deneme sürümü mevcut mu?

 Cevap4: Evet, Aspose.OCR'ı ziyaret ederek ücretsiz olarak deneyebilirsiniz.[sürümler sayfası](https://releases.aspose.com/).

### S5: Aspose.OCR ile ilgili desteği veya topluluk tartışmalarını nerede bulabilirim?

 A5: ziyaret edin[Aspose.OCR forumu](https://forum.aspose.com/c/ocr/16) destek ve toplulukla etkileşim için.