---
date: 2025-12-27
description: Aspose.OCR for .NET ile gelişmiş OCR dil desteği ve yeteneklerini keşfedin.
  Verimli, doğru ve geliştirici dostu.
linktitle: OCR Language Support – Ignored Characters in Image Recognition
second_title: Aspose.OCR .NET API
title: OCR Dil Desteği – Görüntü Tanıma'da Yoksayılan Karakterler
url: /tr/net/ocr-settings/specify-ignored-characters/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Dil Desteği: Görüntü Tanıma İçinde Yoksayılan Karakterleri Belirtme

## Giriş

OCR dil desteği, modern belge otomasyonunun temel taşlarından biridir; uygulamaların birçok alfabe ve sembolden oluşan görüntülerdeki metni okumasını sağlar. Bu öğreticide **Aspose.OCR for .NET**'e tanıma sırasında belirli karakterleri yok saymasını nasıl söyleyeceğinizi öğreneceksiniz—daha temiz çıktı elde etmeniz veya sayfa numaraları ya da dekoratif semboller gibi gürültüyü filtrelemeniz gerektiğinde vazgeçilmez bir ipucu. Kılavuzun sonunda, özelliği uçtan uca gösteren çalıştırmaya hazır bir kod parçacığına sahip olacaksınız.

## Hızlı Yanıtlar
- **“Yoksayılan karakterler” ne anlama geliyor?** OCR motorunun sonuç dizesini oluştururken atladığı karakterler.  
- **Neden kullanmalı?** Belirli semboller iş mantığınız için önemsiz olduğunda doğruluğu artırır.  
- **Hangi API yöntemi bunu yönetir?** `RecognitionSettings.IgnoredCharacters`.  
- **Dil paketleriyle birleştirebilir miyim?** Evet—yoksayılan karakterler, yüklediğiniz herhangi bir dil ile birlikte çalışır.  
- **Lisans gerekli mi?** Üretim kullanımı için geçici ya da tam lisans gerekir.

## Ön Koşullar

Aspose.OCR for .NET tarafından sağlanan zengin işlevselliğe dalmadan önce aşağıdaki ön koşulların yerine getirildiğinden emin olun:

1. Aspose.OCR Kurulumu  

   Aspose.OCR for .NET'i başarıyla kurduğunuzdan emin olun. Gerekli dosyaları [indirme sayfasında](https://releases.aspose.com/ocr/net/) bulabilirsiniz.

2. Belge Dizininin Ayarlanması  

   Belgeleriniz için ayrı bir dizin oluşturun. Bu, örneklerin sorunsuz çalışması için kritik öneme sahiptir. Örneklerdeki `dataDir` değişkenini belge dizininizin yoluyla güncelleyin.

3. Geçici Lisans (İsteğe Bağlı)  

   Aspose.OCR for .NET'i geçici bir lisansla inceliyorsanız, lisansı [buradan](https://purchase.aspose.com/temporary-license/) temin edin.

## Ad Alanlarını İçe Aktarın

Aspose.OCR for .NET ile yolculuğunuza başlamak için gerekli ad alanlarını içe aktarmanız gerekir. Kodunuza aşağıdaki satırları ekleyin:

```csharp
using System.IO;

using Aspose.OCR;
using System;
```

## Neden Yoksayılan Karakterler Belirtilir?

Faturalar, makbuzlar veya çok dilli formlar gibi gerçek dünya senaryolarında, anlamlı veri içinde yer almayan tekrarlayan karakterlerle (ör. ayırıcı olarak kullanılan tireler, sayfa numaraları veya dekoratif semboller) karşılaşabilirsiniz. OCR motoruna bu karakterleri atlamasını söyleyerek, son‑işleme çabasını azaltır ve sonraki analizlerin güvenilirliğini artırırsınız.

## Adım‑Adım Kılavuz

### Adım 1: Belge Dizinini Ayarlayın

Belgelerinizin saklandığı dizini belirtin. `"Your Document Directory"` ifadesini belgelerinizin gerçek yolu ile değiştirin.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

### Adım 2: Aspose.OCR'ı Başlatın

OCR motorunun bir örneğini oluşturun. Bu nesne, sonraki tüm tanıma çağrılarını yönetecek.

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Adım 3: Yoksayılan Karakterlerle Görüntüyü Tanıyın

Görüntü dosyasını, yok saymak istediğiniz karakterleri listeleyen bir `RecognitionSettings` nesnesiyle birlikte gönderin. Bu örnekte `a`, `b` ve `1` karakterlerini yok sayıyoruz.

```csharp
// Recognize image with specified ignored characters
RecognitionResult result = api.RecognizeImage(dataDir + "SpanishOCR.bmp", new RecognitionSettings
{
    IgnoredCharacters = "ab1"
});
```

### Adım 4: Tanınan Metni Görüntüleyin

Son olarak, temizlenmiş metni konsola ya da tercih ettiğiniz başka bir çıkış noktasına yazdırın.

```csharp
// Display the recognized text
Console.WriteLine(result.RecognitionText);
```

## Yaygın Sorunlar ve İpuçları

- **Yanlış yol:** `dataDir` değişkeninin işletim sisteminize uygun bir yol ayırıcı (`\` veya `/`) ile bittiğinden emin olun.  
- **Desteklenmeyen dil:** OCR motorunun kaynak görüntü için ilgili dil paketine sahip olması gerekir; aksi takdirde yoksayılan karakterler doğru uygulanmaz.  
- **Lisans hataları:** Lisans istisnası alıyorsanız, geçici lisans dosyasının projenizde doğru şekilde referans alındığını kontrol edin.

## Sonuç

Aspose.OCR for .NET, geliştiricilere gelişmiş OCR yetenekleri sunarak görüntüleri düzenlenebilir ve aranabilir metne dönüştürme sürecini kolaylaştırır. Bu adım‑adım kılavuzu izleyerek istenmeyen karakterleri nasıl dışarıda bırakacağınızı öğrendiniz; böylece OCR boru hatlarınız daha temiz ve daha güvenilir hâle geldi. Daha derin bilgiler için [belgelere](https://reference.aspose.com/ocr/net/) göz atın ve Aspose.OCR'ın OCR projelerinizi nasıl yükseltebileceğini keşfedin.

## Sıkça Sorulan Sorular

### S1: Aspose.OCR for .NET'i ticari olmayan projelerde kullanabilir miyim?

C1: Evet, Aspose.OCR for .NET hem ticari hem de ticari olmayan projelerde kullanılabilir. Daha fazla bilgi için [lisans detaylarına](https://purchase.aspose.com/buy) bakın.

### S2: Ücretsiz deneme sürümü mevcut mu?

C2: Elbette! Aspose.OCR for .NET'in özelliklerini ve avantajlarını keşfetmek için ücretsiz deneme sürümüne [buradan](https://releases.aspose.com/) ulaşabilirsiniz.

### S3: Aspose.OCR için destek nasıl alınır?

C3: Her türlü soru ve yardım için [Aspose.OCR forumuna](https://forum.aspose.com/c/ocr/16) giderek toplulukla iletişime geçebilir ve uzman tavsiyesi alabilirsiniz.

### S4: Aspose.OCR hangi dilleri destekliyor?

C4: Aspose.OCR, geniş bir dil yelpazesini destekleyerek OCR görevleri için çok yönlü bir seçim sunar. Tam liste için belgelere bakın.

### S5: Aspose.OCR için geçici bir lisans satın alabilir miyim?

C5: Evet, kısa vadeli kullanım için geçici lisansı [buradan](https://purchase.aspose.com/temporary-license/) temin edebilirsiniz.

---

**Son Güncelleme:** 2025-12-27  
**Test Edilen Versiyon:** Aspose.OCR 23.12 for .NET  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}