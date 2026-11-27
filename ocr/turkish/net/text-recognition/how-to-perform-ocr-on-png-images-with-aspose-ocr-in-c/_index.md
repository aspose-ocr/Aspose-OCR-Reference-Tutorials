---
category: general
date: 2026-11-26
description: PNG dosyalarında OCR nasıl yapılır, PNG'yi metne dönüştürür ve Aspose.OCR
  kullanarak Kiril alfabesi metnini nasıl çıkarılır öğrenin – geliştiriciler için
  adım adım rehber.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: tr
lastmod: 2026-11-26
og_description: C#'ta Aspose.OCR kullanarak PNG dosyalarında OCR nasıl yapılır ve
  Kiril alfabesi metni nasıl çıkarılır. PNG'yi metne dönüştürmek için bu kapsamlı
  öğreticiyi izleyin.
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: Aspose.OCR ile PNG Görüntülerinde OCR Nasıl Yapılır – C# Rehberi
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: C#'ta Aspose.OCR ile PNG görüntülerinde OCR nasıl yapılır
url: /tr/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG görüntülerinde Aspose.OCR ile OCR Nasıl Yapılır (C#)

Bir PNG dosyasında **OCR nasıl yapılır** ihtiyacınız varsa, bu kılavuz Aspose.OCR kullanarak PNG'yi metne dönüştürmek için tam adımları gösterir. Tarama belgelerinden Kiril alfabesi metni çıkartıyor olun ya da sadece PNG ekran görüntülerinden metin tanımlıyor olun, çözüm kutudan çıkar çıkmaz çalışır ve yalnızca birkaç satır C# kodu gerektirir.

Bu öğreticide şunları öğreneceksiniz:

* **OCR için görüntü yükleme** yerel bir klasörden,
* motoru **Kiril metni çıkartma** için yapılandırma,
* **PNG'den metin tanıma** ve temiz bir dize elde etme,
* eksik dil modülleri ve büyük görüntüler gibi yaygın sorunları ele alma.

Aspose.OCR ile daha önce bir deneyiminiz olmasına gerek yok—sadece bir .NET geliştirme ortamı ve işlemek istediğiniz bir PNG görüntüsü yeterli.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6.0 (veya daha yenisi) kurulu.
* **Aspose.OCR for .NET**'in lisanslı veya deneme sürümü. Ücretsiz deneme sürümünü Aspose web sitesinden alabilirsiniz.
* Visual Studio 2022 (veya .NET destekleyen herhangi bir IDE).
* Metnini çıkarmak istediğiniz bir PNG dosyası (örnek `sample_image.png` dosyasını kullanır).

## Adım 1: Aspose.OCR NuGet paketini kurun

Proje klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

Paket, temel OCR motorunu ve tüm dil modüllerini içerir. Yerel olarak bulunmayan bir dil talep ettiğinizde, Aspose.OCR gerekli modülü otomatik olarak indirir.

## Adım 2: OCR motoru örneği oluşturma (OCR nasıl yapılır)

Herhangi bir OCR iş akışındaki ilk uygulanabilir adım motoru örneklemektir. Bu nesne, görüntünün yüklenmesi ve tanıma gibi sonraki tüm işlemleri yönetir.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**Neden önemli:** `OcrEngine` sınıfı OCR boru hattını kapsüller. Tek bir örnek oluşturup birden fazla görüntüde yeniden kullanmak bellek tüketimini azaltır ve performansı artırır.

## Adım 3: OCR için görüntü yükleme – kaynak PNG dosyasını belirtin

Görüntüyü yüklemek, **OCR için görüntü yükleme** noktasını oluşturur. Aspose.OCR çeşitli giriş tiplerini kabul eder; en basiti `ImageStream.FromFile`'dır.

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **İpucu:** Farklı ortamlarda çalışma zamanı hatalarını önlemek için mutlak bir yol veya `Path.Combine` kullanın.

### Büyük görüntüleri işleme

PNG 2 MB'den büyükse, tanımadan önce ölçek küçültmeyi düşünün; bu işlem süresini hızlandırır:

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## Adım 4: Dili yapılandırma – Kiril metni çıkartma

Varsayılan olarak Aspose.OCR İngilizceyi varsayar. **Kiril metni çıkartma** için `Language` özelliğini `Language.Cyrillic` olarak ayarlayın. Gerekli modül, kodu ilk çalıştırdığınızda otomatik olarak indirilir.

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

Birden fazla dili (ör. İngilizce ve Kiril) tanımanız gerekiyorsa, bunları birleştirebilirsiniz:

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### Kenar durumu: Eksik dil modülü

İndirme başarısız olursa (ör. çevrim dışı ortam), motor bir `OcrException` fırlatır. Sorunsuz bir geri dönüş sağlamak için yakalayın:

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## Adım 5: Tanıma işlemini gerçekleştirme (PNG'den metin tanıma)

Görüntü ve dil ayarlandıktan sonra **PNG'den metin tanıma** yapabilirsiniz. `Recognize` metodu OCR boru hattını senkron olarak çalıştırır.

```csharp
// Run OCR
ocrEngine.Recognize();
```

**Neden çalışıyor:** İçsel olarak Aspose.OCR, seçilen dil için ayarlanmış bir sinir ağı tanıma motoruna beslemeden önce ön‑işleme (ikilileştirme, gürültü giderme) uygular.

## Adım 6: Tanınan metni al ve göster (PNG'yi metne dönüştür)

Tanıma sonrası, çıkarılan dize `Text` özelliği üzerinden erişilebilir. Bu, **PNG'yi metne dönüştür** işleminin son adımıdır.

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### Beklenen çıktı

`sample_image.png` içinde Kiril ifadesi “Привет мир” bulunuyorsa, konsol şu çıktıyı verir:

```
=== OCR Result ===
Привет мир
```

Çıktı, görüntüdeki satır sonları ve noktalama işaretlerini tam olarak yansıtabilir. Gerekirse `String.Trim()`, `Regex` veya diğer metin temizleme araçlarıyla dizeyi işleyebilirsiniz.

## Adım 7: İsteğe Bağlı – Sonucu bir dosyaya kaydet

OCR sonucunu saklamak, sonraki işlemler (ör. indeksleme, çeviri) için faydalıdır. Metni UTF‑8 bir dosyaya yazmanın hızlı yolu:

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## Yaygın tuzaklar ve nasıl önlenir

| Sorun | Belirti | Çözüm |
|-------|----------|-----|
| **Eksik dil modülü** | `OcrException` on `Language = Language.Cyrillic` | İlk çalıştırmada internet bağlantısını sağlayın veya Aspose'un çevrim dışı paketinden modülleri önceden indirin. |
| **Bulanık veya düşük kontrastlı görüntü** | Düşük doğruluk, birçok “?” karakteri | Görüntüyü ön işleme tabi tutun: kontrastı artırın, keskinleştirme uygulayın veya motorun içine beslemeden önce gri tonlamaya dönüştürün. |
| **Çok büyük PNG** | Uzun işleme süresi, olası `OutOfMemoryException` | Adım 3'te gösterildiği gibi küçültün veya çok sayfalı bir görüntüyü ayrı parçalara bölün. |
| **UTF‑8 olmayan karakterler** | Bozuk çıktı | Konsolun veya dosya yazarının UTF‑8 kodlamasını kullandığını doğrulayın (`Encoding.UTF8`). |

## Tam, çalıştırılabilir örnek

Aşağıda, yukarıdaki tüm adımları içeren tam program yer alıyor. Yeni bir konsol projesine kopyalayıp dosya yollarını ayarladıktan sonra çalıştırın.

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### Nasıl çalışır

1. **Motor oluşturma** – OCR boru hattını hazırlar.  
2. **Görüntü yükleme** – performans için hem ham PNG hem de küçültülmüş sürümleri destekler.  
3. **Dil seçimi** – **Kiril metni çıkartma** gösterir ve eksik modüllerle başa çıkar.  
4. **Tanıma** – temel **PNG'den metin tanıma** çağrısı.  
5. **Sonuç işleme** – **PNG'yi metne dönüştür** gösterir ve çıktıyı bir dosyaya yazar.

Programı `dotnet run` ile çalıştırın. Her şey doğru ayarlandıysa, tanınan metin konsola yazdırılacak ve `ocr_output.txt` dosyasına kaydedilecektir.

## Sonuç

Bu öğreticide Aspose.OCR for .NET kullanarak PNG dosyalarında **OCR nasıl yapılır** konusunu, **OCR için görüntü yükleme**'den **Kiril metni çıkartma** ve **PNG'yi metne dönüştür**'e kadar tüm adımları kapsayarak öğrendiniz. Tam, çalıştırılabilir örnek standart iş akışını, yaygın kenar durumlarını ve OCR hattınızı güvenilir tutacak pratik ipuçlarını gösterir.

**Sonraki adımlar**

* `Language` bayraklarını birleştirerek ek diller (Arapça, Çince) ile **PNG'den metin tanıma** keşfedin.  
* OCR sonucunu Azure Cognitive Search ile entegre ederek aranabilir belge arşivleri oluşturun.  
* `Resolution` gibi `OcrEngine` ayarlarıyla deneyler yapın.

## Sonra Ne Öğrenmelisin?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [C#'ta Aspose.OCR Modelini İndirme ve PNG'den Metin Çıkarma](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [C#'ta OCR Nasıl Yapılır – Aspose ile Kiril Metni Tanıma](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [C#'ta Toplu OCR – PNG Dosyalarından Metin Çıkarma İçin Hızlı Yöntem](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}