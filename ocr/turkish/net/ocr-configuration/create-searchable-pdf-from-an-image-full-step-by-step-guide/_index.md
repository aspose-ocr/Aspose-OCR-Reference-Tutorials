---
category: general
date: 2026-06-06
description: Aranabilir PDF oluşturmayı ve OCR ile görüntüyü PDF'ye dönüştürmeyi öğrenin.
  Katman ekleme, sıkıştırma ayarları ve tam C# kodunu içerir.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- how to ocr image
- how to add layer
- how to set compression
language: tr
og_description: OCR kullanarak bir görüntüden aranabilir PDF oluşturun. Bu kılavuz,
  gizli bir metin katmanı eklemeyi, sıkıştırmayı ayarlamayı ve görüntüyü PDF'ye dönüştürmeyi
  gösterir.
og_title: Aranabilir PDF Oluştur – Tam C# Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  headline: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  name: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - The
      Aspose.OCR and Aspose.Pdf NuGet packages (or any equivalent library that offers
      `OcrEngine` and `PdfSaveOptions`). - A sample image, e.g., `invoice.png`, placed
      in a folder you can reference. - A basic understanding of C# syntax'
  - name: Full Working Example
    text: 'Putting it all together, here’s the complete, ready‑to‑run program:'
  - name: Pro tip
    text: If you need to **convert image to PDF** without OCR (just a plain image
      PDF), set `AddTextLayer = false`. The same `PdfSaveOptions` still lets you control
      compression, which is handy for archiving scanned documents that don’t need
      searchability.
  type: HowTo
tags:
- OCR
- PDF
- C#
- Aspose
title: Bir Görüntüden Aranabilir PDF Oluşturma – Tam Adım Adım Kılavuz
url: /tr/net/ocr-configuration/create-searchable-pdf-from-an-image-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Searchable PDF Oluşturma – Tam C# Öğreticisi

Hiç **tarama yoluyla alınan bir faturadan** saatlerce bir GUI aracıyla uğraşmadan **arama yapılabilir PDF** oluşturmayı düşündünüz mü? Yalnız değilsiniz. Birçok geliştirici, bir görüntüyü hem orijinali gibi görünüp hem de kullanıcıların metni kopyalayıp arayabileceği bir PDF’ye dönüştürmek zorunda kaldığında bir çıkmaza giriyor.  

Bu öğreticide **görüntüyü PDF’ye dönüştürme**, OCR çalıştırma, gizli bir metin katmanı ekleme ve sıkıştırma ayarlarını ince ayar yapma adımlarını adım adım göstereceğiz. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz hazır bir C# kod parçacığına sahip olacaksınız.

## Öğrenecekleriniz

- Bir OCR motoru kurma ve **görüntü dosyalarını OCR** nasıl yapacağınızı anlama.
- **Katman ekleme** seçeneklerini kullanarak arama yapılabilir bir metin katmanı gömme.
- Daha küçük, zip‑sıkıştırmalı PDF’ler için **sıkıştırma ayarlarını** nasıl yapacağınızı öğrenme.
- Düz bir resmi **arama yapılabilir pdf oluşturma** iş akışına dönüştürme ve bunu otomatikleştirme.
- Yaygın tuzaklar ve PDF’lerinizi net ve hızlı tutmak için profesyonel ipuçları.

### Önkoşullar

- .NET 6.0 veya üzeri (kod .NET Framework 4.7+’de de çalışır).
- Aspose.OCR ve Aspose.Pdf NuGet paketleri (veya `OcrEngine` ve `PdfSaveOptions` sunan eşdeğer bir kütüphane).
- `invoice.png` gibi bir örnek görüntü, referans alabileceğiniz bir klasörde bulunmalı.
- C# sözdizimi temelleri—derin OCR bilgisi gerekmez.

> **Pro tip:** Visual Studio kullanıyorsanız paketleri Package Manager Console üzerinden kurun:  
> `Install-Package Aspose.OCR`  
> `Install-Package Aspose.Pdf`

---

![Arama yapılabilir PDF örneği, fatura görüntüsünün gizli metin katmanı ile PDF’ye dönüştürülmüş hali](/images/create-searchable-pdf.png)

## Adım 1: OCR Motorunu Başlatma – **how to ocr image**

İlk olarak resmimizdeki İngilizce metni okuyabilecek bir OCR motoruna ihtiyacımız var. `OcrEngine` sınıfı giriş noktasıdır; sadece dili ayarlayıp daha sonra bir görüntü verirsiniz.

```csharp
using Aspose.OCR;
using Aspose.Pdf;

// Create and configure the OCR engine
OcrEngine engine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

*Neden önemli:* Motoru doğru dille başlatmak doğruluğu büyük ölçüde artırır. Bunu atlamanız durumunda bozuk karakterler elde edebilirsiniz.

## Adım 2: Görüntüyü Yükleme – **convert image to pdf**

Şimdi motoru işlemek istediğimiz dosyaya yönlendiriyoruz. `ImageStream.FromFile` baytları okur ve OCR için hazırlar.

```csharp
// Load the image you want to turn into a searchable PDF
engine.Image = ImageStream.FromFile(@"C:\Docs\invoice.png");
```

Görüntü bir web isteği ya da veritabanından geliyorsa `MemoryStream` üzerinden de yükleyebilirsiniz.

## Adım 3: OCR Tanıma Çalıştırma – **how to ocr image**

Görüntü yüklendikten sonra tek bir çağrıyla ağır işi yaparız. `Recognize` metodu, çıkarılan metni ve orijinal bitmap’i tutan bir `OcrResult` döndürür.

```csharp
// Perform OCR on the loaded image
OcrResult ocrResult = engine.Recognize();
```

*Arka planda:* Motor her pikseli analiz eder, karakterleri algılar ve bir Unicode dizesi oluşturur. Ayrıca daha sonra gizli metin katmanı için gereken konumsal verileri de saklar.

## Adım 4: PDF Kaydetme Seçeneklerini Yapılandırma – **how to add layer** & **how to set compression**

Arama yapılabilir bir PDF’in sihrinin gerçekleştiği yer burası. Aspose.Pdf’e orijinal görüntüyü gömmesini, gizli bir metin katmanı eklemesini ve son dosyayı sıkıştırmasını söyleyen bir `PdfSaveOptions` nesnesi oluştururuz.

```csharp
// Set up PDF options for a searchable PDF
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    IncludeImage = true,          // Keep the original image in the PDF
    AddTextLayer = true,          // Add a hidden text layer with OCR results
    Compression = PdfCompression.Zip   // Use ZIP compression for smaller size
};
```

- **IncludeImage** orijinal taramanın görsel bütünlüğünü korur.
- **AddTextLayer** tarayıcıların ve PDF okuyucuların arama yapabilmesi için görünmez bir katman oluşturur.
- **Compression** kaliteyi kaybetmeden dosya boyutunu azaltır; ZIP çoğu belge için iyi bir varsayılandır.

## Adım 5: Sonucu Kaydetme – **create searchable pdf**

Son olarak, tanımladığımız seçeneklerle OCR sonucunu diske yazarız. `Save` metodu hedef yolu ve `PdfSaveOptions` örneğini alır.

```csharp
// Save the OCR result as a searchable PDF
ocrResult.Save(@"C:\Docs\invoice_searchable.pdf", pdfOptions);
```

`invoice_searchable.pdf` dosyasını Adobe Reader ya da modern bir görüntüleyicide açtığınızda orijinal görüntüyü göreceksiniz, ancak artık metni seçebilir, kopyalayabilir ve arama yapabilirsiniz; sanki yerel bir PDFmiş gibi.

### Tam Çalışan Örnek

Hepsini bir araya getirdiğimizde, çalıştırmaya hazır tam program aşağıdadır:

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine engine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the source image
            string imagePath = @"C:\Docs\invoice.png";
            engine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            OcrResult result = engine.Recognize();

            // 4️⃣ Configure PDF options (layer + compression)
            PdfSaveOptions pdfOptions = new PdfSaveOptions
            {
                IncludeImage = true,
                AddTextLayer = true,
                Compression = PdfCompression.Zip
            };

            // 5️⃣ Save as searchable PDF
            string pdfPath = @"C:\Docs\invoice_searchable.pdf";
            result.Save(pdfPath, pdfOptions);

            Console.WriteLine($"Searchable PDF created at: {pdfPath}");
        }
    }
}
```

**Beklenen çıktı** (konsolda):  
`Searchable PDF created at: C:\Docs\invoice_searchable.pdf`

Oluşan dosyayı açın, **Ctrl F** tuşlarına basın, faturada gördüğünüz bir kelimeyi yazın ve görüntüleyicinin anında ona atladığını izleyin. İşte **create searchable pdf** işlevinin özü.

## Yaygın Tuzaklar & Kaçınma Yöntemleri

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|------|
| Metin aranamaz | `AddTextLayer` **false** bırakılmış veya eski bir Aspose sürümü kullanılıyor | `AddTextLayer = true` olduğundan emin olun ve en yeni NuGet paketine güncelleyin |
| PDF çok büyük (megabayt) | Sıkıştırma `PdfCompression.None` olarak ayarlanmış | `PdfCompression.Zip` ya da görüntüler için `PdfCompression.Jpeg` kullanın |
| Bozuk karakterler | Yanlış dil ayarı veya düşük çözünürlüklü görüntü | `engine.Language`ı doğru şekilde ayarlayın ve en az 300 dpi görüntüler sağlayın |
| Gizli katman bazı görüntüleyicilerde görünmez | PDF standart dışı bir sürümle oluşturulmuş | `PdfSaveOptions.PdfVersion = PdfVersion.PDF_1_7` (varsayılan) kullanın veya görüntüleyiciyi güncelleyin |

### Pro tip

OCR olmadan sadece düz bir görüntü PDF’si oluşturmak isterseniz **convert image to PDF** sırasında `AddTextLayer = false` yapın. Aynı `PdfSaveOptions` sıkıştırma kontrolünü sağlar; bu, arama gerektirmeyen taranmış belgeleri arşivlemek için kullanışlıdır.

## Çözümü Genişletmek

- **Birden çok sayfa**: Görüntü dosyaları listesini döngüye alın, her seferinde `engine.Image = ...` atayın ve `PdfDocument` birleştirme ile tek bir PDF’de toplayın.
- **Farklı diller**: `engine.Language = OcrLanguage.Spanish` (veya desteklenen başka bir dil) yaparak çok dilli faturaları işleyin.
- **Özel sıkıştırma**: Renk açısından zengin görüntüler için `PdfCompression.Jpeg` ve kalite ayarı (`pdfOptions.JpegQuality = 80`) dosyaları daha da küçültebilir.

## Sonuç

C# kullanarak görüntülerden **arama yapılabilir PDF** dosyaları oluşturmak için ihtiyaç duyduğunuz her şeyi ele aldık. OCR motorunu başlatma, resmi yükleme, tanıma yapma, gizli bir metin katmanı yapılandırma ve sıkıştırma ayarlarını belirleme—her adım hızlı ve aranabilir bir belge sunmak için kritik bir rol oynar.  

Artık fatura işleme, sözleşme arşivleme ya da kağıt yığınlarını anında aranabilir PDF’lere dönüştüren toplu tarama araçları otomatikleştirebilirsiniz.  

Bir sonraki zorluğa hazır mısınız? Su işaretleri eklemeyi, birden çok aranabilir PDF’yi birleştirmeyi ya da bu mantığı bir Web API üzerinden sunarak tüm organizasyonun görüntü yükleyip anında aranabilir PDF almasını sağlayın.

---

*Bu rehberi faydalı bulduysanız bir ⭐ verin, ekip arkadaşlarınızla paylaşın ya da kendi düzenlemelerinizi yorum olarak bırakın. Mutlu kodlamalar!*


## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}