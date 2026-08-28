---
description: Aspose.OCR for .NET ile OCR sonuçlarını nasıl kaydedeceğinizi öğrenin
  – görüntüyü PDF'ye dönüştürün, PNG'den metin çıkarın ve tanınan metni DOCX, TXT,
  PDF veya XLSX olarak kaydedin.
linktitle: How to Save OCR Result as Document
second_title: Aspose.OCR .NET API
title: OCR Sonucunu Belge Olarak Kaydetme
url: /tr/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Sonucunu Belge Olarak Kaydetme

## Giriş

Bu öğreticide Aspose.OCR for .NET kullanarak **OCR sonucunu nasıl kaydedeceğinizi** keşfedeceksiniz. Bir görüntüdeki metni tanımayı, ardından bu metni DOCX, TXT, PDF ve XLSX gibi popüler belge formatlarına dönüştürmeyi adım adım göstereceğiz. Sonunda, resimlerden veri çıkarımını otomatikleştirip, bu verileri aranabilir ve düzenlenebilir dosyalar olarak saklayabileceksiniz—arşivleme, raporlama veya sonraki işlemler için mükemmel.

## Hızlı Cevaplar
- **“how to save ocr” ne anlama geliyor?** Bir görüntüden tanınan metni DOCX, PDF vb. bir dosya formatında kalıcı hale getirmeyi ifade eder.  
- **Hangi formatlara dışa aktarabilirim?** DOCX, TXT, PDF ve XLSX kutudan çıktığı gibi desteklenir.  
- **Lisans gerekir mi?** Değerlendirme için ücretsiz deneme çalışır; üretim kullanımı için ticari lisans gereklidir.  
- **Görüntüyü doğrudan PDF'ye dönüştürebilir miyim?** Evet—OCR sonucunu PDF olarak kaydederek aranabilir bir PDF belge elde edebilirsiniz.  
- **PNG destekleniyor mu?** Kesinlikle; aynı API ile **PNG** görüntülerinden metin **çıkarabilirsiniz**.

## OCR Nedir ve Sonuçları Neden Belge Olarak Kaydetmeliyiz?

Optik Karakter Tanıma (OCR), görüntüler içindeki basılı veya el yazısı metni makine tarafından okunabilir dizelere dönüştürür. Bu dizeleri belge olarak kaydetmek şunları yapmanızı sağlar:

* Uyumluluk için aranabilir PDF'ler oluşturun.  
* Veri analizi için elektronik tabloları (XLSX) doldurun.  
* Düzenlenebilir raporlar (DOCX) oluşturun.  
* Hızlı arama için düz metin günlüklerini (TXT) arşivleyin.

## Önkoşullar

Başlamadan önce, şunların kurulu olduğundan emin olun:

- Aspose.OCR for .NET yüklü. **[buradan](https://releases.aspose.com/ocr/net/)** indirebilirsiniz.  
- Kaynak görüntüleri ve çıktı belgelerini tutacak bir klasör. Koddaki `dataDir` değişkenini bu klasöre işaret edecek şekilde güncelleyin.

## Namespace'leri İçe Aktarma

Dosya I/O ve Aspose OCR sınıflarına erişmek için birkaç .NET namespace'ine ihtiyacımız var.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### Adım 1: Aspose.OCR'ı Başlatma

Çalışma dizininizin yolunu ayarlayın ve OCR motorunun bir örneğini oluşturun.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Adım 2: Görüntüyü Tanıma

Görüntü dosyasını (ör. PNG) tanıyıcıya gönderin. Burada **metin görüntülerini tanır** ve bir `RecognitionResult` nesnesine dönüştürürüz.

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### Adım 3: Sonucu Farklı Formatlarda Kaydetme

Şimdi tanınan metni dışa aktarıyoruz. İş akışınıza uygun formatı seçin—**görüntüyü PDF'ye dönüştürmeniz**, **PNG'den metin çıkarmanız** ya da bir elektronik tablo oluşturmanız gerekebilir.

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### Adım 4: Başarı Mesajını Görüntüleme

Basit bir konsol mesajı, işlemin hatasız tamamlandığını onaylar.

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## Yaygın Tuzaklar ve İpuçları

- **Dosya yolları:** Her zaman mutlak yollar kullanın veya `dataDir`'in bir yol ayırıcı (`\` veya `/`) ile bittiğinden emin olun.  
- **Görüntü kalitesi:** Daha yüksek çözünürlüklü görüntüler doğruluğu artırır; daha iyi sonuçlar için ön işleme (eğikliği düzeltme, gürültü azaltma) düşünün.  
- **Lisans modu:** Değerlendirme modunda çıktı bir filigran içerebilir; bunu kaldırmak için geçerli bir lisans uygulayın.

## Sıkça Sorulan Sorular

**S1. Aspose.OCR farklı görüntü formatlarıyla uyumlu mu?**  
C1: Evet, Aspose.OCR geniş bir görüntü formatı yelpazesini destekler, OCR görevlerinizde esneklik sağlar.

**S2. Daha iyi doğruluk için tanıma ayarlarını özelleştirebilir miyim?**  
C2: Kesinlikle! Aspose.OCR, belirli gereksinimlerinize göre OCR sürecini ince ayar yapmanızı sağlayan `RecognitionSettings` sunar.

**S3. Ücretsiz deneme mevcut mu?**  
C3: Evet, ücretsiz deneme ile **[buradan](https://releases.aspose.com/)** başlayabilirsiniz.

**S4. Aspose.OCR için geçici bir lisans nasıl alabilirim?**  
C4: Geçici lisansları **[buradan](https://purchase.aspose.com/temporary-license/)** alabilirsiniz.

**S5. Yardım almak ya da toplulukla iletişime geçmek için nereden ulaşabilirim?**  
C5: Destek ve tartışmalar için **[Aspose Forum](https://forum.aspose.com/c/ocr/16)** üzerinden Aspose.OCR topluluğuna katılın.

---

**Son Güncelleme:** 2026-02-12  
**Test Edilen Versiyon:** Aspose.OCR 24.11 for .NET  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}