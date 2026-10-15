---
category: general
date: 2026-02-09
description: C# offline OCR kullanarak görüntüden metin çıkarın. Tam bir C# OCR örneği,
  OCR için görüntünün nasıl yükleneceğini, Kiril alfabesi metnini tanımayı ve pasaporttan
  metin çıkarmayı gösterir.
draft: false
keywords:
- extract text from image
- c# ocr example
- load image for ocr
- recognize cyrillic text
- recognize text from passport
language: tr
og_description: C# çevrim dışı OCR ile görüntüden metin çıkarın. OCR için bir görüntü
  yükleyen, Kiril alfabesindeki metni tanıyan ve bir pasaporttan metin çıkaran adım
  adım bir C# OCR örneğini öğrenin.
og_title: C# ile Görüntüden Metin Çıkarma – Çevrimdışı OCR Rehberi
tags:
- OCR
- C#
- Aspose
title: C#'ta Görüntüden Metin Çıkarma – Çevrimdışı OCR Örneği
url: /tr/net/text-recognition/extract-text-from-image-in-c-offline-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Görüntüden Metin Çıkarma – Çevrimdışı OCR Örneği

Hiç **görüntüden metin çıkarma** ihtiyacı duydunuz mu ama ağ‑bağımlı API'lerde takıldınız mı? Yalnız değilsiniz. Birçok geliştirici, OCR hizmeti çalışma zamanında dil paketlerini indirmeye çalıştığında, özellikle kısıtlı ortamlarda, bir engelle karşılaşıyor.

Bu rehberde tamamen çevrimdışı çalışan, OCR için bir görüntü yükleyen ve bir pasaporttan Kiril alfabesi metnini tanıyan bir **c# ocr example** üzerinden ilerleyeceğiz. Sonunda, desteklenen herhangi bir görüntünün düz metin içeriğini doğrudan konsola yazdıran hazır bir programınız olacak.

## Öğrenecekleriniz

- Aspose.OCR'ı çevrimdışı işleme için nasıl kuracağınızı.  
- Diskten **load image for OCR** için tam kodu.  
- Motoru **recognize cyrillic text** için nasıl yapılandıracağınızı.  
- Pasaport‑stili fotoğraftan metin çıkaran eksiksiz, kopyala‑yapıştır‑hazır **c# ocr example**.  

Aspose ile ilgili önceden bir deneyim gerekmez; sadece .NET 6 (veya daha yeni) SDK ve Visual Studio 2022 (veya VS Code) yeterlidir.

---

![Aspose OCR kullanarak bir pasaport fotoğrafından görüntüden metin çıkarma](/images/ocr-passport.jpg "görüntüden metin çıkar")

## Adım 1: Görüntüden Metin Çıkarma Projesini Kurma

Kod yazmaya başlamadan önce, Aspose.OCR NuGet paketinin projenize eklendiğinden emin olun:

```bash
dotnet add package Aspose.OCR
```

> **Pro ipucu:** En son kararlı sürüme kilitlemek için `--version` bayrağını kullanın (ör. `13.9.0`). Bu, .NET 6 ile uyumluluğu garanti eder.

Yeni bir konsol uygulaması oluşturmak çok basit:

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
```

Artık internete hiç dokunmadan **görüntüden metin çıkarma** yapacağımız temiz bir başlangıcınız var.

## Adım 2: OCR için Görüntü Yükleme – Pasaport Fotoğrafını Okuma

OCR motorunun ilk ihtiyacı, resmi temsil eden bir bitmap ya da akıştır. Senaryomuzda, `cyrillic_passport.jpg` adlı yerel dosyadan **load image for OCR** yapacağız.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 2: Load the image file (this is the “load image for ocr” part)
var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

// Validate the file exists – helpful when the path is wrong.
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// ImageStream abstracts the underlying format; it works with JPEG, PNG, etc.
var image = ImageStream.FromFile(imagePath);
```

> **Neden önemli:** Ham bir `Bitmap` yerine bir akış sağlamak, Aspose'un format algılamasını dahili olarak yapmasını sağlar, tekrarı ve olası hataları azaltır.

## Adım 3: Çevrimdışı Modu Yapılandırma ve Kiril Alfabesi Dilini Seçme

Aspose.OCR, dil modellerini anında indirebilir, ancak bu çevrimdışı çözüm amacını bozar. Ağ çağrılarını kapatın ve motorun hangi dili kullanacağını açıkça belirtin.

```csharp
// Step 3: Create the OCR engine and switch to offline mode
var ocrEngine = new OcrEngine
{
    Configuration =
    {
        OfflineMode = true,               // No network traffic – perfect for secure environments
        Language = new[] { OcrLanguage.Cyrillic } // We want to **recognize cyrillic text**
    }
};
```

> **Köşe durumu:** Daha sonra aynı belgede Latin karakterlerini tanımanız gerekirse, diziye sadece `OcrLanguage.English` ekleyin. Motor, çok‑dilli algılamayı otomatik olarak yönetecek.

## Adım 4: OCR Motorunu Çalıştırma ve Kiril Metnini Tanıma

Şimdi gerçekten **recognize text from passport**‑stili görüntüler. `Recognize` yöntemi, düz metin, güven puanları ve sınırlama kutuları içeren zengin bir sonuç nesnesi döndürür.

```csharp
// Step 4: Perform the OCR operation
OcrResult result = ocrEngine.Recognize(image);

// Step 5: Output the plain text – this is where we finally **extract text from image**
Console.WriteLine("📝 Extracted Text:");
Console.WriteLine("-------------------");
Console.WriteLine(result.PlainText);
```

### Beklenen Konsol Çıktısı

```
📝 Extracted Text:
-------------------
ПАСПОРТ РФ
Иванов Иван Иванович
01.01.1990
...
```

Sonuç bozuk görünüyorsa, kaynak görüntünün net olduğundan ve `OfflineMode` Kiril dili paketinin Aspose kurulum klasöründe (genellikle `\Aspose.OCR\resources\languages`) bulunduğundan emin olun.

## Tam C# OCR Örneği – Tam Kaynak Kodu

Aşağıda **c# ocr example** tamamen yer almaktadır. `Program.cs` içine kopyala‑yapıştır yapın ve `dotnet run` komutunu çalıştırın. **görüntüden metin çıkarma** için ihtiyacınız olan her şey burada.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class OfflineExample
{
    static void Main()
    {
        // --------------------------------------------------------------
        // Step 1: Create the OCR engine (offline mode)
        // --------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Configuration =
            {
                OfflineMode = true,                     // No network calls
                Language = new[] { OcrLanguage.Cyrillic } // Recognize Cyrillic text
            }
        };

        // --------------------------------------------------------------
        // Step 2: Load the image for OCR (passport photo)
        // --------------------------------------------------------------
        var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ Image not found at {imagePath}");
            return;
        }

        var image = ImageStream.FromFile(imagePath);

        // --------------------------------------------------------------
        // Step 3: Recognize the text
        // --------------------------------------------------------------
        var result = ocrEngine.Recognize(image);

        // --------------------------------------------------------------
        // Step 4: Output the plain text (the final extraction)
        // --------------------------------------------------------------
        Console.WriteLine("📝 Extracted Text:");
        Console.WriteLine("-------------------");
        Console.WriteLine(result.PlainText);
    }
}
```

### Örneği Çalıştırma

```bash
dotnet run
```

Konsolda pasaport detaylarını Kiril alfabesinde göreceksiniz. İşte **görüntüden metin çıkarma** hattınızın çalıştığını bildiğiniz an.

## Yaygın Tuzaklar ve Çözüm Yolları

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| Empty `PlainText` | Yanlış dil modeli veya görüntü çok karanlık | `OfflineMode` dilinin `Cyrillic` içerdiğinden emin olun ve görüntü kontrastını artırın |
| `System.DllNotFoundException` | Eksik yerel Aspose OCR ikili dosyaları | NuGet paketini yeniden yükleyin veya `Aspose.OCR.Native.dll` dosyasını çıkış klasörüne kopyalayın |
| Slow performance on large images | Motor tam çözünürlüğü işliyor | Görüntüyü `ImageStream`'e vermeden önce genişliği ≤ 1500 px olacak şekilde küçültün |
| Garbled characters | Görüntü yanlış döndürülmüş | Akış oluşturulmadan önce `Image.RotateFlip(RotateFlipType.Rotate90FlipNone)` kullanın |

## Sonraki Adımlar – Çevrimdışı OCR İş Akışını Genişletme

- `MemoryStream`'den **Load image for OCR** yapın, ASP.NET Core'da yüklenen dosyalarla çalışırken.  
- Bir klasördeki pasaport taramalarını döngüye alarak toplu modda **recognize text from passport**'a geçin.  
- Sonucu **regular expressions** ile birleştirerek pasaport numarası veya doğum tarihi gibi alanları çıkarın.  
- `ocrEngine.Configuration.UseParallelProcessing = true` ile çok çekirdekli hızlandırmaları deneyin.

---

### Sonuç

Tamamen çevrimdışı bir C# OCR iş akışı kullanarak **görüntüden metin çıkarma** yöntemini size gösterdik. Kısa, bağımsız **c# ocr example**, bir görüntü yükler, motoru **recognize cyrillic text** için yapılandırır ve çıkarılan pasaport verilerini yazdırır — tek bir ağ isteği olmadan.

Kodu istediğiniz gibi değiştirmekten, daha fazla dil eklemekten veya çıktıyı bir veritabanına bağlamaktan çekinmeyin. Görüntüyü OCR için yükleme ve pasaport‑stili fotoğraftan metin tanıma temellerini kavradığınızda, sınır yoktur.

Sorularınız mı var ya da kendi değişikliklerinizi paylaşmak mı istiyorsunuz? Aşağıya bir yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}