---
category: general
date: 2025-12-30
description: Aspose OCR kullanarak C#'de resmi PDF'ye dönüştürün. OCR için resmi nasıl
  ön işleme yapacağınızı, Korece metin içeren resmi nasıl tanıyacağınızı ve hızlıca
  aranabilir PDF resmi oluşturacağınızı öğrenin.
draft: false
keywords:
- convert image to pdf
- preprocess image for ocr
- recognize korean text image
- create searchable pdf image
language: tr
og_description: Aspose OCR ile görüntüyü PDF'ye dönüştürün. Bu öğreticide, OCR için
  görüntünün ön işlenmesi, Korece metin görüntüsünün tanınması ve aranabilir PDF görüntüsü
  oluşturulması gösterilmektedir.
og_title: C#'ta Görüntüyü PDF'ye Dönüştür – Tam OCR Kılavuzu
tags:
- C#
- OCR
- Aspose
- PDF
title: C#'de Görüntüyü PDF'ye Dönüştür – Tam OCR Rehberi
url: /tr/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Görüntüyü PDF'ye Dönüştür – Tam OCR Rehberi

Hiç **convert image to PDF** istediğinizde, içindeki metnin aranabilir olmasını da ister misiniz? Tek başınıza değilsiniz. Birçok geliştirici, özellikle Korece yazılmış taranmış sayfalarla çalışırken aynı duvara çarpıyor. İyi haber şu ki, Aspose OCR ile **preprocess image for OCR**, **recognize Korean text image**, ve sonunda **create searchable PDF image** sadece birkaç satırda yapabilirsiniz.

Bu öğreticide tüm işlem hattını adım adım inceleyeceğiz—Korece bir kitap sayfasının ham JPEG'ini yüklemekten, temizlemeye, metni çıkarmaya ve her şeyi aranabilir bir PDF olarak paketlemeye kadar. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz, çalıştırmaya hazır bir C# konsol uygulamanız olacak.

## İhtiyacınız Olanlar

- **.NET 6.0 veya üzeri** (kod .NET Core ve .NET Framework'te de çalışır)  
- **Aspose.OCR for .NET** NuGet paketi (`Aspose.OCR`) – ücretsiz deneme anahtarları Aspose sitesinde mevcuttur.  
- Korece metin içeren bir örnek görüntü (ör. `korean_book_page.jpg`).  
- Tercih ettiğiniz bir geliştirme ortamı (Visual Studio, VS Code, Rider – ben VS 2022 kullanıyorum).

> **Pro ipucu:** Görüntü dosyalarınızı `Resources/` gibi ayrı bir klasörde tutun, böylece yol makineler arasında tutarlı kalır.

## Sürecin Genel Görünümü

1. **Initialize the OCR engine** ile hız için GPU desteği.  
2. **Add preprocessing filters** (deskew, denoise) tanıma doğruluğunu artırmak için.  
3. **Download and load the Korean language model** – gerekirse Aspose bunu otomatik olarak yapar.  
4. **Run the recognition** giriş görüntüsü üzerinde.  
5. **Export the result as a searchable PDF** yerleşik dışa aktarıcıyı kullanarak.  
6. **Optional, serialize the result to JSON** daha fazla analiz veya günlükleme için.

Aşağıda her adımı ayrıntılı olarak inceleyecek, *neden* önemli olduğunu açıklayacak ve kopyalayıp‑yapıştırabileceğiniz tam kodu vereceğiz.

---

## ## Görüntüyü PDF'ye Dönüştür – Tam İş Akışı

Aşağıdaki kod parçacığı *tam* programdır. Yeni bir konsol projesi (`dotnet new console -n OcrPdfDemo`) oluşturup, otomatik oluşturulan `Program.cs` dosyasını bu kodla değiştirmekten çekinmeyin.

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

- **GPU acceleration** tanıma süresini CPU‑only moda göre yaklaşık yarıya indirir.  
- **Deskew** ve **Denoise**, klasik *preprocess image for OCR* teknikleridir; tarama hatalarını düzelterek motorun karakterleri kaçırmasını önler.  
- **Language model loading** **recognize Korean text image** için kritiktir – Korece model olmadan motor genel bir Latin alfabesine geri döner ve anlamsız sonuçlar üretir.  
- **SearchablePdfExporter**, orijinal bitmap'i ve görünmez bir metin katmanını birleştirerek size **create searchable pdf image** sonucunu verir; bu sonuç herhangi bir PDF görüntüleyicide indekslenebilir.

---

## ## OCR için Görüntü Ön İşleme – İpuçları ve Püf Noktaları

Eklediğimiz iki filtre genellikle yeterli olsa da, inatçı görüntülerle karşılaşabilirsiniz. İşte deneyebileceğiniz birkaç ekstra adım:

| Sorun | Ek Filtre | Nasıl Ekleilir |
|-------|-------------------|------------|
| Düşük kontrast | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Yoğun arka plan gürültüsü | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Karışık yön (dikey & yatay) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Not:** Çok fazla filtre eklemek işleme süresini yavaşlatabilir. Ölçeklendirmeden önce her değişikliği tek bir sayfada test edin.

---

## ## Korece Metin Görüntüsü Tanıma – Yaygın Tuzaklar

Kore alfabesi, görsel olarak yoğun Hangul heceleri içerir. Bozuk çıktı fark ederseniz:

1. **Ensure the language model is fully downloaded** – konsolda “Downloading Korean model…” gibi bir mesajı kontrol edin.  
2. **Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated beyond 12°.  
3. **Boost GPU memory** `ocrEngine.GpuMemoryLimit = 2048;` ayarlayarak (MB cinsinden).  

Bu ayarlamalar **recognize Korean text image** başarısını doğrudan etkiler.

---

## ## Aranabilir PDF Görüntüsü Oluştur – Sonucu Doğrulama

Program tamamlandıktan sonra, `korean_page.pdf` dosyasını herhangi bir PDF okuyucusunda (Adobe Acrobat Reader, Foxit, hatta Chrome) açın. Şunları yapabilmelisiniz:

- **Select text** fareyle tıklayarak, sanki yerel bir PDFmiş gibi seçebilmelisiniz.  
- **Search** yerleşik arama kutusunu kullanarak Korece kelimeleri arayabilmelisiniz.

Metin katmanı boş görünüyorsa, `Export` metodunun doğru görüntü yolunu aldığını ve OCR sonucunun boş olmayan `RecognitionResult.Text` içerdiğini bir kez daha kontrol edin.

---

## ## Tam JSON Çıktısı – Ne Beklenir

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

---

## ## Sorun Giderme & SSS

**S: PDF'im orijinal görüntüye göre çok büyük.**  
C: Dışa aktarıcı, orijinal bitmap'i yerel çözünürlüğünde gömer. Boyut bir sorun ise, tanıma *öncesinde* görüntüyü küçültün:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**S: OCR boş stringler döndürüyor.**  
C: Görüntü yolunun doğru olduğunu ve dosyanın bozulmadığını doğrulayın. Ayrıca GPU sürücüsünün güncel olduğundan emin olun; eski sürücüler sessiz hatalara yol açabilir.

**S: Bir döngüde birden fazla sayfa işleyebilir miyim?**  
C: Kesinlikle. 4‑6 adımlarını `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` döngüsü içinde sarın ve çıktı PDF yolunu buna göre değiştirin.

---

## ## Sonuç

Az önce **convert image to PDF** yaparak aranabilir metni koruduk, hepsi Aspose OCR’ın güçlü işlem hattı sayesinde. **preprocess image for OCR** yaparak doğruluğu artırırsınız; **recognize Korean text image** ile karmaşık yazı sistemlerini işlersiniz; ve **create searchable pdf image** ile taşınabilir, indekslenebilir bir belge elde edersiniz.

Kodu alın, kendi taramalarınıza yönlendirin ve ek filtreler ya da dil modelleriyle deneyler yapın. Aynı desen Çince, Japonca veya herhangi bir Latin temelli dil için de çalışır—sadece `LanguageModel.Korean` ifadesini uygun enum ile değiştirin.

Daha fazla sorunuz mu var? Yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}