---
date: 2025-12-25
description: Aspose OCR for .NET ile OCR doğruluğunu artırın, yazım denetimi ve dil
  desteğinden yararlanarak hatalı yazımları düzeltin ve hatasız metin tanıma için
  sözlükleri özelleştirin.
linktitle: Improve OCR Accuracy with Spell Checking in Images
second_title: Aspose.OCR .NET API
title: Görüntülerde Yazım Denetimi ile OCR Doğruluğunu Artırın
url: /tr/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntülerde Yazım Denetimi ile OCR Doğruluğu Artırma

## Giriiş

Optik Karakter Tanıma (OCR) ile kırılmada nihai hedef **OCR verimi artışı** ve elde edilen orijinal görüntüyle mükemmel bir şekilde eşleşmesini sağlamak. Yanlış yazılmış kelimeler, özellikle kaynak görüntülendiğinde veya mevcut yazı türlerinin ortaya çıkmasında yaygın bir hata bulunur. Aspose.OCR for .NET, yalnızca bu hataların düzeltilmesiyle açıklamaları aynı zamanda motorda özel sözlüklerle genişletmenize olanak sağlayan kapsamlı raporlama inceleme özellikleri sunar. Bu öğreticide, OCR sonuçlarının belirlenmesi için yazım denetiminin kapsamını, ön-ve-sonuç çıktısını izlemenizi ve iyileştirme sürecini belirleme dil özelliklerine göre nasıl özelleştirebileceğinizi sağlar.

## Hızlı Yanıtlar
- **OCR için yazım denetimi ne işe yarar?** OCR'nin çıkışındaki yanlış yazılan sözcükler otomatik olarak tespit edilir ve en olası doğru alternatiflerle değişir.
- **Bu özelliği hangi kütüphane sağlıyor?** Aspose.OCR for .NET, bilgilerin hazır bir yazım denetimi API'sini içerir.
- **İnternet bağlantısına ihtiyacım var mı?** Hayır, yazım denetimi motoru tamamen devre dışı çalışıyor.
- **Kendi terminolojimi ekleyebilir miyim?** Evet, alan‑özel sözcüklerin işlenmesi için özel bir kullanıcı sözlüğü sağlayabilirsiniz.
- **Hangi diller destekleniyor?** Detaylar için “ocr dil desteği sağlayın” bölümüne bakın.

## OCR'da Yazım Denetimi Nedir?

Yazım denetimi, OCR motoru tarafından oluşturulan ham metni inceler, seçilen dilin sözlüğünde bulunmayan belirteçleri belirler ve düzeltmeler önerir veya da uygular. Bu adım, özellikle taranmış belgeler, fişler veya formlarda OCR karakterlerinin yanlış yorumlanması **OCR doğruluğunu artırmak** için hayati öneme sahiptir.

## Neden Aspose OCR Dil Desteğini Kullanmalı?

Aspose.OCR, özet dil paketleriyle birlikte gelir ve ek sözlüklerin ortaya çıkmasına izin verir. **OCR dil desteğini kullanmayı düşünün**, çok dilli belgeleri özel parçalayıcılar yazmadan işleyebilmenizi sağlar ve tanıma yetkisini daha da artırma dile özgü kurallara erişim sunar.

## Önkoşullar

Yazım denetimi sihrine dalmadan önce aşağıdaki ön koşulların yerine getirildiğinden emin olun:

- Aspose.OCR for .NET Library: Aspose.OCR kütüphanesini [yayın sayfası](https://releases.aspose.com/ocr/net/) adresinden indirip kurun.
- Belge Dizini: Belgeleriniz için kayıtlı bir dizin olduğunuzdan emin olun. Koddaki dosyadaki "Belge Dizininiz"in gerçek yolu iletilir.

## Ad Alanlarını İçe Aktar

.NET projenizde gerekli reklam alanlarını içeri aktararak başlayın:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Adım 1: Aspose.OCR'ı Başlatma

OCR sürecini başlatmak için bir Aspose.OCR örneği başlatın.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Adım 2: Görüntüyü Tanıma

Aspose.OCR kullanarak bir görüntüdeki metni tanıyın. İşte bu süreci gösteren bir örnek:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Adım 3: Düzeltme Öncesi

Düzeltmeden önceki OCR sonucunu alın ve düzeltilmiş versiyonla karşılaştırın.

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Adım 4: Düzeltme Sonrası

Yazım denetimini uygulayarak düzeltilmiş sonucu elde edin. Aşağıdaki kod bu adımı göstermektedir:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Adım 5: Yazım Hataları ve Öneriler

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

## Adım 6: Kullanıcı Metnini Düzeltme

Aspose.OCR kütüphanesiyle kullanıcı tarafından sağlanan belirli bir metni düzeltin:

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

| Sayı | Neden Olur | Nasıl Düzeltilir |
|----------|-----|------------|
| Hiçbir öneri geri dönmedi | Dil paketi yüklenmemiş veya metin çok kısa. | `RecognitionSettings(Language.Eng)` ayarının kaynak görüntülerinin diliyle eşleştiğinden ve OCR sonucunun yeterli karakter olabileceğinden emin olun. |
| Özel sözlük uygulanmadı | Yanlış yol veya dosya formatı. | `dictionary.txt`de belirtilenlerin bulunduğu ve her satırda bir kelimenin doğru şekilde biçimlendirildiğini doğrulayın. |
| Yazım denetleyicisi büyük belgeleri yavaşlatır | Her kelime ayrı ayrı işlendiği için ek yüklerden oluşur. | Sayfaları toplu olarak işleyin veya .NET Core üzerinde çalışırken bellek dağıtımını artırın. |

## Sıkça Sorulan Sorular

### S1: Aspose.OCR'ı İngilizce dışındaki diller için kullanabilir miyim?

A1: Evet, Aspose.OCR anında fazla dil desteğine sahiptir. Dilin özelliklerine buna göre yapılandırın.

### S2: Aspose.OCR'ı .NET projeme nasıl entegre edebilirim?

A2: Ayrıntılı entegrasyon adımları için [belgeler](https://reference.aspose.com/ocr/net/) sayfasına bakın.

### S3: Aspose.OCR için deneme sürümü mevcut mu?

C3: Evet, özelliklerin ayrılması için [ücretsiz deneme sürümü](https://releases.aspose.com/) adresinden ücretsiz deneme indirme indirmeleri.

### S4: Yazım denetimi için özel bir sözlük yükleyebilir miyim?

A4: elbette! Öğreticide, kullanıcı tarafından sağlanan bir sözlükle iyileştirmeyi nasıl geliştirebileceğiniz gösterilir.

### S5: Aspose.OCR için nereden destek alabilirim?

A5: Topluluk desteği ve rehberlik için [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) adresini ziyaret edin.

---

**Son Güncelleme:** 25.12.2025
**Test Edilen Sürüm:** Aspose.OCR for .NET en son sürüm
**Yazar:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
