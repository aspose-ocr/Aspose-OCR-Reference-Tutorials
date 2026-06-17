---
category: general
date: 2026-06-06
description: C# OCR kullanarak metin görüntüsünü tanıma – adım adım bir C# OCR örneği,
  taramalardan metin çıkarır ve taramayı dakikalar içinde metne dönüştürür.
draft: false
keywords:
- recognize text image
- c# ocr example
- extract text scan
- convert scan to text
- image to text c#
language: tr
og_description: C# OCR ile metin görüntüsünü tanıyın. Tarama dosyalarından metin çıkaran,
  taramayı metne dönüştüren ve gerçek dünya görüntülerini işleyen pratik bir C# OCR
  örneğini öğrenin.
og_title: C#'de metin görüntüsü tanıma – Tam OCR Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text image using C# OCR – a step‑by‑step c# ocr example that
    extracts text from scans and convert scan to text in minutes.
  headline: recognize text image in C# – Full OCR Guide
  type: TechArticle
- questions:
  - answer: The `Windows.Media.Ocr` namespace is Windows‑only. On Linux or macOS you’d
      swap it for TesseractSharp or IronOcr—both expose a similar `Engine.Recognize`
      method, so the surrounding code stays virtually unchanged.
    question: Does this work on .NET Core on Linux?
  - answer: Handwriting recognition is still experimental. For best results, stick
      to printed fonts or consider a cloud service like Azure Cognitive Services if
      you need high accuracy.
    question: How accurate is the built‑in OCR for handwritten notes?
  - answer: 'Not out of the box. Convert each PDF page to an image first (using `PdfSharp`
      or `Ghostscript`) and then feed the bitmap to the OCR engine. --- ## Conclusion
      You now have a complete, production‑ready **c# ocr example** that can **recognize
      text image** files, **extract text scan** contents, and **co'
    question: Can I process PDFs directly?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: C#'ta metin görüntüsünü tanıma – Tam OCR Rehberi
url: /tr/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta metin görüntüsü tanıma – Tam OCR Öğreticisi

C# kullanarak taranmış bir fotoğraftan doğrudan **metin görüntüsü tanıma** hakkında hiç merak ettiniz mi? Tek başınıza değilsiniz. İster eski makbuzları dijitalleştiriyor olun, ister bir kartvizitten veri çekiyor olun, ya da sadece düşük çözünürlüklü bir taramayı düzenlenebilir metne dönüştürüyor olun, bir görüntüden metin çıkarma yeteneği, her geliştiricinin araç kutusunda bulunması gereken kullanışlı bir hiledir.

Bu rehberde, bir resmi yükleyen, optik karakter tanıma (OCR) çalıştıran ve sonucu konsola yazdıran bir **c# ocr örneği** üzerinden ilerleyeceğiz. Sonuna geldiğinizde **tarama metnini çıkar** dosyalarını, **taramayı metne dönüştür** ve hatta gürültülü görüntüler için süreci ince ayar yapabileceksiniz. Şık üçüncü‑taraf hizmetlere gerek yok—sadece yerleşik Windows.Media.Ocr API'si (veya uyumlu bir OcrEngine) ve birkaç satır kod.

## Öğrenecekleriniz

* C# projesini OCR için nasıl kuracağınızı.
* **metin görüntüsü tanıma** dosyaları için gereken tam kod.
* Düşük çözünürlüklü taramaları ve çok sayfalı belgeleri ele almanın ipuçları.
* Örneği kendi uygulamalarınız için yeniden kullanılabilir bir kütüphane haline getirmenin yolları.

### Önkoşullar

* .NET 6.0 veya daha yenisi (API .NET 5+ üzerinde de çalışır).
* Visual Studio 2022 (Community sürümü yeterli) veya istediğiniz herhangi bir IDE.
* `lowres_scan.jpg` gibi bir örnek görüntü, başvurabileceğiniz bir klasöre yerleştirilmiş.
* async/await konusunda temel bilgi—OCR çağrıları Windows API'sinde eşzamansızdır.

> **Pro tip:** Windows dışı bir platformda iseniz, `Windows.Media.Ocr` ad alanını TesseractSharp gibi çapraz‑platform bir kütüphane ile değiştirin; çevreleyen mantık aynı kalır.

---

## Adım 1: Bir OCR Motoru ile **metin görüntüsü tanıma** için Hazırlık

İlk olarak, bir OCR motoru örneğine ihtiyacımız var. `OcrEngine` sınıfı, herhangi bir **görüntüden metne c#** işleminin giriş noktasıdır.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Create the OCR engine – default language is English.
        OcrEngine engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));
        if (engine == null)
        {
            Console.WriteLine("Failed to create OcrEngine. Make sure you are on Windows 10 version 1809 or later.");
            return;
        }

        // Continue with the rest of the pipeline...
```

**Neden önemli:** Motor, desen tanımanın ağır işini soyutlar. Onu açıkça oluşturarak dil ayarları üzerinde kontrol elde ederiz; bu, daha sonra **tarama metnini çıkar** belgelerini başka dillerde istediğinizde esastır.

## Adım 2: Görüntü Dosyasını Yükleyin – **taramayı metne dönüştür**'ün Temeli

Sonra, görüntüyü diskinizden okur ve OCR motorunun beklediği format olan `SoftwareBitmap`'e dönüştürürüz.

```csharp
        // Load the image file into a SoftwareBitmap.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "lowres_scan.jpg");
        using (FileStream fs = new FileStream(imagePath, FileMode.Open, FileAccess.Read))
        {
            // Decode the image (supports JPEG, PNG, BMP, etc.).
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Optional: upscale low‑resolution images for better accuracy.
            SoftwareBitmap upscaled = SoftwareBitmap.Convert(bitmap, bitmap.BitmapPixelFormat, bitmap.BitmapAlphaMode);
            // Pass the bitmap to OCR.
            await RecognizeAsync(engine, upscaled);
        }
    }
```

**Neden bunu yapıyoruz:** Ham bir dosya akışını doğrudan OCR'a beslemek genellikle düşük çözünürlüklü taramalarda kötü sonuçlar verir. `SoftwareBitmap`'e dönüştürmek, DPI, renk derinliği gibi ayarları manipüle etmemizi ve tanımadan önce filtre uygulamamızı sağlar.

## Adım 3: **metin görüntüsü tanıma** İşlemini Gerçekleştirin

Şimdi nihayet motorun `RecognizeAsync` metodunu çağırıyoruz. İşte sihrin gerçekleştiği yer.

```csharp
    private static async Task RecognizeAsync(OcrEngine engine, SoftwareBitmap bitmap)
    {
        // Run OCR – this returns an OcrResult object.
        OcrResult result = await engine.RecognizeAsync(bitmap);

        // The Result contains a collection of lines and words.
        Console.WriteLine("=== OCR Output ===");
        foreach (var line in result.Lines)
        {
            Console.WriteLine(line.Text);
        }

        // For a quick **image to text c#** check, also output the raw string.
        Console.WriteLine("\nFull Text:\n" + result.Text);
    }
}
```

**Gördükleriniz:** `lowres_scan.jpg` içinde “Hello World” ifadesi varsa, konsol şu çıktıyı verir:

```
=== OCR Output ===
Hello World

Full Text:
Hello World
```

Bu, **c# ocr örneği**'nin tam çalışmasıdır—sadece dört mantıksal adım, ancak dosya yüklemeden son çıktıya kadar her şeyi kapsar.

## Adım 4: Kenar Durumlarını Ele Alma – Tarama Mükemmel Olmadığında

Gerçek dünyadaki görüntüler her zaman net olmayabilir. İşte programı tamamen yeniden yazmadan yapabileceğiniz birkaç ayar:

| Sorun | Hızlı Çözüm |
|-------|-----------|
| **Very low DPI (≤ 72)** | Tanımadan önce `BitmapTransform` kullanarak bitmap'i büyütün. |
| **Skewed text** | Sayfayı düzleştirmek için bir döndürme dönüşümü (`SoftwareBitmap.Rotate`) uygulayın. |
| **Multiple languages** | `OcrEngine.TryCreateFromLanguage(new OcrLanguage("en-fr"))` oluşturun ve `engine.Language`'i buna göre ayarlayın. |
| **Large files** | Görüntüyü parçalar halinde işleyin (`engine.RecognizeAsync(tileBitmap)`) ve sonuçları birleştirin. |

Bu ince ayarlar, **tarama metnini çıkar** rutininizin gürültülü makbuzlarla veya açıyla çekilmiş fotoğraflarla çalışırken bile güvenilir kalmasını sağlar.

## Adım 5: Örneği Yeniden Kullanılabilir Bir Yardımcıya Dönüştürmek (İsteğe Bağlı)

Uygulamanın çeşitli bölümlerinde **taramayı metne dönüştür** planlıyorsanız, mantığı küçük bir yardımcı sınıfa sarın:

```csharp
public static class OcrHelper
{
    private static readonly OcrEngine _engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));

    public static async Task<string> ImageToTextAsync(string filePath)
    {
        using var fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
        var decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
        var bitmap = await decoder.GetSoftwareBitmapAsync();

        var result = await _engine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

Şimdi sadece şu şekilde çağırabilirsiniz:

```csharp
string text = await OcrHelper.ImageToTextAsync("YOUR_DIRECTORY/lowres_scan.jpg");
Console.WriteLine(text);
```

**Neden seveceksiniz:** Yardımcı, OCR altyapısını izole eder, iş mantığına odaklanmanızı sağlar—projeler arasında yeniden kullanılacak bir **c# ocr örneği** için mükemmeldir.

---

![metin görüntüsü tanıma örneği](https://example.com/ocr-demo.png "OCR konsol çıktısının ekran görüntüsü, metin görüntüsü tanıma sonucunu gösteriyor")

*Alt metin:* **metin görüntüsü tanıma** çıktısı, bir C# OCR konsol uygulamasından.

## Sık Sorulan Sorular

**S: Bu .NET Core üzerinde Linux'ta çalışır mı?**  
C: `Windows.Media.Ocr` ad alanı yalnızca Windows içindir. Linux veya macOS'ta TesseractSharp veya IronOcr ile değiştirirsiniz—her ikisi de benzer bir `Engine.Recognize` metodu sunar, bu yüzden çevreleyen kod neredeyse değişmez.

**S: Yerleşik OCR el yazısı notlar için ne kadar doğru?**  
C: El yazısı tanıma hâlâ deneysel bir özelliktir. En iyi sonuçlar için basılı fontları kullanın veya yüksek doğruluk gerekiyorsa Azure Cognitive Services gibi bir bulut hizmetini düşünün.

**S: PDF'leri doğrudan işleyebilir miyim?**  
C: Kutudan çıkar çıkmaz değil. Önce her PDF sayfasını bir görüntüye dönüştürün (`PdfSharp` veya `Ghostscript` kullanarak) ve ardından bitmap'i OCR motoruna besleyin.

## Sonuç

Artık birkaç satır kodla **metin görüntüsü tanıma** dosyalarını, **tarama metnini çıkar** içeriklerini ve **taramayı metne dönüştür** işlemlerini gerçekleştirebilen eksiksiz, üretime hazır bir **c# ocr örneği**'ne sahipsiniz. Akışı—motor oluşturma, görüntü yükleme, eşzamansız tanıma ve sonuç işleme—anlayarak, resimleri aranabilir dizelere dönüştürmesi gereken herhangi bir C# projesine bu deseni uyarlayabilirsiniz.

Bir sonraki adıma hazır mısınız? WinForms veya WPF ile basit bir UI eklemeyi deneyin, farklı dillerle deney yapın veya çıktıyı aranabilir arşivler için bir veritabanına bağlayın. **görüntüden metne c#** tekniklerinde uzmanlaştığınızda sınır yoktur.

İyi kodlamalar, ve taramalarınız her zaman net olsun!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Dil seçimiyle Aspose.OCR kullanarak C# görüntü metni çıkarma](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Görüntüyü Metne Dönüştür – URL'den Görüntü Üzerinde OCR Yap](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [OCR'de Dikdörtgen Hazırlayarak Görüntüden Metin Çıkarma](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}