---
title: OCR Görüntü Tanıma'da Klasörle OCR İşlemi
linktitle: OCR Görüntü Tanıma'da Klasörle OCR İşlemi
second_title: Aspose.OCR .NET API'si
description: Aspose.OCR ile .NET'te OCR görüntü tanımanın gücünün kilidini açın. Görüntülerden metni zahmetsizce çıkarın.
weight: 11
url: /tr/net/ocr-configuration/ocr-operation-with-folder/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Görüntü Tanıma'da Klasörle OCR İşlemi

## giriiş

Aspose.OCR for .NET kullanarak Optik Karakter Tanıma (OCR) dünyasına hoş geldiniz! .NET uygulamalarınızda görsellerden sorunsuz bir şekilde metin çıkarmak istiyorsanız doğru yerdesiniz. Bu eğitim, Aspose.OCR'ın güçlü özelliklerinden yararlanarak, klasörlerle OCR görüntü tanıma sürecinde size rehberlik edecektir.

## Önkoşullar

Eğiticiye dalmadan önce aşağıdaki önkoşullara sahip olduğunuzdan emin olun:

- C# ve .NET geliştirme konusunda çalışma bilgisi.
- Makinenizde Visual Studio yüklü.
-  İndirebileceğiniz Aspose.OCR for .NET kütüphanesi[Burada](https://releases.aspose.com/ocr/net/).
- OCR kavramlarının temel anlayışı.

## Ad Alanlarını İçe Aktar

Aspose.OCR'ı kullanmak için C# kodunuzda gerekli ad alanlarını içe aktardığınızdan emin olun. Komut dosyanızın başına aşağıdakileri ekleyin:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 1. Adım: Belge Dizinini Ayarlayın

```csharp
// ExStart:1
// Belgeler dizininin yolu.
string dataDir = "Your Document Directory";
```

"Belge Dizininiz"i, resimlerinizin depolandığı gerçek yolla değiştirdiğinizden emin olun.

## Adım 2: Aspose.OCR'ı başlatın

```csharp
// AsposeOcr örneğini başlat
AsposeOcr api = new AsposeOcr();
```

İşlevlerinden yararlanmak için AsposeOcr sınıfının bir örneğini oluşturun.

## 3. Adım: Görüntü Yolunu Belirleyin

```csharp
//Resim Yolu
string fullPath = dataDir + "OCR";
```

Belge dizini yolunu, resimlerinizi içeren belirli klasörle birleştirin.

## Adım 4: Görüntüleri Tanıma

```csharp
// Resmi tanı
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
    //varsayılan veya özel
});
```

Belirtilen klasördeki birden fazla görüntü üzerinde OCR gerçekleştirmek için RecognizeMultipleImages yöntemini kullanın.

## Adım 5: Sonuçları Yazdır

```csharp
// Sonucu yazdır
for (int i = 0; i < result.Length; i++)
{
    Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
```

Sonuçlar arasında dolaşın ve her görüntü için tanınan metni yazdırın.

## Adım 6: Sonuç

```csharp
// ExEnd:1
Console.WriteLine("OCROperationWithFolder executed successfully");
```

OCR işleminin klasörlerle başarılı bir şekilde yürütüldüğünü belirtmek için komut dosyanızın sonucuna ulaşıldığından emin olun.

## Çözüm

Tebrikler! Aspose.OCR for .NET kullanarak OCR görüntü tanımayı klasörlere nasıl uygulayacağınızı başarıyla öğrendiniz. Bu güçlü araç, .NET uygulamalarınızdaki resimlerden metin çıkarmak için sayısız olasılığın kapısını açar.

## SSS'ler

### S1: Aspose.OCR for .NET'i ticari projelerde kullanabilir miyim?

 Cevap1: Evet, Aspose.OCR for .NET ticari bir üründür. Lisans bilgileri için şu adresi ziyaret edin:[Burada](https://purchase.aspose.com/buy).

### S2:. Ücretsiz deneme mevcut mu?

 A2: Evet, ücretsiz deneme sürümünü keşfedebilirsiniz[Burada](https://releases.aspose.com/).

### S3: Belgeleri nerede bulabilirim?

 A3: Belgeler mevcut[Burada](https://reference.aspose.com/ocr/net/).

### S4: Geçici lisansı nasıl alabilirim?

 Cevap4: Geçici lisanslar alınabilir[Burada](https://purchase.aspose.com/temporary-license/).

### S5: Desteğe mi ihtiyacınız var veya sorularınız mı var?

 A5: ziyaret edin[Aspose.OCR forumu](https://forum.aspose.com/c/ocr/16) topluluk desteği için.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
