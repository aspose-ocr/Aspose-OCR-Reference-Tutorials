---
category: general
date: 2026-10-11
description: Aspose.OCR ile C#'ta görüntü üzerinde OCR nasıl yapılır, System.Drawing.Common
  kurulumu ve JPG dosyalarından metin çıkarma dahil olmak üzere öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: tr
lastmod: 2026-10-11
og_description: C#'ta Aspose.OCR kullanarak görüntüde OCR gerçekleştirin. Bu rehber,
  System.Drawing.Common'ı nasıl kuracağınızı, OCR için bir görüntüyü nasıl yükleyeceğinizi
  ve JPG'den metni nasıl çıkaracağınızı gösterir.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: C# ile Görüntüde OCR Yapma – Adım Adım Rehber
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Aspose.OCR kullanarak C#'ta görüntüde OCR nasıl yapılır
url: /tr/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Aspose.OCR kullanarak Görüntüde OCR Nasıl Yapılır

Bir .NET uygulamasında **görüntüde OCR gerçekleştirmek** istiyorsanız, bu kılavuz size eksiksiz bir çözüm sunar. Aspose.OCR kullanarak JPG gibi **resim dosyalarından metin tanıyabilir** ve sonucu bir konsol penceresinde görüntüleyebilirsiniz.

Öğrenecekleriniz:

* **install System.Drawing.Common package** – `Image` sınıfını sağlayan kütüphane,
* **load image for OCR** – bir JPEG veya PNG'yi belleğe okur,
* dil modelini yapılandır,
* **perform OCR on image** ve son olarak,
* **extract text from JPG** ve çıktıyı verir.

Adımlar .NET 6+ için yazılmıştır, ancak .NET Framework 4.6.1 ve üzeriyle de çalışır.

---

## Önkoşullar

| Gereksinim | Neden Önemli |
|-------------|----------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | C# konsol uygulaması için çalışma zamanını sağlar. |
| Visual Studio 2022 (or any IDE) | NuGet paketlerini eklemeyi ve programı çalıştırmayı kolaylaştırır. |
| Internet connection (first run only) | Aspose.OCR dil modülünü otomatik olarak indirir. |
| A sample image containing Cyrillic or Latin text (e.g., `sample_cyrillic.jpg`) | **extract text from JPG** işlemini göstermek için kullanılır. |

---

## 1. Adım: System.Drawing.Common paketini kurun

`System.Drawing.Common` NuGet paketi, **load image for OCR** yapacağınız `Image` sınıfını sağlar. Package Manager Console’u açın ve şu komutu çalıştırın:

```powershell
Install-Package System.Drawing.Common
```

> **Pro ipucu:** Linux/macOS'ta platform‑spesifik uyarılar alırsanız proje dosyasına `net6.0-windows` hedefleyin veya `<UseWindowsForms>true</UseWindowsForms>` ekleyin.

---

## 2. Adım: Aspose.OCR NuGet paketini ekleyin

Aspose.OCR OCR motorunu ve dil modellerini içerir. Şu komutla kurun:

```powershell
Install-Package Aspose.OCR
```

Paket hafiftir; gerekli dil verileri (ör. Cyrillic) `OcrEngine.Language` ayarlandığında ilk kez indirilecektir.

---

## 3. Adım: OCR için görüntüyü nasıl yüklersiniz

Görseli yüklemek, **perform OCR on image** yapmadan önce atmanız gereken ilk somut adımdır. `Image.FromFile` metodu, JPG, PNG, BMP ve TIFF dahil GDI+ tarafından desteklenen tüm formatları okur.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*Dosya bulunamazsa `FileNotFoundException` fırlatılır – üretim kodunda bu çağrıyı bir try/catch bloğuna alın.*

---

## 4. Adım: Motoru yapılandırın ve **perform OCR on image**

Bir `OcrEngine` örneği oluşturun, dil modelini seçin, yüklenen görüntüyü atayın ve `Recognize()` metodunu çağırın.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

`Recognize()` metodu, çıkarılan metni, güven puanlarını ve sınırlama kutularını tutan bir `OcrResult` nesnesi döndürür. Dil modülü ilk kullanımda otomatik olarak indirilir, ek dosya gerekmez.

---

## 5. Adım: **Extract text from JPG** ve görüntüleyin

Artık **recognize text from picture** yapabilir ve sonucu çıktı olarak alabilirsiniz. `OcrResult` nesnesinin `Text` özelliği düz metni içerir.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### Beklenen konsol çıktısı

```
Recognized text:
Пример текста на кириллице
```

Kaynak görüntü İngilizce metin içeriyorsa, çıktı resimde yer alan İngilizce cümle olacaktır.

---

## Kenar durumları ve en iyi uygulama ipuçları

| Durum | Öneri |
|-----------|----------------|
| **Large images ( > 5 MB )** | OCR öncesinde en uzun kenarı ≤ 2000 px olacak şekilde görüntüyü yeniden boyutlandırarak bellek kullanımını azaltın ve hızı artırın. |
| **Multiple languages in one picture** | Cyrillic'e ek olarak `ocrEngine.AddLanguage(OcrLanguage.English)` çağırın, ardından `ocrEngine.Language = OcrLanguage.Multilingual` ayarlayın. |
| **Low‑contrast scans** | Bitmap'i motora göndermeden önce `System.Drawing.Graphics` ile kontrastı artırın. |
| **Running on Linux/macOS** | `libgdiplus` yerel bağımlılığının kurulu olduğundan emin olun (`sudo apt-get install -y libgdiplus`). |
| **Repeated OCR calls** | Aynı `OcrEngine` örneğini yeniden kullanın ve sadece `ocrEngine.Image`'ı değiştirerek tekrar tekrar modül yüklenmesini önleyin. |

---

## Tam, çalıştırılabilir program

Aşağıda önceki tüm adımları birleştiren tam konsol uygulaması yer almaktadır. Kodu yeni bir C# konsol projesine kopyalayın, görüntü yolunu değiştirin ve çalıştırın.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Running the program** tanınan dizeyi konsola yazdırır, **performed OCR on image** ve **extracted text from JPG** işlemlerini başarıyla tamamladığınızı doğrular.

---

## Sonuç

Artık Aspose.OCR kullanarak C#’ta **perform OCR on image** dosyalarını, gerekli **System.Drawing.Common package** kurulumundan **loading image for OCR**, uygun dili seçmeye ve nihayet **extract text from JPG** işlemine kadar nasıl yapacağınızı biliyorsunuz. Bu uçtan uca örnek, resim klasörlerini toplu işleme veya OCR’u bir web API’sine entegre etme gibi daha gelişmiş belge‑işleme boru hatları oluşturmanız için sağlam bir temel sağlar.

### Sıradaki adımlar?

* PDF’lerde **recognize text from picture** işlemini, her sayfayı önce bir görüntüye dönüştürerek keşfedin.
* Gürültülü taramalarda doğruluğu ince ayarlamak için `OcrEngine` özellikleri `Resolution`, `Threshold` ve `MaxProcessingTime` ile deneyler yapın.
* OCR çıktısını bir doğal dil işleme kütüphanesiyle birleştirerek çıkarılan içeriği otomatik olarak sınıflandırın.

Kodunuzu diğer görüntü formatları için uyarlamaktan, hata yönetimi eklemekten veya daha büyük uygulamalara entegre etmekten çekinmeyin. Mutlu kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [C#'ta Görüntüden Metin Çıkarma – Tam Aspose OCR Kılavuzu](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Aspose.OCR ile Dil Seçimi Kullanarak C#'ta Görüntü Metni Çıkarma](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Aspose OCR Kullanarak Akıştan Görüntü Metni Çıkarma](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}