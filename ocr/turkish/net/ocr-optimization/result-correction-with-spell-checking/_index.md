---
date: 2026-04-29
description: OCR doğruluğunu artırın ve Aspose OCR for .NET kullanarak görüntüden
  metin tanımayı öğrenin; yazım denetimi ve dil desteğinden yararlanarak hatalı yazımları
  düzeltin ve sözlükleri özelleştirin.
keywords:
- improve ocr accuracy
- recognize text from image
- Aspose OCR spell checking
- custom OCR dictionary
linktitle: Görsellerde Yazım Denetimi ile OCR Doğruluğunu Artırın
second_title: Aspose.OCR .NET API
title: Görüntülerde Yazım Denetimi ile OCR Doğruluğunu Artırın
url: /tr/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntülerde Yazım Denetimi ile OCR Doğruluğunu Artırma

Optik Karakter Tanıma (OCR) ile çalıştığınızda nihai hedef **OCR doğruluğunu artırmak** ve çıkarılan metnin orijinal görüntüyle mükemmel bir şekilde eşleşmesini sağlamaktır. Yanlış yazılmış kelimeler, özellikle kaynak görüntü gürültülü olduğunda veya alışılmadık yazı tipleri içerdiğinde yaygın bir hata kaynağıdır. Aspose.OCR for .NET, yalnızca bu hataları düzeltmekle kalmayıp aynı zamanda motoru özel sözlüklerle genişletmenize olanak tanıyan yerleşik bir yazım denetimi özelliği sunar. Bu öğreticide yazım denetimini kullanarak OCR sonuçlarını nasıl artıracağınızı, ön‑ve‑son çıktıyı göreceğinizi ve düzeltme sürecini belirli dil ihtiyaçlarınıza göre nasıl özelleştireceğinizi öğreneceksiniz.

## Hızlı Yanıtlar
- **Yazım denetimi OCR için ne yapar?** OCR çıktısındaki yanlış yazılmış kelimeleri otomatik olarak algılar ve en olası doğru alternatiflerle değiştirir.  
- **Bu özelliği hangi kütüphane sağlar?** Aspose.OCR for .NET, kullanıma hazır bir yazım denetimi API'si içerir.  
- **İnternet bağlantısına ihtiyacım var mı?** Hayır, yazım denetimi motoru tamamen çevrim dışı çalışır.  
- **Kendi terminolojimi ekleyebilir miyim?** Evet, alan‑spesifik kelimeleri işlemek için özel bir kullanıcı sözlüğü sağlayabilirsiniz.  
- **Bu, görüntüden metin tanımama nasıl yardımcı olur?** OCR kaynaklı hataları düzelterek, son metin temiz olur ve sonraki işleme hazır hâle gelir.

## OCR'da Yazım Denetimi Nedir?
Yazım denetimi, OCR motoru tarafından döndürülen ham metni inceler, seçilen dil sözlüğünde bulunmayan tokenları belirler ve düzeltmeler önerir ya da uygular. Bu adım, özellikle taranmış belgeler, fişler veya formlar gibi OCR'nin karakterleri yanlış yorumlayabileceği durumlarda **OCR doğruluğunu artırmak** için hayati öneme sahiptir.

## Neden Aspose OCR Dil Desteği Kullanmalı?
Aspose.OCR, kapsamlı dil paketleriyle birlikte gelir ve ek sözlüklerin takılmasına izin verir. **aspose ocr language support**'u kullanmak, çok dilli belgeleri özel ayrıştırıcılar yazmadan işleyebilmenizi sağlar ve tanıma kalitesini daha da artıran dile özgü kurallara erişim sunar.

## OCR doğruluğunu artırmanın en çok ne zaman önemi vardır?
- **Yasal ve uyumluluk belgeleri** tek bir yazım hatasının anlamı değiştirebileceği yerler.  
- **Veri çıkarma hatları** OCR sonuçlarını analizlere veya AI modellerine besleyen.  
- **Müşteri odaklı uygulamalar** örneğin, okunabilir metni anında döndürmesi gereken mobil tarayıcılar.  

## Önkoşullar

Spell‑checking sihrine dalmadan önce aşağıdaki önkoşulların yerine getirildiğinden emin olun:

- Aspose.OCR for .NET Kütüphanesi: Aspose.OCR kütüphanesini [release page](https://releases.aspose.com/ocr/net/) adresinden indirin ve kurun.  
- Belge Dizini: Belgeleriniz için belirlenmiş bir dizininiz olduğundan emin olun. Kod parçacıklarındaki `"Your Document Directory"` ifadesini gerçek yol ile değiştirin.

## Ad Alanlarını İçe Aktarın

.NET projenizde gerekli ad alanlarını içe aktararak başlayalım:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Adım 1: Aspose.OCR'ı Başlatın

OCR sürecini başlatmak için bir Aspose.OCR örneği oluşturun.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Adım 2: Görüntüyü Tanı

Şimdi Aspose.OCR kullanarak bir görüntüdeki metni tanıyın. İşte bu süreci gösteren bir kod parçacığı:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Adım 3: Düzeltmeden Önce

Düzeltmeden önceki OCR sonucunu alın ve düzeltilmiş sürümle karşılaştırın.

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Adım 4: Düzeltmeden Sonra

Yazım denetimini uygulayarak düzeltilmiş sonucu elde edin. Aşağıdaki kod parçacığı bu adımı gösterir:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Adım 5: Yanlış Yazılmış Kelimeler ve Öneriler

Aşağıdaki kodu kullanarak yanlış yazılmış kelimelerin bir listesini ve önerilen düzeltmeleri alın:

```csharp
// Get list of misspelled words with suggestions
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
    Console.Write("Word:" + word.Word);
    Console.Write(" StartPosition:" + word.StartPosition);
    Console.WriteLine(" Length:" + word.Length);
    Console.WriteLine("SuggestedWords:");
    foreach (var suggest in word.SuggestedWords)
    {
        Console.Write(suggest.Word + " ");
    }
    Console.WriteLine();
}
```

## Adım 6: Kullanıcı Metnini Düzelt

Aspose.OCR kütüphanesini kullanarak belirli bir kullanıcı‑sağlanan metni düzeltin:

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Adım 7: Kullanıcı Sözlüğü ile Düzeltme

Özel bir kullanıcı sözlüğü ekleyerek düzeltmeyi daha da geliştirin:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Yaygın Sorunlar ve Çözümler

| Sorun | Neden Oluşur | Nasıl Düzeltilir |
|-------|----------------|------------|
| Öneri döndürülmedi | Dil paketi yüklenmemiş veya metin çok kısa. | `RecognitionSettings(Language.Eng)`'in kaynak görüntünün diline uygun olduğundan ve OCR sonucunun yeterli karakter içerdiğinden emin olun. |
| Özel sözlük uygulanmadı | Yanlış yol veya dosya formatı. | `dictionary.txt` dosyasının belirtilen konumda mevcut olduğunu ve her satırda bir kelime olduğunu doğrulayın. |
| Yazım denetleyici büyük belgelerde yavaşlıyor | Her kelimeyi ayrı ayrı işlemek ek yük oluşturur. | Sayfaları toplu işleyin veya .NET Core üzerinde çalışıyorsanız bellek tahsisatını artırın. |

## Sıkça Sorulan Sorular

**Q1: Aspose.OCR'ı İngilizce dışındaki dillerde kullanabilir miyim?**  
A1: Evet, Aspose.OCR birden fazla dili destekler. Dil ayarlarını buna göre ayarlayın.

**Q2: Aspose.OCR'ı .NET projemle nasıl entegre ederim?**  
A2: Ayrıntılı entegrasyon adımları için [documentation](https://reference.aspose.com/ocr/net/) adresine bakın.

**Q3: Aspose.OCR için bir deneme sürümü mevcut mu?**  
A3: Evet, özellikleri [free trial version](https://releases.aspose.com/) ile keşfedebilirsiniz.

**Q4: Yazım denetimi için özel bir sözlük yükleyebilir miyim?**  
A4: Kesinlikle! Eğitim, kullanıcı tarafından sağlanan bir sözlükle düzeltmeyi nasıl artıracağınızı gösterir.

**Q5: Aspose.OCR için nereden destek alabilirim?**  
A5: Topluluk desteği ve rehberlik için [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) adresini ziyaret edin.

---

**Son Güncelleme:** 2026-04-29  
**Test Edilen Versiyon:** Aspose.OCR for .NET latest version  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}