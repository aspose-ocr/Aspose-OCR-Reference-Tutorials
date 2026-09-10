---
category: general
date: 2025-12-30
description: C#'ta bir görüntüden aranabilir PDF oluşturun – TIFF'i PDF'ye dönüştürmeyi,
  görüntüden metin çıkarmayı ve PDF oluşturmayı otomatikleştirmeyi öğrenin.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- convert tiff to pdf
- extract text from image
- how to create pdf
language: tr
og_description: Aspose OCR kullanarak C#'ta bir görüntüden aranabilir PDF oluşturun.
  Bu kılavuz, TIFF'i PDF'ye dönüştürmeyi, metni çıkarmayı ve PDF/A‑1b uyumluluğunu
  sağlamayı gösterir.
og_title: TIFF'ten aranabilir PDF oluşturma – Adım adım C# öğreticisi
tags:
- Aspose OCR
- C#
- PDF generation
title: TIFF'ten Aranabilir PDF Oluşturma – Tam C# Rehberi
url: /tr/net/text-recognition/create-searchable-pdf-from-tiff-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF'ten Aranabilir PDF Oluşturma – Tam C# Kılavuzu

Hiç taranmış bir TIFF'ten **aranabilir PDF** oluşturmanız gerekti, ancak nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz. Birçok geliştirici, arşivleme veya uyumluluk için aranabilir PDF'lere ihtiyaç duyduklarında bu engelle karşılaşır ve iyi haber şu ki, çözüm Aspose OCR ile şaşırtıcı derecede basittir.

Bu öğreticide bir görüntüyü PDF'ye dönüştürmeyi, görüntüden metin çıkarmayı ve çıktıyı PDF/A‑1b standartlarına uygun şekilde iyileştirmeyi adım adım inceleyeceğiz. Sonunda **tiff'i pdf'e dönüştürme**, **görüntüden metin çıkarma** ve **aranabilir ve arşivlenebilir pdf** dosyalarının nasıl oluşturulacağını tam olarak bileceksiniz.

## Gereksinimler

- .NET 6 (veya daha yeni bir .NET sürümü) – kod .NET Core ve .NET Framework'te aynı şekilde çalışır.  
- Aspose.OCR NuGet paketi – `dotnet add package Aspose.OCR` komutuyla kurun.  
- Aranabilir PDF'e dönüştürmek istediğiniz örnek TIFF dosyası (`input.tif`).  
- Bir geliştirme ortamı (Visual Studio, VS Code, Rider… herhangi biri yeterli).  

Hepsi bu. Başka SDK, harici hizmet veya gizli yapılandırma adımı yok.

![Aranabilir PDF örneği](image-placeholder.png "Aranabilir PDF önizlemesi")

## Adım 1 – OCR Motorunu Başlatma ve İngilizce Modelini Yükleme

Bir görüntüyü aranabilir metne dönüştürmeden önce OCR motorunun hangi dili arayacağını bilmesi gerekir. Aspose OCR, ihtiyaca göre yüklenebilen dil paketleriyle birlikte gelir.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Load the English language model (you can swap this for other languages)
ocrEngine.LoadLanguage(LanguageModel.English);
```

**Neden önemli:** Doğru dil modelini yüklemek tanıma doğruluğunu büyük ölçüde artırır. Bu adımı atladığınızda motor, genellikle bozuk metin üreten genel bir modele geri döner – özellikle düşük çözünürlüklü TIFF'lerde.

## Adım 2 – Kaynak Görüntüden Metni Tanıma (İsteğe Bağlı ama Kullanışlı)

OCR çalıştırdığınızda `OcrResult` nesnesi elde edersiniz; bunu inceleyebilir, kaydedebilir veya düz metin olarak saklayabilirsiniz. Bu adım yalnızca nihai PDF ile ilgileniyorsanız isteğe bağlıdır, ancak hata ayıklama için çok faydalıdır.

```csharp
// Perform OCR on the input TIFF
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/input.tif");

// Dump the raw text to the console (useful for validation)
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

**İpucu:** Çıkarılan metin hatalı görünüyorsa, motoru beslemeden önce görüntüyü ön işleme (eğikliği düzeltme, lekeleri temizleme) yapmayı düşünün. Aspose OCR ayrıca burada zincirleyebileceğiniz görüntü iyileştirme yardımcı programları sunar.

## Adım 3 – Aranabilir PDF Dışa Aktarıcısını Ayarlama

Şimdi Aspose'a nihai PDF'in nasıl görünmesini istediğimizi söylüyoruz. `SearchablePdfExporter` çıktı yolunu, PDF/A uyumluluğunu ve birkaç ek özelliği belirlemenizi sağlar.

```csharp
var pdfExporter = new SearchablePdfExporter
{
    // Where the searchable PDF will be saved
    OutputPath = "YOUR_DIRECTORY/output.pdf",

    // Enforce PDF/A‑1b compliance – ideal for long‑term archiving
    PdfACompliance = PdfACompliance.PdfA1b
};
```

**Neden PDF/A‑1b?** Birçok sektör (hukuk, sağlık, finans) arşivleme standartlarına uygun PDF'ler talep eder. `PdfACompliance` ayarı, yazı tiplerinin gömülmesini, renklerin cihaz bağımsız olmasını ve dosyanın doğrulama araçlarından geçmesini sağlar.

## Adım 4 – OCR Sonucunu Doğrudan Aranabilir PDF'e Dışa Aktarma

Motor ve dışa aktarıcı hazır olduğunda, işin büyük kısmı tek bir satırla halledilir. Dışa aktarıcı, içinde bir PDF sayfası oluşturur, tanınan metni görünmez bir katman olarak üstüne yerleştirir ve dosyayı yazar.

```csharp
// Export the OCR result to a searchable PDF
pdfExporter.Export(ocrEngine, "YOUR_DIRECTORY/input.tif");

// Confirmation message
Console.WriteLine("Searchable PDF created at YOUR_DIRECTORY/output.pdf");
```

**Arka planda neler oluyor?**  
1. Orijinal TIFF raster görüntü olarak gömülür.  
2. OCR’dan elde edilen metin üstte, gizli ama seçilebilir bir katman olarak yer alır.  
3. PDF okuyucularının metni indeksleyebilmesi için dil gibi meta veriler eklenir.

## Adım 5 – Çıktıyı Doğrulama (Manuel Kontrol + Programatik Doğrulama)

PDF'in gerçekten aranabilir olduğunu doğrulamak her zaman iyi bir uygulamadır.

```csharp
// Quick sanity check: open the PDF and try to extract its text
using var pdfReader = new Aspose.Pdf.Facades.PdfConverter();
pdfReader.BindPdf("YOUR_DIRECTORY/output.pdf");
var extracted = pdfReader.ExtractText();
Console.WriteLine("Text extracted from the PDF:");
Console.WriteLine(extracted);
```

PDF görüntüleyicisinde metni kopyalayıp yapıştırabiliyor veya yukarıdaki konsol çıktısında görebiliyorsanız, başarılı olmuşsunuz demektir.

## Kenar Durumları ve Yaygın Varyasyonlar

### Diğer Görüntü Formatlarını Dönüştürme

Aynı kod PNG, JPEG, BMP için de çalışır—sadece `Recognize` ve `Export` çağrılarındaki dosya uzantısını değiştirin. Ek yapılandırma gerekmez.

### Çok Sayfalı TIFF Dosyaları

Aspose OCR, çok sayfalı bir TIFF'in her sayfasını otomatik olarak işler ve dışa aktarıcı bunları çok sayfalı bir PDF'e dönüştürür. Bir sayfayı atlamak isterseniz, dışa aktarmadan önce `ocrResult.Pages` koleksiyonunu filtreleyin.

### İngilizce Olmayan Diller

`LanguageModel.English` yerine `LanguageModel.Spanish`, `LanguageModel.French` vb. kullanın veya özel bir dil paketi yükleyin. Belirli bir yerel ayara yönelik PDF meta verilerini de güncellemeyi unutmayın.

### PDF Boyutunu Küçültme

TIFF'ler yüksek çözünürlüklüyse, ortaya çıkan PDF büyük olabilir. OCR'dan önce görüntüyü aşağı örnekleyebilirsiniz:

```csharp
ocrEngine.ImageProcessingOptions = new ImageProcessingOptions
{
    Dpi = 150 // Lower DPI reduces size, but test for acceptable quality
};
```

### Şifre Koruması Olan PDF'ler

Çıktıyı korumak isterseniz, dışa aktarma işleminden sonra `SearchablePdfExporter`'ı Aspose.Pdf şifreleme API'si ile sarmalayın:

```csharp
var pdfDoc = new Aspose.Pdf.Document("YOUR_DIRECTORY/output.pdf");
pdfDoc.Encrypt("userPassword", "ownerPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save("YOUR_DIRECTORY/output_protected.pdf");
```

## Tam Çalışan Örnek

Aşağıda, yukarıda tartışılan tüm adımları ve isteğe bağlı ayarları içeren, kopyala‑yapıştır‑hazır program yer almaktadır.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Export;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Initialize OCR engine and load language model
        // -----------------------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // Optional: lower DPI to shrink output size (adjust as needed)
        // ocrEngine.ImageProcessingOptions = new ImageProcessingOptions { Dpi = 150 };

        // -----------------------------------------------------------------
        // 2️⃣ Recognize text from the source TIFF
        // -----------------------------------------------------------------
        const string inputPath = @"YOUR_DIRECTORY/input.tif";
        var ocrResult = ocrEngine.Recognize(inputPath);
        Console.WriteLine("Extracted text from image:");
        Console.WriteLine(ocrResult.Text);

        // -----------------------------------------------------------------
        // 3️⃣ Configure the searchable PDF exporter
        // -----------------------------------------------------------------
        var pdfExporter = new SearchablePdfExporter
        {
            OutputPath = @"YOUR_DIRECTORY/output.pdf",
            PdfACompliance = PdfACompliance.PdfA1b // archival compliance
        };

        // -----------------------------------------------------------------
        // 4️⃣ Export OCR result to searchable PDF
        // -----------------------------------------------------------------
        pdfExporter.Export(ocrEngine, inputPath);
        Console.WriteLine("Searchable PDF created successfully.");

        // -----------------------------------------------------------------
        // 5️⃣ Verify by extracting text from the generated PDF
        // -----------------------------------------------------------------
        using var converter = new PdfConverter();
        converter.BindPdf(@"YOUR_DIRECTORY/output.pdf");
        var extractedFromPdf = converter.ExtractText();
        Console.WriteLine("Text extracted from the PDF:");
        Console.WriteLine(extractedFromPdf);
    }
}
```

**Beklenen çıktı:**  
- Konsol, TIFF'ten alınan ham OCR metnini yazdırır.  
- `output.pdf` adlı bir dosya `YOUR_DIRECTORY` içinde oluşur.  
- Adobe Reader’da `output.pdf` açıldığında metni seçip kopyalayabilir, bunun aranabilir olduğunu doğrulayabilirsiniz.

## Özet

Aspose OCR kullanarak TIFF görüntülerinden **aranabilir PDF** dosyaları oluşturmak için ihtiyacınız olan her şeyi ele aldık. OCR motorunu başlatma, metin çıkarma, PDF/A uyumluluğunu ayarlama ve son belgeyi doğrulama adımlarını ayrıntılı olarak açıkladık. Artık **görüntüyü pdf'e dönüştürme**, **tiff'i pdf'e dönüştürme**, **görüntüden metin çıkarma** ve **aranabilir katmanlı pdf nasıl oluşturulur** sorularının yanıtını biliyorsunuz.

## Sonraki Keşifler

- **Toplu işleme:** Mantığı bir döngüye sararak onlarca görüntüyü otomatik olarak işleyin.  
- **Özel yazı tipleri:** Kurumsal fontları gömerek marka tutarlılığı sağlayın.  
- **Bulut entegrasyonu:** PDF'leri oluşturduktan hemen sonra Azure Blob Storage veya AWS S3'e kaydedin.  
- **UI ön yüz:** Kullanıcıların sürükle‑bırak ile anında dönüşüm yapabileceği basit bir WinForms/WPF uygulaması geliştirin.

Farklı dil modelleri, DPI ayarları ve PDF/A seviyeleriyle denemeler yapmaktan çekinmeyin. API, hayal edebileceğiniz hemen hemen her iş akışına uyum sağlayacak kadar esnek.

---

*Kodlamanız keyifli olsun, PDF'leriniz her zaman aranabilir olsun!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}