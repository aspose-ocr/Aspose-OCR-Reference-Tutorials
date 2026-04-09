---
category: general
date: 2026-04-08
description: Aranabilir PDF'yi hızlı bir şekilde oluşturun ve Aspose.OCR kullanarak
  C#'ta PDF görüntülerini sıkıştırmayı, PDF'ye font eklemeyi ve metin görüntülerini
  tanımayı öğrenin.
draft: false
keywords:
- create searchable pdf
- compress pdf images
- embed fonts pdf
- image to searchable pdf
- recognize text image
language: tr
og_description: Aspose.OCR ile hızlıca aranabilir PDF oluşturun. Tek bir öğreticide
  PDF görüntülerini sıkıştırmayı, PDF'ye font eklemeyi ve metin görüntülerini tanımayı
  öğrenin.
og_title: Aranabilir PDF Oluştur – Tam C# Rehberi
tags:
- Aspose.OCR
- C#
- PDF Generation
title: Aranabilir PDF Oluşturma – Görüntüden PDF'ye Tam C# Rehberi
url: /tr/net/text-recognition/create-searchable-pdf-complete-c-guide-for-image-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aranabilir PDF Oluşturma – Tam C# Kılavuzu

Tarayıcıdan bir görüntüden **aranabilir pdf** oluşturmanız mı gerekiyor? Dev bir PNG'ye bakıp onu hafif, metin‑aranabilir bir belgeye nasıl dönüştürebileceğinizi merak eden tek kişi değilsiniz. İyi haber, Aspose.OCR ile bunu birkaç satırda yapabilirsiniz ve ayrıca **compress PDF images**, **embed fonts PDF**, ve **recognize text image** nasıl yapılır öğrenmiş olacaksınız.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: bir görüntüyü yüklemek, OCR çalıştırmak, PDF kaydetme seçeneklerini ayarlamak ve sonunda aranabilir bir PDF'i diske yazmak. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz hazır bir yönteme ve daha sonra karşılaşabileceğiniz uç durumlar için birkaç profesyonel ipucuna sahip olacaksınız.

## Gereksinimler

- **.NET 6+** (kod .NET Framework 4.7'de de çalışır, ancak modern sözdizimi için .NET 6 hedefleyeceğiz).  
- **Aspose.OCR for .NET** – NuGet üzerinden kurun: `Install-Package Aspose.OCR`.  
- Aranabilir hâle getirmek istediğiniz metni içeren bir görüntü dosyası (PNG, JPEG, TIFF).  
- Biraz merak – geri kalanını aşağıda bulacaksınız.

> **Pro tip:** Eğer onlarca sayfayı işleme planlıyorsanız, dil verilerini tekrar tekrar yükleme yükünden kaçınmak için tek bir `OcrEngine` örneğini yeniden kullanmayı düşünün.

## Adım 1: OCR Motorunu Kurun – Metin Görüntüsünü Tanıma

İlk olarak, kaynak bitmap'ten karakterleri okuyabilen bir OCR motoruna ihtiyacımız var. Aspose.OCR, dili (English, French, vb.) belirtmenize izin verir ve ham metin ile görüntü verisini içeren bir `OcrResult` nesnesi döndürür.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

public static OcrResult LoadAndRecognize(string imagePath)
{
    // Initialize the OCR engine – “en” is the ISO code for English.
    var ocrEngine = new OcrEngine { Language = "en" };

    // Recognize the image and get the result.
    OcrResult result = ocrEngine.RecognizeImage(imagePath);

    // Quick sanity check – throw if nothing was detected.
    if (string.IsNullOrWhiteSpace(result.Text))
        throw new InvalidOperationException("No text was recognized in the image.");

    return result;
}
```

**Neden önemli:**  
- Dili ayarlamak doğruluğu dramatik şekilde artırır; motor sahne arkasında dil‑özel sözlükleri yükler.  
- `OcrResult` yalnızca çıkarılan dizeyi tutmakla kalmaz, aynı zamanda temel bitmap'i de içerir; bunu daha sonra PDF'e gömerek belgenin görsel olarak orijinal taramaya tamamen aynı kalmasını sağlayacağız.

## Adım 2: PDF Kaydetme Seçeneklerini Yapılandırın – Compress PDF Images & Embed Fonts

Aranabilir bir PDF, aslında taranmış görüntünün üzerine görünmez bir metin katmanı eklenmiş normal bir PDF'tir. Sıkıştırmayı göz ardı ederseniz, son dosya çok büyük olabilir. `PdfSaveOptions` sınıfı, görüntü kalitesi, font gömme ve fontların alt küme olarak eklenip eklenmeyeceği üzerinde ayrıntılı kontrol sağlar.

```csharp
public static PdfSaveOptions GetPdfSaveOptions()
{
    return new PdfSaveOptions
    {
        // Reduce file size by compressing the raster image.
        CompressImages = true,

        // ImageQuality ranges from 0 (worst) to 100 (best). 75 is a good balance.
        ImageQuality = 75,

        // Embedding fonts ensures the text layer looks the same on any machine.
        EmbedFonts = true,

        // Subsetting keeps only the glyphs we actually use – another size saver.
        FontSubset = true
    };
}
```

**Neden embed fonts PDF yapmalısınız:**  
PDF, OCR katmanında kullanılan tam fonta sahip olmayan bir sistemde açıldığında metin bozuk görünebilir. Fontları gömmek, platformlar arasında görsel tutarlılığı garanti eder; bu da yasal veya arşiv belgeleri için kritik öneme sahiptir.

## Adım 3: Sonucu Aranabilir PDF Olarak Kaydedin – Image to Searchable PDF

Şimdi her şeyi birleştiriyoruz: `OcrResult`'u alın, `PdfSaveOptions`'ı uygulayın ve dosyayı yazın. `SaveAsSearchablePdf` yöntemi ağır işi yapar—OCR çıktısını yansıtan gizli bir metin katmanı oluşturur ve orijinal görüntüyü korur.

```csharp
public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
{
    // Step 1: Recognize the image.
    OcrResult ocrResult = LoadAndRecognize(inputImage);

    // Step 2: Prepare PDF options.
    PdfSaveOptions pdfOptions = GetPdfSaveOptions();

    // Step 3: Write the searchable PDF.
    ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);

    Console.WriteLine($"Searchable PDF created at: {outputPdf}");
}
```

### Tam Çalışan Örnek

Aşağıda, yeni bir .NET console projesine kopyalayıp yapıştırabileceğiniz bağımsız bir konsol programı yer alıyor. Görüntünün çalıştırılabilir dosyaya göre `YOUR_DIRECTORY` adlı bir klasörde bulunduğunu varsayar.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

class Program
{
    static void Main()
    {
        string inputPath = "YOUR_DIRECTORY/input.png";
        string outputPath = "YOUR_DIRECTORY/output.pdf";

        try
        {
            CreateCompressedSearchablePdf(inputPath, outputPath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // --- Methods from the previous steps -------------------------------------------------
    public static OcrResult LoadAndRecognize(string imagePath)
    {
        var ocrEngine = new OcrEngine { Language = "en" };
        OcrResult result = ocrEngine.RecognizeImage(imagePath);
        if (string.IsNullOrWhiteSpace(result.Text))
            throw new InvalidOperationException("OCR did not detect any text.");
        return result;
    }

    public static PdfSaveOptions GetPdfSaveOptions()
    {
        return new PdfSaveOptions
        {
            CompressImages = true,
            ImageQuality = 75,
            EmbedFonts = true,
            FontSubset = true
        };
    }

    public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
    {
        OcrResult ocrResult = LoadAndRecognize(inputImage);
        PdfSaveOptions pdfOptions = GetPdfSaveOptions();
        ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);
        Console.WriteLine("Searchable PDF created.");
    }
}
```

Programı çalıştırdığınızda `output.pdf` oluşturulur; bu dosyayı Adobe Reader, Foxit veya herhangi bir PDF görüntüleyicide açıp yalnızca görüntüde bulunan kelimeleri anında arayabilirsiniz.

## Adım 4: Çıktıyı Doğrulayın – Arama Çalışıyor mu?

Dosya oluşturulduktan sonra açın ve yerleşik aramayı (Ctrl + F) deneyin. “invoice”, “date” veya “total” gibi kelimeleri bulabiliyorsanız **aranabilir PDF** başarıyla oluşturulmuş demektir.  

Arama hiçbir şey döndürmüyorsa:

1. **Check OCR accuracy** – kaynak görüntü düşük çözünürlükte olabilir. OCR'dan önce DPI'yi artırmayı düşünün (Aspose motorunda `Resolution` ayarlayabilirsiniz).  
2. **Confirm font embedding** – PDF'in özelliklerine gidin ve *Fonts* bölümüne bakın; gömülü fontun listelendiğini görmelisiniz.  
3. **Inspect image compression** – çok düşük `ImageQuality` görsel katmanı okunamaz hâle getirebilir, bu da bazı araçların doğru çalışmasını engelleyebilir.

## Common Variations & Edge Cases

| Senaryo | Ayarlanacak Şey | Neden |
|----------|----------------|-----|
| **Multi‑page TIFF** | Her çerçeve üzerinde döngü kurun, sayfa başına `RecognizeImage` çağırın, ardından `PdfSaveOptions` ile `AppendMode = true` kullanın. | Her taranmış sayfayı kendi aranabilir sayfası olarak tutar. |
| **Non‑English language** | `Language = "fr"` (veya uygun ISO kodu) olarak değiştirin ve isteğe bağlı olarak özel bir sözlük sağlayın. | Aksanlı karakterler ve dile özgü glifler için tanıma doğruluğunu artırır. |
| **Very large images** | OCR'dan önce bitmap'i küçültün (`ocrEngine.Image = Image.FromFile(...).GetThumbnailImage(...)`). | Bellek kullanımını azaltır ve OCR hızını artırır, doğruluktan çok fazla ödün vermez. |
| **Need OCR confidence** | `ocrResult.RecognizedWords`'e erişin ve `Confidence` özelliğini inceleyin. | Düşük güvenilirlikteki kelimeleri manuel inceleme için işaretlemenizi sağlar. |

## Performance Tips

- **Reuse the `OcrEngine`** when processing a batch of files – it caches language data.  
- **Parallelize** the recognition step with `Parallel.ForEach` if you’re on a multi‑core machine, but keep PDF writes sequential to avoid file‑access conflicts.  
- **Tune `ImageQuality`**: 85‑90 gives near‑lossless images, while 60‑70 is often enough for text‑heavy documents.

## Sonuç

Aspose.OCR kullanarak görüntülerden **create searchable pdf** dosyaları oluşturmak için ihtiyacınız olan her şeyi, ayrıca **compress pdf images**, **embed fonts pdf** ve **recognize text image** nasıl yapılır konularını öğrendik. Tam kod örneği herhangi bir C# projesine eklenmeye hazır ve ek ipuçları, çözümü daha büyük iş yüklerine veya farklı dillere uyarlamanıza yardımcı olacak.

Bir sonraki adıma hazır mısınız? Bir filigran eklemeyi, birden fazla aranabilir PDF'i birleştirmeyi veya bu rutini bir web API'ye entegre etmeyi deneyin; böylece kullanıcılar taramaları yükleyip anında aranabilir PDF alabilir. Olanaklar sonsuzdur ve temeller yerinde olduğu sürece iş akışını genişletmek çok kolay olacaktır.

İyi kodlamalar, PDF'leriniz küçük, aranabilir ve mükemmel render edilmiş olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}