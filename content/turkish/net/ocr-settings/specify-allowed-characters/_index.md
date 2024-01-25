---
title: OCR Görüntü Tanıma'da İzin Verilen Karakterleri Belirtin
linktitle: OCR Görüntü Tanıma'da İzin Verilen Karakterleri Belirtin
second_title: Aspose.OCR .NET API'si
description: Aspose.OCR ile .NET'te kusursuz OCR'nin kilidini açın. Resimlerdeki metni zahmetsizce tanıyın. Dönüştürücü bir geliştirme deneyimi için hemen indirin.
type: docs
weight: 13
url: /tr/net/ocr-settings/specify-allowed-characters/
---
## giriiş

Sürekli gelişen teknoloji ortamında, Optik Karakter Tanıma (OCR), makinelerin görüntülerdeki metni anlamasını sağlayan dönüştürücü bir araç olarak ortaya çıktı. Aspose.OCR for .NET, .NET uygulamalarında güçlü OCR özellikleri arayan geliştiricilere kusursuz entegrasyon sağlayan güçlü bir çözüm olarak öne çıkıyor.

## Önkoşullar

Eğiticiye dalmadan önce aşağıdaki önkoşulların mevcut olduğundan emin olun:

- .NET geliştirme konusunda çalışma bilgisi.
-  Aspose.OCR for .NET kütüphanesi. İndirebilirsin[Burada](https://releases.aspose.com/ocr/net/).
- Visual Studio veya tercih edilen herhangi bir .NET geliştirme ortamına aşinalık.

## Ad Alanlarını İçe Aktar

Aspose.OCR for .NET'in işlevselliklerinden etkili bir şekilde yararlanmak için .NET projenize gerekli ad alanlarını içe aktarın:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Şimdi öğreticiyi bir dizi kapsamlı adıma ayıralım:

## Adım 1: OCR Görüntü Tanıma'da İzin Verilen Karakterleri Belirleyin

Başlamak için belge dizininizin yolunu ayarlayın:

```csharp
string dataDir = "Your Document Directory";
```

## Adım 2: Aspose.OCR'ı İzin Verilen Sembollerle Başlatın

İzin verilen sembolleri belirterek bir AsposeOcr örneği oluşturun. Bu durumda, rakamlara (0-9) izin veriyoruz:

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

## 3. Adım: Görüntüyü Tanıyın

Bir görüntüdeki metni tanımak için AsposeOcr örneğini kullanın:

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

## 4. Adım: Tanınan Metni Görüntüleme

Tanınan metni konsola yazdırın:

```csharp
Console.WriteLine(result);
```

## Adım 5: İkinci Durum - Görüntüyü Belirli Ayarlarla Tanıyın

Bu sefer daha spesifik ayarlarla başka bir AsposeOcr örneğini başlatın:

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

## Adım 6: İkinci Durumda Tanınan Metni Görüntüleme

Tanınan metni ikinci durumda konsola yazdırın:

```csharp
Console.WriteLine(result2.RecognitionText);
```

## Adım 7: Başarılı Uygulama

Son olarak SpecifyAllowedCharacters eğitiminin başarıyla yürütüldüğünü onaylayın:

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Bu adımları izleyerek Aspose.OCR for .NET'i kullanarak OCR görüntü tanımada izin verilen karakterleri belirleme özelliğinin kilidini açtınız.

## Çözüm

Aspose.OCR for .NET, geliştiricilerin OCR özelliklerini uygulamalarına sorunsuz bir şekilde entegre etmelerine olanak tanır ve çeşitli alanlarda yenilikçi çözümlerin kapılarını açar. OCR'nin gücünü benimseyin ve doğru metin tanıma özelliğiyle projelerinizi geliştirin.

## SSS'ler

### S1: Aspose.OCR for .NET hem yeni başlayanlar hem de deneyimli geliştiriciler için uygun mu?

A1: Kesinlikle! Aspose.OCR for .NET, kusursuz entegrasyon için sezgisel işlevler sağlayarak her seviyedeki geliştiriciye hitap eder.

### S2: Aspose.OCR for .NET'i birden fazla dildeki karakterleri tanımak için kullanabilir miyim?

C2: Evet, Aspose.OCR çeşitli dillerde tanımayı destekleyerek çeşitli uygulamalar için çok yönlü hale getiriyor.

### S3: Aspose.OCR for .NET ne sıklıkta güncellenir?

 C3: En son teknolojilerle uyumluluğu sağlamak ve olası sorunları çözmek için güncellemeler düzenli olarak yayınlanmaktadır. Kontrol edin[dokümantasyon](https://reference.aspose.com/ocr/net/) En son bilgiler için.

### S4: Aspose.OCR for .NET'in ücretsiz deneme sürümü mevcut mu?

 Cevap4: Evet, Aspose.OCR'ın yeteneklerini aşağıdaki dosyayı indirerek keşfedebilirsiniz.[ücretsiz deneme](https://releases.aspose.com/).

### S5: Nereden yardım alabilirim veya destek için toplulukla bağlantı kurabilirim?

 A5: ziyaret edin[Aspose.OCR forumu](https://forum.aspose.com/c/ocr/16) toplulukla etkileşime geçmek ve uzman yardımı almak.