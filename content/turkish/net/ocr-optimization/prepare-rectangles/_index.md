---
title: OCR Görüntü Tanıma'da Dikdörtgenler Hazırlama
linktitle: OCR Görüntü Tanıma'da Dikdörtgenler Hazırlama
second_title: Aspose.OCR .NET API'si
description: Kapsamlı kılavuzumuzla Aspose.OCR for .NET'in potansiyelini ortaya çıkarın. Görüntü tanıma için dikdörtgenlerin nasıl hazırlanacağını adım adım öğrenin. Sorunsuz OCR entegrasyonuyla .NET uygulamalarınızı yükseltin.
type: docs
weight: 11
url: /tr/net/ocr-optimization/prepare-rectangles/
---
## giriiş

Sürekli gelişen teknoloji ortamında, Optik Karakter Tanıma (OCR), görüntüleri makine tarafından okunabilir metne dönüştürmede çok önemli bir rol oynamaktadır. Aspose.OCR for .NET, OCR yeteneklerinin .NET uygulamalarına kusursuz entegrasyonunu arayan geliştiriciler için güçlü bir çözüm olarak öne çıkıyor. Bu kapsamlı kılavuzda Aspose.OCR for .NET kullanarak OCR görüntü tanımada dikdörtgen hazırlama sürecini inceleyeceğiz.

## Önkoşullar

Eğiticiye dalmadan önce aşağıdaki önkoşulların yerine getirildiğinden emin olun:

- .NET geliştirme konusunda çalışma bilgisi.
-  Aspose.OCR for .NET kütüphanesi kuruldu. İndirebilirsin[Burada](https://releases.aspose.com/ocr/net/).
- Görüntü tanıma kavramlarının temel anlayışı.

## Ad Alanlarını İçe Aktar

OCR yolculuğumuzu başlatmak için gerekli ad alanlarını içe aktararak başlayalım:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 1. Adım: Belge Dizininizi Kurun

 Belgelerinizin saklandığı dizini belirterek başlayın. Yer değiştirmek`"Your Document Directory"` belgelerinizin gerçek yolu ile.

```csharp
// Belgeler dizininin yolu.
string dataDir = "Your Document Directory";

// AsposeOcr örneğini başlat
AsposeOcr api = new AsposeOcr();
```

## Adım 2: Birden Çok Dikdörtgenli Görüntüyü Tanıyın

Bu adımda, birden çok dikdörtgen kullanarak bir görüntüdeki metnin nasıl tanınacağını göstereceğiz. Şu alt adımları izleyin:

### 2.1 Dikdörtgenleri Tanımlayın

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### 2.2 OCR Tanıma İşlemini Gerçekleştirin

```csharp
// ilk durum
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Tanınan metni görüntüle
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## 3. Adım: Tanıma Ayarlarıyla Görüntüyü Tanıyın

Bu adımda, görüntü tanıma için RecognitionSettings'i kullanan alternatif bir yöntemi göstereceğiz:

### 3.1 Tanıma Ayarlarını Tanımlayın

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### 3.2 Tanınan Metni Görüntüleme

```csharp
// Tanınan metni görüntüle
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Çözüm

Tebrikler! Aspose.OCR for .NET'i kullanarak OCR görüntü tanımada dikdörtgen hazırlama sürecini başarıyla tamamladınız. Bu kılavuz, OCR'yi .NET uygulamalarınıza sorunsuz bir şekilde entegre etmenizi sağlayarak metin tanıma yeteneklerini geliştirmenizi sağlar.

### SSS'ler

### S1: Aspose.OCR for .NET'i diğer .NET çerçeveleriyle kullanabilir miyim?

Cevap1: Evet, Aspose.OCR for .NET çeşitli .NET çerçeveleriyle uyumludur.

### S2: Aspose.OCR for .NET'in ücretsiz deneme sürümü mevcut mu?

 A2: Kesinlikle! Ücretsiz deneme sürümüne erişebilirsiniz[Burada](https://releases.aspose.com/).

### S3: Aspose.OCR for .NET desteğini nasıl alabilirim?

 A3: Ziyaret edin[Aspose.OCR forumu](https://forum.aspose.com/c/ocr/16) özel destek için.

### S4: Test amacıyla geçici bir lisans alabilir miyim?

 Cevap4: Evet, geçici bir lisans alabilirsiniz[Burada](https://purchase.aspose.com/temporary-license/).

### S5: Aspose.OCR for .NET belgelerini nerede bulabilirim?

 A5: Belgeler mevcut[Burada](https://reference.aspose.com/ocr/net/).