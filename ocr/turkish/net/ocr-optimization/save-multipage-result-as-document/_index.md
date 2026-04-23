---
date: 2026-04-23
description: Aspose.OCR kullanarak C# ile görüntüleri PDF'ye dönüştürmeyi, çok sayfalı
  OCR sonuçlarını belge olarak kaydetmeyi ve görüntülerden metin çıkarmayı öğrenin.
keywords:
- extract text from images
- batch image to pdf
- convert scanned images pdf
linktitle: Görüntüleri PDF'ye Dönüştür C# – Çok Sayfalı OCR Sonucunu Kaydet
second_title: Aspose.OCR .NET API
title: Görüntülerden Metin Çıkar – Görüntüleri PDF'e Dönüştür C#
url: /tr/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntülerden Metin Çıkarma – Görüntüleri PDF C#'a Dönüştürme

## Giriş

Bu öğreticide, Aspose.OCR for .NET kullanarak **extract text from images** ve **convert images to PDF C#** işlemlerini keşfedecek ve çok sayfalı OCR sonucunu bir belge olarak kaydedeceksiniz. Arşivleme için **batch image to pdf**, uyumluluk için **convert scanned images pdf** gibi ihtiyaçlarınız olsun ya da sadece resimlerden aranabilir metin çekmek isteyin, her adımı net açıklamalar, gerçek dünya ipuçları ve en iyi uygulama önerileriyle ele alacağız.

## Hızlı Yanıtlar
- **Bu öğreticide ne ele alınıyor?** Birden fazla görüntüyü PDF/Docx/Txt/Xlsx'ye dönüştürme ve Aspose.OCR ile C#'ta görüntülerden metin çıkarma.
- **Hangi çıktı formatları destekleniyor?** Docx, Text, Pdf ve Xlsx (PDF'yi doğrudan da çıktı olarak alabilirsiniz).
- **Lisans gereklimi?** Değerlendirme için ücretsiz deneme çalışır; üretim için kalıcı bir lisans gereklidir.
- **Hangi .NET sürümleri uyumludur?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
- **Dönüştürürken metin çıkarabilir miyim?** Evet—kaydetmeden önce OCR sonuçlarını kullanarak metni alabilirsiniz.

## “extract text from images” nedir ve PDF dönüşümüyle neden birleştirilir?
Görüntülerden metin çıkarmak, OCR (Optik Karakter Tanıma) kullanarak görsel karakterleri aranabilir, düzenlenebilir dizelere dönüştürmek anlamına gelir. **convert images to PDF C#** yaptığınızda, bu dizeleri PDF'e gömerek belgenin aranabilir ve indekslenebilir olmasını sağlarsınız—dijital arşivleme ve veri madenciliği için mükemmeldir.

## Bu görev için neden Aspose.OCR kullanılmalı?
- **Yüksek doğruluk** onlarca dilde.  
- **Çok sayfalı destek** – tek bir çağrıda görüntü toplularını işleyin (**batch image to pdf** senaryoları için idealdir).  
- **Doğrudan kaydetme** popüler ofis formatlarına ekstra dönüşüm adımları olmadan.  
- **Tam .NET entegrasyonu** – yerel bağımlılık yok, Windows, Linux ve bulut çalışma zamanlarında çalışır.

## Önkoşullar

Başlamadan önce, şunların olduğundan emin olun:

1. Aspose.OCR for .NET'i kurun. [buradan](https://releases.aspose.com/ocr/net/) indirebilirsiniz.  
2. Ücretsiz deneme veya satın alınmış bir lisans edinin – deneme sürümünü [buradan](https://releases.aspose.com/) alabilir veya bir lisans [buradan](https://purchase.aspose.com/buy) satın alabilirsiniz.  
3. Resmi [belgelendirmeyi](https://reference.aspose.com/ocr/net/) inceleyerek API yüzeyine aşina olun.  
4. [destek forumlarında](https://forum.aspose.com/c/ocr/16) topluluğa katılarak herhangi bir engelle ilgili yardım alın.  

Her şey hazır olduğuna göre, kodlamaya başlayalım.

## Ad Alanlarını İçe Aktarma

Gerekli ad alanlarını C# dosyanıza ekleyerek başlayın:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

Bu içe aktarmalar, koleksiyonlara, dosya işlemlerine, LINQ'e ve Aspose OCR sınıflarına erişim sağlar.

## Adım 1: Belge Dizinini Ayarlama

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

`"Your Document Directory"` ifadesini, kaynak görüntülerinizin bulunduğu ve çıktı dosyalarını kaydetmek istediğiniz mutlak ya da göreli yol ile değiştirin.

## Adım 2: Aspose.OCR'ı Başlatma

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

`AsposeOcr` nesnesi oluşturmak, **convert images to PDF C#** iş akışı da dahil olmak üzere tüm OCR işlemlerine erişim sağlar.

## Adım 3: Görüntüleri Tanıma

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

`RecognizeMultipleImages` yöntemi listedeki her dosyayı işler ve bir `RecognitionResult` koleksiyonu döndürür. İstediğiniz sayıda görüntüyü besleyebilirsiniz; bu, **convert scanned images pdf** senaryoları için mükemmeldir.

## Adım 4: Sonuçları Tercih Edilen Formatlarda Kaydetme

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

Aşağı akışınıza en uygun formatı seçin:

- **Docx** – aranabilir metin içeren düzenlenebilir Word belgesi.  
- **Text** – hızlı veri madenciliği için düz metin çıkarma (**extract text from images**).  
- **Pdf** – arşivleme için ideal klasik PDF çıktısı.  
- **Xlsx** – tablo verileri için elektronik tablo temsili.

## Yaygın Kullanım Senaryoları

- **Dijital arşivleme:** Taralı kağıt sözleşmeleri aranabilir PDF'lere dönüştürün.  
- **Veri girişi otomasyonu:** Makbuz veya faturalardan metin çıkarın ve bir veritabanına besleyin.  
- **Toplu işleme:** Tek bir işte binlerce görüntüyü minimal kodla işleyin—**batch image to pdf** ihtiyaçları için mükemmeldir.

## Sorun Giderme ve İpuçları

- **Büyük görüntü setleri:** Bellek dalgalanmalarını önlemek için görüntüleri daha küçük partilerde işleyin.  
- **Görüntü kalitesi:** Optimal OCR doğruluğu için görüntülerin en az 300 dpi olduğundan emin olun.  
- **Lisans hataları:** OCR yöntemlerini çağırmadan önce lisans dosyanızın doğru yüklendiğini doğrulayın.  
- **Boş sonuçlar:** OCR motoru okunamayan sayfalar için boş bir `RecognitionResult` döndürür; `result[i].Text`'in null ya da boş olup olmadığını kontrol edin ve buna göre işleyin.

## Sık Sorulan Sorular

**S: OCR kullanmadan görüntüleri PDF C#'a dönüştürebilir miyim?**  
**C:** Evet, saf görüntü‑PDF dönüşümü için Aspose.PDF veya diğer kütüphaneleri kullanabilirsiniz, ancak OCR aranabilir metin ekler.

**S: Dönüştürmeden sonra C#'ta görüntülerden metin nasıl çıkarılır?**  
**C:** `RecognizeMultipleImages` tarafından döndürülen `result` listesi, bir `.txt` dosyasına yazabileceğiniz veya doğrudan işleyebileceğiniz `Text` özelliklerini içerir.

**S: Özel sayfa kenar boşlukları veya yönlendirme ayarlanabilir mi?**  
**C:** PDF veya Docx olarak kaydederken, `SaveMultipageDocument` çağrısından önce Aspose.Words veya Aspose.PDF API'leri ile belge düzenini değiştirebilirsiniz.

**S: Bir görüntü okunamazsa ne olur?**  
**C:** OCR motoru o sayfa için boş bir `RecognitionResult` döndürür; `result[i].Text`'in null ya da boş olup olmadığını kontrol edip buna göre işleyebilirsiniz.

**S: API bulut dağıtımını destekliyor mu?**  
**C:** Evet, kütüphane Azure Functions ve AWS Lambda dahil olmak üzere herhangi bir .NET çalışma zamanında, sürüm gereksinimlerini karşıladığı sürece çalışır.

---

**Son Güncelleme:** 2026-04-23  
**Test Edilen Sürüm:** Aspose.OCR 24.11 for .NET  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}