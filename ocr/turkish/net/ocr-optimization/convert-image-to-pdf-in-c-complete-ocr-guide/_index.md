---
category: general
date: 2026-09-13
description: Aspose OCR kullanarak C#'de taranmış bir sayfayı PDF'ye dönüştürmeyi
  öğrenin. Bu rehber, ön işleme, Korece metin tanıma ve aranabilir bir PDF oluşturmayı
  gösterir.
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: Aspose OCR ile C#'de taranmış bir sayfayı PDF'ye dönüştürmeyi öğrenin.
  Eğitim, görüntü ön işleme, Korece metin için GPU hızlandırmalı OCR ve birkaç dakika
  içinde aranabilir bir PDF oluşturmayı kapsar.
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: C# ile OCR kullanarak taranmış bir sayfayı PDF'ye dönüştürme
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: C# ile OCR kullanarak taranmış bir sayfayı PDF'ye dönüştürme
url: /tr/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile OCR Kullanarak Tarama Sayfasını PDF'e Dönüştürme

Eğer metni aranabilir tutarak **tarama sayfasını PDF'e dönüştürmek** istiyorsanız, doğru yerdesiniz. Bu öğretici, Aspose OCR kullanarak **preprocess image for OCR**, **recognize Korean text image** ve sonunda **create searchable PDF image** işlemlerini basit bir C# konsol uygulamasıyla nasıl yapacağınızı adım adım gösterir.

## Hızlı Yanıtlar
- **OCR işlemini hangi kütüphane yönetir?** Aspose.OCR for .NET  
- **GPU'yu kullanabilir miyim?** Evet – GPU hızlandırmasını etkinleştirerek işlem süresini 2×'ye kadar artırabilirsiniz  
- **Korece dil paketine ihtiyacım var mı?** İlk kullanımda otomatik olarak indirilir  
- **Çıktı aranabilir olacak mı?** Oluşturulan PDF, görünmez bir metin katmanı içerir  
- **Hangi .NET sürümleri destekleniyor?** .NET 6.0 ve sonrası (.NET Core ve .NET Framework dahil)

## Gereksinimler
- **.NET 6.0 or later** – .NET Core, .NET Framework ve .NET 5/6+ üzerinde çalışır  
- **Aspose.OCR for .NET** NuGet paketi (`Aspose.OCR`) – deneme anahtarları Aspose sitesinde ücretsizdir  
- Korece karakterler içeren bir örnek görüntü, ör. `korean_book_page.jpg`  
- Favori IDE'niz (Visual Studio 2022, VS Code, Rider, vb.)

> **Pro tip:** Görüntüleri `Resources/` klasöründe saklayın, böylece yollar makineler arasında tutarlı kalır.

## İşlemin Genel Görünümü
1. OCR motorunu GPU desteğiyle başlatın.  
2. **preprocess image for OCR** filtrelerini, örneğin deskew ve denoise, ekleyin.  
3. Korece dil modelini indirin ve yükleyin (otomatik olarak işlenir).  
4. Görüntü üzerinde OCR çalıştırın.  
5. Sonucu **SearchablePdfExporter** ile **create searchable PDF image** oluşturmak için dışa aktarın.  
6. (İsteğe bağlı) OCR çıktısını JSON'a serileştirerek sonraki işlem hatları için kullanın.  

Aşağıda her adımı genişletiyoruz, *neden* önemli olduğunu açıklıyoruz ve kopyalayıp yapıştırabileceğiniz tam kodu veriyoruz.

## Tarama Sayfasını PDF'e Dönüştürme Nasıl Çalışır?
`OcrEngine`, Aspose.OCR içinde görüntüler üzerinde optik karakter tanıma yapan ana sınıftır.  
`SearchablePdfExporter`, orijinal görüntüyü ve arama için görünmez bir metin katmanı içeren bir PDF oluşturur.  
`RecognitionResult`, OCR motoru tarafından döndürülen metin ve güven puanı verilerini tutar.

Resminizi `new OcrEngine()` ile yükleyin ve `engine.Recognize("korean_book_page.jpg")` çağrısını yapın, ardından `RecognitionResult`'ı `SearchablePdfExporter.Export`'a geçirin. Bu iki adımlı akış bitmap'i okur, Unicode metni çıkarır ve ikisini tek bir PDF'e gömer; metin katmanı görünmez ama aranabilir. GPU hızlandırması tanıma süresini yaklaşık yarıya indirir, deskew ve denoise filtreleri ise gürültülü taramalarda doğruluğu %15'e kadar artırır.

## Görüntüyü PDF'e Dönüştür – Tam İş Akışı
Aşağıdaki kod parçacığı *tam* programdır. Yeni bir konsol projesi oluşturun (`dotnet new console -n OcrPdfDemo`) ve otomatik oluşturulan `Program.cs` dosyasını yer tutucuda gösterilen kodla değiştirin.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### Neden Bu Çalışıyor
- **GPU acceleration** CPU‑only moda göre tanıma süresini yaklaşık yarıya indirir.  
- **Deskew** ve **Denoise**, klasik *preprocess image for OCR* teknikleridir; motorun karakterleri kaçırmasına neden olan yaygın tarama kusurlarını düzeltir.  
- **Language model loading**, **recognize Korean text image** için esastır – Korece model olmadan motor genel bir Latin alfabesine geri döner ve anlamsız sonuç üretir.  
- **SearchablePdfExporter**, orijinal bitmap'i ve görünmez bir metin katmanını birleştirir, size **create searchable pdf image** sonucunu verir ve bu sonucu herhangi bir PDF görüntüleyicide indeksleyebilirsiniz.

## Neden Bu Çalışıyor
- **GPU acceleration** CPU‑only moda göre tanıma süresini yaklaşık yarıya indirir.  
- **Deskew** ve **Denoise**, klasik *preprocess image for OCR* teknikleridir; motorun karakterleri kaçırmasına neden olan yaygın tarama kusurlarını düzeltir.  
- **Language model loading**, **recognize Korean text image** için esastır – Korece model olmadan motor genel bir Latin alfabesine geri döner ve anlamsız sonuç üretir.  
- **SearchablePdfExporter**, orijinal bitmap'i ve görünmez bir metin katmanını birleştirir, size **create searchable pdf image** sonucunu verir ve bu sonucu herhangi bir PDF görüntüleyicide indeksleyebilirsiniz.

## OCR İçin Görüntü Ön İşleme – İpuçları ve Püf Noktaları
`DeskewFilter`, taranan sayfaların dönüşünü düzeltir.  
`ContrastFilter`, OCR doğruluğunu artırmak için görüntü kontrastını ayarlar.  
`BinarizationFilter`, eşik değerine göre görüntüyü siyah‑beyaz yapar, arka plan gürültüsünü azaltır.  
`OrientationFilter`, karışık portre/landscape sayfaları algılar ve düzeltir.  

| Sorun | Ek filtre | Nasıl eklenir |
|-------|-----------|----------------|
| Low contrast | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Heavy background noise | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Mixed orientation (portrait & landscape) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Not:** Çok fazla filtre eklemek işlem süresini yavaşlatabilir. Ölçeklendirmeden önce her değişikliği tek bir sayfada test edin.

## Korece Metin Görüntüsü Tanıma – Yaygın Tuzaklar
Korece yazı sistemleri, görsel olarak yoğun Hangul hecelerine sahiptir. Eğer bozuk çıktı görürseniz:
1. **Dil modelinin tamamen indirildiğinden emin olun** – konsolda “Downloading Korean model…” gibi bir mesajı kontrol edin.  
2. `DeskewFilter` içinde **`MaxAngle` değerini artırın** eğer taramalarınız 12°'den fazla döndürülmüşse.  
3. `ocrEngine.GpuMemoryLimit = 2048;` ayarlayarak **GPU belleğini artırın** (değer MB cinsindendir).  

`LanguageModel.Korean`, OCR için Korece dil verilerini yükler ve doğru Hangul tanımasını sağlar.  

Bu ayarlamalar, **recognize Korean text image** başarısını doğrudan etkiler.

## Aranabilir PDF Görüntüsü Oluştur – Sonucu Doğrulama
Program tamamlandıktan sonra, `korean_page.pdf` dosyasını herhangi bir PDF okuyucusunda (Adobe Acrobat Reader, Foxit, hatta Chrome) açın. Şunları yapabilmelisiniz:
- **Metni seçin** fareyle, sanki yerel bir PDF gibi.  
- **Arama** yapın Korece kelimeler için yerleşik arama kutusunu kullanarak.  

Eğer metin katmanı boş görünüyorsa, `Export` metodunun doğru görüntü yolunu aldığını ve OCR sonucunun boş olmayan `RecognitionResult.Text` içerdiğini iki kez kontrol edin.

## Tam JSON Çıktısı – Ne Beklenir
Konsol, güzel biçimlendirilmiş bir JSON yükü yazdırır. Kısaltılmış bir örnek şu şekildedir:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

## Sorun Giderme & SSS
**Q: PDF'im orijinal görüntüye göre çok büyük.**  
A: Dışa aktarıcı, orijinal bitmap'i yerel çözünürlüğünde gömer. Boyut bir sorun ise, tanımadan *önce* görüntüyü küçültün:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: OCR boş stringler döndürüyor.**  
A: Görüntü yolunun doğru olduğunu ve dosyanın bozulmadığını doğrulayın. Ayrıca, GPU sürücüsünün güncel olduğundan emin olun; eski sürücüler sessiz hatalara neden olabilir.

**Q: Bir döngüde birden fazla sayfayı işleyebilir miyim?**  
A: Kesinlikle. 4‑6 adımlarını `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` döngüsü içinde sarın ve çıktı PDF yolunu buna göre değiştirin.

## Sonuç
Az önce **image to PDF**'yi aranabilir metni koruyarak dönüştürdük, bu tamamen Aspose OCR'nin güçlü işlem hattı sayesinde. **preprocess image for OCR** yaparak doğruluğu artırırsınız; **recognize Korean text image** ile karmaşık yazı sistemlerini işlersiniz; ve **create searchable pdf image** ile taşınabilir, indekslenebilir bir belge elde edersiniz.

Kodu alın, kendi taramalarınıza yönlendirin ve ek filtreler ya da dil modelleriyle deney yapın. Aynı desen Çince, Japonca veya herhangi bir Latin temelli dil için de çalışır—sadece `LanguageModel.Korean`'ı uygun enum ile değiştirin.

Daha fazla sorunuz mu var? Yorum bırakın, iyi kodlamalar!

---

**Son Güncelleme:** 2026-09-13  
**Test Edilen:** Aspose.OCR 24.11 for .NET  
**Yazar:** Aspose

## İlgili Öğreticiler
- [Tarama Dosyalarından Aranabilir PDF Oluşturma Aspose Ocr Kullanarak](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [OCR Ön İşleme Boru Hattı Görüntüden Metin Tanıma](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [Aspose Ocr ile Görüntüden Metin Tanıma Tam C Rehberi](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}