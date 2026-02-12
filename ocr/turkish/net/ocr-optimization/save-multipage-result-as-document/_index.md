---
date: 2025-12-30
description: Aspose.OCR kullanarak C# ile görüntüleri PDF'ye dönüştürmeyi, çok sayfalı
  OCR sonuçlarını belge olarak kaydetmeyi ve C# ile görüntülerden metin çıkarmayı
  öğrenin.
linktitle: Convert Images to PDF C# – Save Multipage OCR Result
second_title: Aspose.OCR .NET API
title: Görüntüleri PDF'ye Dönüştür C# – Çok Sayfalı OCR Sonucunu Kaydet
url: /tr/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüleri PDF'e Dönüştürme C# – Çok Sayfalı OCR Sonucunu Kaydetme

## Giriş

Bu öğreticide **Aspose.OCR for .NET** kullanarak **görüntüleri PDF C#**'e nasıl dönüştüreceğinizi ve ortaya çıkan çok sayfalı OCR çıktısını bir belge olarak nasıl kaydedeceğinizi keşfedeceksiniz. Arşivleme için **tar scanned images to PDF**'e dönüştürmeniz ya da veri işleme için **extract text from images C#** yapmanız gerekirse, bu kılavuz gerçek dünya örnekleri ve en iyi uygulama ipuçlarıyla her adımı size gösterir.

## Hızlı Yanıtlar
- **Bu öğreticide ne ele alınıyor?** Aspose.OCR ile C#'ta birden çok görüntüyü PDF/Docx/Txt/Pdf/Xlsx formatına dönüştürme.
- **Hangi formatlar destekleniyor?** Docx, Text, Pdf ve Xlsx (PDF'yi doğrudan da çıktı alabilirsiniz).
- **Lisans gerekli mi?** Değerlendirme için ücretsiz deneme çalışır; üretim için kalıcı bir lisans gerekir.
- **Hangi .NET sürümleri uyumlu?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
- **Dönüştürürken metin çıkarabilir miyim?** Evet—OCR sonuçlarını kaydetmeden önce metin olarak alabilirsiniz.

## “convert images to PDF C#” nedir?

C#'ta görüntüleri PDF'e dönüştürmek, bir veya daha fazla bitmap dosyasını (PNG, JPEG, TIFF vb.) programatik olarak alıp, görsel düzeni koruyan ve isteğe bağlı olarak OCR ile aranabilir metin gömülü bir PDF belgesi üretmek anlamına gelir. Aspose.OCR bu süreci basit ve yüksek derecede özelleştirilebilir hâle getirir.

## Bu görev için Aspose.OCR neden kullanılmalı?

- **Yüksek doğruluklu** OCR motoru, birçok dilde çalışır.
- **Çok sayfalı destek** – tek bir çağrıda görüntü topluluklarını işleyebilir.
- **Doğrudan kaydetme** popüler ofis formatlarına ekstra dönüşüm adımı olmadan.
- **Tam .NET entegrasyonu** – yerel bağımlılık veya dış araç gerektirmez.

## Önkoşullar

Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

1. Aspose.OCR for .NET'i kurun. İndirmek için [buraya](https://releases.aspose.com/ocr/net/) tıklayın.
2. Ücretsiz bir deneme ya da satın alınmış bir lisans edinin – deneme sürümünü [buradan](https://releases.aspose.com/) alabilir veya [buradan](https://purchase.aspose.com/buy) satın alabilirsiniz.
3. API yüzeyine aşina olmak için resmi [belgelere](https://reference.aspose.com/ocr/net/) göz atın.
4. Herhangi bir engelle karşılaşırsanız yardım almak için [destek forumlarına](https://forum.aspose.com/c/ocr/16) katılın.

Her şey hazır olduğuna göre, kodlamaya başlayalım.

## Namespace'leri İçe Aktarma

C# dosyanıza gerekli namespace'leri ekleyin:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

Bu içe aktarmalar, koleksiyonlar, dosya işlemleri, LINQ ve Aspose OCR sınıflarına erişim sağlar.

## Adım 1: Belge Dizinini Ayarlama

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

`"Your Document Directory"` ifadesini, kaynak görüntülerinizin bulunduğu ve çıktı dosyalarınızı kaydetmek istediğiniz mutlak ya da göreli yol ile değiştirin.

## Adım 2: Aspose.OCR'ı Başlatma

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Bir `AsposeOcr` nesnesi oluşturmak, **convert images to PDF C#** iş akışı dahil tüm OCR işlemlerine erişim sağlar.

## Adım 3: Görüntüleri Tanıma

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

`RecognizeMultipleImages` metodu listedeki her dosyayı işler ve bir `RecognitionResult` koleksiyonu döndürür. **convert scanned images to PDF** senaryoları için ideal olan istediğiniz sayıda görüntüyü besleyebilirsiniz.

## Adım 4: Sonuçları İstenilen Formatlarda Kaydetme

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

İş akışınıza en uygun formatı seçin:

- **Docx** – aranabilir metin içeren düzenlenebilir Word belgesi.
- **Text** – hızlı veri madenciliği için düz metin çıkarımı (**extract text from images C#**).
- **Pdf** – arşivleme için klasik PDF çıktısı.
- **Xlsx** – tablo verileri için elektronik tablo temsili.

## Yaygın Kullanım Senaryoları

- **Dijital arşivleme:** Tar scanned paper contracts'ı aranabilir PDF'lere dönüştürme.
- **Veri girişi otomasyonu:** Makbuz veya faturalardan metin çıkarıp bir veritabanına aktarma.
- **Toplu işleme:** Minimum kodla binlerce görüntüyü tek bir işte işleme.

## Sorun Giderme & İpuçları

- **Büyük görüntü setleri:** Bellek dalgalanmalarını önlemek için görüntüleri daha küçük partiler halinde işleyin.
- **Görüntü kalitesi:** optimum OCR doğruluğu için görüntülerin en az 300 dpi olduğundan emin olun.
- **Lisans hataları:** OCR metodlarını çağırmadan önce lisans dosyanızın doğru yüklendiğini doğrulayın.

## Ek Sıkça Sorulan Sorular

**S: OCR kullanmadan images to PDF C# nasıl dönüştürülür?**  
C: Saf görüntü‑PDF dönüşümü için Aspose.PDF veya diğer kütüphaneler kullanılabilir, ancak OCR aranabilir metin ekler.

**S: Dönüştürmeden sonra images from C# metin çıkarımı nasıl yapılır?**  
C: `RecognizeMultipleImages` tarafından döndürülen `result` listesi, `.txt` dosyasına yazabileceğiniz veya doğrudan işleyebileceğiniz `Text` özelliklerine sahiptir.

**S: Özel sayfa kenar boşlukları veya yönlendirme ayarlanabilir mi?**  
C: PDF veya Docx kaydederken, `SaveMultipageDocument` çağrısından önce Aspose.Words veya Aspose.PDF API'leri ile belge düzenini değiştirebilirsiniz.

**S: Bir görüntü okunamazsa ne olur?**  
C: OCR motoru o sayfa için boş bir `RecognitionResult` döndürür; `result[i].Text` değerinin null ya da boş olup olmadığını kontrol edip uygun şekilde işleyebilirsiniz.

**S: API bulut dağıtımını destekliyor mu?**  
C: Evet, kütüphane Azure Functions ve AWS Lambda dahil herhangi bir .NET çalışma zamanında çalışır; yalnızca sürüm gereksinimlerini karşılaması yeterlidir.

---

**Son Güncelleme:** 2025-12-30  
**Test Edilen Versiyon:** Aspose.OCR 24.11 for .NET  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}