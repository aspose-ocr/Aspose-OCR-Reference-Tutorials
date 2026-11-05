---
category: general
date: 2026-02-20
description: C#'ta DjVu dosyalarında OCR nasıl yapılır? Görüntüden metin tanımayı
  öğrenin ve Aspose OCR ile DjVu'yu hızlıca metne dönüştürün.
draft: false
keywords:
- how to perform OCR
- recognize text from image
- how to read djvu
- extract text from image
- convert djvu to text
language: tr
og_description: C#'ta DjVu dosyalarında OCR nasıl yapılır. Bu öğreticide, görüntüden
  metin tanıma, DjVu okuma ve Aspose OCR kullanarak DjVu'yu metne dönüştürme yöntemlerini
  gösteriyoruz.
og_title: C#'ta DjVu Dosyalarında OCR Nasıl Yapılır – Tam Kılavuz
tags:
- OCR
- C#
- DjVu
- Aspose
title: C#'ta DjVu Dosyalarında OCR Nasıl Yapılır – Adım Adım Rehber
url: /tr/net/text-recognition/how-to-perform-ocr-on-djvu-files-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta DjVu Dosyalarında OCR Nasıl Yapılır – Tam Kılavuz

DjVu belgesinde **OCR nasıl yapılır** diye hiç merak ettiniz mi, saçınızı yolmak zorunda kalmadan? Tek başınıza değilsiniz. Birçok geliştirici, DjVu kapsayıcıları içinde bulunan **görüntüden metin tanıma** kaynaklarıyla karşılaştıklarında bir duvara çarpar. İyi haber? Birkaç satır C# ve Aspose OCR kütüphanesiyle, bu gizli metni anında çıkarabilirsiniz.

Bu öğreticide, bir DjVu sayfasını düz metne dönüştürmek için bilmeniz gereken her şeyi adım adım göstereceğiz. Sonunda **DjVu nasıl okunur**, **görüntüden metin nasıl çıkarılır** ve hatta **DjVu'dan metne nasıl dönüştürülür** konularını öğreneceksiniz. Harici hizmetler yok, belirsiz referanslar yok—sadece kendi içinde çalışan, çalıştırılabilir bir örnek.

## Önkoşullar

- .NET 6.0 SDK veya daha yeni bir sürüm (kod .NET Framework 4.8 ile de çalışır).
- Visual Studio 2022 veya C# destekleyen herhangi bir editör.
- Aspose OCR for .NET lisansı (ücretsiz deneme sürümü test için yeterlidir).
- Referans verebileceğiniz bir klasöre yerleştirilmiş bir örnek DjVu dosyası (`sample.djvu`).

Bu gereksinimleri önceden hazırlamak akışı sorunsuz tutar—daha sonra “referans eksik” sürprizleriyle karşılaşmazsınız.

## DjVu Sayfasında OCR Nasıl Yapılır

Temel fikir basit: DjVu sayfasını bir görüntü olarak yükleyin, OCR motoruna verin ve oluşan dizeyi okuyun. Şimdi bunu adım adım inceleyelim.

### Adım 1: Aspose OCR'yi Kurun

Proje klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

Bu, en yeni Aspose OCR ikili dosyalarını ve bağımlılıklarını indirir. NuGet Package Manager UI'ı tercih ediyorsanız, **Aspose.OCR** aratıp **Install** (Yükle) düğmesine tıklamanız yeterlidir.

### Adım 2: OCR Motorunu Başlatın

`OcrEngine` örneği oluşturmak, **OCR yapmayı** istediğinizde yaptığınız ilk şeydir. Bunu, tarayıcının beynini açmak gibi düşünün.

```csharp
using Aspose.OCR;

// ...

// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **Pro tip:** Birden fazla sayfa için tek bir `OcrEngine` yeniden kullanmak belleği tasarruf ettirir ve işleme hızını artırır.

### Adım 3: DjVu Sayfasını Görüntü Olarak Yükleyin

DjVu dosyaları çoğu görüntü API'sı tarafından doğrudan desteklenmez, ancak Aspose her sayfayı bir bitmap olarak ele alabilir. Burada dosyayı okumak için `System.Drawing.Image` kullanıyoruz.

```csharp
using System.Drawing;

// ...

// Step 3: Load a DjVu page as an image
string djvuPath = @"C:\Path\To\Your\Directory\sample.djvu";
Image djvuPage = Image.FromFile(djvuPath);
```

> **Neden bu çalışıyor:** `Image.FromFile` DjVu akışını OCR motorunun anlayabileceği bir raster formata otomatik olarak çözer. Çok sayfalı bir DjVu'dan belirli bir sayfa işlemek istiyorsanız, önce sayfayı çıkarmak için Aspose PDF veya Aspose Imaging kullanın.

### Adım 4: Görüntüden Metin Tanıma

Şimdi sihir gerçekleşiyor. `Recognize` yöntemi bitmap'i tarar ve tespit edilen karakterleri içeren bir dize döndürür.

```csharp
// Step 4: Perform OCR to extract text from the image
string extractedText = ocrEngine.Recognize(djvuPage);
```

Bu noktada, aslında bir DjVu kapsayıcısının içinde bulunan **görüntüden metin tanıma** verisini başarıyla elde ettiniz. Dize satır sonları, noktalama işaretleri ve kaynak dil destekliyorsa Unicode karakterler de içerebilir.

### Adım 5: Sonucu Görüntüle veya Sakla

Hızlı bir doğrulama için metni konsola dökebilirsiniz. Gerçek bir uygulamada muhtemelen bir dosyaya ya da veritabanına yazarsınız.

```csharp
// Step 5: Display the recognized text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(extractedText);
```

Hepsini bir araya getirdiğimizde, işte tam çalıştırılabilir program:

```csharp
// File: DjvuOcrExample.cs
using System;
using System.Drawing;
using Aspose.OCR;

class DjvuExample
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load a DjVu page as an image
        Image djvuPage = Image.FromFile(@"C:\Path\To\Your\Directory\sample.djvu");

        // Perform OCR to extract text from the image
        string extractedText = ocrEngine.Recognize(djvuPage);

        // Display the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**Beklenen çıktı** (kısaltılmış olarak):

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
Lorem ipsum dolor sit amet, consectetur...
```

Eğer bozuk karakterler görürseniz, DjVu dosyasının şifreli olmadığını ve `ocrEngine.Language` içinde doğru dili ayarladığınızı iki kez kontrol edin. Varsayılan olarak İngilizce kabul edilir; `ocrEngine.Language = Language.French;` atayarak Fransızca, Almanca vb. dillere geçebilirsiniz.

## Görüntüden Metin Tanıma – Yaygın Tuzaklar

Sağlam bir örnek olmasına rağmen, geliştiriciler sık sık birkaç kenar durumuna takılır:

| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| **Boş çıktı** | Görüntü çözünürlüğü çok düşük (<300 dpi). | `Recognize` çağırmadan önce `ocrEngine.ImageResolution = 300;` kullanın. |
| **Yanlış dil** | OCR varsayılan olarak İngilizce'dir. | `ocrEngine.Language = Language.Spanish;` olarak ayarlayın (veya desteklenen herhangi bir dil). |
| **Bellek sızıntısı** | Büyük DjVu sayfaları işlendikten sonra bellekte kalır. | İşiniz bittiğinde `djvuPage.Dispose();` çağırın. |
| **Çok sayfalı DjVu** | Sadece ilk sayfa yüklenir. | Sayfalar arasında döngü yapmak için Aspose Imaging'in `DjvuImage` sınıfını kullanın. |

Bu sorunları erken aşamada ele almak, sayısız hata ayıklama saatinden tasarruf sağlar.

## C#'ta DjVu Dosyalarını Okumak – Basit OCR'ın Ötesinde

Projeniz tek bir sayfadan daha fazlasını gerektiriyorsa, önce her sayfayı bir görüntü olarak çıkarmanız gerekir. Aspose Imaging bunu zahmetsiz hale getirir:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;

// ...

string djvuPath = @"sample.djvu";
using (DjvuImage djvu = (DjvuImage)Image.Load(djvuPath))
{
    for (int i = 0; i < djvu.Frames.Count; i++)
    {
        using (Image page = djvu.Frames[i].ConvertToRaster())
        {
            // Run OCR on each page
            string pageText = ocrEngine.Recognize(page);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
    }
}
```

Bu desen, **DjVu'dan metne dönüştürme** işlemini sayfa sayfa yapmanızı sağlar ve büyük arşivlerin toplu işlenmesi için mükemmeldir.

## Görüntüden Metin Çıkarma – Doğruluğu İnce Ayarlama

Varsayılan OCR ayarları temiz taramalar için iyidir, ancak doğruluğu artırabilirsiniz:

```csharp
ocrEngine.ImagePreprocessingOptions = new ImagePreprocessingOptions()
{
    // Binarize the image to improve contrast
    BinarizationMethod = BinarizationMethod.Otsu,
    // Deskew the image if it’s tilted
    Deskew = true,
    // Remove noise
    NoiseRemoval = true
};
```

Bu ince ayarlar, DjVu kaynağında el yazısı notlar veya düşük kontrastlı grafikler olduğunda özellikle faydalıdır.

## DjVu'yu Metne Dönüştür – Tam Uçtan Uca Örnek

Aşağıda, her şeyi bir araya getiren kompakt bir sürüm bulunuyor: çok sayfalı bir DjVu'yu yükleme, her sayfayı ön işleme, OCR gerçekleştirme ve çıktıyı bir `.txt` dosyasına kaydetme.

```csharp
using System;
using System.IO;
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;
using Aspose.OCR;
using Aspose.OCR.Models;

class DjvuToTextConverter
{
    static void Main()
    {
        // Prepare OCR engine with preprocessing
        OcrEngine ocr = new OcrEngine
        {
            ImagePreprocessingOptions = new ImagePreprocessingOptions()
            {
                BinarizationMethod = BinarizationMethod.Otsu,
                Deskew = true,
                NoiseRemoval = true
            }
        };

        string inputPath = @"C:\Docs\sample.djvu";
        string outputPath = @"C:\Docs\sample_extracted.txt";

        using (DjvuImage djvu = (DjvuImage)Image.Load(inputPath))
        using (StreamWriter writer = new StreamWriter(outputPath))
        {
            for (int i = 0; i < djvu.Frames.Count; i++)
            {
                using (var page = djvu.Frames[i].ConvertToRaster())
                {
                    string text = ocr.Recognize(page);
                    writer.WriteLine($"--- Page {i + 1} ---");
                    writer.WriteLine(text);
                }
            }
        }

        Console.WriteLine($"Extraction complete. Text saved to {outputPath}");
    }
}
```

Bu betiği çalıştırdığınızda, her sayfanın içeriği düzgün bir şekilde ayrılmış `sample_extracted.txt` dosyası oluşturulur. **DjVu'dan metne dönüştürme** işlemini indeksleme, arama veya arşivleme için en hızlı yol budur.

## Sonuç

DjVu dosyalarında **OCR nasıl yapılır** konusunu baştan sona ele aldık, **görüntüden metin tanıma** yollarını inceledik. 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}