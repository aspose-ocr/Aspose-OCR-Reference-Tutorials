---
category: general
date: 2026-04-06
description: Görüntü dosyalarında OCR nasıl yapılır, TIF'ten metin nasıl çıkarılır,
  OCR için görüntü nasıl yüklenir ve sonuç Aspose OCR kullanarak C#'ta EPUB'a nasıl
  dönüştürülür, öğrenin.
draft: false
keywords:
- perform OCR on image
- convert image to EPUB
- how to generate EPUB
- extract text from TIF
- load image for OCR
language: tr
og_description: C#'ta görüntüde OCR yapın, TIF'ten metin çıkarın, OCR için görüntüyü
  yükleyin ve sonucu EPUB'a dönüştürün. Tam kodlu adım adım rehber.
og_title: Görüntüde OCR Yap → EPUB – Tam C# Öğreticisi
tags:
- C#
- Aspose OCR
- EPUB conversion
- Image processing
title: Görüntüde OCR Yap ve EPUB'a Dönüştür – Tam C# Rehberi
url: /tr/net/text-recognition/perform-ocr-on-image-and-convert-to-epub-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntü Üzerinde OCR Yap ve EPUB’a Dönüştür – Tam C# Öğreticisi

Hiç **görüntü dosyalarında OCR** yapmanız gerekti ama metni okunabilir bir e‑kitap formatına nasıl alacağınızı bilemediniz mi? Tek başınıza değilsiniz. Birçok geliştirici, taranmış bir sayfa (çoğu zaman .TIF) olduğunda bunu temiz bir EPUB’a dönüştürmek için manuel kopyala‑yapıştır yapmaktan kaçınmak ister.  

Bu rehberde tüm süreci adım adım inceleyeceğiz: **OCR için görüntüyü yükleme**, metni çıkarma ve son olarak **görüntüyü EPUB’a dönüştürme** işlemlerini Aspose OCR kütüphanesiyle gerçekleştireceğiz. Sonunda, taranmış bir sayfayı alıp mükemmel yapılandırılmış bir EPUB dosyası üretebilen bağımsız bir programınız olacak—ekstra araçlara ihtiyaç duymadan.

## Öğrenecekleriniz

- C#’ta **OCR için görüntüyü yükleme** (büyük TIF dosyalarını da kapsayan) nasıl yapılır.  
- Aspose OCR ile **görüntü üzerinde OCR** gerçekleştirmenin tam adımları ve her bir çağrının önemi.  
- **TIF’ten metin çıkarma** ve e‑kitap yayıncılığı için temizleme teknikleri.  
- **Görüntüyü EPUB’a dönüştürmenin** en basit yolu ve özelleştirme seçenekleri.  
- Büyük taramalar sırasında ortaya çıkan bellek sorunları gibi yaygın tuzaklar ve hızlı çözümler.

### Ön Koşullar

| Gereksinim | Neden Önemli |
|-------------|----------------|
| .NET 6.0 veya üzeri (kod ayrıca .NET Framework 4.8’de de çalışır) | Aşağıdaki C# 10 sözdiziminin çalışması için runtime sağlar. |
| Aspose.OCR NuGet paketi (`Aspose.OCR` ve `Aspose.OCR.Export`) | Karakterleri tanıyan ve EPUB’u yazan motor. |
| İşlemek istediğiniz bir TIF görüntüsü (`book_page.tif`) | Örneğimiz tek sayfalı bir tarama kullanıyor, ancak aynı mantık çok sayfalı TIFF’lerde de çalışır. |
| Visual Studio 2022 (veya tercih ettiğiniz başka bir IDE) | Hata ayıklamayı ve paket yönetimini sorunsuz hâle getirir. |

Eğer bunlara sahipseniz, bir fincan kahve alın ve başlayalım.

![Görüntü üzerinde OCR yapma, metin çıkarma ve bir EPUB dosyası oluşturma sürecini gösteren iş akışı diyagramı](perform-ocr-on-image-workflow.png "görüntü üzerinde OCR iş akışı")

## Adım 1: OCR İçin Görüntüyü Yükleme

Motorun bir şey tanıyabilmesi için geçerli bir `System.Drawing.Image` örneğine ihtiyacı vardır. `Image.FromFile` yöntemi çoğu raster formatı için çalışır, ancak TIF’lerde çok‑çerçeveli sorunlarla karşılaşabilirsiniz. Çağrıyı bir `using` bloğu içinde sarmak, dosya tutamacının hızlıca serbest bırakılmasını sağlar—bu, bir parti içinde onlarca sayfa işlediğinizde çok önemlidir.

```csharp
using System.Drawing;

// Path to your source scan – change this to your actual file location
string sourcePath = @"C:\Scans\book_page.tif";

// Load the image safely
using (Image sourceImage = Image.FromFile(sourcePath))
{
    // The image is now ready for OCR
    // (We’ll hand it off to the engine in the next step)
}
```

**Neden Önemli:**  
- **Bellek güvenliği:** `using`, GDI+ kaynaklarının dispose edilmesini sağlar, uzun süren servislerin çökmesini önler.  
- **Format esnekliği:** `Image.FromFile` TIFF, PNG, JPEG vb. formatları otomatik algılar, böylece her dosya türü için ayrı yükleyici yazmanıza gerek kalmaz.

> **Pro ipucu:** Belirli TIFF’lerde “parameter is not valid” hatası alıyorsanız, yalnızca‑okuma kipinde açılmış bir `FileStream` ile `Image.FromStream` kullanmayı düşünün. Bu, bazı GDI+ tuhaflıklarını atlatır.

## Adım 2: Görüntü Üzerinde OCR Yapma

Şimdi görüntü bellekte olduğuna göre Aspose OCR motorunu başlatıyoruz. `OcrEngine` sınıfı hafiftir; birden çok sayfa için tek bir örnek yeniden kullanılabilir ve bu da ek yükü azaltır.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Create the OCR engine – you can pass a license object here if you have one
OcrEngine ocrEngine = new OcrEngine();

// Inside the using block from Step 1
using (Image sourceImage = Image.FromFile(sourcePath))
{
    // Run the recognition process
    OcrResult ocrResult = ocrEngine.Recognize(sourceImage);

    // The Result property holds the extracted plain text
    string extractedText = ocrResult.Text;

    // Optional: Write the raw text to console for quick verification
    Console.WriteLine("=== Extracted Text ===");
    Console.WriteLine(extractedText);
}
```

**Neden Önemli:**  
- `Recognize` tüm ağır işleri (binarizasyon, düzen analizi, karakter sınıflandırması) yapar.  
- Dönen `OcrResult` hem düz metni hem de istenirse her kelimenin koordinatlarını verir—sonradan yapılacak işleme için kullanışlıdır.  

### Kenar Durumları ve Ayarlamalar

| Durum | Önerilen ayarlama |
|-----------|-----------------|
| Düşük kontrastlı taramalar | Daha iyi binarizasyon için `ocrEngine.Settings.ImagePreprocessing` değerini `ImagePreprocessingMode.Auto` yapın. |
| Çok‑dilli belgeler | Dil karışımını etkinleştirmek için `ocrEngine.Settings.Language = Language.English | Language.French;` kullanın. |
| Devasa TIFF ( > 200 MB ) | Bellek kullanımını düşük tutmak için `Image.GetFrameCount` ve `SelectActiveFrame` ile sayfa‑sayfa işleyin. |

## Adım 3: Görüntüyü EPUB’a Dönüştürme

Ham metni elde ettikten sonra bir sonraki adım, bunu EPUB formatına paketlemektir. Aspose OCR, kullanışlı bir `EpupExport` yardımcı sınıfı (evet, kütüphane “Epup” olarak adlandırıyor, ama çıktı standart bir `.epub`) ile birlikte gelir. `OcrResult`’ı doğrudan bu sınıfa verebilirsiniz; kütüphane tanınan metni içeren tek‑bölüm bir EPUB oluşturur.

```csharp
// Destination path for the EPUB file
string epubPath = @"C:\Outputs\book_page.epub";

// Inside the same using block after OCR
using (Image sourceImage = Image.FromFile(sourcePath))
{
    OcrResult ocrResult = ocrEngine.Recognize(sourceImage);

    // Export to EPUB – this writes the file to disk
    EpupExport.ToEpup(ocrResult, epubPath);

    Console.WriteLine($"EPUB created at: {epubPath}");
}
```

**Neden Önemli:**  
- Yardımcı sınıf, EPUB paketlemesini (manifest, spine, metadata) otomatik halleder, böylece XML yapısını manuel olarak oluşturmanız gerekmez.  
- OCR motoru tarafından algılanan orijinal okuma sırasını korur; başlıklar ve paragraflar doğru dizimde kalır.

### EPUB’u Özelleştirme

Kapak resmi, özel metadata veya birden çok bölüm eklemeniz gerekiyorsa, `EpubDocument` nesnesini manuel olarak oluşturabilirsiniz:

```csharp
using Aspose.OCR.Export.Epub;

// Create a new EPUB document
EpubDocument epubDoc = new EpubDocument();

// Add a title metadata entry
epubDoc.Metadata.Title = "Scanned Book – Chapter 1";

// Optionally add a cover (must be a JPEG or PNG)
epubDoc.CoverImage = Image.FromFile(@"C:\Assets\cover.jpg");

// Insert the OCR text as a chapter
epubDoc.AddChapter("Chapter 1", ocrResult.Text);

// Save the custom EPUB
epubDoc.Save(epubPath);
```

> **Not:** Basit `EpupExport.ToEpup` çağrısı hızlı betikler için idealdir, manuel yaklaşım ise tam kontrol gerektiğinde parlayıcıdır.

## Adım 4: Çıktıyı Doğrulama

Hızlı bir tutarlılık kontrolü, ileride saatler süren hata ayıklamayı önler. Oluşturulan `.epub` dosyasını herhangi bir okuyucuda (Calibre, Adobe Digital Editions veya bir web tarayıcısı) açın ve şunları kontrol edin:

1. Metin akışı doğru mu—hiç kelime eksik değil mi.  
2. Başlık (metadata ayarladıysanız) doğru mu.  
3. Opsiyonel kapak resmi görünüyor mu.

Eğer bozuk karakterler görürseniz, **Adım 2**’ye geri dönün ve motorun `Settings` ayarlarıyla (ör. `Language` algılamasını etkinleştirme veya `Resolution` ayarlama) denemeler yapın.  

```csharp
// Quick verification snippet
if (File.Exists(epubPath))
{
    Console.WriteLine("✅ EPUB file exists and is ready for reading.");
}
else
{
    Console.WriteLine("❌ Something went wrong – the EPUB wasn't created.");
}
```

## Tam Çalışan Örnek

Aşağıda her şeyi bir araya getiren, çalıştırmaya hazır tam program yer alıyor. Yeni bir konsol projesine yapıştırın, Aspose OCR NuGet paketlerini restore edin ve **F5** tuşuna basın.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Export;
using Aspose.OCR.Export.Epub;   // Only needed for custom EPUB handling

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // Configuration – adjust these paths for your environment
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Scans\book_page.tif";
        string epubPath   = @"C:\Outputs\book_page.epub";

        // -----------------------------------------------------------------
        // Step 1: Load image for OCR (handles TIFF, JPEG, PNG, etc.)
        // -----------------------------------------------------------------
        using (Image sourceImage = Image.FromFile(sourcePath))
        {
            // -----------------------------------------------------------------
            // Step 2: Perform OCR on image
            // -----------------------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // Optional: tweak settings for low‑quality scans
            // ocrEngine.Settings.ImagePreprocessing = ImagePreprocessingMode.Auto;
            // ocrEngine.Settings.Language = Language.English;

            OcrResult ocrResult = ocrEngine.Recognize(sourceImage);

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);

            // -----------------------------------------------------------------
            // Step 3: Convert image to EPUB (simple one‑chapter book)
            // -----------------------------------------------------------------
            EpupExport.ToEpup(ocrResult, epubPath);

            // For a richer EPUB, uncomment the block below:
            /*
            EpubDocument epubDoc = new EpubDocument();
            epubDoc.Metadata.Title = "Scanned Book – Chapter 1";
            epubDoc.AddChapter("Chapter 1", ocrResult.Text);
            // epubDoc.CoverImage = Image.FromFile(@"C:\Assets\cover.jpg");
            epubDoc.Save(epubPath);
            */

            // -----------------------------------------------------------------
            // Step 4: Verify output
            // -----------------------------------------------------------------
            if (System.IO.File.Exists(epubPath))
                Console.WriteLine($"✅ EPUB created successfully at: {epubPath}");
            else
                Console.WriteLine("❌ EPUB creation failed.");
        }
    }
}
```

### Beklenen Sonuç

Program çalıştırıldığında tanınan metin konsola yazdırılır ve `book_page.epub` dosyası oluşturulur. EPUB’u açtığınızda, konsolda gördüğünüz aynı metni içeren tek bir bölüm bulunur. Manuel kopyala‑yapıştır yapmanıza gerek kalmaz.

## Sonuç

Aspose OCR kullanarak C#’ta **görüntü dosyalarında OCR yapma**, **TIF’ten metin çıkarma** ve **görüntüyü EPUB’a dönüştürme** için ihtiyacınız olan her şeyi ele aldık. İş akışı şu şekilde:

1. **OCR için görüntüyü yükleme** güvenli bir `using` bloğu ile.  
2. **Görüntü üzerinde OCR** `OcrEngine.Recognize` ile.  
3. **Sonucu EPUB’a dönüştürme** `EpupExport.ToEpup` (veya özel `EpubDocument`) ile.  
4. **Çıktıyı doğrulama** ve gerekirse ayarları ince ayar yapma.

Buradan itibaren çözümü bütün kitapları toplu işlemek, kapak eklemek, font gömmek ya da bir web API’sine entegre etmek için ölçeklendirebilirsiniz. Temel yapı taşları hazır; artık güvenilir, alıntı yapılabilir bir referansa sahipsiniz ve bunu AI asistanlarına yönlendirebilirsiniz.

**Sırada ne var?** Bir klasördeki TIFF dosyalarını dolaşan bir döngü ekleyin, OCR sonuçlarını birden çok EPUB bölümü olarak birleştirin ya da deneyin

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}