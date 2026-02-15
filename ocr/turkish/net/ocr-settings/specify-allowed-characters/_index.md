---
description: Aspose.OCR for .NET ile izin verilen karakterleri nasıl belirleyeceğinizi
  öğrenin ve rakam görüntülerini verimli bir şekilde tanıyın. OCR'yi yalnızca rakamlara
  sınırlamak için adım adım kılavuzu izleyin.
linktitle: Specify Allowed Characters OCR – Using Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: İzin Verilen Karakterleri Belirleyin OCR – .NET için Aspose.OCR Kullanarak
url: /tr/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# İzin Verilen Karakterleri Belirleme OCR – Aspose.OCR for .NET Kullanarak

Bu öğreticide, Aspose.OCR for .NET ile **specify allowed characters ocr** nasıl yapılacağını öğrenecek ve OCR çıktısını yalnızca ihtiyacınız olan karakterlerle sınırlayabileceksiniz. Bu, seri numaraları, fatura kimlikleri veya barkod benzeri dizeler gibi **recognize digits image** dosyalarını tanımanız gerektiğinde özellikle kullanışlıdır. Kurulumu, kodu ve birkaç pratik senaryoyu adım adım inceleyecek ve tekniği hemen uygulayabileceksiniz.

## Hızlı Yanıtlar
- **What does “specify allowed characters ocr” do?** OCR'ı önceden tanımlanmış bir karakter kümesiyle sınırlar, hedef veriler için doğruluğu artırır.  
- **Which characters can I allow?** İhtiyacınız olan herhangi bir kombinasyon—rakamlar, harfler veya özel semboller (ör. “0123456789”).  
- **Why limit characters?** Beklenen karakter kümesi bilindiğinde yanlış tanıma oranını azaltır ve işleme hızını artırır.  
- **Do I need a license?** Geliştirme için ücretsiz deneme sürümü çalışır; üretim için ticari lisans gereklidir.  
- **Which .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## “specify allowed characters ocr” nedir?
OCR bir görüntüyü taradığında, her görsel deseni olası karakterlerin tam alfabesiyle eşleştirmeye çalışır. **specify allowed characters ocr** sayesinde, motoru beyaz listenizin dışındaki her şeyi yok saymaya yönlendirirsiniz; bu da sınırlı veri setleri için tanıma doğruluğunu büyük ölçüde artırır.

## Neden Aspose.OCR ile digits image tanımalısınız?
Aspose.OCR, .NET geliştiricileri için temiz ve akıcı bir API sunar. Yerleşik `AllowedCharacters` seçeneği, özel bir sonrası işleme mantığı yazmadan yalnızca rakam senaryolarına odaklanmanızı sağlar. Bu aşağıdakiler için mükemmeldir:
- Sayaç okumalarını, fatura numaralarını veya ürün kodlarını okuma.  
- Taranan formlardan elde edilen kullanıcı girişi verilerini doğrulama.  
- Karakter kümesinin önceden bilindiği toplu işleme süreçlerini hızlandırma.

## Önkoşullar

Before diving into the code, make sure you have:

- .NET geliştirme konusunda çalışır bilgi.  
- **Aspose.OCR for .NET** kütüphanesi. Bunu [buradan](https://releases.aspose.com/ocr/net/) indirebilirsiniz.  
- Visual Studio (veya tercih ettiğiniz herhangi bir .NET IDE).  

## Ad Alanlarını İçe Aktarın

In your .NET project, import the necessary namespaces to leverage Aspose.OCR functionality:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Şimdi, öğreticiyi kapsamlı adımlar serisine ayıralım:

## İzin Verilen Karakterleri OCR Belirleme – Adım Adım Kılavuz

### Adım 1: Görüntü klasörünüzün yolunu ayarlayın

İlk olarak, örnek görüntülerinizin nerede saklandığını tanımlayın.

```csharp
string dataDir = "Your Document Directory";
```

### Adım 2: Aspose.OCR'ı yalnızca rakam beyaz listesiyle başlatın

Bir `AsposeOcr` örneği oluşturun ve izin vermek istediğiniz karakterleri geçirin—bu örnekte tüm rakamlar.

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### Adım 3: Rakam içeren tek bir satırı tanıyın

`RecognizeLine` metodunu kullanarak yalnızca sayı içeren bir görüntüden metni çıkarın.

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### Adım 4: Tanınan rakamları çıktıya verin

Sonucu konsola yazdırın, böylece çıktıyı doğrulayabilirsiniz.

```csharp
Console.WriteLine(result);
```

### Adım 5: Daha fazla kontrol için RecognitionSettings kullanın

Daha ince kontrol gerekiyorsa—örneğin tek satır tanımayı zorlamak gibi—`RecognitionSettings` kabul eden aşırı yüklemeyi kullanabilirsiniz.

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### Adım 6: İkinci durum sonucunu gösterin

```csharp
Console.WriteLine(result2.RecognitionText);
```

### Adım 7: Başarılı yürütmeyi doğrulayın

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Bu adımları izleyerek, **specify allowed characters ocr** ve Aspose.OCR for .NET kullanarak **recognize digits image** içeriğini verimli bir şekilde nasıl tanıyacağınızı öğrendiniz.

## Yaygın Tuzaklar ve Sorun Giderme
- **Empty result:** Görüntü kalitesinin yeterli olduğundan emin olun (net kontrast, minimum gürültü).  
- **Wrong characters returned:** Beyaz liste dizesinin beklediğiniz karakterlerle tam olarak eşleştiğini iki kez kontrol edin.  
- **File not found:** `dataDir`'in doğru klasöre işaret ettiğini ve dosya adının büyük/küçük harfe duyarlı olarak eşleştiğini doğrulayın.

## Sık Sorulan Sorular

### Q1: Aspose.OCR for .NET hem yeni başlayanlar hem de deneyimli geliştiriciler için uygun mu?  
**A:** Kesinlikle! API, yeni başlayanlar için sezgisel olacak şekilde tasarlanmış, aynı zamanda ileri düzey kullanıcılar için gelişmiş seçenekler sunar.

### Q2: Aspose.OCR for .NET'i birden fazla dilde karakter tanımak için kullanabilir miyim?  
**A:** Evet, Aspose.OCR geniş bir dil yelpazesini destekler. Çok dilli senaryolar için allowed‑characters özelliğiyle dil paketlerini birleştirebilirsiniz.

### Q3: Aspose.OCR for .NET ne sıklıkla güncellenir?  
**A:** Yeni özellikler eklemek, doğruluğu artırmak ve uyumluluğu sağlamak için düzenli olarak güncellemeler yayınlanır. En son sürüm detayları için [documentation](https://reference.aspose.com/ocr/net/) adresini kontrol edin.

### Q4: Aspose.OCR for .NET için ücretsiz bir deneme sürümü var mı?  
**A:** Evet, [free trial](https://releases.aspose.com/) indirerek özellikleri keşfedebilirsiniz.

### Q5: Yardım almak veya toplulukla iletişime geçmek için nereden ulaşabilirim?  
**A:** Sorular sormak, deneyimlerinizi paylaşmak ve Aspose mühendisleri ile diğer geliştiricilerden yardım almak için [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) adresini ziyaret edin.

---

**Son Güncelleme:** 2026-02-15  
**Test Edilen Versiyon:** Aspose.OCR 24.11 for .NET  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}