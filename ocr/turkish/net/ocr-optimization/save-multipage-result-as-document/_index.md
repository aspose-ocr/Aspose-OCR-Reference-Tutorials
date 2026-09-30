---
date: 2026-04-29
description: Aspose.OCR kullanarak C# ile görüntüleri PDF'ye dönüştürmeyi, çok sayfalı
  OCR sonuçlarını belge olarak kaydetmeyi ve C# ile görüntülerden metin çıkarmayı
  öğrenin.
keywords:
- convert images to pdf
- extract text from images
- c# ocr library
- convert images to xlsx
- generate pdf from tiff
linktitle: Görselleri PDF'e Dönüştür C# – Çok Sayfalı OCR Sonucunu Kaydet
second_title: Aspose.OCR .NET API
title: Görüntüleri PDF'ye Dönüştür C# – Çok Sayfalı OCR Sonucunu Kaydet
url: /tr/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüleri PDF C#'a Dönüştür – Çok Sayfalı OCR Sonucunu Kaydet

## Giriş

Bu öğreticide, .NET için güçlü **Aspose.OCR** kütüphanesini kullanarak **görüntüleri PDF C#'a dönüştürmeyi** keşfedeceksiniz. **Taralı TIFF dosyalarını aranabilir PDF'lere dönüştürmeniz**, görüntülerden veri madenciliği için metin çıkarmanız veya bir grup resimden bir Excel çalışma kitabı oluşturmanız gerekirse, bu kılavuz her adımı net açıklamalar, gerçek dünya ipuçları ve en iyi uygulama önerileriyle size gösterir.

## Hızlı Yanıtlar
- **Bu öğretici neyi kapsıyor?** Aspose.OCR kullanarak C#'ta birden fazla görüntüyü PDF, Docx, Text ve Xlsx formatına dönüştürmek ve OCR sonucunu çok sayfalı bir belge olarak kaydetmek.  
- **Hangi çıktı formatları destekleniyor?** Docx, Text, Pdf ve Xlsx (PDF'yi doğrudan da çıktı alabilirsiniz).  
- **Bir lisansa ihtiyacım var mı?** Değerlendirme için ücretsiz deneme çalışır; üretim için kalıcı bir lisans gereklidir.  
- **Hangi .NET sürümleri uyumlu?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Dönüştürürken metin çıkarabilir miyim?** Evet—kaydetmeden önce aranabilir metni elde etmek için OCR sonuçlarını kullanın.

## “görüntüleri PDF C#'a dönüştür” nedir?
C#'ta görüntüleri PDF'ye dönüştürmek, programlı olarak bir veya daha fazla bitmap dosyasını (PNG, JPEG, TIFF vb.) alıp görsel düzeni koruyan ve isteğe bağlı olarak OCR aracılığıyla aranabilir metin gömen bir PDF belgesi oluşturmak anlamına gelir. Aspose.OCR, çok sayfalı desteği ve popüler ofis formatlarına doğrudan kaydetme özelliği dahil olmak üzere bu süreci uçtan uca yöneten bir **c# ocr library** sağlar.

## Bu görev için Aspose.OCR neden kullanılmalı?
- **Yüksek doğruluklu OCR**; onlarca dili destekler.  
- **Çok sayfalı işleme** – bir klasör içindeki tüm görüntüleri besleyin ve tek bir aranabilir PDF elde edin.  
- **Doğrudan dışa aktarım**; ikinci bir dönüşüm adımına gerek kalmadan Docx, Text, Pdf ve Xlsx formatlarına.  
- **Saf .NET** – yerel bağımlılık yok, Windows, Linux ve bulut çalışma zamanlarında çalışır.

## Önkoşullar
1. .NET için Aspose.OCR'ı kurun. [buradan](https://releases.aspose.com/ocr/net/) indirebilirsiniz.  
2. Ücretsiz bir deneme veya satın alınmış lisans edinin – deneme sürümünü [buradan](https://releases.aspose.com/) alabilir veya bir lisans satın alabilirsiniz [buradan](https://purchase.aspose.com/buy).  
3. API yüzeyiyle tanışmak için resmi [belgelere](https://reference.aspose.com/ocr/net/) göz atın.  
4. Herhangi bir engelle karşılaştığınızda yardım almak için [destek forumlarında](https://forum.aspose.com/c/ocr/16) topluluğa katılın.  

Şimdi her şey hazır, kodlamaya başlayalım.

## Ad Alanlarını İçe Aktarın
Gerekli ad alanlarını C# dosyanıza ekleyerek başlayın:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

Bu içe aktarmalar, koleksiyonlara, dosya işlemlerine, LINQ'a ve Aspose OCR sınıflarına erişim sağlar.

## Adım 1: Belge Dizinini Ayarlayın
```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

`"Your Document Directory"` ifadesini, kaynak görüntülerinizin bulunduğu ve çıktı dosyalarını kaydetmek istediğiniz mutlak ya da göreli yol ile değiştirin.

## Adım 2: Aspose.OCR'ı Başlatın
```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

`AsposeOcr` nesnesi oluşturmak, **görüntüleri PDF C#'a dönüştür** iş akışı da dahil olmak üzere tüm OCR işlemlerine erişim sağlar.

## Adım 3: Görüntüleri Tanıyın
```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

`RecognizeMultipleImages` yöntemi listedeki her dosyayı işler ve bir `RecognitionResult` koleksiyonu döndürür. İstediğiniz sayıda görüntüyü besleyebilirsiniz; bu, **taralı görüntüleri PDF'ye dönüştür** senaryoları için mükemmeldir.

## Adım 4: Sonuçları Tercih Edilen Formatlarda Kaydedin
```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

Aşağı akışınıza en uygun formatı seçin:

- **Docx** – aranabilir metinli düzenlenebilir Word belgesi.  
- **Text** – hızlı veri madenciliği için düz metin çıkarımı (**görüntülerden metin çıkar**).  
- **Pdf** – arşivleme için ideal klasik PDF çıktısı.  
- **Xlsx** – tablo verileri için elektronik tablo temsili (**görüntüleri xlsx'ye dönüştür**).

## Görüntüleri PDF C#'a Dönüştürme – Adım Adım Özet
1. **Dönüştürmek istediğiniz görüntülerle klasörü hazırlayın**.  
2. **OCR işlevlerine erişmek için bir `AsposeOcr` örneği oluşturun**.  
3. **Her dosya için OCR sonuçlarını almak üzere `RecognizeMultipleImages`'ı çağırın**.  
4. **İhtiyacınız olan formatta `SaveMultipageDocument` kullanarak çok sayfalı sonucu kaydedin**.

## Yaygın Kullanım Senaryoları
- **Dijital arşivleme:** Taralı kağıt sözleşmeleri aranabilir PDF'lere dönüştürün.  
- **Veri girişi otomasyonu:** Makbuz veya faturalardan metin çıkarın ve bir veritabanına besleyin.  
- **Toplu işleme:** Tek bir işte binlerce görüntüyü minimal kodla işleyin.  
- **TIFF'ten PDF oluşturma:** Orijinale sadık kalması gereken yüksek çözünürlüklü taranmış belgeler için idealdir.

## Sorun Giderme ve İpuçları
- **Büyük görüntü setleri:** Bellek dalgalanmalarını önlemek için görüntüleri daha küçük partilerde işleyin.  
- **Görüntü kalitesi:** optimum OCR doğruluğu için görüntülerin en az 300 dpi olduğundan emin olun.  
- **Lisans hataları:** OCR yöntemlerini çağırmadan önce lisans dosyanızın doğru yüklendiğini doğrulayın.  
- **Boş sonuçlar:** Bir görüntü okunamazsa, ilgili `RecognitionResult` boş bir `Text` özelliğine sahip olur—kaydetmeden önce null veya boş dizeleri kontrol edin.

## Sıkça Sorulan Sorular
**S: Görüntüleri OCR kullanmadan PDF C#'a dönüştürebilir miyim?**  
C: Evet, saf görüntü‑PDF dönüşümü için Aspose.PDF veya diğer kütüphaneleri kullanabilirsiniz, ancak OCR PDF'ye aranabilir metin ekleyerek çok daha kullanışlı hâle getirir.

**S: Dönüştürmeden sonra C#'ta görüntülerden metin nasıl çıkarılır?**  
C: `RecognizeMultipleImages` tarafından döndürülen `result` listesi her sayfa için bir `Text` özelliği içerir. Bu dizeleri bir `.txt` dosyasına yazabilir veya doğrudan uygulamanızda işleyebilirsiniz.

**S: Özel sayfa kenar boşlukları veya yönlendirme ayarlamak mümkün mü?**  
C: PDF veya Docx olarak kaydederken, `SaveMultipageDocument`'ı çağırmadan önce Aspose.Words veya Aspose.PDF API'leriyle belge düzenini değiştirebilirsiniz.

**S: Bir görüntü okunamazsa ne olur?**  
C: OCR motoru o sayfa için boş bir `RecognitionResult` döndürür; bunu tespit edip sorunlu dosyayı atlayabilir veya kaydedebilirsiniz.

**S: API bulut dağıtımını destekliyor mu?**  
C: Evet, kütüphane Azure Functions ve AWS Lambda dahil olmak üzere herhangi bir .NET çalışma zamanında, sürüm gereksinimlerini karşıladığı sürece çalışır.

## Sonuç
Artık **görüntüleri PDF C#'a dönüştürmek**, aranabilir metin çıkarmak ve hatta bir grup resimden Word, düz metin veya Excel dosyaları üretmek için eksiksiz, üretime hazır bir iş akışına sahipsiniz. Farklı çıktı formatlarıyla denemeler yapmaktan, belirli diller için OCR ayarlarını düzenlemekten veya kodu daha büyük belge‑işleme hatlarına entegre etmekten çekinmeyin.

---

**Son Güncelleme:** 2026-04-29  
**Test Edilen:** Aspose.OCR 24.11 for .NET  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}