---
category: general
date: 2026-05-28
description: C#'ta Aspose OCR kullanarak aranabilir PDF oluşturun. PDF üzerinde OCR
  çalıştırmayı, metin PDF'sini tanımayı ve OCR taranmış bir PDF'yi aranabilir PDF'ye
  dönüştürmeyi öğrenin.
draft: false
keywords:
- create searchable pdf
- run ocr on pdf
- recognize text pdf
- ocr scanned pdf
- aspose ocr pdf
language: tr
og_description: Aspose OCR kullanarak C# ile aranabilir PDF oluşturun. PDF üzerinde
  OCR çalıştırmak, metin tanıma ve OCR taranmış PDF dosyalarını işlemek için bu adım
  adım kılavuzu izleyin.
og_title: Aspose OCR ile Aranabilir PDF Oluşturun – PDF'de OCR Çalıştırın
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  headline: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  type: TechArticle
- description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  name: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  steps:
  - name: Multiple Languages (OCR Scanned PDF)
    text: 'If your source PDF contains both English and Spanish text, combine languages:'
  - name: Password‑Protected PDFs
    text: 'When dealing with secured PDFs, supply the password before calling `Recognize`:'
  - name: Controlling Image Quality
    text: 'Higher DPI yields better OCR results but consumes more memory. Adjust the
      DPI if you notice garbled characters:'
  - name: License vs. Evaluation Mode
    text: 'In evaluation mode a watermark appears on each page. To remove it, apply
      your license before any OCR call:'
  - name: What’s Next?
    text: '- Explore the **aspose ocr pdf** API further: extract plain text, export
      to DOCX, or generate searchable PDFs in bulk. - Combine the searchable PDF output
      with Aspose.PDF to add bookmarks or watermarks. - Experiment with different
      DPI settings or custom OCR dictionaries for niche fonts.'
  type: HowTo
tags:
- Aspose
- OCR
- PDF
- C#
title: Aspose OCR ile Aranabilir PDF Oluşturun – PDF Üzerinde OCR Çalıştırın
url: /tr/net/text-recognition/create-searchable-pdf-with-aspose-ocr-run-ocr-on-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR ile Aranabilir PDF Oluşturma – PDF Üzerinde OCR Çalıştırma

Hiç taranmış belgeler yığınından **aranabilir PDF oluşturma** dosyaları oluşturmanız gerekti mi? Yalnız değilsiniz. Birçok ofis iş akışında, tamamen aranabilir bir arşive ulaşmanızın önündeki tek engel, PDF sayfalarında OCR çalıştıran birkaç satır kod.

Bu öğreticide, Aspose OCR for .NET kütüphanesini kullanarak **aranabilir PDF** dosyalarını nasıl **oluşturacağınızı** adım adım gösteren tam, çalıştırmaya hazır bir örnek üzerinden ilerleyeceğiz. Sonunda *PDF üzerinde OCR çalıştırma*, *metin PDF'lerini tanıma* ve *OCR taranmış PDF*'yi üçüncü taraf hizmetler kullanmadan aranabilir bir sürüme dönüştürme konularını öğreneceksiniz.

> **Önkoşullar** – Güncel bir .NET SDK (6.0+ önerilir), geçerli bir Aspose.OCR for .NET lisansı (veya geçici bir değerlendirme anahtarı) ve işlemek istediğiniz bir PDF.

![Create searchable PDF diagram](alt="Aspose OCR kullanarak oluşturulabilir PDF iş akışını gösteren diyagram")  

---

## Bu Kılavuzda Neler Ele Alınıyor

- C# projesinde Aspose OCR kütüphanesini kurma.  
- Kaynak bir PDF'yi (istediğiniz sayıda sayfa) yükleme.  
- Motoru **aranabilir PDF** çıktısı verecek şekilde yapılandırma.  
- OCR sürecini çalıştırma ve sonucu kaydetme.  
- Çok sayfalı belgeler, dil seçimi ve yaygın hatalarla başa çıkma ipuçları.  

Her adımı izlerseniz, Adobe Reader'da açabileceğiniz, **Ctrl + F** tuş kombinasyonuna basıp orijinal taramada yer alan herhangi bir kelimeyi anında arayabileceğiniz bir dosya elde edeceksiniz.

## Adım 1: Aspose OCR for .NET'i Yükleyin

Kod yazmaya başlamadan önce, projenize NuGet paketini ekleyin:

```bash
dotnet add package Aspose.OCR
```

> **Pro ipucu:** En son kararlı sürüme kilitlemek için `--version` bayrağını kullanın (ör. `Aspose.OCR 23.10`). Bu, .NET 6 ve üzeri ile uyumluluğu sağlar.

## Adım 2: OCR Motoru Örneği Oluşturma

İşlemin kalbi `OcrEngine`'dir. Görüntüleri okuyup metin üreten bir beyin gibi düşünebilirsiniz. Başlatması oldukça basittir:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Instantiate the OCR engine
            var ocrEngine = new OcrEngine();
```

`OcrEngine` nesnesi, giriş görüntü akışını ve Aspose'a çıktının nasıl olmasını istediğinizi belirten yapılandırmayı tutacaktır.

## Adım 3: Kaynak PDF'yi Yükleyin (PDF Üzerinde OCR Çalıştırma)

Aspose OCR doğrudan bir PDF'yi alabilir; her sayfayı dahili olarak bir görüntüye dönüştürür. Yer tutucu yolu, taranmış belgenizin konumuyla değiştirin:

```csharp
            // Step 3: Load the source PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);
```

> **Neden çalışıyor:** `ImageStream.FromFile` yöntemi PDF formatını otomatik olarak algılar ve OCR için bir raster temsili hazırlar. Ek bir dönüşüm adımına gerek yoktur.

## Adım 4: Çıktı Formatı ve Dili Yapılandırma

Burada Aspose'a ne istediğimizi söylüyoruz. `OutputFormat`'u `SearchablePdf` olarak ayarlamak, motorun tanınan metni orijinal sayfa görüntülerinin arkasına gömmesini sağlar ve **aranabilir PDF** üretir. Doğruluğu artırmak için dili de seçebilirsiniz—İngilizce varsayılan dildir, ancak Fransızca, Almanca vb. dillerine geçebilirsiniz.

```csharp
            // Step 4: Choose output format and language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf; // creates searchable PDF
            ocrEngine.Configuration.Language = Language.English;               // *recognize text PDF* in English
```

İki dilli bir belge işlemeniz gerekiyorsa, `Language` enum bayraklarını kullanarak dilleri birleştirebilirsiniz.

## Adım 5: OCR Sürecini Çalıştırma – Metin PDF'lerini Tanıma

Şimdi zor iş burada gerçekleşir. `Recognize` yöntemi her sayfayı tarar, glifleri çıkarır ve hem orijinal görüntüyü hem de görünmez bir metin katmanını içeren dahili bir PDF akışı oluşturur. Bu, *metin PDF'lerini tanıma* adımıdır.

```csharp
            // Step 5: Execute OCR – this *recognizes text PDF* and builds the searchable stream
            ocrEngine.Recognize();
```

> **Sık sorulan soru:** *PDF 200 sayfa olursa ne olur?*  
> Motor sayfaları sırasıyla işler ve sonuçları akıtarak bellek tüketimini düşük tutar. Ancak, çok büyük dosyalar için `ocrEngine.Configuration` içindeki `MemoryLimit` ayarını artırmak isteyebilirsiniz.

## Adım 6: Aranabilir PDF'yi Kaydetme

Son olarak, çıktıyı diske yazın. `Save` yöntemi dahili akışı, herhangi bir PDF görüntüleyiciyle açabileceğiniz yeni bir dosyaya yazar.

```csharp
            // Step 6: Save the searchable PDF to disk
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

Programı çalıştırın (`dotnet run`) ve konsolda dosyanın oluşturulduğunu onaylayın. `handbook_searchable.pdf` dosyasını açın ve orijinal taramada bulunduğunu bildiğiniz bir kelimeyi aramayı deneyin – eşleşmeleri anında görmelisiniz.

## Kenar Durumları ve İleri Senaryoları Ele Alma

### Birden Çok Dil (OCR Taranmış PDF)

Kaynak PDF'niz hem İngilizce hem de İspanyolca metin içeriyorsa, dilleri birleştirin:

```csharp
ocrEngine.Configuration.Language = Language.English | Language.Spanish;
```

Aspose OCR, sözlükleri anlık olarak değiştirerek karışık dil belgelerinde doğruluğu artırır.

### Şifre Koruması Olan PDF'ler

Korunan PDF'lerle çalışırken, `Recognize` çağrısından önce şifreyi sağlayın:

```csharp
ocrEngine.Image = ImageStream.FromFile(inputPath, "MySecretPassword");
```

Şifre yanlış ise, `Recognize` bir `InvalidPasswordException` fırlatır; bunu yakalayarak kullanıcıdan doğru şifreyi isteyebilirsiniz.

### Görüntü Kalitesini Kontrol Etme

Daha yüksek DPI, daha iyi OCR sonuçları verir ancak daha fazla bellek tüketir. Bozuk karakterler fark ederseniz DPI'yi ayarlayın:

```csharp
ocrEngine.Configuration.Dpi = 300; // default is 200
```

### Lisans vs. Değerlendirme Modu

Değerlendirme modunda her sayfada bir filigran görünür. Bunu kaldırmak için herhangi bir OCR çağrısından önce lisansınızı uygulayın:

```csharp
var license = new License();
license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");
```

## Üretim Kullanımı için Pro İpuçları

- **Toplu işleme:** Temel mantığı, PDF listesi üzerinde dönen bir `foreach` döngüsü içinde paketleyin. Her dosyadan sonra `OcrEngine`'i serbest bırakarak yerel kaynakları temizleyin.
- **Günlükleme:** Detaylı OCR istatistiklerini yakalamak için `ocrEngine.Configuration.Logger`'ı kullanın (ör. saniyede tanınan karakter sayısı). Düşük doğruluk sorunlarını giderirken bu çok değerlidir.
- **Performans ayarı:** Çok çekirdekli sunucularda, her iş parçacığı için ayrı `OcrEngine` nesneleri oluşturun; kütüphane, her örnek izole olduğunda iş parçacığı güvenlidir.
- **Hata yönetimi:** `Recognize` ve `Save` işlemlerini her zaman `try/catch` bloklarıyla sarın. Yaygın istisnalar arasında `FileNotFoundException`, `OutOfMemoryException` ve `UnsupportedFormatException` bulunur.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Apply license (optional – removes evaluation watermark)
            // var license = new License();
            // license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");

            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Load PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Configure output as searchable PDF and set language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
            ocrEngine.Configuration.Language = Language.English;

            // 4️⃣ Run OCR – *recognize text PDF*
            ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Beklenen çıktı** (konsol):

```
Searchable PDF created at: C:\Docs\handbook_searchable.pdf
```

Ortaya çıkan dosyayı açın, **Ctrl + F** tuşlarına basın ve orijinal taranan sayfalarda yer alan herhangi bir kelimeyi bulabileceksiniz. Bu, *OCR taranmış PDF*'yi **aranabilir PDF**'ye dönüştürmenin büyüsü.

## Sonuç

Aspose OCR for .NET ile **aranabilir PDF** dosyalarının nasıl **oluşturulacağını** gösterdik; paketin kurulumu, çok dilli ve şifre korumalı PDF'lerin işlenmesi gibi tüm konuları kapsadık. Bu adımları izleyerek PDF belgelerinde güvenilir bir şekilde *OCR çalıştırabilir*, *metin PDF'lerini tanıyabilir* ve herhangi bir *OCR taranmış PDF*'yi tamamen aranabilir bir varlığa dönüştürebilirsiniz.

### Sıradaki Adımlar?

- **aspose ocr pdf** API'sini daha fazla keşfedin: düz metin çıkarın, DOCX'e dışa aktarın veya toplu olarak aranabilir PDF'ler oluşturun.  
- Aranabilir PDF çıktısını Aspose.PDF ile birleştirerek yer imleri veya filigranlar ekleyin.  
- Farklı DPI ayarları veya özel OCR sözlükleriyle nadir yazı tipleri için deneyler yapın.

Örneği istediğiniz gibi değiştirin, belge yönetimi hattınıza entegre edin veya yorumlarda sorularınızı sorun. Kodlamanın tadını çıkarın ve okunamaz taramaları aranabilir altına dönüştürmenin keyfini yaşayın!

## İlgili Öğreticiler

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cómo hacer OCR a PDF en .NET con Aspose.OCR](/ocr/spanish/net/text-recognition/recognize-pdf/)
- [كيفية إجراء OCR لملف PDF في .NET باستخدام Aspose.OCR](/ocr/arabic/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}