---
category: general
date: 2026-03-13
description: Aspose OCR kullanarak herhangi bir görüntüden aranabilir PDF oluşturun.
  Görüntüyü EPUB’a dönüştürmeyi, aranabilir metin eklemeyi ve C#’ta aranabilir PDF
  üretmeyi öğrenin.
draft: false
keywords:
- create searchable pdf
- convert image to epub
- ocr image to pdf
- add searchable text
- generate searchable pdf
language: tr
og_description: Aspose OCR kullanarak herhangi bir görüntüden aranabilir PDF oluşturun.
  Bu kılavuz, görüntüyü EPUB'a dönüştürmeyi, aranabilir metin eklemeyi ve C#'ta aranabilir
  PDF oluşturmayı gösterir.
og_title: Aranabilir PDF Oluştur – Görüntüyü EPUB'a Dönüştür ve Metin Ekle
tags:
- Aspose OCR
- C#
- PDF
- EPUB
title: Aranabilir PDF Oluştur – Görüntüyü EPUB'a Dönüştür ve Metin Ekle
url: /tr/net/text-recognition/create-searchable-pdf-convert-image-to-epub-add-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aranabilir PDF Oluştur – Görüntüyü EPUB’a Dönüştür ve Metin Ekle

Tarayıcıdan alınmış bir makbuz ya da herhangi bir görüntüden **aranabilir PDF** oluşturmak ister misiniz? Bu öğreticide, Aspose OCR kullanarak nasıl aranabilir PDF oluşturacağınızı, aynı zamanda **görüntüyü EPUB’a dönüştüreceğinizi** ve **aranabilir metin** katmanları ekleyeceğinizi tek bir C# projesinde göstereceğiz.  

Görünüşte güzel ama aranamayan PDF'lerle hiç zorlandınız mı, yalnız değilsiniz. İyi haber, gizli bir metin katmanı düz bir görüntüyü tamamen aranabilir bir belgeye dönüştürebilir ve Aspose bunu neredeyse ağrısız bir hâle getiriyor.

## Öğrenecekleriniz

* Aspose OCR motorunu başlatmayı ve dili ayarlamayı nasıl yapacağınızı.  
* **Görüntüyü EPUB’a dönüştürmek** için tam adımlar, e‑kitap dağıtımı için.  
* PDF yazarını yapılandırarak çıktının gizli, aranabilir bir metin katmanı içermesini nasıl sağlayacağınızı.  
* Çok sayfalı makbuzlar veya İngilizce dışı diller gibi uç durumları ele almak için ipuçları.  

İhtiyacınız olan tek şey önceden bir .NET geliştirme ortamı (Visual Studio 2022 veya daha yeni) ve bir Aspose OCR NuGet paketidir. Harici hizmetler, karmaşık yapılandırma dosyaları yok—sadece kopyalayıp yapıştırıp çalıştırabileceğiniz sade C#.

## Önkoşullar

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0+   | .NET Standard 2.0+ hedefleyen Aspose OCR, .NET 6 sayesinde en yeni çalışma zamanı iyileştirmelerini sunar. |
| Aspose.OCR NuGet package | Kodda kullanılan `OcrEngine`, `EpubWriter` ve `PdfWriter` sınıflarını sağlar. |
| An image file (e.g., `receipt.jpg`) | OCR çalıştıracağınız kaynak. Herhangi bir raster görüntü (PNG, JPEG, BMP) çalışır. |
| Basic C# knowledge | Kod parçacıklarını okuyacak ve düzenleyeceksiniz, dili sıfırdan öğrenmeyecek. |

Paketi aşağıdaki komutla kurabilirsiniz:

```bash
dotnet add package Aspose.OCR
```

> **Pro ipucu:** Visual Studio kullanıyorsanız, NuGet Package Manager UI aynı işi yapar—sadece “Aspose.OCR” arayın.

## Adım 1 – Aspose OCR ile Aranabilir PDF Oluştur

İlk olarak ihtiyacımız olan, hangi dili tanıyacağını bilen bir `OcrEngine` örneğidir. İngilizce varsayılan dildir, ancak `ocrEngine.Language` ayarını değiştirerek Fransızca, Almanca vb. dillerle değiştirebilirsiniz.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialise the OCR engine and set the language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English          // Change this if your document isn’t English
};
```

İlk önce motoru başlatmak neden önemli? Motor tanıma modelini bellekte tutar, bu yüzden bir kez oluşturup birden çok görüntüde yeniden kullanmak CPU ve RAM tasarrufu sağlar. Daha büyük toplu işlerinizde aynı örneği tüm işlem boyunca canlı tutarsınız.

## Adım 2 – Görüntüyü Yükle ve OCR Uygula

Sonra motoru işlemek istediğimiz dosyaya yönlendiririz. `ImageStream.FromFile` görüntüyü OCR motorunun anlayacağı bir formata okur.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Run the recognition engine – this populates the internal text buffer
ocrEngine.Recognize();
```

> **Görüntü çok sayfalı olsaydı ne olur?**  
> Aspose OCR, çok sayfalı TIFF dosyalarını doğrudan destekler. TIFF dosyasının yolunu verin; motor her sayfayı otomatik olarak döner.

## Adım 3 – Görüntüyü EPUB’a Dönüştür

Tarayıcıdan alınan belgenin bir e‑kitap versiyonuna da ihtiyacınız varsa, Aspose bunu tek satırda yapar. `EpubWriter`, aynı `OcrEngine` örneğini kullanır, yani OCR sonuçları ekstra işlem yapmadan yeniden kullanılır.

```csharp
// Export the recognised content to an ePub file
EpubWriter epubWriter = new EpubWriter();
epubWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt.epub");
```

Neden EPUB’a dışa aktarılıyor? EPUB, yeniden akışa uygun bir formattır—mobil okuyucular için mükemmeldir. OCR metni seçilebilir hâle gelir ve orijinal görüntü arka plan olarak kalır, taramanın görünümünü korur.

## Adım 4 – PDF’e Aranabilir Metin Katmanı Ekle

Şimdi gerçekten **aranabilir PDF oluşturan** kısım geliyor. `AddSearchableTextLayer` etkinleştirilerek PDF yazıcısı OCR çıktısını yansıtan görünmez bir metin katmanı ekler. Kullanıcılar metni yerel bir PDF gibi arayabilir, kopyalayabilir veya vurgulayabilir.

```csharp
// Configure PDF writer to include a hidden searchable text layer
PdfWriter pdfWriter = new PdfWriter
{
    AddSearchableTextLayer = true   // Enables the hidden text layer for searchability
};

// Save the OCR result as a searchable PDF
pdfWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt_searchable.pdf");
```

> **Yaygın tuzak:** `AddSearchableTextLayer` ayarını unutmak, aynı görünüme sahip ama aranabilir metin içermeyen bir PDF oluşturur. Aranabilir bir belgeye ihtiyacınız olduğunda bu bayrağı her zaman iki kez kontrol edin.

## Adım 5 – Tam Çalışan Örnek

Her şeyi bir araya getirerek, yeni bir .NET projesine ekleyebileceğiniz ve hemen çalıştırabileceğiniz bağımsız bir konsol uygulaması burada.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace OcrToPdfAndEpub
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the source image
            string imagePath = "YOUR_DIRECTORY/receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            ocrEngine.Recognize();

            // 4️⃣ Convert to EPUB (optional but handy)
            EpubWriter epubWriter = new EpubWriter();
            string epubPath = "YOUR_DIRECTORY/receipt.epub";
            epubWriter.Save(ocrEngine, epubPath);
            Console.WriteLine($"EPUB saved to {epubPath}");

            // 5️⃣ Create searchable PDF
            PdfWriter pdfWriter = new PdfWriter
            {
                AddSearchableTextLayer = true
            };
            string pdfPath = "YOUR_DIRECTORY/receipt_searchable.pdf";
            pdfWriter.Save(ocrEngine, pdfPath);
            Console.WriteLine($"Searchable PDF saved to {pdfPath}");
        }
    }
}
```

### Beklenen Çıktı

* `receipt.epub` – Calibre, Apple Books veya herhangi bir e‑reader’da açabileceğiniz bir EPUB dosyası.  
* `receipt_searchable.pdf` – **Ctrl + F** tuşlarına basıp orijinal görüntüde yer alan herhangi bir kelimeyi bulabileceğiniz bir PDF.

PDF’i Adobe Acrobat’ta açıp **Dosya → Özellikler → Açıklama** bölümüne bakarsanız, **Yazı Tipleri** sekmesinin altında gizli bir metin akışı göreceksiniz; bu, aranabilir katmanın mevcut olduğunu doğrular.

## Yaygın Sorular & Uç Durumlar

**S: Bu, İngilizce dışı dillerle çalışır mı?**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}